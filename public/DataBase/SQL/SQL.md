# SQL

SQL (Structured Query Language / Lenguaje de consulta estructurado) es un tipo de lenguaje que permite la comunicación de un usuario a una base de datos mediante queries. Las bases de datos SQL son bases de datos estructuradas en forma de tablas, siendo conformadas por lineas verticales (Columnas) y lineas horizontales (Registros), las cuales se llenan con la información que guardemos en las mismas.  

| id | name  | age | active |
|----|-------|-----|--------|
| 1  | jack  | 20  | true   |
| 2  | lisa  | 25  | true   |
| 3  | marie | 20  | false  |
| 4  | harry | 26  | true   |

Las tablas se generan con los datos que nosotros le asignemos, pero a su vez siempre tendrán un `id` que se genera automáticamente, el cual es autoincremental (incrementa el valor dependiendo el ultimo id generado).  
Estas tablas pueden compartir datos con otras tablas, ya que son `relacionales`, por ejemplo, podemos tener una tabla de usuarios que guarden productos en un cart, relacionando estos productos al id del usuario en particular.

| id | product   | qty | price | user_id |
|----|-----------|-----|-------|---------|
| 1  | pizza     | 2   | 15    | 1       |
| 2  | milk      | 1   | 20    | 1       |
| 3  | chocolate | 5   | 8     | 3       |

Como vemos, hay dos columnas de id, una de ellas (`id`) representa el id del producto en particular, pero también tenemos la columna de `user_id`, la cual representa el id del usuario que realizó el pedido.  
A estos dos tipos de id se los conoce como `Primary key - PK` (id que se genera en base) y `Foreign key - FK` (id que se toma desde otra tabla).  
Por ultimo, podemos necesitar que dos tablas compartan la misma información, para ello crearemos una tabla intermedia que se componga de un PK generado para la relación, y tomar las FK de las tablas que necesitemos para identificar los datos. Pongamos de ejemplo que nuestros usuarios tienen registrados descuentos, para ello creamos una base de datos con los descuentos disponibles.

| id | discount | %  | available |
|----|----------|----|-----------|
| 1  | senior   | 15 | true      |
| 2  | student  | 10 | true      |
| 3  | spring   | 5  | false     |

Y nuestros usuarios pueden tener el id relacionado dependiendo del descuento que posean, quedando nuestra 3ra tabla de la siguiente manera.

| id | user_id | discount_id |
|----|---------|-------------|
| 1  | 2       | 2           |
| 2  | 4       | 2           |

Como vemos, los usuarios tienen su columna particular (`user_id`) en la que se toma el id del mismo para poder reconocer que usuario tiene el descuento, y tenemos la columna de los descuentos (`discount_id`) para marcar que descuentos se aplicarán. Con esta información podemos ver que Lisa (`user con id 2`) tiene un descuento de estudiante (`descuento con id 2`), al igual que lo tiene Harry (`user con id 4`).  
Esta tabla esta compuesta por una PK (primer columna de id) y dos FK (los id que recuperan los datos desde otras tablas).
