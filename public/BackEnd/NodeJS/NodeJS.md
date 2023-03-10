# NodeJS

[NodeJS](https://nodejs.org/es/) es un entorno de ejecución en el lado del servidor, basado en JavaScript, el cual soporta una gran carga de procesos y peticiones simultáneas, con un tiempo de respuesta muy corto. El mismo es uno de los más utilizados a la hora de crear un servidor back-end, pudiendo hacer uso de `paquetes npm`.

## Guía de Temas

1. [Instalación](#instalación)
2. [Express](#express)
3. [Configuración de entorno](#configuración-del-entorno)
    - [Nodemon](#nodemon)
4. Código básico de Node
    - [Primeros pasos](#coding)
    - [Métodos](#métodos)
    - [Static Pages](#static-pages)
    - [Middlewares](#middlewares)
    - [Rutas](#declaración-de-rutas)
5. Obtención de datos
    - [Params](#datos-desde-params)
    - [Query](#datos-desde-query)
    - [Body](#datos-desde-body)
6. Base de datos con Mongoose
    - [Introducción a Mongoose](#mongoose)
    - [Conectar base de datos](#conectar-mongo)
7. CRUD de datos en MongoDB con Mongoose
    - [¿Que es CRUD?](#crud--clae)
    - [(C)RUD - Create](#crud---create)
    - [C(R)UD - Read](#crud---read)
    - [CR(U)D - Update](#crud---update)
    - [CRU(D) - Delete](#crud---delete)
8. [MVC](#mvc)
    - [Routes](#routes)
    - [Controllers](#controllers)
9. [Final](#cierre)

---

## Instalación

Para iniciar el uso de `NodeJS` es necesario instalarlo en nuestro dispositivo, para ello se tendrá que acceder a su [página web](https://nodejs.org/es/) e instalar la versión recomendada para su sistema, ignorando la última versión, ya que en su mayoría agregan [funcionalidades nuevas](https://node.green/) pero están en una versión de pruebas.  
Al final la instalación es recomendado reiniciar la PC, luego de ello podemos comprobar su instalación desde [la consola](https://linube.com/ayuda/articulo/174/abrir-una-consola-de-comandos#:~:text=Windows%20y%20Mac.-,En%20Windows,En%20ella%20debes%20escribir%20cmd.) con el siguiente comando.

```cmd
node -v
```

Esto devolverá la versión actual de Node.

## Express

[ExpressJS](https://expressjs.com/) es un framework diseñado para Node que nos ayuda a crear aplicaciones grandes con módulos propios, trabajando con las peticiones y respuestas HTTP para gestionar las rutas y endpoints. Actualmente es difícil ver un entorno de Node que no utilice Express, es por ello que vamos a instalarlo como lo indica su [documentación](https://expressjs.com/en/starter/installing.html).

```cmd
npm install express
```  

## Configuración del entorno

Para comenzar a utilizar Node con Express debemos configurar un entorno de pruebas. Para ello empezaremos creando una carpeta dedicada a nuestro entorno y abriremos la misma en nuestro editor. Luego de esto debemos utilizar el siguiente comando para iniciar el entorno.

```cmd
npm init -y
```

Este comando creará nuestro archivo `package.json`, este contiene toda la configuración y datos de nuestro proyecto, desde el nombre del autor hasta los paquetes que utilizaremos en el mismo. Estos datos se generaron automáticamente por el uso de la flag `-y`, pero es posible editarlas al crearlo en un inicio sin colocar la flag, o podemos editarlo ahora mismo en el archivo en cuestión.

## Nodemon

Ya que estamos hablando de los paquetes, para probar nuestro servidor vamos a instalar el paquete llamado `Nodemon`, el cual funciona escuchando nuestro servidor y sus cambios, sin que sea necesario cerrarlo y levantarlo cada vez que querramos mostrar algún cambio. Para instalar el mismo lo haremos como lo indica su [documentación](https://www.npmjs.com/package/nodemon), con el siguiente comando.

```cmd
npm i nodemon -D
```

> En este caso la flag `-D` indica que solamente se instalará como dependencia de desarrollo.

Con el paquete instalado podemos ver que en nuestro `package.json` se generó una nueva dependencia para Nodemon, indicando que será necesario instalarlo para su uso como dependencia.  
El siguiente paso será crear el script que dará inicio a Nodemon, para ello iremos al apartado llamado `scripts` y crearemos el script de la siguiente manera.

```json
"scripts": {
    "dev": "nodemon app.js"
}
```

Lo que indica este script es que usaremos Nodemon para ver el archivo `app.js`, que será el archivo principal de nuestro servidor, el que crearemos en el siguiente paso, pero antes de eso agregaremos otro script llamado `start` de la siguiente manera.

```json
"scripts": {
    "dev":"nodemon app.js",
    "start": "node app.js"
}
```

`start` es el script default que se utilizará para dar inicio al servidor, pero a diferencia de Nodemon este debe ser iniciado cada vez que hagamos algún cambio en el código.

## Coding

Ahora que tenemos todo configurado es momento de pasar a probar nuestro código, para ello creamos a la altura de la raíz del directorio un archivo llamado `app.js`, en el mismo crearemos nuestro primer servidor de la siguiente manera.

```js
const express = require('express');         // Importamos express
const app = express();      // Y creamos la variable app iniciando express

app.listen(3000, () => {        // Con ello creamos nuestro servidor en el puerto 3000
    console.log('listening on port 3000');      // Y creamos un log en consola para ver que todo esté funcionando
})
```

Para probar el mismo debemos ingresar `npm run dev` en la consola, luego de ello debemos dirigirnos a `https://localhost:3000/` y ver como se imprime el texto que indicamos anteriormente.

## Métodos

Con el servidor iniciado podemos crear nuestras primeras respuestas a los métodos más utilizados `GET, POST, PUT, DELETE`, siendo el primero que utilizaremos el GET. Para ello debemos indicar que usaremos el mismo desde `app` de la siguiente manera.

```js
const express = require('express');
const app = express();

app.get("/", (req, res) => {        // Escuchamos el método GET de la página principal
    res.send("hello world!")        // Y le indicamos que le devolveremos
})

app.listen(3000, () => {
    console.log('listening on port 3000');
})
```

De momento esto nos devolverá el string `hello world!` en pantalla cuando ingresemos en `https://localhost:3000`, pero no es lo único que podemos devolver, también es posible devolver un json como respuesta de la siguiente manera.

```js
const express = require('express');
const app = express();

app.get("/", (req, res) => {
    res.json({"text" : "hello world!"})
})

app.listen(3000, () => {
    console.log('listening on port 3000');
})
```

## Static pages

Como podemos ver, hay diferentes tipos de respuesta que podemos dar, pero estas son unicamente strings sin formato siquiera, pero esto puede cambiar si enviamos un archivo estático desde el back como página principal, un archivo HTML con su respectivo CSS. Para esto debemos crear una carpeta llamada `views` y dentro de la misma el archivo `index.html`. Aquí podemos crear nuestro HTML como querramos, pero para este ejemplo rápido usaremos un template que nos ofrece [w3School en su página web]("https://www.w3schools.com/w3css/tryit.asp?filename=tryw3css_templates_coming_soon&stacked=h"). Luego, debemos indicar que enviaremos el archivo `index.html` como middleware (explicado luego de este punto) de la siguiente manera.

```js
const express = require('express');
const app = express();
const path = require('path');       // Requerimos path para buscar el archivo

app.use(express.static(         // Creamos el middleware con `use` y luego usamos static
    path.join(__dirname, 'views')       // Y le indicamos donde está nuestro archivo principal
))

app.listen(3000, () => {
    console.log('listening on port 3000');
})
```

Hecho esto podemos ingresar en nuestro localhost y ver como nos devuelve el archivo con sus respectivos estilos.

## Middlewares

Anteriormente vimos que, aunque no indicamos que se use un método GET de nuestra página principal podemos mostrar el archivo estático con el uso de `.use`, esto es conocido como `middleware`, un middleware es un método que intercepta los pedidos que se envían por nuestras páginas y poder manipularlos de diferentes maneras, ya sea simplemente generar un log en consola hasta hacer comprobaciones de los datos. Para ver su funcionamiento crearemos un middleware simple que nos ayude a ver los métodos que se utilizaron, además de la hora a la que se enviaron los mismos.

```js
const express = require('express');
const app = express();
const path = require('path');


// Middleware de información

app.use((req, res, next) => {                   // Los middlewares SIEMPRE van antes que cualquier ruta
    console.log(`${req.method}, at ${new Date().toString()}`)       // Creamos la función del mismo
    next();         // E indicamos que siga con la ruta
})


// Archivos estáticos

app.use(express.static(
    path.join(__dirname, 'views')
))


// Puertos

app.listen(3000, () => {
    console.log('listening on port 3000');
})
```

Como no indicamos puntualmente en donde se utilizará este middleware, el mismo funcionará para todos los métodos que estén debajo del mismo, indicando en consola el método utilizado y la hora local del pedido.

## Declaración de rutas

Pudimos ver que los middlewares funcionan antes de todas las rutas, para probar esto podemos crear diferentes rutas, cada una ocn su respectiva respuesta. Para este ejemplo nos olvidaremos del archivo estático y crearemos una ruta principal, una ruta de información y una ruta de contacto de la siguiente manera.

```js
const express = require('express');
const app = express();
const path = require('path');


// Middleware de información

app.use((req, res, next) => {
    console.log(`${req.method}, at ${new Date().toString()}`)
    next();
})


// Rutas

app.get("/", (req, res) => {
    res.json({
        "text": "hello world!"
    })
})

app.get("/info", (req, res) => {
    res.send("general info")
})

app.get("/contact", (req, res) => {
    res.send("contact page")
})


// Puertos

app.listen(3000, () => {
    console.log('listening on port 3000');
})
```

Al ir a cualquiera de estas páginas podemos ver como se imprime en consola todos los métodos utilizados y la hora a la que se hizo la petición, pudiendo ver el accionar del middleware.  
Hasta ahora solo vimos como mostrar respuestas a páginas declaradas, pero si se quisiera entrar en una página que no esté declarada solo tendríamos un error genérico, pero esto podemos modificarlo para mostrar una página personalizada cuando no se encuentre la ruta en particular, al final de las rutas, quedando de la siguiente manera.

```js
// [...]        (Resto del código)

app.get("/contact", (req, res) => {
    res.send("contact page")
})

app.use((req, res) => {             // Lo indicamos al final de cada ruta
    res.status(404)         // Enviamos un status 404 para el navegador
        .send("Error 404!, no se encontró la página solicitada")        // Y lo que queremos enviar como respuesta
})


// Puertos

app.listen(3000, () => {
    console.log('listening on port 3000');
})
```

## Datos desde Params

Algo muy importante del lado del servidor es la posibilidad de recibir datos desde la misma URL, a esto se lo llama tomar los datos por `params`, pudiendo definir los parámetros que se tomarán desde que creamos la ruta. Por ejemplo, si queremos ingresar a los datos de un user podemos utilizar `/user/:username`, siendo `:username` el parámetro que cambiará cuando el usuario lo indique, creando la ruta de la siguiente manera.

```js
//  [...]

// Archivos estáticos

app.use(express.static(
    path.join(__dirname, 'views')
))


// Rutas

app.get("/users/:username", (req, res) => {             // Indicamos donde se tomará el parámetro
    console.log({"username": req.params.username})      // Hacemos un log del username
    res.send(`Bienvenido ${req.params.username}`)       // Y lo devolvemos como respuesta
})

app.get("/contact", (req, res) => {
    res.send("contact page")
})

//  [...]
```

Para ver un ejemplo de esto podemos ir a `https://localhost:3000/users/moon` y ver como se toma el username `moon` para la respuesta.

> Es posible tomar más de un dato desde los params, indicandolo al momento de crear la ruta.

## Datos desde Query

Así como podemos tomar los datos desde los parámetros, también podemos pedir datos como `queries`, las queries son datos que se envían luego de la llamada a la ruta, los cuales se indican con un signo de interrogación (`?`), indicando el nombre de la variable y el valor, pudiendo indicar más de una variable con el uso del símbolo `&`. La ruta no necesita pedir los datos puntualmente como se hizo con los params, pero si se pueden pedir los mismos al momento de crear la ruta de la siguiente manera.

```js
//  [...]

app.get("/user", (req, res) => {
    console.log({ "username": req.query.username, "id": req.query.id })     // Utilizamos los mismos datos que antes, pero tomaos desde la query
    res.send(`Bienvenido ${req.query.username}`)
})

//  [...]
```

Para comprobar que esto funciona debemos ir a la ruta `https://localhost:300/user?username=moon&id=pfar1835`, y ver como esto se imprime en pantalla

## Datos desde Body

Pro ultimo tenemos una forma más "privada" (pero no completamente segura) para enviar los datos, ya que si se comparte el dispositivo se puede ver que queda en el historial el link con los datos. Para evitar esto podemos hacer uso del body del request, pero los datos necesitan pasar por un middleware que nos provee Express antes de poder obtenerlos, por lo que el código nos quedará de la siguiente forma.

```js
//  [...]


// Middlewares

app.use(express.urlencoded({        // Indicamos el middleware al inicio del código
    extended: false
}))

//  [...]

app.post("/user", (req, res) => {       // Creamos la respuesta al método POST del servidor
    console.log(req.body)               // Tomamos los datos enviados por el usuario
    res.json({
        'user': req.body.usernamePost       // Y generamos la respuesta
    })
})

//  [...]
```

A diferencia de las queries o los params, para probar esto será necesario hacer uso de un gestor de peticiones como puede ser [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) en Visual Studio Code, y enviando los datos como formulario, pero también es posible hacerlo a traves de un formulario en el lado del cliente. Para ello lo primero que haremos será agregar un formulario simple a nuestro `index.html` de la siguiente manera.

```html
<form action="/user" method="post">         <!-- Indicamos la ruta y el método que utilizaremos -->
    <input type="text" id="usernamePost" name="usernamePost">       <!-- E indicamos en el name el nombre de la variable que escribimos cuando pedimos desde el body en el lado del servidor -->
    <input type="number" id="idPost" name="idPost">
    <button type="submit">Enviar</button>
</form>
```

Si indicamos los datos en el formulario y lo enviamos podemos ver en consola como se toman los datos, y como nos redirige a la página en cuestión.

## Mongoose

Para terminar nuestro mini proyecto con Express vamos a incluir MongoDB en el mismo con la ayuda de Mongoose. [MongoDB](https://www.mongodb.com/) es una de las bases de datos relacionales más utilizadas en la actualidad, usaremos la misma junto a [Mongoose](https://mongoosejs.com/), la cual es una librería ODM (Object Data Modeling) que nos facilita el uso y conexión de MongoDB con nuestro back-end, dándonos una serie de funciones puntuales para crear nuestro CRUD.  
Para comenzar a usar Mongoose debemos instalarlo en nuestro proyecto como lo indica su [documentación](https://mongoosejs.com/docs/index.html).

```cmd
npm i mongoose
```

## Conectar MongoDB

Lo primero que debemos hacer será crearnos una cuenta en MongoDB y una base de datos, para ello podemos seguir el [tutorial de FreeCodeCamp](https://www.freecodecamp.org/news/get-started-with-mongodb-atlas/), hecho esto será necesario agregar nuestra URI de MongoDB a un archivo `.env` para que la misma quede oculta. Para ello comenzamos creando el archivo `.env` a nivel de la raíz de nuestro proyecto, luego de esto debemos crear un archivo llamado `.gitignore`, el cual tomará las reglas de que archivo ignorar a la hora de subir un repositorio a GitHub. Normalmente este mismo se compone de las siguientes lineas.

```gitignore
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
lerna-debug.log*

node_modules
dist
dist-ssr
*.local
to-do-list.txt

# Editor directories and files
.vscode/*
!.vscode/extensions.json
.idea
.DS_Store
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?
.env
```

Ya con nuestro .env creado y el .gitignore configurado podemos guardar nuestra URI como variable privada de la siguiente manera.

```env
MONGO_URI="mongodb+srv://<username>:<password>@<cluster-name>.prx1c.mongodb.net/<db-name>?retryWrites=true&w=majority"
```

> La URI la podemos encontrar en el apartado de `connect` de nuestro cluster en MongoDB

También será necesario instalar un paquete de NPM para poder leer los datos de nuestro .env llamado `dotenv`, usando el comando que nos indica su [página](https://www.npmjs.com/package/dotenv).

```cmd
npm i dotenv
```

Con esto instalado podemos conectar nuestro Cluster al proyecto de la siguiente manera.

```js
const express = require('express');
const app = express();
const path = require('path');
const mongoose = require('mongoose');       // Importamos Mongoose
require("dotenv").config()          // Y dotenv para manejar nuestras variables privadas


// MongoDB

mongoose.set('strictQuery', false);         // Suprimimos el warning (ver. < Mongoose v7)

mongoose.connect(process.env.MONGO_URI, {       // Usamos .connect de Mongoose y le indicamos nuestra URI
    useNewUrlParser: true,
    useUnifiedTopology: true                    // Junto a sus configuraciones
})


// Middlewares

app.use(express.urlencoded({
    extended: false
}))


// Archivos estáticos

app.use(express.static(
    path.join(__dirname, 'views')
))


// Rutas

app.use((req, res) => {
    res.status(404)
        .send("Error 404!, no se encontró la página solicitada")
})


// Puertos

app.listen(3000, () => {
    console.log('listening on port 3000');
})
```

## CRUD / CLAE

CRUD son las siglas para Create (Crear), Read (Leer), Update (Actualizar) y Delete (Eliminar), las 4 operaciones básicas que se realizan en una base de datos para trabajar con los datos almacenados. En este caso haremos uso del mismo para crear una base de datos que guarde usuarios, la cual podremos modificar a medida que lo necesitemos. Para empezar a utilizar el CRUD debemos crear nuestros usuarios, es decir, empezar con Create de CRUD.

## (C)RUD - Create

Para empezar a crear y subir los datos debemos crear una carpeta para guardar los Schemes. Los Schemes son los bloques que contendrá un modelo para enviarse a la base de datos, siendo similar a las `Interfaces` de TypeScript. Para comenzar con ello debemos crear una carpeta llamada `models`, y dentro de la misma un archivo llamado `user.js`. En este crearemos nuestro modelo de usuario a crear de la siguiente manera.

```js
const mongoose = require('mongoose')        // Requerimos mongoose para pedir sus métodos

let userSchema = new mongoose.Schema({      // Creamos un nuevo esquema con el nombre que indicamos
    username: {                             // Creamos el dato que contendrá el mismo
        type: String,                       // Indicamos el tipo de dato que será
        required: true,                     // Indicamos que sera obligatorio
        unique: true                        // Y que no se podrá repetir
    },
    id: {
        type: Number,
        required: true,
        unique: true
    },
})

module.exports = mongoose.model('User', userSchema)     // A final exportamos el modelo para poder usarlo en otra parte del proyecto
```

Teniendo nuestro primer modelo de usuario hecho podemos volver al archivo principal en donde lo llamaremos y haremos uso del método POST para pasarle los datos desde el formulario y subirlo a nuestra base de datos, quedando de la siguiente manera.

```js
const express = require('express');
const app = express();
const path = require('path');
const mongoose = require('mongoose');
require("dotenv").config()
const userModel = require("./models/user")      // Importamos el modelo que usaremos luego

// MongoDB

mongoose.set('strictQuery', false);

mongoose.connect(process.env.MONGO_URI, {
    useNewUrlParser: true,
    useUnifiedTopology: true
})


// Middlewares

app.use(express.urlencoded({
    extended: false
}))


// Archivos estáticos

app.use(express.static(
    path.join(__dirname, 'views')
))


// Rutas

app.post("/user", (req, res) => {         // Usamos el mismo post que configuramos anteriormente
    try {   
        const user = new userModel({            // Creamos el user con sus respectivos datos
            username: req.body.usernamePost,
            id: req.body.idPost
        })
        user.save((err) => {          // Lo guardamos en la base de datos
            if (err) console.error(err)     // Y comprobamos que no haya errores
        })
        res.json({
            username: req.body.usernamePost,
            id: req.body.idPost,
            status: "saved on db"
        })
    } catch (error) {
        console.log(error)
    }
})

//  [...]
```

Esta forma funciona siempre y cuando querramos guardar solo un dato, pero si tenemos un array de datos será necesario usar el método `.create()` de la siguiente manera.

```js
//  [...]

app.post("/user", (req, res) => {
    try {
        userModel.create([{       // Usamos create y le pasamos un array de datos para subir
            username: "John",
            id: 1234
        }, {
            username: "Johnny",
            id: 123456
        }], (err) => {
            if (err) console.error(err)
        })
        res.json({
            username: req.body.usernamePost,
            id: req.body.idPost,
            status: "saved on db"
        })
    } catch (error) {
        console.log(error)
    }
})

//  [...]
```

## C(R)UD - Read

Ya tenemos configuradas dos formas de subir (create) datos a nuestra base de datos, ahora es momento de poner en practica la lectura (read) de la base de datos, pidiendo los mismos que subimos anteriormente. Para ello haremos uso del método `.find()` de la siguiente manera.

```js
//  [...]

app.post("/user", (req, res) => {
    try {
        userModel.find(({                       // Usamos find para buscar en la base de datos
            username: req.body.usernamePost     // Y le pasamos el dato a comparar
        }), (err, docs) => {
            if (err) console.error(err);
            console.log(docs);               // Imprimimos los datos en consola
            res.json({
                user: docs[0].username      // Y devolvemos el primer resultado
            })
        })
    } catch (error) {
        console.log(error)
    }
})

//  [...]
```

En este caso, `.find()` nos devuelve un array de coincidencias, es por eso que en el caso de querer traer solamente un dato de la base de datos utilizamos `.findOne()` de la siguiente manera.

```js
//  [...]

app.post("/user", (req, res) => {
    try {
        userModel.findOne(({                       // Usamos find para buscar en la base de datos
            username: req.body.usernamePost     // Y le pasamos el dato a comparar
        }), (err, doc) => {
            if (err) console.error(err);
            console.log(doc);               // Imprimimos el dato en consola
            res.json({
                user: doc.username      // Y devolvemos el resultado
            })
        })
    } catch (error) {
        console.log(error)
    }
})

//  [...]
```

Sumado a esto, si queremos ser más puntuales con la búsqueda de un dato podemos hacerlo a través del ID que se genera automáticamente cuando creamos un dato. Para esto usaremos el método `.findById()`, siendo este es el más usado para traer solo un dato, quedando la llamada de la siguiente manera.

```js
//  [...]

app.post("/user", (req, res) => {
    try {
        userModel.findById("63d81bc4495a547b6a89e287"), (err, doc) => {         // Le pasamos el _id generado por MongoDB
            if (err) console.error(err);
            console.log(doc);               // Imprimimos el dato en consola
            res.json({
                user: doc.username      // Y devolvemos el resultado
            })
        }
    } catch (error) {
        console.log(error)
    }
})

//  [...]
```

> Hay que tener en cuenta que todos los métodos de `.findById()` en si toman la base de `.findOne({_id: id})`

## CR(U)D - Update

Ademas de crear los datos también podemos modificarlos en la base de datos. Para ello haremos uso del método `.findOneAndUpdate()`, el mismo nos pedirá los datos a cambiar en el momento que lo llamemos, quedando el mismo de la siguiente manera.

```js
//  [...]

app.post("/user", (req, res) => {
    try {
        userModel.findOneAndUpdate({ username: req.body.usernamePost },         // Pasamos la condición como primer parámetro
        { id: 55905 },      // Como 2do parámetro pasamos lo que queremos editar
        { new: true },      // Y si queremos que nos devuelva el documento editado pasamos { new : true}
        (err, updatedDoc) => {
            if (err) console.error(err);
            res.send({
                updatedDoc
            })
        })
    } catch (error) {
        console.log(error)
    }
})
        
//  [...]
```

Como lo vimos anteriormente, también podemos buscar por ID y editarlo, cambiando el método `.findOneAndUpdate()` por el método `.findByIdAndUpdate()`, y pasando el Id como primer parámetro.

## CRU(D) - Delete

Por ultimo nos queda la función de eliminar nuestros datos de la base de datos. Para ello seguiremos la misma base que teníamos hasta el momento, pero para ello usaremos `.findByIdAndDelete()`, la cual recibe el ID del dato para buscarlo.

```js
//  [...]

app.post("/user", (req, res) => {
    try {
        userModel.findByIdAndDelete(id, (err, data) => {        // Le pasamos el id del dato
            if (err) console.error(err);
            res.send({
                data,                   // Imprimimos el dato eliminado
                msg: "deleted!"
            })
        })
    } catch (error) {
        console.log(error)
    }
})

//  [...]
```

También es posible eliminar varios datos a la vez, utilizando `.remove()` y pasando el dato que comparten estos datos.

```js
//  [...]

app.post("/user", (req, res) => {
    try {
        userModel.remove(({
            age: 20             // Indicamos que dato comparten todos los que eliminaremos
        }), (err) => {
            if (err) console.error(err);
            res.send({
                msg: "datos eliminados"
            })
        })
    } catch (error) {
        console.log(error)
    }
})

//  [...]
```

## MVC

Por ultimo podemos explicar el patrón `MVC (model - view - controller / modelo - vista - controlador)`, el cual es un patrón de arquitectura que separa y organiza las funcionalidades de nuestro proyecto en 3 diferentes secciones, `Models`, el cual se encarga de los modelos de las bases de datos, como lo vimos cuando configuramos nuestro [CRUD](#crud---create), `Views`, el cual se encarga de todas las vistas que tendremos en nuestro front, es decir, todo lo que el usuario recibe e interactúa, esto también lo vimos cuando creamos nuestro HTML para enviarlo como [página estática](#static-pages), y por ultimo los `Controllers`, el cual se encarga de controlar las respuestas de nuestras rutas, como lo vimos desde el principio de nuestro proyecto.  
Gracias a este patrón tenemos un mejor control de todo, pudiendo ver claramente la división entre las rutas y sus funciones, facilitándonos algún cambio a futuro.

## Routes

Es momento de crear nuestras rutas, para ello necesitaremos crear la carpeta `routes` a nivel de la raíz, y dentro de la misma creamos el archivo `userRoutes.js`, a la cual enviaremos todas nuestras rutas anteriormente creadas de la siguiente manera.

```js
const express = require('express');             // Importamos Express
const router = express.Router()                 // Y el router de Express
const userModel = require("../models/user")     // De momento importamos el modelo para comprobar que funciona

router.get("/", (req, res) => {                 // Cambiamos app por router y "/users" por raíz
    userModel.find((err, docs) => {
        if (err) return console.error(err)
        res.send(docs)
    })
})

router.post("/", (req, res) => {
    try {
        const user = new userModel({
            username: req.body.usernamePost,
            id: req.body.idPost
        })
        user.save((err) => {
            if (err) console.error(err)
        })
        res.json({
            username: req.body.usernamePost,
            id: req.body.idPost,
            status: "saved on db"
        })
    } catch (error) {
        console.log(error)
    }
})

router.put("/user", (req, res) => {
    try {
        userModel.findOneAndUpdate({
            username: req.body.usernamePost
        }, {
            id: 55905
        }, {
            new: true
        }, (err, data) => {
            if (err) console.error(err);
            res.send({
                data
            })
        })
    } catch (error) {
        console.log(error)
    }
})


router.delete("/", (req, res) => {
    try {
        userModel.remove(({
            age: 20
        }), (err, data) => {
            if (err) console.error(err);
            res.send({
                data
            })
        })
    } catch (error) {
        console.log(error)
    }
})

module.exports = router;            // Y al final exportamos las rutas
```

> Es posible crear un middleware que solo afecte a la ruta en cuestión, creándola dentro de este archivo mismo archivo.

Con esto hecho ya separamos las rutas principales de `"/users"`, ahora debemos importarlas en nuestro `index.js` de la siguiente manera.

```js
const express = require('express');
const app = express();
const path = require('path');
const mongoose = require('mongoose');
require("dotenv").config()

const userRoutes = require("./routes/userRoutes")       // Importamos las rutas


//  [...]


// Rutas

app.use("/users", userRoutes)       // Y le indicamos que ruta tomará como base, pasando las rutas como 2do parámetro

app.use((req, res) => {
    res.status(404)
        .send("Error 404!, no se encontró la página solicitada")
})


//  [...]
```

## Controllers

Lo ultimo que nos queda por separar serían los controladores, para los cuales debemos crear una carpeta a nivel raíz llamado `controllers`, y dentro de la misma crearemos el archivo `userControllers.js`, dentro del cual colocaremos nuestros controladores de la siguiente manera.

```js
const userModel = require("../models/user")         // Importamos los modelos

module.exports = {                      // Creamos el objeto a importar


    // Create users

    users_createNewUser: (req, res) => {            // Y creamos cada controlador que usaremos en las rutas
        try {
            const user = new userModel({
                username: req.body.usernamePost,
                id: req.body.idPost
            })
            user.save((err) => {
                if (err) console.error(err)
            })
            res.json({
                username: req.body.usernamePost,
                id: req.body.idPost,
                status: "saved on db"
            })
        } catch (error) {
            console.log(error)
        }
    },


    // Read users

    users_getAllUsers: (req, res) => {
        userModel.find((err, docs) => {
            if (err) return console.error(err)
            res.send(docs)
        })
    },


    // Update users

    users_updateOneUser: (req, res) => {
        try {
            userModel.findOneAndUpdate({
                username: req.body.usernamePost
            }, {
                id: 55905
            }, {
                new: true
            }, (err, data) => {
                if (err) console.error(err);
                res.send({
                    data
                })
            })
        } catch (error) {
            console.log(error)
        }
    },


    // Delete users

    users_deleteManyUsersByData: (req, res) => {
        try {
            userModel.remove(({
                age: 20
            }), (err, data) => {
                if (err) console.error(err);
                res.send({
                    data
                })
            })
        } catch (error) {
            console.log(error)
        }
    }

}
```

Con este cambio será necesario también cambiar las rutas para poder importar los controladores, por lo que nuestras rutas quedarán de la siguiente manera.

```js
const express = require('express');
const {
    users_createNewUser,
    users_getAllUsers,
    users_updateOneUser,
    users_deleteManyUsersByData
} = require('../controllers/userControllers');      // Importamos lo que necesitemos desde los controladores
const router = express.Router()


// Create users

router.post("/", users_createNewUser)               // Y cambiamos las rutas para que tomen los controladores


// Read users

router.get("/", users_getAllUsers)


// Update users

router.put("/user", users_updateOneUser)


// Delete users

router.delete("/", users_deleteManyUsersByData)


module.exports = router;
```

## Cierre

Con todo esto hecho vimos desde como se inicia un proyecto con Node y Express hasta como configurar una base de datos para usar su CRUD con su respectivo MVC, pero a la vez abrimos varias posibilidades para realizar diferentes proyectos, desde un gestor de usuarios simples hasta un e-commerce completo.

## Referencias

[FreeCodeCamp](https://www.freecodecamp.org/learn/back-end-development-and-apis/)
[W3school](https://www.w3schools.com/nodejs/default.asp)
