# Ejercicios SQL - MySQL

## Web Dev Simplified

Los siguientes ejercicios están basados en el [curso de SQL de Web Dev Simplified](https://github.com/WebDevSimplified/Learn-SQL).

### 1. Create a Songs Table

This table should be called `songs` and have four properties with these exact names.

1. `id`: An integer that is the primary key, and auto increments.
2. `name`: A string that cannot be null.
3. `length`: A float that represents the length of the song in minutes that cannot be null.
4. `album_id`: An integer that is a foreign key referencing the albums table that cannot be null.

After successfully creating the table copy the code from [data.sql](data.sql) into MySQL Workbench, and run it to populate all of the data for the rest of the exercises. If you do not encounter any errors, then your answer is most likely correct.

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

### 2. Select only the Names of all the Bands

Change the name of the column the data returns to `Band Name`

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

### 3. Select the Oldest Album

Make sure to only return one result from this query, and that you are not returning any albums that do not have a release year.

| id | name                   | release_year | band_id |
|----|------------------------|--------------|---------|
| 5  | ...And Justice for All | 1988         | 2       |

```sql

    SELECT * FROM albums
    WHERE release_year IS NOT NULL
    ORDER BY release_year
    LIMIT 1;

```

### 4. Get all Bands that have Albums

There are multiple different ways to solve this problem, but they will all involve a join.

Return the band name as `Band Name`.

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

### 5. Get all Bands that have No Albums

This is very similar to #4 but will require more than just a join.

Return the band name as `Band Name`.

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

### 6. Get the Longest Album

This problem sounds a lot like #3 but the solution is quite a bit different. I would recommend looking up the SUM aggregate function.

Return the album name as `Name`, the album release year as `Release Year`, and the album length as `Duration`.

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

### 7. Update the Release Year of the Album with no Release Year

Set the release year to 1986.

You may run into an error if you try to update the release year by using `release_year IS NULL` in the WHERE statement of your UPDATE. This is because MySQL Workbench by default will not let you update a table that has a primary key without using the primary key in the UPDATE statement. This is a good thing since you almost never want to update rows without using the primary key, so to get around this error make sure to use the primary key of the row you want to update in the WHERE of the UPDATE statement.

```sql

    UPDATE albums 
    SET release_year = 1986
    WHERE id = 4;

```

### 8. Insert a record for your favorite Band and one of their Albums

If you performed this correctly you should be able to now see that band and album in your tables.

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

### 9. Delete the Band and Album you added in #8

The order of how you delete the records is important since album has a foreign key to band.

```sql

    SELECT * FROM bands;-- bad_id = 8

    DELETE FROM albums 
    WHERE band_id = 8;
    DELETE FROM bands 
    WHERE id = 8;

```

### 10. Get the Average Length of all Songs

Return the average length as `Average Song Duration`.

| Average Song Duration |
|-----------------------|
| 5.352472513259112     |

```sql

    SELECT AVG(length) AS 'Average Song Duration'
    FROM songs;

```

### 11. Select the longest Song off each Album

Return the album name as `Album`, the album release year as `Release Year`, and the longest song length as `Duration`.

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

### 12. Get the number of Songs for each Band

This is one of the toughest question on the list. It will require you to chain together two joins instead of just one.

Return the band name as `Band`, the number of songs as `Number of Songs`.

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
