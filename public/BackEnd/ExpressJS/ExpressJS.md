# ExpressJS

[ExpressJS](https://expressjs.com/) es un framework diseñado para NodeJS que nos ayuda a crear aplicaciones grandes con módulos propios, trabajando con las peticiones y respuestas HTTP para gestionar las rutas y endpoints.  
Para empezar debemos instalarlo, para ello usaremos el comando que nos indica en su [documentación](https://expressjs.com/en/starter/installing.html).

```cmd

    npm install express

```

> Para poder instalarlo es necesario tener instalado NodeJS

## Configuración del entorno

Para poder hacer las pruebas de nuestro proyecto vamos a necesitar configurar ciertas cosas, empezando por crear un proyecto con NodeJS, para ello abriremos nuestra consola en VSC y escribiremos el siguiente comando.

```cmd

    npm init -y

```

> El `-y` nos toma las configuraciones predeterminadas, ya que no sera necesario que estén especificadas para esta prueba

Luego debemos crear nuestro archivo js principal, en el que escribiremos todo nuestro código de pruebas, para ello creamos un archivo llamado `index.js`.  
Para que nuestro servidor pueda iniciarse podemos usar Node, pero deberemos volver a iniciarlo cada vez que se haga un cambio en el archivo, es por eso que haremos uso del paquete llamado [`Nodemon`](https://www.npmjs.com/package/nodemon), el cual nos ayuda detectando los cambios en nuestro servidor y reiniciándose cuando sea necesario, para ello usaremos el comando que nos indica de la siguiente manera.

```cmd

    npm i nodemon -D

```

> Con `-D` indicamos que solo se instalará como una dependencia de desarrollador, ya que no será necesario para el funcionamiento posterior del mismo

Por ultimo debemos configurar los scripts que nos ayudarán para iniciar Nodemon, para ello iremos al archivo llamado `package.json` y cambiaremos los scripts, quedándonos de la siguiente forma.

```json

    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "start": "node index.js",       // Inicia el servidor con Node
        "dev": "nodemon index.js"       // Inicia el servidor con Nodemon
    }

```

> Para su uso deberemos escribir `npm run dev` en la consola cuando lo necesitemos

## Routes

Lo primero que podemos probar de Express son las rutas, es decir, las respuestas que daremos dependiendo de la url que se envíen. Para ello crearemos nuestro primer servidor y primer respuesta en el archivo `index.js` de la siguiente forma.

```js

    const express = require('express');         // Requerimos Express 
    const app = express();      // Creamos nuestro servidor con Express
    const port = process.env.PORT || 5000;      // Indicamos en que puerto se abrirá el mismo

    app.get('/', (req, res) => {        // Cuando el usuario consulte la pagina raíz
        res.send("HOME")        // Se envía el texto HOME como respuesta
    })

    app.listen(port);       // Escuchamos el puerto que indicamos anteriormente

    console.log(`Server running on port ${port}`);      // Mensaje por consola que nos indica que todo funciona perfectamente

```

Esto podemos usarlo para crear varias respuesta dependiendo de las rutas, por ejemplo, crearemos una respuesta para la información y otra para el contacto de la siguiente forma.

```js

    const express = require('express');
    const app = express();
    const port = process.env.PORT || 5000;

    app.get('/', (req, res) => {
        res.send("HOME")
    })

    app.get('/about', (req, res) => {
        res.send("ABOUT")               // Se genera al pedir la ruta "about"
    })

    app.get('/contact', (req, res) => {
        res.send("CONTACT")               // Se genera al pedir la ruta "contact"
    })


    app.listen(port);

    console.log(`Server on port ${port}`);

```

Todas estas respuestas son en base a una página que existe, pero si queremos mandar una respuesta predeterminada para una pagina que no existe podemos crearla de la siguiente forma.

```js

    [...]       // Resto del código 

    app.get('/contact', (req, res) => {
        res.send("CONTACT")
    })

    app.use((req, res) => {         // Luego de todas las respuestas
        res.status(404)         // Enviamos el status de error 404
            .send(` 
            Error 404!, no se encontró la página solicitada.<br>
            <hr>
            <a href="/">Volver al inicio</a>
            `)          // Generamos la respuesta
    })

    [...]

```

## Body

El cliente puede mandar distintos tipos de request a nuestro servidor, esto se hace mediante el `body` de nuestro request. Para poder obtener estos datos es necesario que se haga un parse antes, lo cual podemos hacer gracias a Express a traves uno de los middlewares disponibles de la siguiente manera.

```js

    const express = require('express');
    const app = express();
    const port = process.env.PORT || 5000;


    app.use(express.json())         // Indicamos que tomará datos JSON
    app.use(express.urlencoded({ extended:false }))         // Indicamos que tomará datos de form o URL básicos


    app.post('/login', (req, res) => {      // Indicamos la URL de donde se tomara el request
        console.log(req.body);          // Tomamos los datos del body y lo imprimimos en consola
        res.send('all done!')        // Creamos una respuesta visual
    })


    app.listen(port);

    console.log(`Server on port ${port}`);

```

> En este caso usaremos `.post` ya que el usuario enviará información al servidor, no pedirá

Para hacer las pruebas necesarias sin crear un formulario en HTML podemos usar dos extensiones diferentes de VSC, una de ellas es [`RapidAPI`](https://marketplace.visualstudio.com/items?itemName=RapidAPI.vscode-rapidapi-client) o ['Thunder Client'](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client). Ambas tienen la misma base de funcionamiento, deberemos poner nuestro servidor ('http://localhost:5000/') con el método POST de envío y en el body del mismo debemos enviar los datos con formato JSON.

```json

    {
        "name": "Jolyne",
        "surname": "Cujoh"
    }

```

Con los pasos que hicimos anteriormente, al enviar los datos deberemos verlos impreso en consola.

## Params

Así como el usuario puede pasar los datos por body del request, también puede pasarlos como parámetros en los datos de la URL. Esto se puede obtener gracias al método `.params` de la siguiente manera.

```js

    const express = require('express');
    const app = express();
    const port = process.env.PORT || 5000;


    app.get('/login/:username', (req, res) => {         // El : indica que luego se tomará el parámetro indicado
        console.log(req.params);        // Imprimimos el objeto en consola
        res.send(`Bienvenido ${req.params.username}`);      // Usamos la propiedad "username" que creamos y mandamos en el parámetro
    })


    app.listen(port);

    console.log(`Server on port ${port}`);

```

> El nombre del parámetro será el que nosotros declaremos en la URL, y el valor el que le pasamos

Para probar esto deberemos ir a la ruta que indicamos, agregando el parámetro que querramos.  
También es posible enviar mas de un parámetro, siempre y cuando lo indiquemos en la url.

```js

    [...]

    app.get('/login/:name/:surname', (req, res) => {        // Indicamos la cantidad y nombre de los parámetros
        console.log(req.params);
        res.send(`Nombre: ${req.params.name}, Apellido: ${req.params.surname}`);
    })

    [...]

```

## Query

Los datos no solo se pasan por parámetros en la URL, sino que se pueden pasar como `queries`, los cuales son variables que se crean para poder obtener desde el servidor con el método `.query`. La particularidad de éstas es que para enviarse se hacen luego del símbolo `?`, ademas de que se pueden enviar varias separadas con el símbolo `&`.  
Para tomar las queries se hace de la siguiente manera.

```js

    const express = require('express');
    const app = express();
    const port = process.env.PORT || 5000;


    app.get('/api', (req, res) => {         // Indicamos la URL
        console.log(req.query);         // Tomamos los datos con el método "query" y los imprimimos
        res.send(`Los datos se recibieron correctamente`);
    })


    app.listen(port);

    console.log(`Server on port ${port}`);

```

> TODOS los valores enviados por URL son de tipo string

Para que esto funcione debemos ingresar a la URL `http://localhost:5000/api?variable=valor`, la cual imprime en consola `{variable: "valor"}`.  
Esto mismo se utiliza bastante en los motores de búsqueda para poder ingresar los valores necesarios, normalmente usando `?q=lo%20que%20se%20quiere%20buscar` siendo `%20` el valor que se le asigna a un espacio.

## Middlewares

Los `middlewares` son funciones que, como su nombre lo indica, se encuentran en medio de las diferentes rutas, siendo las que interceptan los request antes de que lleguen a las rutas. Estos pueden tener diferentes usos, desde tomar los datos de las request hasta evitar que un usuario sin autorización ingrese en una pagina en concreto.  
Los middlewares tienen una función especial llamada `next()`, la cual indica que puede seguir luego de lo que se hizo en la función. Para mostrar esto tendremos dos ejemplos, el primero que solo toma los datos y el segundo que comprueba las queries.

```js

    const express = require('express');
    const app = express();
    const port = process.env.PORT || 5000;

    // Middleware de información

    app.use((req, res, next) => {        // Llamamos al next para poder usarlo luego
        let time = new Date();      // Tomamos la fecha del request
        console.log(`${req.method} at ${time}`);        // Imprimimos todo en consola
        next();         // Indicamos que siga con la petición
    })

    // Rutas básicas

    app.get('/', function (req, res) {
        res.send("home")
    })

    app.get("/login", (req, res) => {
        res.send("login page")
    })


    // Middleware de autenticación

    app.use((req, res, next) => {
        if (req.query.mail === "userMail@example.com") {        // Comprobamos si se envió la query mail
            console.log(`user = ${req.query.mail}`);
            next();         // Si es la que indicamos, sigue
        }
        res.send("User not found!");        // Si no, se envía lo indicado como respuesta y no sigue a "/profile"
    })

    // Rutas privadas

    app.use("/profile", (req, res) => {
        res.send("profile page");
    })


    app.listen(port);

    console.log(`Server on port ${port}`);

```

En este ejemplo el middleware de comprobación intercepta todas las request, si no cumplen con la condición nunca se podrá llegar a la siguiente ruta, es decir, si entramos en `/profile` nos dará error, en cambio, si entramos en `/profile?mail=userMail@example.com` nos muestra los datos de la ruta `/profile`.

Ademas de esto también es posible usar métodos creados por la comunidad, para esto debemos buscarlos en [npm](https://www.npmjs.com/), a medida que necesitemos hacer algo en en particular en nuestro código.  
Un ejemplo de esto es el middleware llamado [`Morgan`](https://www.npmjs.com/package/morgan), el cual intercepta los datos del usuario y los muestra por consola.  
Para poder instalarlo deberemos hacer uso del comando que nos indica en su página.

```cmd

    npm i morgan

```

Hecho esto, debemos importarlo en nuestro código y usarlo como vimos anteriormente.

```js

    const express = require('express');
    const app = express();
    const port = process.env.PORT || 5000;
    const morgan = require('morgan');       // Requerimos morgan


    // Middleware de información

    app.use(morgan("tiny"))         // Lo usamos antes como middleware, pasando las propiedades como indica su documentación

    // Rutas básicas

    [...]

```

## Static

Express tiene la posibilidad de mostrar archivos estáticos que se encuentren en el lado del Front-end, para ello se usa el middleware `static` y el modulo `path` para poder indicar la ruta que se esta utilizando. Para ello necesitamos crear una carpeta `public` con nuestro `index.html` y una hoja de estilos css (no es necesario, pero sirve para mostrar mejor el ejemplo).  
Hecho esto, en nuestro archivo js configuraremos lo necesario para acceder a los archivos del Front.

```js

const express = require('express');
const app = express();
const port = process.env.port || 5000;
const path = require('path');       // Requerimos el modulo path para tener la ruta principal


app.use(express.static(         // Utilizamos el middleware
    path.join(__dirname, 'public')      // Le pasamos join para concatenar la raíz con la carpeta public
));


app.listen(port, () => {
    console.log('listening on port ' + port);
});

```

> Normalmente static se utiliza luego de las rutas, ya que al ser un middleware intercepta las peticiones que hace el usuario y puede ocasionar fallos de lógica

Con esta configuración hecha podemos visualizar todo lo que se escriba en el archivo `index.html`, pudiendo desarrollar el Front a gusto, funcionando todo tipo de archivo (HTML, CSS, Js, etcétera).

## Router

A medida que nuestra aplicación crezca vamos a ver que nuestro archivo principal se va a llenar de rutas, lo que no queda visualmente bien, ya que estará todo desordenado. Para ello podemos separar nuestras rutas en diferentes módulos con ayuda del paquete de Express llamado `Router`.  
Para poder hacer uso del mismo primero crearemos una carpeta llamada `routes` en la que tendremos todas nuestras rutas. Dentro de esta crearemos el archivo llamado `home.js`, para crear nuestra primer ruta inicial de la siguiente manera.

```js

    const { Router } = require('express');      // Requerimos Router desde Express

    const router = Router()         // Hacemos uso de Router para generar las respuestas

    router.get('/', (req, res) => {         // Cambiamos app por router, y el resto es igual
        res.send('Welcome!')
    })

    module.exports = router;        // Importamos el modulo para usarlo en el archivo principal

```

También podemos crear un archivo para los usuarios llamado `users.js`, indicando las diferentes rutas que se relacionen con los usuarios.

```js

    const { Router } = require("express")

    const router = Router();

    router.get('/register', (req, res) => {
        res.send("User register")
    })

    router.get('/login', (req, res) => {
        res.send("User login")
    })

    router.get('/users', (req, res) => {
        res.send("Main page user")
    })

module.exports = router;

```

Hecho esto podemos importarlas en el archivo principal y utilizarlos para generar las rutas.

```js

    const express = require('express');
    const app = express();
    const port = process.env.port || 5000;

    const RouterHome = require('./routes/home')         // Le asignamos un nombre a la ruta e importamos nuestros archivos
    const RouterUsers = require('./routes/users')

    app.use(RouterHome)         // Los utilizamos con el método "use" para generar las respuestas
    app.use(RouterUsers)

    app.listen(port, () => {
        console.log('listening on port ' + port);
    });

```

Gracias a esto nuestra aplicación queda mucho mas legible y ordenada, ademas de separar cada archivo con su respectivo funcionamiento.

## Templates engines

Desde el Back-end es posible generar contenido del gracias a los llamados `motores de plantillas`, que como su nombre lo indica son generadores de plantillas HTML que a su vez agregan mejores funcionalidades, como la posibilidad de generara contenido en base a los datos que enviemos. En este caso haremos uso del engine [`EJS`](https://ejs.co/), el cual instalaremos como lo indica [su documentación](https://ejs.co/#install).

```cmd

    npm install ejs

```

Luego de instalarlo debemos crear la carpeta en donde tendremos los archivos para el Front, llamada `views`, y dentro de la misma agregaremos nuestro archivo base que servirá como lienzo base para todo el Front, llamado `index.ejs`.

```html

    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Node EJS</title>
    </head>

    <body>
        <h1>Welcome!</h1>
    </body>

    </html>

```

Por el momento solo tendremos la base normal de HTML, pero lo cambiaremos luego para ver lo que realmente puede ofrecer el engine.  
Luego, en nuestro archivo js indicaremos las configuraciones necesarias para el funcionamiento del mismo de la siguiente manera.

```js

    const express = require('express');
    const app = express();
    const port = process.env.port || 5000;
    const path = require('path')
    require('ejs');         // Requerimos ejs


    const RouterHome = require('./routes/home')
    const RouterUsers = require('./routes/users')
    
    
    app.set("view engine", "ejs");       // Indicamos que motor se usará
    app.set('views', path.join(__dirname, 'views'))         // Indicamos en donde esta nuestra carpeta de vistas


    app.use(RouterHome)
    app.use(RouterUsers)


    app.listen(port, () => {
        console.log('listening on port ' + port);
    });

```

Ahora ya es posible utilizar nuestro engine en las rutas, para ello usaremos el método `render()`, indicando que plantilla usaremos y a la vez, enviando los datos que generaremos en el HTML, que es una de las nuevas posibilidades que nos otorgan los engines.

```js

    const { Router } = require('express');

    const router = Router()

    router.get('/', (req, res) => {
        let title = "Mensaje enviado con EJS"        // Creamos el dato que vamos a pasar como parámetro
        res.render('index', { title })      // Usamos "render" indicando el archivo base y pasamos title como parámetro
    })

    module.exports = router;

```

Por ultimo, para que el dato se vea en el Front, debemos hacer uso del mismo en nuestro archivo `.ejs` como lo indica su documentación, con `<%=  %>`, quedándonos de la siguiente forma.

```html

    <body>
        <h1><%= title %></h1>
    </body>

```

Ahora podremos ver que la ruta `http://localhost:5000/` nos muestra el titulo que nosotros le pasamos, el cual podemos cambiar a gusto y se reflejará el cambio cada vez que recarguemos la página.  
Pero esto a la larga también generará código repetido, pero en el lado del HTML, es por eso que podemos dividir nuestro código en forma de `partials (o componentes)`, para ello empezamos creando la carpeta `partials` dentro de la carpeta `views`, dentro de la misma crearemos dos archivos `.ejs` para los elementos que se repiten en todos los archivos, la parte del head y el final del HTML, siendo los mismos los archivos `top.ejs` y `bottom.ejs` respectivamente.

```HTML

    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Node EJS</title>
    </head>

    <body>

```

Y en el `bottom.ejs` lo que nos queda al final del HTML.

```HTML

    </body>

    </html>

```

Para mostrar el funcionamiento del mismo crearemos un archivo de vista llamado `users.ejs` para mostrarlo en la ruta de los usuarios, en el cual importaremos los dos partials que creamos anteriormente de la siguiente forma.

```HTML

    <%- include('partials/top') %>      <!-- Usamos include y le pasamos como parámetro la ubicación de nuestro partial -->

    <h1>Users</h1>

    <%- include('partials/bottom') %>

```

Y por ultimo nos queda usar `render` para indicar que archivo se va a utilizar en la ruta `'/users'`, en nuestro archivo `users.js` dentro de `routes`.

```js

    router.get('/users', (req, res) => {
        res.render("users")
    })

```

Así como podemos pasar variables desde el back con EJS, también es posible ejecutar funcionalidades de JavaScript en el mismo, como poder recorrer arrays y generar código con ello. Para ello empezaremos usando el modulo [`Axios`](https://axios-http.com/docs/intro), el cual nos permite usar un Fetch como lo haríamos en el Front.  
Primero instalaremos Axios con el comando que nos indica su pagina.

```cmd

    npm i axios

```

Hecho esto lo usaremos en nuestro js de usuarios para hacer un pedido a [`JSON Placeholder`](https://jsonplaceholder.typicode.com/) de la siguiente manera.

```js

    const { Router } = require("express")
    const axios = require("axios")      // Importamos Axios para su uso

    const router = Router();

    router.get('/users', async (req, res) => {      // Creamos la función asíncrona ya que espera a una base de datos
        let usersFromJSONPlaceholder = await axios.get('https://jsonplaceholder.typicode.com/users')        // Guardamos los datos en una variable
        res.render("users", {
            users: usersFromJSONPlaceholder.data        // Enviamos esos datos hacia el Front
        })
    })

    module.exports = router;

```

Y en nuestro `users.ejs` creamos nuestro bucle forEach de EJS de la siguiente manera.

```HTML

    <%- include('partials/top') %>

    <h1>Users</h1>
    
    <ul>

        <% users.forEach(user => { %>       <!-- Por cada elemento en el array -->
        <li>user: <%= user.username %><br> mail: <%= user.email %> </li>        <!-- Creamos el item en la lista -->
        <hr>
        <% }) %>

    </ul>

    <%- include('partials/bottom') %>

```

## REST API

REST API se llama al servidor que sirve como mediador entre el cliente y el servidor, el cual se comunica en base a las peticiones que el mismo cliente envía, y las respuesta que maneja el servidor con la base de datos. En este caso haremos una API simple que nos permita interactuar con una base de datos que contiene diferentes usuarios.  
En este ejemplo usaremos el método [CRUD](https://codigofacilito.com/articulos/crud-backend) y un cliente de peticiones para probarlas. Empezaremos creando un nuevo proyecto, en el mismo iniciaremos npm e instalaremos los módulos que usaremos mas adelante.

```cmd

    npm init -y
    npm i express morgan
    npm i nodemon -D

```

Luego, crearemos los archivos necesarios, siendo estos `.gitignore` para incluir nuestra carpeta de `node_modules` y luego el archivo `server.js` para todo nuestro código.  
Hecho esto configuraremos nuestro `package.json` para incluir los scripts necesarios.

```json

    "scripts": {
        "dev": "nodemon server.js",
        "start": "node server.js"
    }

```

En nuestro archivo js agregaremos la base de Express, incluyendo `Morgan`.

```js

    const express = require('express');
    const app = express();
    const port = process.env.port || 5000;
    const morgan = require('morgan');

    const usersDB = [
        {
            name : "Johnny",
            i: 1
        }
    ];       // Array que simula nuestra base de datos 

    app.use(express.json());
    app.use(express.urlencoded({extended: false}));
    app.use(morgan('dev'));

    app.listen(port, () => {
        console.log('listening on port ' + port);
    });

```

Empezaremos creando las respuestas base para las diferentes request.

```js

    [...]

    app.get('/user', (req, res) => {        // Obtenemos todos los usuarios
        res.json(usersDB)       // Enviamos los datos en formato JSON
    })

    app.get('/user/:id', (req, res) => {        // Obtenemos un usuario
        res.json(usersDB)
    })

    app.post('/user', (req, res) => {       // Agregamos usuarios
        res.json(usersDB)
    })

    app.put('/user/edit/:id', (req, res) => {       // Editamos un usuario
        res.json(usersDB)
    })

    app.delete('/user/delete/:id', (req, res) => {      // Borramos un usuario
        res.json(usersDB)
    })

    [...]

```

Para hacer uso de esta API debemos usar un gestor de peticiones como los nombrados anteriormente, para simular las respuestas de una API. Podemos probar esto haciendo una petición GET a la ruta `http://localhost:5000/user`, la cual nos devolverá el usuario que tenemos agregado.  

### Agregar usuario

Hecho esto, podemos agregar las siguientes rutas, empezando por agregar un nuevo usuario con el método POST, la misma tomará los datos que enviemos desde el body con formato JSON y lo usara para enviarlo dentro de nuestro array.

```js

    app.post('/user', (req, res) => {
        let userData = req.body         // Tomamos los datos enviados por el body
        let newUser = {
            ...userData,        // Tomamos solo los datos de nombre
            id: usersDB.length + 1      // Y le generamos un id en base a la longitud del array + 1
        }
        usersDB.push(newUser)       // Sumamos el nuevo usuario a nuestra base de datos
        res.json(newUser)       // Respondemos con el usuario que se creó
    })

```

> Para probar esto, debemos hacer una petición POST con el dato del usuario (`{ "name" : "DIO" }`) dentro del body en formato JSON

### Buscar usuario

Luego de esto podemos buscar un usuario por su id en la base de datos. Para esto usaremos el método `.find()` propio de JavaScript, quedándonos de la siguiente manera.

```js

    app.get('/user/:id', (req, res) => {        // Indicamos que se tiene que pasar un parámetro por URL
        let findUserInDB = usersDB.find((user) => user.id === parseInt(req.params.id))      // Buscamos el usuario en base al id que nos pasaron como parámetro
        findUserInDB 
            ? res.json(findUserInDB)        // Si el usuario se encuentra se envía como respuesta JSON
            : res.status(404)       // Si el usuario no se encuentra se envía un estado 404
                .json({
                    "message": "User not found"         // Y el mensaje de error
                })
    })

```

### Editar un usuario

Basándonos en la idea de poder buscar un usuario por su id, podemos editar sus datos. Para ello usaremos la base de buscar el usuario y luego usaremos el método `.map()` para generar el nuevo array con los datos modificados.

```js

    app.put('/user/:id', (req, res) => {        // indicamos el método
        let userData = req.body         // Tomamos los datos
        let findUserInDB = usersDB.find((user) => user.id === parseInt(req.params.id))       // Lo buscamos en la base de datos
        if (findUserInDB) {
            usersDB = usersDB.map((userInMap) => userInMap.id === parseInt(req.params.id) ? {       // Hacemos un map por cada elemento en el array
                ...userInMap,       // Tomamos los datos del usuario encontrado
                ...userData         // Y agregamos/cambiamos los que nos envió el usuario
            } : userInMap)          // Sino, lo dejamos como estaba
            res.json(usersDB);
        }
        return res.status(404).json({
            "message": "User not found"
        })
    })

```

### Eliminar usuario

Por ultimo nos queda eliminar el usuario de la base de datos, lo cual haremos de la misma forma que el anterior pero esta vez usando el método `.splice()` y `.findIndex()` para buscar el index del usuario en cuestión.

```js

    app.delete('/user/:id', (req, res) => {
        let findIndexUserInDB = usersDB.findIndex((user) => user.id === parseInt(req.params.id))        // Si lo encuentra retorna su índice
        if (findIndexUserInDB !== -1) {         // Si no es "-1", es decir, si existe
            usersDB.splice(findIndexUserInDB, 1)        // Elimina el usuario en base a su index
            return res.json(usersDB);
        }
        res.status(404).json({
            "message": "User not found"
        })
    })

```

Con esto hecho ya tendríamos armado nuestra primer APIrest simple pero funcional, sabiendo las bases de como funcionan las peticiones y las respuestas. En un ambiente real esta misma se debe linkear con una base de datos externa, la cual tiene sus propios métodos y funciones para poder modificarlas, pero la lógica es similar en ambos casos.
