# SQL

SQL (Structured Query Language / Lenguaje de consulta estructurado) es un tipo de lenguaje que permite la comunicación de un usuario a una base de datos mediante queries. Las bases de datos SQL son bases de datos estructuradas en forma de tablas, siendo conformadas por lineas verticales (Columnas) y lineas horizontales (Registros), las cuales se llenan con la información que guardemos en las mismas.  

| id | name  | age | mail              | active |
|:--:|:-----:|:---:|:-----------------:|:------:|
| 1  | jack  | 20  | jack@gmail.com    | true   |
| 2  | lisa  | 25  | lisa@gmail.com    | true   |
| 3  | marie | 20  | marie@hotmail.com | false  |
| 4  | harry | 26  | harry@gmail.com   | true   |

Las tablas se generan con los datos que nosotros le asignemos, pero a su vez siempre tendrán un `id` que se genera automáticamente, el cual es autoincremental (incrementa el valor dependiendo el ultimo id generado).  
Estas tablas pueden compartir datos con otras tablas, ya que son `relacionales`, por ejemplo, podemos tener una tabla de usuarios que guarden productos en un cart, relacionando estos productos al id del usuario en particular.

| id | product   | qty | price | user_id |
|:--:|:---------:|:---:|:-----:|:-------:|
| 1  | pizza     | 2   | 15    | 1       |
| 2  | milk      | 1   | 20    | 1       |
| 3  | chocolate | 5   | 8     | 3       |

Como vemos, hay dos columnas de id, una de ellas (`id`) representa el id del producto en particular, pero también tenemos la columna de `user_id`, la cual representa el id del usuario que realizó el pedido.  
A estos dos tipos de id se los conoce como `Primary key - PK` (id que se genera en base) y `Foreign key - FK` (id que se toma desde otra tabla).  
Por ultimo, podemos necesitar que dos tablas compartan la misma información, para ello crearemos una tabla intermedia que se componga de un PK generado para la relación, y tomar las FK de las tablas que necesitemos para identificar los datos. Pongamos de ejemplo que nuestros usuarios tienen registrados descuentos, para ello creamos una base de datos con los descuentos disponibles.

| id | discount | %  | available |
|:--:|:--------:|:--:|:---------:|
| 1  | senior   | 15 | true      |
| 2  | student  | 10 | true      |
| 3  | spring   | 5  | false     |

Y nuestros usuarios pueden tener el id relacionado dependiendo del descuento que posean, quedando nuestra 3ra tabla de la siguiente manera.

| id | user_id | discount_id |
|:--:|:-------:|:-----------:|
| 1  | 2       | 2           |
| 2  | 4       | 2           |

Como vemos, los usuarios tienen su columna particular (`user_id`) en la que se toma el id del mismo para poder reconocer que usuario tiene el descuento, y tenemos la columna de los descuentos (`discount_id`) para marcar que descuentos se aplicarán. Con esta información podemos ver que Lisa (`user con id 2`) tiene un descuento de estudiante (`descuento con id 2`), al igual que lo tiene Harry (`user con id 4`).  
Esta tabla esta compuesta por una PK (primer columna de id) y dos FK (los id que recuperan los datos desde otras tablas).

## Instalación

Para empezar a utilizar SQL será necesario instalarlo en nuestro sistema operativo (en este caso Windows). Para ello empezamos yendo a la [`página de descargas`](https://dev.mysql.com/downloads/installer/) y elegimos nuestro sistema operativo, descargando la versión que pesa más.  
Luego de descargarse el instalador lo iniciamos, eligiendo la opción `Custom`, instalando los siguiente paquetes (para que se seleccionen debemos hacer click en la flecha verde hacia la derecha).

> MySQL Servers |> MySQL Server |> MySQL Server 8.0 |> MySQL Server 8.0.30
> Applications |> MySQL Workbench |> MySQL Workbench 8.0 |> MySQL Workbench 8.0.30
> Applications |> MySQL Shell |> MySQL Shell 8.0 |> MySQL Shell 8.0.30

Luego de esto damos siguiente y ejecutar, nos saldrá la ventana de configuración, en la cual debemos dejar todo como default y seguimos, elegimos la version actual de contraseñas y configuramos una contraseña que guardaremos para luego.  
Hecho esto podemos seguir sin agregar un nuevo usuario y llegamos hasta la pantalla final (Installation complete), en la cual solo dejaremos seleccionada la opción de `Start MySQL Workbench after setup` (Iniciar MySQL Workbench luego de instalar) y finalizamos.
Al abrirse el Workbench veremos que hay una instancia de SQL detectada (`Local instance MySQL, en el apartado de MySQL Connections`), hacemos click en la misma y ponemos la contraseña que habíamos guardado anteriormente.  
Con esto hecho tendremos MySQL configurado en nuestra PC, por lo que podremos comenzar a trabajar con SQL.

## Crear Database

Con todo esto podemos empezar creando nuestra primer base de datos. Para ello debemos hacer uso del comando `create database` y el nombre de la base de datos, quedando de la siguiente manera.

```sql
create database users_test_db;
```

> Para que el comando funcione debemos dar click en el rayo que tenemos arriba, o usar `CTRL + enter`.

## Crear tabla

Con nuestra base de datos creada podemos empezar a armar nuestra primer tabla, para ello debemos empezar seleccionando nuestra base de datos con el siguiente comando.

```sql
use users_test_db;
```

> Siempre que escribimos una linea en SQL debe terminar con un punto y coma (;)

Luego de seleccionarla podemos crear nuestra primer tabla, que tomaremos en base a la que mostramos anteriormente, quedando el comando de la siguiente manera.

```sql
create table users(
    id int not null auto_increment,      -- El ID será número entero y se auto incrementará con cada nuevo dato
    name not null varchar(255),          -- El dato Name será un Varchar (string), con una longitud maxima de 255 caracteres
    age not null int,                -- La edad será un número entero
    mail not null varchar(255),      -- El mail también será un Varchar (string)
    active not null BIT,             -- Al no poder usar Booleans, usaremos BIT, el cual toma el 0 como 'false' y el 1 como 'true'
    PRIMARY KEY (id)        -- Indicamos que nuestra Primary Key será el dato ID
);
```

> `NOT NULL` indica que los datos no pueden estar vacíos/ser NULL

Como podemos ver, los tipos de datos no son iguales que en JS, pero si cumplen la misma función, quedando el mismo de la siguiente manera.

| SQL     | JS      |
|:-------:|:-------:|
| int     | number  |
| varchar | string  |
| BIT     | boolean |

## (C)RUD - Create

Ya tenemos nuestra primer tabla, ahora es momento de empezar a tener los datos dentro de la misma. Para ello empezamos usando el comando `INSERT` de la siguiente manera.

```sql
INSERT INTO users (name, age, mail, active) VALUES ('jack', 20, 'jack@gmail.com', 1)
```

> INSERT INTO `<nombre de la tabla>` (`<datos a insertar>`) VALUES (`<valores a insertar>`)

Perfecto, ya tenemos nuestro primer usuario en nuestra tabla, pero no vamos a crear uno por uno cada usuario, es por eso que agregaremos los próximos 3 en un solo comando de la siguiente manera.

```sql
INSERT INTO users (name, age, active) VALUES ('lisa', 25, 'lisa@gmail.com', 1), ('marie', 20, 'maire@hotmail.com' 0), ('harry', 26,'harry@gmail.com' 1);
```

Ya tenemos nuestros 4 usuarios de ejemplo en nuestra base de datos creados correctamente, es tiempo de poder traerlos de la base de datos.

## C(R)UD - Read

Para ver como vamos con nuestra base de datos podemos seleccionar todos nuestros datos y mostrarlos, para ello hacemos uso del comando `SELECT` de la siguiente manera.

```sql
SELECT * FROM users;
```

> SELECT `<que vamos a seleccionar>` FROM `<tabla>`

Si tenemos datos duplicados podemos hacer uso `DISTINCT` para ignorar los mismos.

```sql
SELECT DISTINCT * FROM users;
```

Con este comando podemos ver como nos trae todos los datos que tiene nuestra tabla. El siguiente paso es poder elegir que dato nos vamos a traer, por ejemplo, si solo queremos ver los datos que tiene Harry deberemos indicar su id como filtro de la consulta de la siguiente manera.

```sql
SELECT * FROM users WHERE id = 4;
```

> SELECT `<que vamos a seleccionar>` FROM `<tabla>` WHERE `<condición a cumplir>`

De esta forma nos traemos el usuario que necesitamos en este momento, pero también podemos seleccionar que dato nos traemos, como puede ser por ejemplo, la columna de edad.

```sql
SELECT age FROM users WHERE id = 4;
```

Obteniendo de esta manera el dato `26`, que es la edad que pusimos en nuestra base de datos.  
Si necesitamos traernos datos basados en dos o mas ids podemos usar `IN` de la siguiente manera.

```sql
SELECT age FROM users WHERE id IN (2,3);
```

Sumado a esto podemos traernos dos columnas a la vez, e incluso ponerle un nombre en particular con el comando `as`.

```sql
SELECT id, age AS edad FROM users;
```

También es posible traernos varios datos que cumplan con una misma condición, por ejemplo, los usuarios que estén activos en nuestra base de datos.

```sql
SELECT * FROM users WHERE active = 1;
```

> Hay que recordar que en este caso los activos (true) se representan con el numero `1`

O tomar mas de un dato en particular para filtrar, por ejemplo, los usuarios activos mayores a 21 años.

```sql
SELECT * FROM users WHERE active = 1 AND age > 21;
```

Esto nos traerá los usuarios de Lisa y Harry, ya que ambos cumplen con las dos condiciones indicadas anteriormente.  
Así como tenemos la condición `AND` para indicar que se deben cumplir ambas, también tenemos el `OR` para traernos todos los que cumplan una u otra condición.

```sql
SELECT * FROM users WHERE active = 0 OR age > 23;
```

Esto nos traerá el dato de Marie, que aunque no cumple con ser mayor a 23, si cumple con el dato de estar inactiva.  
Si necesitamos traernos un dato cuando NO tenga una condición usamos `NOT`.

```sql
SELECT * FROM users WHERE NOT id = 7;
```

Asi nos traemos todos los datos excepto el que tenga el id 7;
Si necesitamos buscar datos entre dos edades podemos usar el comando `between`, pasando ambas edades a comparar.

```sql
SELECT * FROM users WHERE age BETWEEN 19 AND 24;
```

Esto nos devuelve todos los usuarios entre ese rango de edad.  
También podemos traernos todos los datos excluyendo solamente a uno, denegando la comparación de la siguiente manera.  

```sql
SELECT * FROM users WHERE name != 'harry';
```

Con esto traeremos todos los usuarios exceptuando a Harry.  
También podemos buscar entre los datos ciertas palabras, ya sea que contengan, inicien con o terminen con de la siguiente manera.

```sql
SELECT * FROM users WHERE email LIKE '%gmail%';
```

> Para decir que debe empezar con se utiliza `gmail%`, y para terminar con se utiliza `%gmail`

En este caso tendremos todos los que usuarios que estén registrados con gmail, dado que no importa lo que tenga antes o después de la palabra `gmail`.  
Si queremos traernos los datos ordenados por edad podemos usar `order by` de la siguiente manera.

```sql
SELECT * FROM users ORDER BY age ASC;
```

> Si queremos que sea de mayor a menor utilizamos `DESC`

Esto nos ordenará todos los datos de menor a mayor basado en la edad.  
Además podemos seleccionar unicamente el dato mayor o menor de la tabla, por ejemplo, en cuanto a edad.

```sql
SELECT max(age) FROM users;
```

> También es posible traer el menor dato usando `min()`

Y podemos darle un nombre/apodo usando `as`.

```sql
SELECT max(age) as oldest FROM users;
```

> `as` nos servirá también más adelante para cambiar los nombres de las tablas

Podemos traernos también la suma de ciertos valores, el average o la cantidad de veces que se existen los mismos haciendo uso de `count(), sum() o avg()`.

```sql
SELECT count(email) FROM users WHERE email LIKE '%gmail%';          -- Cuenta la cantidad de emails que sean gmail

SELECT sum(id) FROM users WHERE id > 6;         -- Suma todos los id que haya mayores a 6

SELECT avg(id) From users;          -- Devuelve el average entre todos los id
```

Podemos buscar los datos que estén (o no) vacíos, usando `IS NULL` de la siguiente manera.

```sql
SELECT * FROM users WHERE age IS NULL;
```

> Si usamos `NOT NULL` nos traería todos los datos que no estén vacíos

En este caso no nos traería ningún dato, ya que ningún dato está vacío.

## CR(U)D - Update

Es momento de actualizar los datos de nuestra base de datos, en este caso, podemos indicar que Marie ya vuelve a ser activa, es por eso que debemos cambiar el dato de `active` de 0 a 1, esto lo hacemos con el comando `UPDATE`, siempre usando el `id` en el `WHERE` para no tener errores, quedando de la siguiente manera.

```sql
UPDATE users SET `active` = 1 WHERE id = 3;
```

> UPDATE `<tabla>` SET `<columna que vamos a modificar>` = `<valor>` WHERE `<condición>`

Con esto tenemos a todos nuestro usuarios activos.

## CRU(D) - Delete

Para terminar de tener nuestro CRUD es necesario saber como eliminar datos, para ello debemos utilizar el comando `DELETE`, también usando el id para seleccionar el dato en particular, quedando de la siguiente manera.

```sql
 DELETE from users where id = 2;
```

> DELETE from `<tabla>` where `<condición>`

Ya eliminamos un dato de nuestra base de datos, así también podemos eliminar todos los otros datos con una simple comprobación.

```sql
DELETE from users where id < 6;
```

Como todos los id cumplen con esa condición, serán eliminados. Hecho esto podemos volver a usar los mismos comandos anteriores para volver a generar los usuarios, y veremos como el id en vez de empezar en `1` empieza en `5`, ya que el ultimo que creamos tenia un id de `4`.

## Join

Uno de las funciones más importantes de SQL es la posibilidad de unir dos tablas referenciando datos entre ellas. Para ello debemos crear una nueva tabla en la que tomaremos el id de los usuarios como referencia de la siguiente manera.

```sql
create table product (
    id INT not null,
    product_name varchar(50) not null,
    created_by int not null,
    brand varchar(50) not null,
    category varchar(50) not null,
    primary key(id),
    foreign key(created_by) references users(id)        -- Indicamos que el valor "created_by" será una clave que tomaremos de la tabla a la que referenciamos
);
```

Pero en este caso tenemos un problema de sintaxis, ya que escribimos `product` en el nombre de la tabla en vez de `products`, para ello podemos usar `rename` y renombrar nuestra tabla de la siguiente manera.

```slq
rename table product to products;
```

Ahora podemos usar `SELECT` para seleccionar nuestra tabla y ver que el nombre se cambió, pero no tiene datos, es por eso que los agregaremos antes de seguir.

```sql
insert into products (product_name, created_by, brand, category) 
values 
    ('phone', 5, 'samsung', 'phone'),
    ('phone', 6, 'samsung', 'phone'),
    ('earbuds', 6, 'samsung', 'earbuds'),
    ('case', 6, 'samsung', 'accessories'),
    ('charger', 7, 'google', 'accessories'),
    ('phone', 7, 'google', 'phone'),
    ('case', 8, 'xiaomi', 'accessories');
```

Teniendo ambas tablas creadas podemos empezar seleccionando el id y el nombre de los usuarios de la tabla de usuarios de la siguiente manera.

```sql
select user_table.id, user_table.name from users as user_table;
```

En este caso hicimos uso de `as` para nombrar a la tabla de usuarios como `user_table`, seguido de esto podemos tomar los datos de la tabla de productos y unirlos usando `left join` de la siguiente manera.

```sql
select user_table.id, user_table.name, product_list.product_name, product_list.brand from users as user_table left join products as product_list on user_table.id = product_list.created_by;
```

> select <`datos para las columnas`> from <`tabla`> as <`apodo de la tabla`> left join <`que tabla unimos`> as <`el apodo`> on <`dato de la foreign key a comparar`>;

Explicando un poco la query tenemos seleccionados los datos de ambas tablas, a las cuales asignamos nombres para reconocerlos mejor, y utilizamos `left join` para que nos traiga TODOS los datos que tiene la primer tabla, aún cuando no estén linkeados a ningún dato de producto.  
Su contraparte sería `right join` para que la tabla con más importancia sea la tabla de productos.  
Por ultimo también podemos usar `inner join`, el cual solo trae los datos que coincidan en ambas tablas.

## Cross join

Por ultimo tenemos `cross join`, el cual toma todas las filas de una columna y las une con todas las filas de la otra, sin realizar una relación entre ellas. Hay que tener cuidado al usar esto ya que la respuesta puede ser muy larga dependiendo de la cantidad de filas que tengan nuestras columnas.

```sql
select user_table.id, user_table.name, product_list.product_name, product_list.brand from users as user_table cross join products as product_list;
```
