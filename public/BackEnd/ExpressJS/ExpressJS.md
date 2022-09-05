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

Esto podemos usarlo para crear varias respuesta dependiendo de las rutas, por ejemplo, crearemos una respuesta para la informacion y otra para el contacto de la siguiente forma.

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

    [...]       // Resto del codigo 

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
