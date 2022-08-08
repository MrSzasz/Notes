# NodeJS

[NodeJS](https://nodejs.org/es/) es un entorno de ejecución en el lado del servidor, basado en JavaScript, el cual soporta una gran carga de procesos y peticiones simultaneas, con un tiempo de respuesta muy corto.

## Instalación

Para iniciar el uso de `NodeJS` es necesario instalarlo en nuestro dispositivo, para ello se tendrá que acceder a su [pagina web](https://nodejs.org/es/) e instalar la version recomendada para su sistema, ignorando la ultima version, ya que en su mayoría agregan [funcionalidades nuevas](https://node.green/) pero están en una version de pruebas.
Luego de la instalación es recomendado reiniciar la pc, luego de ello es bueno abrir [la consola](https://linube.com/ayuda/articulo/174/abrir-una-consola-de-comandos#:~:text=Windows%20y%20Mac.-,En%20Windows,En%20ella%20debes%20escribir%20cmd.) y comprobar la version que se instalo de Node con el siguiente comando.

```cmd

    node -v

```

## Coding

Para probar el funcionamiento de `nodejs` podemos hacer un archivo con la extension `.js`, la misma utilizada por `JavaScript`, en el mismo podemos tener un `console.log()` común y corriente.

```js

    console.log('hola')

```

La diferencia en este caso es que, al ser `node`, este deberá ser ejecutado en [la consola](https://damiandeluca.com.ar/como-usar-la-terminal-integrada-de-visual-studio-code), para lo cual deberíamos abrirla (`ctrl + ñ` en VSC por default) y luego correr nuestro archivo con el siguiente comando.

```cmd

    node app.js

```

> No es necesario agregar la extension del archivo (`.js`) luego del comando `node`, funciona de ambas formas.

## Módulos

Es posible modularizar el código, llevando parte del código a otro archivo y luego llamándolo cuando sea necesario, esto es posible gracias a los `exports` y `requires`.  
Para poder crear nuestros propios módulos utilizaremos el `export` en el archivo que querramos que se pueda usar en otro lado.

```js

    const animals = ["🦊", "🐱", "🐶", "🦅", "🐢"]

    module.exports = animals

```

Y luego debe ser llamado con la palabra reservada `require`, en el cual ya puede ser utilizado con normalidad.

```js

    const animals = require("./animals")    //El require siempre requerirá el archivo sin ser necesario agregar la extension

    animals.forEach(anim => {
        console.log(anim)   // 🦊, 🐱, 🐶, 🦅, 🐢
    });

```

Sumado a esto también es posible exportar mas de un dato, basándose en la misma premisa para la exportación y su uso.

```js

    const animals = ["🦊", "🐱", "🐶", "🦅", "🐢"]
    const names = ["fox", "cat", "dog", "eagle", "turtle"]

    module.exports = {animals, names}

```

> En este caso es importante remarcar que datos se van a exportar dentro de los `{}`

El cambio que se hace al querer importarlos es el mismo, se debe aclarar todos los datos que van a usarse.

```js

    const {animals, names} = require("./animals")

    animals.forEach(an => {
        console.log(an)     // 🦊, 🐱, 🐶, 🦅, 🐢
    });

    console.log(`Hay un total de ${names.length} animales`)     // Hay un total de 5 animales

```

> También es posible exportar solo un dato si es el único que se va a utilizar

Node tiene incorporado unos cuantos módulos que se pueden utilizar con diferentes fines, es posible ver todos, leer su documentación en implementación [desde aca](https://nodejs.org/dist/latest-v16.x/docs/api/).  
Ademas es [posible instalar diferentes módulos](https://www.npmjs.com/), que sean necesarios para correr la app que se este creando, pero al momento de su ejecución en otros dispositivos serán necesarios instalarlos también.  
Esto se logra con un registro en formato `JSON` llamado `package.json`, el cual deja una descripción de nuestro proyecto junto a los paquetes que van a ser necesarios instalar para su correcto funcionamiento. Este mismo se crea automáticamente con el siguiente comando.

```cmd

    npm init -y

```

En el archivo que se creo es posible cambiar ciertos parámetros, siendo los mas importantes los siguientes.

- ***name***: Nombre del archivo.

- ***description***: Descripción del proyecto.

- ***main***: Archivo principal.

- ***scripts***: Scripts que usaremos para diferentes acciones, como iniciar el proyecto.

> Si no se usa `-y` con el `init` es posible ir uno por uno editando estos parámetros al momento de su creación.

Es importante saber que cada vez que se instala una dependencia se creara la propiedad `dependencies`, el cual deja en claro que dependencia (y version de la misma) se necesitara instalar.  
El apartado de `dependencies` registra las dependencias necesarias para el funcionamiento de la app, y cada una de ellas tendrá una version con un símbolo delante, los cuales tienen diferentes significados.

- `^` : Se actualizara el paquete unicamente en la version base => ^2.**34.56** (no pasa de la version 2).

- `~` : Se actualizaran solamente los parches del paquete => 2.34.**56** (No pasa de la version 2.34).

- `*` : Se actualizara por completo => **2.34.56** (Puede ir a la version 3).

> Al tener el `*` puede dar problemas si un paquete se actualiza, ya que pueden cambiar (o deprecar) código que se este utilizando en el proyecto.

Para probar la instalación de dependencias y paquetes se puede comenzar con la instalación de `nodemon`, el cual es un paquete que nos ayuda a la hora de probar nuestro código, ya que funciona como lo haría `live server` en HTML, actualizándose con cada cambio para no tener que estar constantemente corriendo la aplicación cada vez que la necesitemos.  
Para comenzar se deberá instalar `nodemon` como lo indica su [documentación](https://www.npmjs.com/package/nodemon) con el siguiente comando.

```cmd

    npm i nodemon

```

> También es posible instalarlo globalmente utilizando -`g`.

Luego de esto se agregara como dependencia y se creara la carpeta `node_modules`, la cual contiene todos los archivos necesarios para el funcionamiento de las diferentes dependencias. Esta carpeta no se debe de compartir cuando se sube a `Github`, por lo que es conveniente crear el archivo `.gitignore` y allí agregarla, escribiendo solamente el nombre de la carpeta.

```text

    node_modules
    
```

Como una linea de texto normal, automáticamente luego de iniciar `GIT` esta carpeta sera ignorada y no se subirá al repositorio. Esto mismo sera importante mas adelante cuando necesitemos agregar archivos privados.

Para el uso de `nodemon` se deberá crear un script en el apartado del mismo nombre dentro del archivo `package.json`, agregando una palabra que se utilizará para iniciarlo.

```json

    "scripts": {
        "dev": "nodemon app.js",    // Inicia el archivo con Nodemon
        "start": "node app.js"    // Inicia el archivo normalmente y se utilizará en su implementación automática
    }

```

Luego de esto, para iniciar el archivo se deberá utilizar el comando que creamos anteriormente, en este caso `npm run dev`.

## Servidor HTTP

El protocolo HTTP es el protocolo que permite la comunicación y transferencia de información de un cliente con el servidor. Para crear nuestro primer servidor sera necesario usar el modulo `HTTP` y darle las instrucciones de lo que se deberá escuchar y responder.

```js

    const http = require('http');   // Modulo requerido

    const server = http.createServer((req, res) => { 
        res.end("Esta es mi pagina :D");    // Esto es lo que se vera en la pagina cuando se inicie el servidor
    });

    const PORT = process.env.PORT || 5000;  // Puerto que usaremos para iniciar en el navegador
    server.listen(PORT, () => console.log("El servidor funciona a la perfección!!"));   // Log en consola para saber si el mismo esta en funcionamiento

```

Al iniciar el servidor con `npm run dev` (es decir, con `nodemon` como lo configuramos anteriormente) en la consola se deberá ver el mensaje que pusimos anteriormente, pero para probar si el mismo esta funcionando podemos ir a nuestro navegador y escribir `localhost:5000` (siendo 5000 el puerto que pusimos nosotros) para ver la respuesta del mismo (siendo `Esta es mi pagina :D` en este caso).  
Existen un conjunto de métodos importantes de HTTP, los cuales sirven para trabajar con los datos en el servidor, los mismos son los siguientes.

- ***GET***: LLama los datos de la base de datos.

- ***POST***: Agrega datos a la base de datos.

- ***PUT***: Sirve para modificar los datos en la base de datos.

- ***DELETE***: Este método se utiliza para eliminar un dato en la base de datos.

## Express

Luego de haber visto como se crea un servidor HTTP podemos pasar a usar `Express`, el cual es un paquete que nos ayuda y agiliza la creación de APIs solidas.  
Para ello lo primero que se deberá hacer es instalar `express` como lo dice en su [documentación](https://expressjs.com/en/starter/installing.html).

```cmd

    npm install express

```

> Aunque en la página se agregue `--save` al comando, desde versiones actuales de `npm` esto ya no es necesario.

Ahora que tenemos `express` instalado podemos pasar a la creación de un servidor con el mismo, para ello modificaremos el servidor que teníamos creado con anterioridad, agregando los `require` necesarios y la forma de escritura que nos proporciona `express` en su [documentación oficial](https://expressjs.com/en/starter/hello-world.html).

```js

    const express = require('express');     // Importa express
    const app = express();

    app.get('/', (req, res) => {
        res.send("Esta es mi pagina :D");       // Esto es lo que se vera en la pagina cuando se inicie el servidor
    })

    const PORT = process.env.PORT || 5000;      // Puerto que usaremos para iniciar en el navegador
    app.listen(PORT, () => console.log("El servidor funciona a la perfección!!"));      // Log en consola para saber si el mismo esta en funcionamiento

```

Al utilizar `npm run dev` se inicializara como lo hizo con el servidor anterior, la única diferencia visual sera que `express` tiene un formateo por detrás, el cual cambia la fuente por default.  
Aun asi, podemos hacer respuestas diferentes dependiendo de la pagina que se visite, no unicamente el directorio raíz (`/`), para esto se utilizará un middleware de express con la palabra reservada `use`.

```js

    app.use(express.static(__dirname + "/public"));

```

Para que esto funcione se deberá crear la carpeta `public`, la cual contendrá todos los archivos públicos del Front, como pueden ser los archivos de estilo (`css`), los scripts (`js`), etcetera.  
En el `index.html` se escribirá el código que se mostrara en la dirección raíz (`/`).

```html

    <!DOCTYPE html>
    <html lang="es">

    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>NODE TEST</title>

        <link rel="stylesheet" href="./styles/style.css">
    </head>

    <body>
        <h1>Bienvenidos a la pagina principal creada con NODEJS</h1>
    </body>

    </html>

```

También es posible usar el método `GET` para mandar información por URL y utilizarla luego, ya sea para redirigir a otro sitio o para hacer un request de esos datos. Esto se puede demostrar usando el método desde un formulario.

```HTML

    <form action="/form" method="GET">      <!-- Se define el método del envío de los datos, y con Action la pagina a la que se va a redirigir -->
            <input type="text" name="nombre" placeholder="nombre">
            <input type="text" name="apellido" placeholder="apellido">
            <button type="submit">Enviar</button>
    </form>

```

> El método `GET` es un método visible, asi que no se debería usar para enviar información sensible

Gracias a esto es posible enviar los datos al completar el formulario, para luego tomarlos con `node`.

```js

    const express = require('express');
    const app = express();

    app.use(express.static(__dirname + "/public"));     // Toma los archivos estáticos como plantillas

    app.get('/form', (req, res) => {        // Toma los datos al completar el formulario con el método GET
        console.log(req.query);     // Imprime los datos en consola, con formato de objeto 
        res.send('Formulario enviado!!')        // Esto es lo que se vera en la pagina "/form"
    })

    const PORT = process.env.PORT || 5000;
    app.listen(PORT, () => console.log("El servidor funciona a la perfección!!"));

```

> Los datos de `req.query` se verán con el formato de un objeto => { nombre: 'Tomas', apellido: 'Lugo' }

El método `GET`, al ser visible, es peligroso para enviar datos sensibles, es por eso que para esos casos se utiliza el método `POST`, el mismo envía los datos de la misma forma y se pueden interceptar para su uso, pero para el mismo cambia un poco la forma del mismo.  
En este caso los datos se envían a traves del `body`, no de la URL, es por eso que se tiene que usar un `middleware` para parsear los datos y poder recuperarlos, de lo contrario unicamente se recibiría como respuesta `undefined`.

```js

    app.use(express.static(__dirname + "/public"));
    app.use(express.urlencoded({ extended: true }));    // Middleware para poder tomar los datos que se envían a traves del body

    app.post('/form', (req, res) => {
        console.log(req.body);    // Como se hizo anteriormente, toma los datos enviados y los muestra en consola
        res.send('Formulario enviado!!')
    })

    app.listen(PORT, () => console.log("El servidor funciona a la perfección!!"));

```

> El único cambio que se hizo en el HTML es que se cambio el método `GET` a `POST` del formulario

Sumado a esto es posible hacer validaciones simples de los datos del formulario, redirigiendo a una pagina de error si es que faltan datos.

```js

    app.post('/form', (req, res) => {
        const { nombre, apellido } = req.body;  // Hace un destructuring de los datos para obtenerlos como variables
        if (!nombre || !apellido) return res.redirect("/error.html");   // Comprueba los datos, si no se completan se hace una redirección a la pagina de error
        res.send('Formulario enviado!!')
    })

```

> Para la redirección se creo el archivo `error.html` dentro de la carpeta `public`

Los datos que se obtienen del formulario pueden servir para diferentes motivos, ya sea para usarlos como request a una base de datos como para la creación de un archivo de texto. Esto ultimo es posible gracias al paquete que viene con `node` llamado `fileSystem`, el cual genera archivos en base al código.  
Para iniciar el mismo es necesario hacer un `require`.

```js

    const fs = require('fs');

```

`FileSystem` solo creara un archivo, no una carpeta, asi que para desarrollar el ejemplo se creara una carpeta por fuera de `public` a la que llamaremos `archivos`, la misma contendrá los futuros archivos creados por `fs`.  
Sumado a esto se modifico el formulario para darle sentido a la explicación.

```HTML

    <form action="/form" method="POST">
        <input type="text" name="nombre" placeholder="nombre">
        <input type="text" name="texto" placeholder="texto">
        <button type="submit">enviar</button>
    </form>

```

Es necesario llamar a `fs` luego de la comprobación para que la misma tome los datos y los transforme en el archivo en cuestión, usando el método `fs.writeFile`, el cual recibe los siguientes parámetros.

```js

    fs.writeFile(<NOMBRE DEL ARCHIVO>, <DATOS DENTRO DEL ARCHIVO>, (<CALLBACK>)) 

```

Para su correcto funcionamiento tomaremos los datos y crearemos dinámicamente el archivo en base al nombre ingresado por el usuario.

```js

    app.post('/form', (req, res) => {
        const { nombre, texto } = req.body;

        if (!nombre || !texto) return res.redirect("/error.html")       // Comprueba que existan

        fs.writeFile(`archivos/${nombre}.txt`, texto, (err)=>{      // Método para la creación del archivo 
            if (err) return res.redirect("/error.html")     // Acción si es que existe un error en la creación del mismo
            res.send('Se creo el archivo con éxito!!')      // Respuesta al crear el archivo
        })
    })

```

> Esto dará como resultado la creación del archivo con el nombre ingresado en el form y la extension `.txt` (`tomas.txt` en este caso), y contendrá el texto como cuerpo del archivo.

Si se quiere facilitar el archivo creado para el usuario es posible usar el método `res.download` para generar la descarga automática.

```js

    app.post('/form', (req, res) => {
        const { nombre, texto } = req.body;
        if (!nombre || !texto) return res.redirect("/error.html")

        fs.writeFile(`archivos/${nombre}.txt`, texto, (err)=>{
            if (err) return res.redirect("/error.html")
            res.download(__dirname + `/archivos/${nombre}.txt`)     // Genera la descarga al crear el archivo
        })
    })

```

## Motores de plantillas

Antes de React, Vue y Angular existieron ciertos motores de plantilla que servían para generar código mas rápido y reutilizable, ademas de dinámico y liviano.

> Antes de seguir es necesario eliminar el archivo de `index.html`, ya que podrá interferir en la explicación.

Para comenzar a usar las plantillas es necesario instalar [`Handlebars`](https://handlebarsjs.com/), para ello vamos a utilizar el comando que se sugiere en su [página de npm](https://www.npmjs.com/package/express-handlebars).

```cmd

    npm i express-handlebars

```

Luego se precisa hacer las carpetas para los layouts como las indica la documentación, estando por fuera organizadas de la siguiente forma.

```text

    views (carpeta)
        |-> layouts (carpeta)
                  |-> main.hbs (archivo)
        |-> components (carpeta)

```

Esto nos servirá mas adelante para probar `node`, pero `nodemon` no detecta automáticamente los cambios en `handlebars`, por lo que es necesario crear un archivo de configuraciones.  
Al nivel de la carpeta raíz (fuera de public) crearemos un archivo llamado `nodemon.json` que contendrá el siguiente comando.

```json

    {
        "ext": "js,json,hbs"
    }

```

Esto hará que `nodemon` detecte los cambios en los archivos con esas extensiones (se pueden agregar mas si se desea) y reiniciará el servidor.  
Luego de esto nos queda configurar la extensión `.hbs` para que `node` lo detecte, para esto es necesario hacer un `require` de los handlebars en el `index.js`.

```js

    const { create } = require("express-handlebars")

```

Luego, habrá que indicarle a `node` la ruta donde se encuentran las plantillas y extensiones que se deberán renderizar.

```js

    const express = require('express');
    const { create } = require("express-handlebars")

    const app = express();

    const hbs = create({
        extname: ".hbs",    // Toma la extension
        partialsDir: ["views/components"],    // Define la ruta donde se encuentran los componentes
    });

    app.engine(".hbs", hbs.engine);     // Define el motor de plantillas
    app.set("view engine", ".hbs");     // Define la extension del mismo
    app.set("views", "./views");    // Define la ruta en donde se encuentran las plantillas

    const PORT = process.env.PORT || 5000;

```

Hay que saber que la base de todo el contenido se creara en el archivo `main.hbs`, aca es donde debería tener todo el contenido del head y demás, para luego agregar el contenido dinámico en otros archivos.  
Ahora, dentro del mismo nos quedaría algo así.

```HTML

<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>= URL shortener =</title>
    </head>


    <body>
        {{{body}}}
    </body>


    </html>

```

> La etiqueta `{{{body}}}` sirve para agregar el contenido que tendremos en los otros archivos

Para crear el contenido que ira dentro de esta etiqueta crearemos un archivo llamado `home.hbs` dentro de la carpeta `views` (por fuera de la carpeta `layouts`), ahora lo que agreguemos en este archivo quedara reflejado en el main.

```HTML

    <h1>Bienvenidos al convertor de URLs</h1>

```

Por ultimo deberemos decirle a node que renderice estos archivos, para ello usaremos el método `render`.  
Nuestro archivo `index.js` debería habernos quedado asi.

```js

    const express = require('express');
    const { create } = require("express-handlebars")

    const app = express();

    const hbs = create({
        extname: ".hbs",
        partialsDir: ["views/components"],
    });


    app.engine(".hbs", hbs.engine);
    app.set("view engine", ".hbs");
    app.set("views", "./views");

    app.get('/', (req, res) => {
        res.render("home")      // Renderiza el archivo que indiquemos cuando sea la ruta raíz
    })

    app.use(express.static(__dirname + "/public"))
    app.use(express.urlencoded({extended: true}))

    const PORT = process.env.PORT || 5000;
    app.listen(PORT, () => console.log(`server listening on port ${PORT} :D`))

```

> El middleware `use static` debe estar DESPUÉS del render, dado que si esta antes solo se renderizará lo que este dentro de la carpeta `public`

Los handlebars nos dan la posibilidad de crear paginas dinámicas con contenido dividido en `componentes` (anteriormente conocidos como `partials`), los cuales son pedazos de código que se repiten en otros lados, organizando mejor todo el código.  
Para hacer una demostración podemos empezar con el uso de [`Bootstrap`](https://getbootstrap.com/docs/5.2/getting-started/introduction/), el cual llamaremos en base a su [`CDN`](https://getbootstrap.com/docs/5.2/getting-started/download/#cdn-via-jsdelivr) en el archivo `main.hbs`, ya que este, al ser la base de todas las paginas, renderizará Bootstrap en todos los lugares necesarios.  
A la par de esto, dentro de la carpeta `components` crearemos un archivo llamado `NavBar.hbs` que contendrá nuestro [navbar](https://getbootstrap.com/docs/5.2/components/navbar/), quedando de la siguiente forma.

```HTML

    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">Navbar</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li class="nav-item">
                        <a class="nav-link active" aria-current="page" href="/">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Features</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

```

Este componente lo llamaremos dentro de `main.hbs` para que se repita en todas las paginas, poniendo el nombre del archivo dentro de `{{> }}` (llaves dobles). El body de nuestro archivo principal debería quedarnos de la siguiente forma.

```HTML

    <body>
   
        {{> NavBar}}    <!-- Llamado al componente NavBar -->

    <div>
        
        {{{body}}}      <!-- Llamado al componente principal general -->
        
    </div>
    <script
        src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-A3rJD856KowSb7dwlZdYEkO39Gagi7vIsF0jrRAoQmDKKtQBHUuLZ9AsSv4jD4Xa"
        crossorigin="anonymous"
    ></script>      <!-- Script de Bootstrap -->
    </body>

```

También es posible "modularizar" las rutas para un código mas limpio utilizando `router` de `express`. Para ello es necesario crear la carpeta `routes` al mismo nivel de la raíz (por fuera de public). Dentro de la misma crearemos el archivo `home.js`, usando el método `router` y pasando los datos de la ruta hacia el home que se encuentra en el `index.js`, quedando el mismo de la siguiente forma.

```js

    const express = require('express');
    const router = express.Router();    // Uso del método Router

    router.get('/', (req, res) => {     // Aquí se usa "router" en vez de "App"
        const links = [
            {link: "google.com/1", short: "JH244k1"},
            {link: "google.com/2", short: "JH245k2"},
            {link: "google.com/3", short: "JH246k3"},
            {link: "google.com/4", short: "JH246k4"},
        ]
        res.render("home", {links: links})
    })

    module.exports = router;    // Al ser un modulo se tiene que exportar

```

Esto se tiene que llamar en el index principal, reemplazando la redirección anterior de la siguiente forma.

```js

    const express = require('express');
    const { create } = require("express-handlebars")

    const app = express();

    const hbs = create({
        extname: ".hbs",
        partialsDir: ["views/components"],
    });


    app.engine(".hbs", hbs.engine);
    app.set("view engine", ".hbs");
    app.set("views", "./views");

    app.use(express.static(__dirname + "/public"))
    app.use(express.urlencoded({extended: true}))
    app.use("/", require("./routes/home"))      // Es el llamado que se usaba anteriormente para las rutas

    const PORT = process.env.PORT || 5000;
    app.listen(PORT, () => console.log(`server listening on PORT ${port} :D`))

```

Esto puede repetirse las veces que sea necesaria, para ponerlo como ejemplo vamos a crear una ruta de login, para ello comenzamos creando un archivo llamado `login.hbs` dentro de la carpeta `views`, el cual contendrá un `h1` como marca para indicar en que pagina estamos.

```HTML

    <h1>LOGIN</h1>

```

Luego, dentro de la carpeta `routes` crearemos su propio archivo llamado `auth.js` en el cual crearemos la ruta hacia el mismo como se indico anteriormente.

```js

    const express = require('express');
    const router = express.Router();

    router.get('/login', (req, res) => {
        res.render("login")
    })

    module.exports = router;

```

> Como podemos ver, la base es la misma, lo único que cambia son los componentes a renderizar dependiendo de la ruta base que se requiere

Como vimos anteriormente, hay que agregar esta nueva ruta al `index.js` que teníamos para node, quedando debajo de la ruta que genera el contenido principal.

```js


    app.use(express.static(__dirname + "/public"))
    app.use(express.urlencoded({extended: true}))
    app.use("/", require("./routes/home"))
    app.use("/auth", require("./routes/auth"))      // Nueva ruta

    const PORT = process.env.PORT || 5000;
    app.listen(PORT, () => console.log(`server listening on port ${PORT} :D`))

```

Como podemos ver, esta nueva ruta se generará cuando la URL sea `/auth/login`, por lo que sera preciso cambiar los datos que se encuentra en el NavBar para acceder correctamente a ellas.

```HTML

    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container-fluid">
            <a class="navbar-brand" href="/">Navbar</a>     <!-- Ruta que lleva a la pagina principal -->
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li class="nav-item">
                        <a class="nav-link active" aria-current="page" href="/">Home</a>    <!-- Ruta que lleva a la pagina principal -->
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="/auth/register">Register</a>    <!-- Ruta que lleva a la pagina de registro -->
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="/auth/login">Login</a>    <!-- Ruta que lleva a la pagina de inicio de sesión -->
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="/auth/logout">Logout</a>    <!-- Ruta que cierra la sesión -->
                    </li>
                </ul>
            </div>
        </div>
    </nav>

```

Con esto hecho tenemos disponible dos rutas, la ruta raíz (`"/"`) que nos lleva a la pagina principal, y la ruta que nos lleva al login (`"/auth/login"`).

## MongoDB

Para seguir con nuestro proyecto vamos a hacer uso de [`MongoDB`](https://www.mongodb.com/) como nuestra base de datos. `MongoDB` es una base de datos no relacional (`NoSql`) que nos servirá para almacenar nuestros datos y hacer pedidos a la misma.  
Para ello lo primero que tendremos que hacer es crear nuestra cuenta gratuita en su [página oficial](https://account.mongodb.com/account/register), yendo por las opciones gratuitas, luego de ello nos pedirá crear un usuario y contraseña, tomamos nota de los mismos ya que lo utilizaremos posteriormente.

> También se pueden ver los pasos en [este](https://youtu.be/EkV2IBZL4C8) y [este](https://youtu.be/xkHyM-K3Cd8?t=11729) tutorial

Luego, es preciso crear un archivo `.env` al nivel de la raíz (fuera de public) en el que tendremos guardados nuestros datos privados, el mismo debe agregarse dentro del archivo `.gitignore`, quedando el mismo de la siguiente forma.

```text

    node_modules
    .env

```

Dentro de este nuevo archivo agregaremos nuestro `URI` proporcionado por MongoDB, al que reemplazaremos los datos entre <> con nuestros datos.

```text

    mongodb+srv://<username>:<password>@linkshortener.htlxrqb.mongodb.net/<dataBaseName>

```

Esto quedará dentro de nuestro `.env` como valor de `URI` de la siguiente forma.

```env

    URI=mongodb+srv://user:abcde12345@linkshortener.htlxrqb.mongodb.net/linkdatabase

```

Sumado a esto podemos instalar [`dotenv`](https://www.npmjs.com/package/dotenv), el cual es un paquete que nos ayudara a la gestión de las variables de entorno. Para ello usaremos el siguiente comando.

```cmd

    npm i dotenv

```

Con nuestra base de datos configurada podemos empezar a crear y modificar datos en la misma, para ello usaremos un paquete que nos ayudara con el proceso, llamado [`mongoose`](https://mongoosejs.com/), el cual deberemos instalar con el comando indicado en su [documentación](https://mongoosejs.com/docs/index.html).

```cmd

    npm install mongoose

```

Ahora es necesario crear nuestro archivo en el que llamaremos a nuestra base de datos, para ello crearemos la carpeta `database` al mismo nivel que la carpeta raíz, dentro de ella crearemos el archivo `db.js` en el que usaremos `mongoose` para la conexión con MongoDB.

```js

    const mongoose = require('mongoose');   // Requerimos Mongoose

    mongoose.connect(process.env.URI)   // Conectamos Mongoose con los datos de Mongo en .env
        .then(()=>{console.log("Base de datos conectada!!")})   // Nos indica que la conexión fue exitosa
        .catch(err=>{console.log("Error: " + err)})     // Si hay un error lo detecta y aclara cual es

```

Ademas de esto, en el `index.js` deberemos agregar el pedido a la base de datos y a Mongoose, ambos usando `require` al inicio del archivo, quedando el mismo de la siguiente manera.

```js

    const express = require('express');
    const { create } = require("express-handlebars")
    require("dotenv").config();     // Requerimos dotenv para la configuración del .env
    require("./database/db");   // Llamamos a la configuración de la base de datos

```

Ahora que terminamos de configurar la base de datos es necesario usar mongoose para crear nuestra colección de datos en Mongo, para ello deberemos crear una carpeta para los `models` en el mismo nivel de la carpeta raíz, dentro de esta deberemos crear el archivo que va a contener las colecciones (en este caso, la colección de URLs), al cual llamaremos `Url.js` (en singular y comenzando con mayúsculas).

```js

    const mongoose = require('mongoose');   // Requerimos mongoose de base
    const { Schema } = mongoose;    // Requerimos el método Schema para crear la colección

    const urlSchema = new Schema({      // Al ser una clase, Schema usa el método new
        link: {                         // Nombre del objeto que ira dentro del documento
            type: 'string',     // Tipo de dato que se enviara
            unique: true,       // Indicamos que sera un dato único e irrepetible
            required: true      // Sera un dato requerido
        },
        short: {
            type: 'string',
            unique: true,
            required: true,
        }

    });

    const Url = mongoose.model('Url', urlSchema);       // Indicamos que modelo usaremos para la colección
    module.exports = Url;       // Exportamos la Url para poder usarla en otros lados, y utilizar sus métodos para modificar o agregar datos

```

> Para generar los shorts para los url utilizaremos [`nanoid`](https://www.npmjs.com/package/nanoid), el cual instalaremos con el comando `npm i nanoid`

Para seguir con la idea de usar un `modelo vista controlador` necesitaremos tener los controladores, es por eso que crearemos la carpeta `controllers` al mismo nivel que la carpeta raíz, aquí es donde tendremos los controladores que nos ayudaran para mantener los request y responses ordenados.  
Luego de crear la carpeta deberemos crear el archivo `homeController.js`, el cual contendrá el controlador para la pagina inicial de nuestro proyecto, llevando el callback que esta en `/routes/home`, quedando de la siguiente forma.

```js

    const readURLs = async (req, res) => {      // Le asignamos un nombre para llamarlo en home
        res.render("home")
    }

    module.exports = {          // Exportamos el modulo
        readURLs,
    }

```

Con este cambio podemos modularizar `home.js` quedando de las siguiente forma.

```js

    const express = require('express');
    const { readURLs } = require('../controllers/homeController');      // Si no se importa automáticamente debe escribirse manualmente
    const router = express.Router();

    router.get('/', readURLs)       // Reemplazamos el callback con el modulo

    module.exports = router;

```

Para leer los datos, es necesario TENER datos para leer, es por eso que crearemos los datos desde nuestra pagina principal, para ello crearemos la respuesta para el request en el controlador del `homeController`, el cual quedaría de la siguiente manera.

```js

    const Url = require("../models/Url");   // Llamamos al modelo de la base de datos que creamos anteriormente
    const { nanoid } = require("nanoid");   // Llamamos a nanoid para usarlo luego

    const readURLs = async (req, res) => {
        res.render("home")
    }

    const addURLs = async (req, res) => {

        const { urlInput } = req.body       // Tomamos el dato enviado por el formulario

        try {
            const url = new Url({link: urlInput, short: nanoid(8)})      // El link lo tomaremos desde el input y el short se crea aleatoriamente 
            await url.save()            // Guarda los datos en la base de datos
            res.redirect("/")         // Al crearse con éxito nos devuelve a la pagina principal
        } catch (err) {
            console.log(err);   // Si hay un error durante la creación lo podremos ver en consola
            res.send("OH NO! Hubo un error! Error: " + err)     //Y también nos saldrá en la pagina
        }
    }

    module.exports = {
        readURLs,
        addURLs,        // Lo exportamos para usarlo en el home.js
    }

```

Luego de esto, deberemos llamar a `addURLs` en el `home.js` como un método `POST` que vendrá desde un input.

```js

    const express = require('express');
    const { readURLs, addURLs } = require('../controllers/homeController');     // VSC importa automáticamente si lo necesitamos
    const router = express.Router();

    router.get('/', readURLs)
    router.post('/', addURLs)       // El autocompletar lo importa automáticamente

    module.exports = router;

```

Ahora es necesario agregar un input que nos ayudara a enviar los datos con un método `POST`, para ello crearemos un nuevo componente en su carpeta que se llame `Form.hbs`, en el mismo crearemos nuestro input.

```HTML

    {{#if url}}         <!-- If propio de handlebars que nos servirá mas adelante para editar los datos -->
        <form class="w-75 m-auto" action="/update/{{url._id}}" method="post">       <!-- El action sirve para la redirección y el método para subir los datos -->
            <input value="{{url.link}}" class="form-control mb-2" type="text" name="urlInput" id="urlInput" placeholder="Inserte una URL valida" required>
            <button type="submit" class="btn btn-primary w-100">Editar URL</button>
        </form>
    {{else}}
        <form class="w-75 m-auto" action="/" method="post">
            <input class="form-control mb-2" type="text" name="urlInput" id="urlInput" placeholder="Inserte una URL valida" required>
            <button type="submit" class="btn btn-success w-100">Agregar URL</button>
        </form>
    {{/if}}

```

> La primer parte del formulario se renderizará unicamente cuando querramos editar un dato en la base de datos

Este componente lo agregaremos en la pagina principal (`/views/home.hbs`) para que se renderice unicamente ahi.

```HTML

    <h1>Bienvenidos al convertor de URLs con Node y Handlebars</h1>
    <h2>Agregue su URL</h2>

    {{> Form}}      <!-- Importamos el componente -->

```

También es necesario validar que la entrada sea una URL valida, para ello crearemos nuestro propio middleware. Empezaremos creando la carpeta `middlewares` al nivel de la raíz, y dentro del mismo crearemos el archivo llamado `validateUrl.js`.

```js

    const {URL} = require('url');       // Requerimos el modulo url de Node

    const validateUrls = (req, res, next) => {
        try {
            const { urlInput } = req.body;      //Tomamos la url
            const urlFrontEnd = new URL(urlInput)       // Valida que sea url
            if (urlFrontEnd.origin !== "null") {    // Si no es null sigue al método
                if(urlFrontEnd.protocol === "https:" || urlFrontEnd.protocol === "http:"){
                    return next()            
                }
            }
            throw new Error("Link invalido")        // Si es null genera un nuevo error
        } catch (err) {
            console.log("Oh no! Hubo un error: " + err)
            return res.send("error!")       // Nos manda a una pagina de error
        }
    }

    module.exports = validateUrls;      // Lo exporta

```

Por ultimo debemos hacer uso de este nuevo middleware cuando añadimos la url en `home.js`, quedando el mismo de la siguiente forma.

```js

    const express = require('express');
    const { readURLs, addURLs, deleteURLs } = require('../controllers/homeController');
    const validateUrls = require('../middlewares/validateUrls');        // Importa el middleware recién creado
    const router = express.Router();

    router.get('/', readURLs)
    router.post('/', validateUrls, addURLs)     // Primero valida la url, si es valida sigue al método de añadir Url
    router.get('/delete/:linkId', deleteURLs)

    module.exports = router;

```

> Con esto hecho podemos probar nuestro proyecto, iniciamos el servidor (`npm run dev`) y agregamos una url, si no hay problemas deberíamos ver el nuevo dato en la base de datos de MongoDB.

Ahora que pudimos crear nuestro primer dato es necesario poder leer esos datos, para ello usaremos el método `find`, el cual nos trae todos los datos de la base de datos, y el método `lean`, que "formatea" los datos en datos mas simples.  
Para ello nos iremos a `homeController.js` y agregaremos los datos a `readURLs`.

```js

    const readURLs = async (req, res) => {

        try {
            const links = await Url.find().lean()       // Toma los datos de la base de datos 
            res.render("home", {links: links})      // Lo usaremos para renderizar los datos en la pagina principal
        } catch (err) {
            console.log(err);
            res.send("OH NO! Hubo un error! Error: " + err)
        }
    }

```

Teniendo estos datos deberemos mostrarlos en pantalla, para ello crearemos un nuevo componente llamado `UrlCard.hbs` que creara una card por cada dato que viene de nuestra base de datos (es decir, `forEach`), utilizando un método propio de handlebars.

```HTML

    {{#each links }}        <!-- ForEach propio de handlebars -->

    <div class="card m-auto my-3 w-75 text-center">
    <div class="card-body">
        <h5 class="card-title">Link id: {{this._id}}</h5>       <!-- El this. toma de base el parámetro pasado y sus propiedades como un forEach normal de JS -->
        <h6 class="card-subtitle mb-2 text-muted">Short URL: {{this.short}}</h6>
        <a href={{this.link}} class="card-link" target="_blank">Link: {{this.link}}</a>
        <div>
            <button data-shortUrl="{{this.short}}" class="btn btn-success" href="#">copiar</button>         <!-- Tomaremos el dataAttribute cuando editemos en la base de datos-->
            <a class="btn btn-primary" href="#">editar</a>
            <a class="btn btn-danger" href="/delete/{{this._id}}">eliminar</a>      <!-- Esto lo usaremos como parámetros para eliminar -->
        </div>
    </div>
    </div>

    {{/each}}       <!-- Cierre del forEach de handlebars -->

```

> Este nuevo componente deberemos llamarlo en el `home.hbs` como lo hicimos con el `Form`

Luego de esto podemos probar una manera (no muy eficiente) de borrar un dato, para esto deberemos crear una nueva respuesta en el `homeController` llamada `deleteUrls`, la cual deberá hacer uso del método `findByIdAndDelete` basado en el id del link a borrar.

```js

    const deleteURLs = async (req, res) => {

        const { linkId } = req.params           // Tomamos el parámetro pasado por URL

        try {
            await Url.findByIdAndDelete(linkId)     // Busca el link en base al id en el parámetro
            res.redirect("/")
        } catch (err) {
            console.log(err);
            res.send("OH NO! Hubo un error! Error: " + err)
        }

    }

    module.exports = {
        readURLs,
        addURLs,
        deleteURLs,         // Lo exporta para usarlo como callback
    }

```

> Esto no es muy eficiente ya que se llaman los datos cada vez que se cumple una acción, dando como resultado un uso mayor al debido de la base de datos

Hecho esto debemos llamarlo en el `home.js` para que se ejecute cada vez que se pase la URL.

```js

    router.get('/', readURLs)
    router.post('/', addURLs)
    router.get('/delete/:linkId', deleteURLs)       // Cuando la URL se pase con el id, se ejecutará y eliminará de la base de datos

```

Lo que nos queda por hacer para tener el CRUD (create, read, update, delete) completo es poder editar nuestros links guardados. Para ello crearemos la nueva respuesta en el `homeController.js`, primero para crearemos la redirección para el formulario de edición.

```js

    const updateUrlsForm = async (req, res) => {
        
        const { linkId } = req.params           // Tomamos el parámetro pasado por URL
        
        try {
            const url = await Url.findById(linkId).lean()       // Busca el link en la base de datos
            res.render("home", {url})           // Renderiza el home pasando el objeto como parámetro para que funcione el if del formulario
        } catch (err) {
            console.log(err);
            res.send("OH NO! Hubo un error! Error: " + err)
        }
    }

    module.exports = {
        readURLs,
        addURLs,
        deleteURLs,
        updateUrlsForm,
    }

```

Ahora debemos agregarlo al `home`, agregándolo directamente para que se haga la autoimportación.

```js

    router.get('/', readURLs)
    router.post('/', validateUrls, addURLs)
    router.get('/delete/:linkId', deleteURLs)
    router.get('/update/:linkId', updateUrlsForm)

    module.exports = router;

```

Por ultimo debemos crear la respuesta para editar el link en la base de datos, para ello deberemos usar el método `findByIdAndUpdate`, el cual busca y trae el objeto de la base de datos.

```js

    const updateUrls = async (req, res) => {        // Creamos la respuesta
        
        const { linkId } = req.params           // Toma el id del objeto
        const { urlInput } = req.body           // Toma el dato escrito en el input

        try {
            await Url.findByIdAndUpdate(linkId, {link: urlInput})       // Toma el dato del id y después crea el objeto y lo edita en la base de datos
            res.redirect("/")       // Redirige a la pagina principal
        } catch (err) {
            console.log(err);
            res.send("OH NO! Hubo un error! Error: " + err)
        }
    }

    module.exports = {
        readURLs,
        addURLs,
        deleteURLs,
        updateUrlsForm,
        updateUrls,         // Exporta para usarlo luego
    }

```

Esta ultima la agregaremos al `home` para dar por finalizado el CRUD.

```js

    router.get('/', readURLs)
    router.post('/', validateUrls, addURLs)
    router.get('/delete/:linkId', deleteURLs)
    router.get('/update/:linkId', updateUrlsForm)
    router.post('/update/:linkId', validateUrls, updateUrls)        // Agregamos la validación de URL que creamos anteriormente

    module.exports = router;

```

Para el completo funcionamiento de nuestra pagina es necesario tomar los datos del link acortado y poder usarlo para redirigir a la pagina guardada, para ello usaremos el Front-End.  
En la carpeta public crearemos nuestra carpeta contenedora de scripts, dentro de ella crearemos el archivo `app.js` que contendrá el siguiente script.

```js

    document.addEventListener("click", (e)=>{       // Detecta el click en el documento
        if (e.target.getAttribute("data-shortUrl")){        // Si hacemos click en el botón con el atributo
            const url = `http://localhost:5000/${e.target.getAttribute("data-shortUrl")}`        // Crea la URL
        
            navigator.clipboard
                .writeText(url)     // Copia la URL al portapapeles
                .then(()=>{
                    console.log("Copiado con éxito!")       // Verificación si funciona
                })
                .catch((err)=>{console.log("Oh no! Hubo un error: " + err)});
        }
    })

```

> Este script hay que importarlo en el `main.hbs` para que lo detecte el front-end

## Autorización

Ahora que tenemos nuestra pagina completamente funcional es tiempo de agregar usuarios y sus autorizaciones, para ello empezamos creando un archivo llamado `auth.js` en nuestra carpeta de rutas y un `authController.js` en la carpeta de los controladores.  
Para nuestro controlador crearemos dos respuestas, `loginForm` y `registerForm`, exportando ambos.

```js

    const loginForm = (req, res) => {
        res.render("login")             // Render para el login
    }

    const registerUser = async (req, res) => {
        res.json(req.body)          // Toma los datos del formulario de registro
    }

    const registerForm = (req, res) => {
        res.render("register")          // Render para el register
    }

    module.exports = {                  // Exportamos los módulos
        loginForm,
        registerForm,
        registerUser,
    }

```

Los mismos deberemos llevarlos a `auth.js`, creando como respuesta a los requires, importando ambos (si se crea primero los módulos, VSC los importa automáticamente).

```js

    const express = require('express');
    const { loginForm, registerUser, registerForm } = require('../controllers/authController');   // Importamos los módulos
    const router = express.Router();

    router.get('/register', registerForm)       // Creamos el router para el register
    router.post('/register', registerUser)       // Creamos el router para los datos del formulario de registro
    router.get('/login', loginForm)             // Creamos el router para el login

    module.exports = router;

```

Ademas deberemos crear la vista del register, es decir, crear el archivo `register.hbs` en la carpeta de `views`, en el cual agregaremos nuestro formulario de registro.

```HTML

    <h1 class="text-center">Ingrese los datos para crear un nuevo usuario</h1>

    <form class="d-flex flex-column w-50 gap-2 m-auto" action="/auth/register" method="post">
        <input type="text" name="userName" id="userName" placeholder="Inserte su nombre" required>
        <input type="text" name="userMail" id="userMail" placeholder="ejemplo@mail.com" required>
        <input type="password" name="userPass" id="userPass" placeholder="********" required>
        <input type="password" name="userPassConfirmation" id="userPassConfirmation" placeholder="Repita su contraseña" required>
        <button class="form-control btn btn-primary" type="submit">Registrarse</button>
    </form>

```

Para poder guardar los datos de los usuarios es necesario crear nuestro modelo, para ello crearemos el archivo `User.js` en la carpeta de modelos.

```js

    const mongoose = require('mongoose');   // Requerimos Mongoose
    const { Schema } = mongoose;    // Método para creare Schemas de Mongoose

    const userSchema = new Schema({

        userName: {                  // Nombre de usuario
            type: String,
            lowercase: true,                 // Transforma el dato en lowercase
            required: true,                  // Lo vuelve obligatorio
        },
        userMail:{
            type: String,
            lowercase: true,
            required: true,
            unique: true,                  // Verifica que no se repita
            index: { unique: true }        // Verifica que el index no se repita
        },
        userPass:{
            type: String,
            required: true,
        },
        tokenConfirmation:{                  // Lo usaremos para confirmar el mail
            type: String,
            default: null,
        },
        isConfirmed:{                  // Detecta si confirmo el mail
            type: Boolean,
            default: false,
        }    

    });

    module.exports = mongoose.model('User', userSchema);        // Exporta el esquema

```

Esto lo usaremos en el controlador para llevarlo como respuesta y enviarlo a la base de datos, pero primero debemos confirmar que el usuario no este registrado.

```js

    const registerUser = async (req, res) => {
        
        const { userName, userMail, userPass } = req.body       // Toma los datos enviados por el formulario

        try {
            let user = await User.findOne({ userMail: userMail})      // Comprueba que no exista el mail en la base de datos
            if(user) throw new Error(`El mail ${user.userMail} ya esta en uso`)       // Si el usuario existe genera un nuevo error
            user = new User({userName, userMail, userPass, tokenConfirmation: nanoid()})        // Si no existe genera un nuevo usuario con el esquema que creamos anteriormente
            await user.save()           // Guarda el usuario en la base de datos
            res.redirect("/auth/login")        // Envía a la pagina de login
        } catch (err) {
            console.log("Oh no! Hubo un error: " + err.message)
            res.send("ERROR: " + err.message)
        }
    }

```

> El método `User` es necesario importarlo al inicio del documento, en VSC se hace la autoimportación (`const User = require("../models/User")`) junto a `nanoid` (`const nanoid = require("nanoid")`)

Ya tenemos la creación del usuario y el envío de datos a la base de datos, pero la contraseña es un dato sensible, por lo que hay que encriptarla antes de subirla a la misma, para ello haremos uso del paquete llamado `bcrypt.js`, el cual genera una encriptación de la misma.  
Para instalar el paquete usaremos el comando indicado en su [documentación](https://www.npmjs.com/package/bcryptjs).

```cmd

    npm i bcryptjs

```

Para generar nuestra encriptación usaremos el método `.pre` de `mongoose`, el cual realiza una acción antes de guardarla en la base de datos. Esto lo haremos en el modelo del user.

```js

    userSchema.pre("save", async function(next){            // Usamos .pre para realizar la acción antes de guardar los datos
        const user = this;      // Definimos el user en base al this
        if(!user.isModified("userPass")) return next();     // Si la contraseña no se modifica no se vuelve a hacer el hash

        try {
        
            const salt = await bcrypt.genSalt(10);      // Genera los saltos 
            const hash = await bcrypt.hashSync(user.userPass, salt);        // Encripta la contraseña en base a los saltos
            user.userPass = hash;       // Reemplaza la contraseña con el hash

            next();

        } catch (err) {
        
            console.log(err)
            throw new Error("Oh no! Hubo un error al codificar la contraseña")
        
        }
    })

```

> Para usar `bcrypt` es necesario importarlo al inicio con `const bcrypt = require('bcryptjs')`

El siguiente paso sera confirmar la cuenta del usuario con el token, para ello crearemos un nuevo controlador que importaremos en el auth llamado `tokenConfirmation`.

```js

    const tokenConfirmation = async (req, res) => {
        const { tokenForConfirmation } = req.params;        // Tomamos el token que enviaremos por URL

        try {
            const user = await User.findOne({ tokenConfirmation: tokenForConfirmation });       // Buscamos el usuario en la base de datos
            if(!user) throw new Error("No se encontró el usuario")      // Si no se encuentra el usuario se genera un nuevo error

            user.isConfirmed = true;        // Si se encuentra cambiamos la confirmación
            user.tokenConfirmation = null;      // Ademas, borramos el token
            await user.save();              // Guardamos los nuevos datos del usuario
            res.redirect("/auth/login")         // Redirigimos a la pagina de login
        } catch (err) {
            console.log("Oh no! Hubo un error: " + err.message)
            res.send("ERROR: " + err.message)
        }
    }

```

> Como con todos los controladores, deberemos exportarlo

Luego, usamos el controlador en `auth.js`, el cual debería quedar de la siguiente forma.

```js

    const express = require('express');
    const { loginForm, registerForm, registerUser, tokenConfirmation } = require('../controllers/authController');
    const router = express.Router();

    router.get('/register', registerForm)
    router.post('/register', registerUser)
    router.get('/confirmation/:tokenForConfirmation', tokenConfirmation)
    router.get('/login', loginForm)

    module.exports = router;

```

> De momento podemos generar la confirmación manual del token, ingresando a `/auth/confirmation/{aca va el token en la base de datos}`

Ahora seguiremos con el siguiente paso lógico, crear el login para el usuario. Para ello empezamos creando el formulario para el mismo en el archivo `login.hbs`.

```js

    <h1 class="text-center">Inicie sesión con sus datos</h1>

    <form class="d-flex flex-column w-50 gap-2 m-auto" action="/auth/login" method="post">
        <input type="text" name="userMail" id="userMail" placeholder="ejemplo@mail.com" required>
        <input type="password" name="userPass" id="userPass" placeholder="********" required>
        <button class="form-control btn btn-primary" type="submit">Iniciar sesión</button>
    </form>

```

Uno de los métodos que usaremos será la comprobación de contraseña, para ello crearemos un método junto a `bcrypt` en nuestro modelo `User.js`.

```js

    userSchema.methods.comparePassword = async function(candidatePassword) {        // methods nos facilita la creación de métodos
        return await bcrypt.compare(candidatePassword, this.userPass)       // Compara la contraseña que le pasamos junto a la contraseña almacenada
    }

```

Ahora deberemos crear los controladores para mostrar el formulario de inicio de sesión y para comprobar los datos en la base de datos, ambos en `authController.js`.

```js

    const loginForm = (req, res) => {
        res.render("login")             // Render para el formulario de inicio de sesión
    }

    const loginUser = async (req, res) => {
        
        const { userMail, userPass } = req.body;      // Toma los datos del formulario

        try {
            
            const user = await User.findOne({ userMail });      // Busca el usuario en la base de datos

            if(!user) throw new Error("No existe el usuario")       // Error por si no existe el usuario

            if(!user.isConfirmed) throw new Error("Falta confirmar la cuenta")      // Error por si no esta confirmada la cuenta

            if(!await user.comparePassword(userPass)) throw new Error("Contraseña incorrecta")      // Error que compara la contraseña ingresada con la que esta en la base de datos gracias a nuestro método

            res.redirect("/")
        } catch (err) {
            console.log("Oh no! Hubo un error: " + err.message)
            res.send("ERROR: " + err.message)
        }
        
    }

    module.exports = {
        registerForm,
        registerUser,
        tokenConfirmation,
        loginUser,
        loginForm,
    }

```

Por ultimo debemos agregar los controladores a `auth.js` para generar la respuesta al require de la url, quedándonos este de la siguiente forma.

```js

    const express = require('express');
    const { registerForm, registerUser, tokenConfirmation, loginForm, loginUser } = require('../controllers/authController');
    const router = express.Router();

    router.get('/register', registerForm)
    router.post('/register', registerUser)
    router.get('/confirmation/:tokenForConfirmation', tokenConfirmation)
    router.get('/login', loginForm)
    router.post('/login', loginUser)

    module.exports = router;

```

Hecho todo esto ya podemos comprobar el registro e inicio de sesión de nuestros usuarios.  
Para seguir con nuestra pagina es necesario mantener los datos de nuestros usuarios en sesiones, para ello haremos uso de unos cuantos paquetes de validaciones y sesiones.  
Los paquetes que usaremos serán [Connect Flash](https://www.npmjs.com/package/connect-flash) (Paquete para mantener los mensajes de error), [Express Session](https://www.npmjs.com/package/express-session) (Paquete para mantener la sesión), [Express Validator](https://www.npmjs.com/package/express-validator) (Paquete para las validaciones) y [Connect Mongo](https://www.npmjs.com/package/connect-mongo) (Paquete para enviar los datos de sesión a Mongo), los mismos los instalaremos de la siguiente forma.

```js

    npm i express-session
    npm i connect-mongo
    npm i express-validator
    npm i connect-flash

```

Teniendo esto instalado procederemos a crear una sesión y configurarla en el `index.js` de la siguiente manera.

```js

    app.use(
        session({
            secret: "secret-key-name",      // Nombre secreto, usado solo de ejemplo
            resave: false,      // No fuerza el autoguardado
            saveUninitialized: false,       // No lo guarda si no esta inicializado
            name: "secret-name-session",        // Nombre de la sesión
    }))

    app.use(flash());

```

> Es necesario recordar que ambos se tienen que importar al inicio del documento, por debajo de `express`, siendo las mismas `const session = require('express-session')` y `const flash = require('connect-flash')` respectivamente

Para generar las validaciones usaremos `express-validator` en el `auth.js` antes de que se envíen los datos de registro y de inicio de sesión, para ello usaremos los datos del body de la siguiente manera.

```js

    const { body } = require('express-validator');

    router.post('/register', [
        body("userName", "Ingrese un nombre de usuario válido")
            .trim()         // Elimina los espacios al inicio y final
            .notEmpty()     // Comprueba que no este vació
            .escape(),      // Comprueba que no sea HTML
        
        body("userMail", "Ingrese un mail válido")
            .trim()
            .isEmail()
            .normalizeEmail(),        // Valida el mail en su formato
        
        body("userPass", "La contraseña debe tener mínimo 6 caracteres")
            .trim()
            .notEmpty()
            .escape()
            .isLength({         // Comprueba que no tenga menos de 6 caracteres
                min: 6
            })
            .custom((value, { req }) => {       // Crea una comprobación personalizada
                if (value !== req.body.userPassConfirmation) {      // Si las contraseñas no coinciden
                    throw new Error("Las contraseñas no coinciden")     // Genera un error
                } else {
                    return value;       // Sino devuelve el valor de al contraseña
                }
            })
    ], registerUser)

    router.post('/login', [
        body("userMail", "Ingrese un mail válido")
            .trim()
            .notEmpty()
            .escape(),
        
        body("userPass", "La contraseña debe tener mínimo 6 caracteres")
            .trim()
            .notEmpty()
            .escape()
            .isLength({
                min: 6
            })
    ], loginUser)

```

Y en el controlador de autenticaciones (`authController.js`) tomaremos las respuesta de los errores para devolverlos como respuestas con el uso de `flash` y las validaciones (`validationResult`) que vienen del `auth.js`, para luego pasarlos como parámetros y pintarlos en el home.

```js

    const { validationResult } = require("express-validator")       // Importamos el resultado de la validación

    const registerForm = (req, res) => {
        res.render("register", {messages: req.flash("messages")});      // Envía los datos de error para generar las alertas
    }

    const registerUser = async (req, res) => {

        const errors = validationResult(req)        // Toma los errores

        if(!errors.isEmpty()){          // Si hay errores
            req.flash("messages", errors.array())       // Guarda los errores en el array
            return res.redirect("/auth/register")
        }
        
        const { userName, userMail, userPass } = req.body
        
        try {
            let user = await User.findOne({ userMail: userMail})
            if(user) throw new Error(`El mail ${user.userMail} ya esta en uso`)
            user = new User({userName, userMail, userPass, tokenConfirmation: nanoid()})
            await user.save()
            
            req.flash("messages", [{ msg: "¡Registrado con éxito! Revise su correo para verificar su usuario"}])        // Crea el mensaje de error
            res.redirect("/auth/login")
        } catch (err) {
            req.flash("messages",[{ msg: err.message }])        // Envía el mensaje de error para generarlo como alerta
            res.redirect("/auth/register")
        }
    }

    const tokenConfirmation = async (req, res) => {
        const { tokenForConfirmation } = req.params;
        
        try {
            const user = await User.findOne({ tokenConfirmation: tokenForConfirmation });
            if(!user) throw new Error("No se encontró el usuario")
            
            user.isConfirmed = true;
            user.tokenConfirmation = null;
            await user.save();
            req.flash("messages", [{ msg: "¡Cuenta verificada con éxito!"}])
            res.redirect("/auth/login")
        } catch (err) {
            req.flash("messages",[{ msg: err.message }])
            res.redirect("/auth/login")
        }
    }

    const loginForm = (req, res) => {
        res.render("login", {messages: req.flash("messages")});
    }

    const loginUser = async (req, res) => {
        
        const errors = validationResult(req)

        if(!errors.isEmpty()){
            req.flash("messages", errors.array())
            return res.redirect("/auth/login")
        }

        const {userMail, userPass} = req.body

        try {
            
            const user = await User.findOne({ userMail })
            if(!user) throw new Error("No existe el usuario")

            if(!user.isConfirmed) throw new Error("Falta confirmar la cuenta")

            if(!await user.comparePassword(userPass)) throw new Error("Contraseña incorrecta")

            res.redirect("/")
        } catch (err) {
            req.flash("messages",[{ msg: err.message }])
            res.redirect("/auth/login")
        }
    }

```

Para mostrar los errores es necesario crear una alerta en el `main.hbs`, para que genere cada uno de los mismos cuando los haya, quedando el body de la siguiente manera.

```HTML

    <body>

        {{> NavBar}}

        <div>

        {{#each messages }}

                <div class="alert alert-danger w-75 m-auto my-3">{{this.msg}}</div>         <!-- Toma los errores y los envía como alertas -->
        
        {{/each}}

        {{{body}}}
        
        </div>

        <script src="../scripts/app.js"></script>
        <script
        src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-A3rJD856KowSb7dwlZdYEkO39Gagi7vIsF0jrRAoQmDKKtQBHUuLZ9AsSv4jD4Xa"
        crossorigin="anonymous"
        ></script>

    </body>

```

Ya tenemos hechos los registros e inicio de sesión, es momento de mantener ese inicio de sesión y proteger nuestros links guardados, para ello usaremos el paquete llamado [`passport`](http://www.passportjs.org/), el cual instalaremos con el siguiente comando.

```cmd

    npm install passport

```

Ahora usaremos el mismo en el `index.js`, el cual hará la verificación del usuario para comprobar si tiene una sesión abierta, importando el mismo con `require`.

```js

    const passport = require('passport');       // Llamamos a passport
    const User = require('./models/User');      // Llamamos al User

    app.use(passport.initialize());         // Inicializamos passport
    app.use(passport.session());        // Creamos la sesión

    passport.serializeUser((user, done)=> done(null, {id: user._id, userName: user.userName}));         // Guarda los datos del usuario en la sesión
    
    passport.deserializeUser(async (user, done)=> {         // Toma los datos guardados en la sesión
        const userInDataBase = await User.findById(user.id)         // Busca los datos en la base de datos
        return done(null, {id: userInDataBase._id, userName: userInDataBase.userName});         // Comprueba que sea correcto
    });

```

Luego de esto necesitaremos crear un middleware que verifique que el usuario tenga una sesión valida abierta antes de entrar en los links, esto lo haremos creando el archivo `userVerification.js` en su carpeta correspondiente.

```js

    module.exports = (req, res, next) => {      // Creamos el middleware
        if (req.isAuthenticated()) {          // Si el usuario esta autenticado
            return next();          // Siga con el redireccionamiento
        }
        res.redirect("/auth/login");        // Si no lo esta, se envía al login
    }

```

Este middleware lo usaremos en nuestro `/routes/home.js` para que verifique la sesión antes de ir a la pagina principal.

```js

    const userVerification = require('../middlewares/userVerification');        // Requerimos el middleware recién creado

    router.get('/', userVerification, readURLs)         // Usamos el mismo como comprobación antes de ir a la pagina principal

```

Hecho esto, configuramos el inicio de sesión en la respuesta del login que tendremos en el `authController`, quedando de la siguiente manera.

```js

    req.login(user, function(err){          // Usamos el método de passport para el login
        if(err) throw new Error("Hubo un error en la sesión");      // Si hay un error lo devuelve 
        return res.redirect("/")        // Si no, redirige a la pagina principal
    })

```

> De este modo, ahora podemos intentar entrar en la pagina principal (`"/"`) y nos devolverá a la pagina de inicio de sesión (`"/auth/login"`) hasta que iniciemos sesión

Aunque tengamos la sesión iniciada, no queremos que esto sea asi siempre, asi que para ello crearemos la lógica para cerrar sesión, empezando por crear nuestra respuesta en el `authController`.

```js

    const logOut = (req, res) => {
        req.logout(function (err) {              // Usamos el método para cerrar sesión de passport
        if (err) { return next(err) }       // Si hay un error lo devuelve
        return res.redirect("/auth/login");         // Nos redirige a la pagina de inicio de sesión
        });
    }

    module.exports = {
        registerForm,
        registerUser,
        tokenConfirmation,
        loginUser,
        loginForm,
        logOut      // Lo exportamos para su uso luego
    }

```

Y este lo utilizamos en el `auth.js` para crear la redirección en base al request.

```js

    router.get('/logout', logOut)

```

> Como todos los otros, es necesario importarlo junto a los otros controladores

Ahora que tenemos las validaciones podemos llevarlas al input de las urls y sumarlas a nuestro middleware, ademas de agregar la validación de usuario, para ello empezaremos editando el `home.js` para agregar los métodos de `express-validator` y el `userVerification` quedándonos de la siguiente forma.

```js

    const express = require('express');
    const {
        body
    } = require('express-validator');
    const { readURLs, addURLs, deleteURLs, updateUrlsForm, updateUrls, redirectToShortUrl} = require('../controllers/homeController');
    const userVerification = require('../middlewares/userVerification');
    const router = express.Router();

    router.get('/', userVerification, readURLs)
    router.post('/', [userVerification,
        body("urlInput", "Ingrese una URL válida")
        .trim()
        .notEmpty()
        .isURL()        // Comprueba que lo ingresado sea una URL valida
    ], validateUrls, addURLs)
    router.get('/delete/:linkId', userVerification, deleteURLs)
    router.get('/update/:linkId', userVerification, updateUrlsForm)
    router.post('/update/:linkId', [userVerification, 
        body("urlInput", "Ingrese una URL válida")
        .trim()
        .notEmpty()
        .isURL()
    ], validateUrls, updateUrls)
    router.get('/:shortUrl', redirectToShortUrl)

    module.exports = router;

```

Para luego poder agregar los errores en los controladores (`homeController.js`).

```js

    const Url = require("../models/Url");
    const {
        validationResult
    } = require("express-validator")
    const nanoid = require("nanoid");

    const readURLs = async (req, res) => {

        try {
            const links = await Url.find().lean()
            res.render("home", {
                links: links,
                messages: req.flash("messages")         // Renderiza el home con el mensaje que se envió
            });
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            res.redirect("/")       // Redirige al home con el mensaje de error
        }
    }

    const addURLs = async (req, res) => {

        const errors = validationResult(req)        // Toma los errores de las validaciones

        if (!errors.isEmpty()) {
            req.flash("messages", errors.array())       // Junta los errores en array
            return res.redirect("/")
        }

        const { urlInput } = req.body

        try {
            const url = new Url({
                link: urlInput,
                short: nanoid(8)
            })
            await url.save()
            res.redirect("/")
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            res.redirect("/")
        }

    }

    const deleteURLs = async (req, res) => {

        const {
            linkId
        } = req.params

        try {
            await Url.findByIdAndDelete(linkId)
            res.redirect("/")
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            res.redirect("/")
        }

    }

    const updateUrlsForm = async (req, res) => {

        const {
            linkId
        } = req.params

        try {
            const url = await Url.findById(linkId).lean()
            res.render("home", {
                url,
                messages: req.flash("messages")
            })
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            res.redirect(`/update/${linkId}`)
        }

    }

    const updateUrls = async (req, res) => {

        const errors = validationResult(req)

        if (!errors.isEmpty()) {
            req.flash("messages", errors.array())
            return res.redirect(`/update/${linkId}`)
        }

        const {
            linkId
        } = req.params
        const {
            urlInput
        } = req.body

        try {
            await Url.findByIdAndUpdate(linkId, {
                link: urlInput
            })
            res.redirect("/")
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            res.redirect(`/update/${linkId}`)
        }

    }

    const redirectToShortUrl = async (req, res) => {
        const {
            shortUrl
        } = req.params;
        try {
            const urlInDB = await Url.findOne({
                short: shortUrl
            })
            res.redirect(urlInDB.link)
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            res.redirect("/")
        }
    }

    module.exports = {
        readURLs,
        addURLs,
        deleteURLs,
        updateUrlsForm,
        updateUrls,
        redirectToShortUrl,
    }

```

Y deberemos cambiar los mismos errores en el middleware que valida las urls, quedando el mismo de la siguiente forma

```js

    const { URL } = require('url');

    const validateUrls = (req, res, next) => {
        try {
            const { urlInput } = req.body;
            const urlFrontEnd = new URL(urlInput)
            
            if (urlFrontEnd.origin !== "null") {
                if (urlFrontEnd.protocol === "https:" || urlFrontEnd.protocol === "http:") {
                    return next()
                }
                throw new Error("El link debe tener http:// o https://")        // Genera el error si no es https o http
            }
            throw new Error("No valido")
        } catch (err) {
            if(err.message === "Invalid URL") {
            req.flash("messages", [{msg: "URL invalida"}])
            }else{   
                req.flash("messages", [{msg: err.message}])
            }
            
            return res.redirect("/")
        }
    }

    module.exports = validateUrls;

```

Para añadir seguridad a la pagina y los formularios haremos uso del paquete llamado [`csurf`](https://github.com/expressjs/csurf), instalándolo con el siguiente comando.

```cmd

    npm install csurf

```

Luego deberemos llamarlo en el `index.js` con su respectivo require.

```js

    const csrf = require('csurf');      // Lo importamos

    app.use(csrf())         // Lo inicializamos

    app.use((req, res, next) => {
        res.locals.csrfToken = req.csrfToken();         // Generamos el token para los forms
        res.locals.messages = req.flash("messages");    // General para reemplazarlo en los controladores
        next();
    })

    app.use("/", require("./routes/home"))
    app.use("/auth", require("./routes/auth"))

```

> Ahora que creamos el general para el token podemos crear el general para los mensajes de `flash()` y reemplazarlos en los render, pasando de `res.render("login",{messages: req.flash("messages")})` a quedar `res.render("login")`, tomando el `authController` como ejemplo

Ahora que tenemos el token tenemos que agregar el input oculto en todos los formularios. El siguiente ejemplo toma el formulario del componente `Form.hbs`.

```HTML

    {{#if url}}
            <form class="w-75 m-auto" action="/update/{{url._id}}" method="post">
                <input type="hidden" name="_csrf" value="{{csrfToken}}">        <!-- Al ser hidden se mantiene oculto, y el valor se toma por la generación que hicimos en el index.js -->
                <input value="{{url.link}}" class="form-control mb-2" type="text" name="urlInput" id="urlInput" placeholder="Inserte una URL valida" required>
                <button type="submit" class="btn btn-primary w-100">Editar URL</button>
            </form>
        {{else}}
            <form class="w-75 m-auto" action="/" method="post">
                <input type="hidden" name="_csrf" value="{{csrfToken}}">
                <input class="form-control mb-2" type="text" name="urlInput" id="urlInput" placeholder="Inserte una URL valida" required>
                <button type="submit" class="btn btn-success w-100">Agregar URL</button>
            </form>
    {{/if}}

```

Ya tenemos las sesiones y autenticaciones, es momento de crear los links para cada uno de los usuarios sin que se compartan entre ellos, por lo que sera necesario eliminar nuestra colección de Urls actual.  
Luego deberemos agregar un nuevo apartado a nuestro schema de URLs, quedando el mismo de la siguiente forma.

```js

    const urlSchema = new Schema({

        link: {
            type: 'String',
            unique: true,
            required: true
        },
        short: {
            type: 'String',
            unique: true,
            required: true,
        },
        user:{                              // Nueva característica que se linkea al id
            type: Schema.Types.ObjectId,    // Toma el id del user
            ref: 'User',                    // Toma el esquema del user para tener el id
            required: true,
        }
    });

```

Al haber modificado esto es momento de modificar todo nuestro controller para que compruebe que el usuario sea el correcto, quedando de la siguiente manera.

```js

    const readURLs = async (req, res) => {

        try {
            const links = await Url.find({ user: req.user.id }).lean()      // Al buscar toma como parámetro el id del usuario qur armamos anteriormente
            res.render("home", { links: links });
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            res.redirect("/")
        }
    }

    const addURLs = async (req, res) => {

        const errors = validationResult(req)

        if (!errors.isEmpty()) {
            req.flash("messages", errors.array())
            return res.redirect("/")
        }

        const { urlInput } = req.body

        try {
            const url = new Url({
                link: urlInput,
                short: nanoid(8),
                user: req.user.id,      // Toma el id del user
            })

            await url.save()

            req.flash("messages", [{
                msg: "¡Url agregada!"
            }])

            res.redirect("/")

        } catch (err) {

            req.flash("messages", [{
                msg: err.message
            }])

            res.redirect("/")
        }

    }

    const deleteURLs = async (req, res) => {

        const { linkId } = req.params

        try {
            const urlFromDataBase = await Url.findById(linkId)      // Busca el id en base al link
            
            if (!url.user.equals(req.user.id)) {        // Si no coincide la url de la base de datos con la enviada, se genera el error
                throw new Error("URL no encontrada")
            }
            
            await urlFromDataBase.remove();         // Si se encuentra, se elimina
            
            req.flash("messages", [{
                msg: "URL eliminada"
            }])
            
            res.redirect("/")
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            
            res.redirect("/")
        }

    }

    const updateUrlsForm = async (req, res) => {

        const { linkId } = req.params

        try {
            const urlFromDataBaseForEdit = await Url.findById(linkId).lean()
            
            if (!url.user.equals(req.user.id)) {
                throw new Error("URL no encontrada")
            }
            
            return res.render("home", {
                urlFromDataBaseForEdit
            })
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            
            res.redirect(`/update/${linkId}`)
        }

    }

    const updateUrls = async (req, res) => {

        const errors = validationResult(req)

        if (!errors.isEmpty()) {
            req.flash("messages", errors.array())
            return res.redirect(`/update/${linkId}`)
        }

        const { linkId } = req.params
        const { urlInput } = req.body

        try {
            const urlFromDataBase = await Url.findById(linkId)
            
            if (!url.user.equals(req.user.id)) {
                throw new Error("URL no encontrada")
            }
            
            await urlFromDataBase.updateOne({ link: urlInput });        // Modifica solamente la propiedad con la url pasada por el input
            
            req.flash("messages", [{
                msg: "URL editada"
            }])
            
            res.redirect("/")
        } catch (err) {
            req.flash("messages", [{
                msg: err.message
            }])
            
            res.redirect(`/update/${linkId}`)
        }

    }

    const redirectToShortUrl = async (req, res) => {
        const { shortUrl } = req.params;
        
        try {
            const urlInDB = await Url.findOne({
                short: shortUrl
            })
            
            res.redirect(urlInDB.link)
        } catch (err) {
            req.flash("messages", [{
                msg: "URL no encontrada"
            }])
            
            res.redirect("/auth/login")
        }
    }

```

No podemos hacer que el usuario escriba su propio token cada vez que necesite confirmar su cuenta, por eso le enviaremos un mail cuando se registre. Para ello haremos uso del paquete [`nodemailer`](https://nodemailer.com/about/), el cual instalaremos con el siguiente comando.

```cmd

    npm i nodemailer

```

Para la prueba de los mails usaremos [`mailtrap`](https://mailtrap.io/), en el cual deberemos crear una cuenta. Al iniciar sesión deberemos ir a nuestro inbox y seleccionar la integración con NodeJs/Nodemailer.

```text

    home (https://mailtrap.io/inboxes)
        |
        |> My inbox
            |
            |> Integrations |> Node.js |> Nodemailer        // Copiamos el modulo que nos da

```

Los datos que nos da nodemailer deberían ser ocultos, por ello tenemos que crear una variable en el `.env` que luego tomaremos para reemplazarla como usuario y contraseña. En el mismo tendremos los datos `user` y `pass` del modulo respectivamente.

```env

    mailUser= <código del user de nodemailer>
    mailPass= <código del pass de nodemailer>

```

Ahora podemos llevar el modulo al `authController` para enviarlo cada vez que se crea el usuario, quedando el mismo de la siguiente forma.

```js

    const nodemailer = require('nodemailer');
    require("dotenv").config();

    const transport = nodemailer.createTransport({
        host: "smtp.mailtrap.io",
        port: 2525,
        auth: {
            user: process.env.mailUser,
            pass: process.env.mailPass
        }
    });

    await transport.sendMail({
        from: 'URL shortener',
        to: user.userMail,
        subject: "Verifique su casilla de correo",
        html: `<a href="http://localhost:5000/auth/confirmation/${user.tokenConfirmation}"> Haga click aquí para verificar su cuenta </a><br>
        O copie y pegue el siguiente link en su navegador:<br> 
        http://localhost:5000/auth/confirmation/${user.tokenConfirmation}`,
    });

```

Con esto tenemos nuestro mail hecho, el cual podemos probar su uso gracias a mailtrap.
