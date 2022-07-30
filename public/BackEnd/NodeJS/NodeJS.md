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

    const animals = require("./animals") //El require siempre requerirá el archivo sin ser necesario agregar la extension

    animals.forEach(anim => {
        console.log(anim) // 🦊, 🐱, 🐶, 🦅, 🐢
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
        console.log(an) // 🦊, 🐱, 🐶, 🦅, 🐢
    });

    console.log(`Hay un total de ${names.length} animales`) // Hay un total de 5 animales

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
        "dev": "nodemon app.js", // Inicia el archivo con Nodemon
        "start": "node app.js" // Inicia el archivo normalmente y se utilizará en su implementación automática
    }

```

Luego de esto, para iniciar el archivo se deberá utilizar el comando que creamos anteriormente, en este caso `npm run dev`.

## Servidor HTTP

El protocolo HTTP es el protocolo que permite la comunicación y transferencia de información de un cliente con el servidor. Para crear nuestro primer servidor sera necesario usar el modulo `HTTP` y darle las instrucciones de lo que se deberá escuchar y responder.

```js

    const http = require('http'); // Modulo requerido
    const port = 5000; // Puerto que usaremos para iniciar en el navegador

    const server = http.createServer((req, res) => { 
        res.end("Esta es mi pagina :D"); // Esto es lo que se vera en la pagina cuando se inicie el servidor
    });

    server.listen(port, () => console.log("El servidor funciona a la perfección!!")); // Log en consola para saber si el mismo esta en funcionamiento

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

    const express = require('express'); // Importa express
    const app = express();
    const port = 5000; // Puerto que usaremos para iniciar en el navegador

    app.get('/', (req, res) => {
        res.send("Esta es mi pagina :D"); // Esto es lo que se vera en la pagina cuando se inicie el servidor
    })

    app.listen(port, () => console.log("El servidor funciona a la perfección!!")); // Log en consola para saber si el mismo esta en funcionamiento

```

Al utilizar `npm run dev` se inicializara como lo hizo con el servidor anterior, la única diferencia visual sera que `express` tiene un formateo por detrás, el cual cambia la fuente por default.  
Aun asi, podemos hacer respuestas diferentes dependiendo de la pagina que se visite, no unicamente el directorio raíz (`/`), para esto se utilizará un middleware de express con la palabra reservada `use`.

```js

    app.use(express.static("public"));

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

    <form action="/form" method="GET"> // Se define el método del envío de los datos, y con Action la pagina a la que se va a redirigir
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
    const port = 5000;

    app.use(express.static("public")); // Toma los archivos estáticos como plantillas

    app.get('/form', (req, res) => { // Toma los datos al completar el formulario con el método GET
        console.log(req.query); // Imprime los datos en consola, con formato de objeto 
        res.send('Formulario enviado!!') // Esto es lo que se vera en la pagina "/form"
    })


    app.listen(port, () => console.log("El servidor funciona a la perfección!!"));

```

> Los datos de `req.query` se verán con el formato de un objeto => { nombre: 'Tomas', apellido: 'Lugo' }

El método `GET`, al ser visible, es peligroso para enviar datos sensibles, es por eso que para esos casos se utiliza el método `POST`, el mismo envía los datos de la misma forma y se pueden interceptar para su uso, pero para el mismo cambia un poco la forma del mismo.  
En este caso los datos se envían a traves del `body`, no de la URL, es por eso que se tiene que usar un `middleware` para parsear los datos y poder recuperarlos, de lo contrario unicamente se recibiría como respuesta `undefined`.

```js

    app.use(express.static("public"));
    app.use(express.urlencoded({ extended: true })); // Middleware para poder tomar los datos que se envían a traves del body

    app.post('/form', (req, res) => {
        console.log(req.body); // Como se hizo anteriormente, toma los datos enviados y los muestra en consola
        res.send('Formulario enviado!!')
    })

    app.listen(port, () => console.log("El servidor funciona a la perfección!!"));

```

> El único cambio que se hizo en el HTML es que se cambio el método `GET` a `POST` del formulario

Sumado a esto es posible hacer validaciones simples de los datos del formulario, redirigiendo a una pagina de error si es que faltan datos.

```js

    app.post('/form', (req, res) => {
        const { nombre, apellido } = req.body; // Hace un destructuring de los datos para obtenerlos como variables
        if (!nombre || !apellido) return res.redirect("/error.html"); // Comprueba los datos, si no se completan se hace una redirección a la pagina de error
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

        if (!nombre || !texto) return res.redirect("/error.html") // Comprueba que existan

        fs.writeFile(`archivos/${nombre}.txt`, texto, (err)=>{ // Método para la creación del archivo 
            if (err) return res.redirect("/error.html") // Acción si es que existe un error en la creación del mismo
            res.send('Se creo el archivo con éxito!!') // Respuesta al crear el archivo
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
            res.download(__dirname + `/archivos/${nombre}.txt`) // Genera la descarga al crear el archivo
        })
    })

```