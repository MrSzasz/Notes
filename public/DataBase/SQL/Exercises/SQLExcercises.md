# Ejercicios SQL - MySQL

## Web Dev Simplified

Los siguientes ejercicios están basados en el [curso de SQL de Web Dev Simplified](https://github.com/WebDevSimplified/Learn-SQL).

### 1. Crear la tabla `Songs`

Esta tabla debe llamarse `songs` y tiene las 4 siguientes propiedades.

1. `id`: Un dato tipo INT que es PK y auto incremental que no debe ser null.
2. `name`: Un string que no debe ser null.
3. `length`: Un dato FLOAT que representa la duración de la canción en minutos y no puede ser null.
4. `album_id`: Un INT que es FK para referenciar los álbumes de la tabla, el cual no puede ser null.

Después de crear la tabla copiar [este código](https://github.com/WebDevSimplified/Learn-SQL/blob/master/data.sql) y iniciarlo para llenar las tablas con datos.

```sql

    create table songs(
        id int auto_increment not null,
        name varchar(255) not null,
        length float not null,
        album_id int not null,
        primary key(id),
        foreign key(album_id) references albums(id)
    );

```

### 2. Seleccionar solo los nombres de las bandas

Cambiar el nombre de la columna para que el return sea `Band Name`.

| Band Name         |
|-------------------|
| Seventh Wonder    |
| Metallica         |
| The Ocean         |
| Within Temptation |
| Death             |
| Van Canto         |
| Dream Theater     |

```sql

    SELECT bands.name AS 'Band Name'
    FROM bands;

```

### 3. Seleccionar le álbum mas antiguo

Solo devolver un resultado, y que el mismo no sea el album que no tiene fecha de lanzamiento.

| id | name                   | release_year | band_id |
|----|------------------------|--------------|---------|
| 5  | ...And Justice for All | 1988         | 2       |

```sql

    SELECT * FROM albums
    WHERE release_year IS NOT NULL
    ORDER BY release_year
    LIMIT 1;

```

### 4. Seleccionar todas las bandas que tengan álbumes (JOIN)

Devolver el nombre de la banda como `Band Name`.

| Band Name         |
|-------------------|
| Seventh Wonder    |
| Metallica         |
| The Ocean         |
| Within Temptation |
| Death             |
| Van Canto         |

```sql

    SELECT DISTINCT bands.name AS 'Band Name'
    FROM bands 
    JOIN albums ON bands.id = albums.band_id;

```

### 5. Traer todas las bandas que no tienen álbumes

Devolver el nombre de la banda como `Band Name`.

| Band Name     |
|---------------|
| Dream Theater |

```sql

    SELECT bands.name AS 'Band Name'
    FROM bands
    LEFT JOIN albums ON bands.id = albums.band_id
    WHERE albums.name IS NULL;

    -- wds
    SELECT bands.name AS 'Band Name'
    FROM bands LEFT JOIN albums 
    ON bands.id = albums.band_id
    GROUP BY albums.band_id
    HAVING COUNT(albums.id) = 0;

```

### 6. Traer el album más largo (SUM)

Devolver el nombre del album como `Name`, el año de lanzamiento como `Release Year`, y la duración como `Duration`.

| Name           | Release Year | Duration          |
|----------------|--------------|-------------------|
| Death Magnetic | 2008         | 74.76666593551636 |

```sql

    SELECT 
        albums.name AS 'Name',
        albums.release_year AS 'Release Year',
        SUM(songs.length) AS 'Duration'
    FROM albums
    JOIN songs ON albums.id = songs.album_id
    GROUP BY songs.albums_id
    ORDER BY Duration DESC
    LIMIT 1;

```

### 7. Actualizar el año de lanzamiento del album que no lo tiene

Colocar el año de lanzamiento como 1986.

> Es necesario usar la PK para actualizar los datos, por el funcionamiento de MySQL Workbench

```sql

    UPDATE albums 
    SET release_year = 1986
    WHERE id = 4;

```

### 8. Insertar un album de tu banda favorita

Al hacerlo correctamente debe verse el album y la banda del mismo.

```sql

    insert into bands (name) values('System of a Down');
    insert into albums (name, release_year, band_id) 
        values
            ('System of a Down', 1998, 8),
            ('Toxicity', 2001, 8),
            ('Steal this album!', 2022, 8),
            ('Mezmerize', 2005, 8),
            ('Hypnotize', 2005, 8);

```

### 9. Borrar la banda que se agregó en el punto anterior

> El orden es importante, ya que posee una FK para asociar

```sql

    SELECT * FROM bands;-- bad_id = 8

    DELETE FROM albums 
    WHERE band_id = 8;
    DELETE FROM bands 
    WHERE id = 8;

```

### 10. Obtener la duración promedio de todas las canciones

Devolver la duración promedio como `Average Song Duration`.

| Average Song Duration |
|-----------------------|
| 5.352472513259112     |

```sql

    SELECT AVG(length) AS 'Average Song Duration'
    FROM songs;

```

### 11. Seleccionar la canción mas larga de cada album

Devolver el nombre del album como `Album`, el año de lanzamiento como `Release Year`, y la duración de la canción mas larga como `Duration`.

| Album                       | Release Year | Duration |
|-----------------------------|--------------|----------|
| Tiara                       | 2018         | 9.5      |
| The Great Escape            | 2010         | 30.2333  |
| Mercy Falls                 | 2008         | 9.48333  |
| Master of Puppets           | 1986         | 8.58333  |
| ...And Justice for All      | 1988         | 9.81667  |
| Death Magnetic              | 2008         | 9.96667  |
| Heliocentric                | 2010         | 7.48333  |
| Pelagial                    | 2013         | 9.28333  |
| Anthropocentric             | 2010         | 9.4      |
| Resist                      | 2018         | 5.85     |
| The Unforgiving             | 2011         | 5.66667  |
| Enter                       | 1997         | 7.25     |
| The Sound of Perseverance   | 1998         | 8.43333  |
| Individual Thought Patterns | 1993         | 4.81667  |
| Human                       | 1991         | 4.65     |
| A Storm to Come             | 2006         | 5.21667  |
| Break the Silence           | 2011         | 6.15     |
| Tribe of Force              | 2010         | 8.38333  |

```sql

    SELECT 
        albums.name AS 'Album',
        albums.release_year AS 'Release Year',
        MAX(songs.length) AS 'Duration'
    FROM albums
    JOIN songs ON albums.id = songs.album_id
    GROUP BY songs.album_id;

```

### 12. Obtener la cantidad de canciones de cada banda (joins)

Devolver el nombre de la banda como `Band`, y la cantidad de canciones como `Number of Songs`.

| Band              | Number of Songs |
|-------------------|-----------------|
| Seventh Wonder    | 35              |
| Metallica         | 27              |
| The Ocean         | 31              |
| Within Temptation | 30              |
| Death             | 27              |
| Van Canto         | 32              |

```sql

    -- me
    SELECT 
        bands.name AS 'Band',
        COUNT(songs.album_id) 'Number of Songs'
    FROM bands
    JOIN albums ON bands.id = albums.band_id
    JOIN songs ON albums.id = songs.album_id
    GROUP BY bands.id;

    -- wds
    SELECT
        bands.name AS 'Band',
        COUNT(songs.id) AS 'Number of Songs'
    FROM bands
    JOIN albums ON bands.id = albums.band_id
    JOIN songs ON albums.id = songs.album_id
    GROUP BY albums.band_id;

```
