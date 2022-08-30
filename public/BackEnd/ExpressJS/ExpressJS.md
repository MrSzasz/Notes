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
