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
    <input type="text" id="idPost" name="idPost">
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

## Referencias

[FreeCodeCamp](https://www.freecodecamp.org/learn/back-end-development-and-apis/)
[W3school](https://www.w3schools.com/nodejs/default.asp)
