# MongoDB

[MongoDB](https://www.mongodb.com/) es una base de datos NoSQL utilizada mayormente para tener stacks entre el front (Angular, React, Vue, etc.) y el back (NodeJS y Express), conformando los diferentes stacks modernos (MERN, MEAN, MEVN).  

## Configuración

> Antes de empezar a usar MongoDB debemos tener nuestro proyecto con [Node](../../BackEnd/NodeJS/NodeJS.md) creado anteriormente

Con esto hecho, podemos empezar yendo a la pagina de [MongoDB](https://www.mongodb.com/) y creamos una cuenta/iniciamos sesión. Empezamos creando nuestra primer base de datos (`build a database`), eligiendo el servicio compartido (`shared`), bajamos y podemos continuar (`create cluster`) o cambiar el nombre del cluster. Luego de esto creamos nuestro usuario (`mongodb-test` en este caso) y generamos la contraseña automáticamente (`LhTWXkG4fHB5qGnK`).

> Es importante guardar estos datos aparte, ya que los necesitaremos para conectarnos luego.

Luego de crear el usuario elegimos el entorno local (`local environment`), en la lista de IPs agregamos una IP general (`0.0.0.0/0`), y confirmamos.  
El ultimo paso es ir a la pestaña de base de datos (`database`), elegir conectar (`connect`), conectar nuestra aplicación (`connect your application`) y copiar lo que nos indica Mongo (`mongodb+srv://<username>:<password>@<url>`), en el cual reemplazaremos el `<password>` con nuestra contraseña, y lo guardaremos para usarlo luego.

## Instalaciones

Hecho esto ya tenemos nuestra primer base de datos en MongoDB hecha y subida, por lo que podemos seguir con las instalaciones de paquetes que usaremos luego, empezando por el principal que será [`Mongoose`](https://mongoosejs.com/) como lo indica su [`documentación`](https://mongoosejs.com/docs/index.html).

```cmd

    npm i mongoose

```

Mongoose nos ayudará con las conexiones y el CRUD luego, facilitando el manejo de los datos.  
También es necesario saber que estaremos trabajando con datos sensibles como contraseñas y usuarios, es por eso que instalaremos [`Dotenv`](https://www.npmjs.com/package/dotenv), el cual nos ayudará con el manejo del archivo `.env`, en donde guardaremos nuestros datos sensibles. Para ello usaremos el siguiente comando.

```cmd

    npm i dotenv

```

## Conexión

Con los paquetes necesarios instalados podemos crear la primer conexión a nuestra base de datos. Empezamos creando una carpeta llamada `database`, la misma contendrá un archivo js llamado `db.js`, allí mismo tendremos que pasar nuestros datos de conexión como lo indica Mongoose.

```js

    const mongoose = require('mongoose');       // Llamamos a mongoose
    require('dotenv').config()      // Requerimos dotenv para poder usar las variables de entorno

    const mongooseDB = mongoose.connect(process.env.MONGODB_URI)        // Generamos la conexión en base a la URI de Mongo
        .then(console.log('database connection established'))       // Generamos la respuesta para saber que se estableció la conexión 

    module.exports = mongooseDB         // Exportamos la base de datos

```

## .env

Tenemos la conexión configurada, pero debemos pasar los datos, es por eso que crearemos un archivo al nivel de la raíz llamado `.env`, el cual agregaremos a nuestro `.gitignore` para que no se envié con los demás archivos. `.env` sirve para guardar variables privadas, las cuales pasaremos luego a nuestro deploy por separado.  
El primer dato que debemos agregar es nuestra URI, quedándonos de la siguiente manera (con los datos que nos dió Mongo).

```env

    MONGODB_URI = mongodb+srv://mongodb-test:<password>@cluster0.ylcagwq.mongodb.net/?retryWrites=true&w=majority

```

Con nuestra URI configurada debemos ver el mensaje que enviamos por consola, confirmando que la conexión fue exitosa.

## Schema

Es momento de crear nuestro esquema de usuario, el cual nos servirá para definir que datos le pasaremos a nuestra base de datos. Para ello empezamos creando una carpeta llamada `models`, en la que agregaremos el archivo js llamado `User.js`, configurando la base de ejemplo para nuestros datos.

```js

    const mongoose = require('mongoose');
    const { Schema } = mongoose;        // Importamos el esquema


    const userSchema = new Schema({         // Creamos un nuevo esquema
        name: String                    // Con el valor "name", de tipo "string"
    });


    module.exports = mongoose.model(         // Exportamos el esquema como modelo para usarlo en otro archivo
        'User',                              // Con el nombre que lo usaremos luego
        userSchema);                         // Y el esquema que tomaremos de referencia 

```

## (C)RUD - Create

Con las configuraciones hechas podemos crear nuestro primer usuario, basándonos en el modelo que usamos en la [`sección de NodeJS`](../../BackEnd/NodeJS/NodeJS.md). Empezamos yendo a `/routes/users.js`, y en el post crearemos nuestro primer dato para guardar, usando el método `.save()` de Mongoose de la siguiente manera.

```js

    require('../database/db')       // Importamos la base de datos
    const User = require("../models/User")      // Y el modelo que creamos

    router.post('/users', async (req, res) => {         // Creamos la función asíncrona ya que estaremos pidiendo datos
        try {                                       // Usamos un "try catch" 
            const userToDB = new User({             // Creamos el nuevo usuario en base al modelo que armamos
                ...req.body                     // Le pasamos los datos que enviamos por el body
            })
            await userToDB.save()               // Esperamos los datos y los guardamos en nuestra base de datos
            res.json({message: 'success'})      // Creamos un mensaje que nos indica que todo salio bien

        } catch (err) {
            console.error(err);             // y enviamos un error si hay algo que salio mal
        }
    })

```

Con esto creamos nuestro primer paso para el CRUD, pudiendo crear un dato en nuestra base de datos.
