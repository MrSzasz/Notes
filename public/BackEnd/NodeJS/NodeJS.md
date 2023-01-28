# NodeJS

[NodeJS](https://nodejs.org/es/) es un entorno de ejecución en el lado del servidor, basado en JavaScript, el cual soporta una gran carga de procesos y peticiones simultáneas, con un tiempo de respuesta muy corto. El mismo es uno de los más utilizados a la hora de crear un servidor back-end, pudiendo hacer uso de `paquetes npm`.

## Guía de Temas

1. [Instalación](#instalación)
2. [Express](#express)
3. [Configuración de entorno](#configuración-del-entorno)
    - [Nodemon](#nodemon)
4. Código de Node
    - [Primeros pasos](#coding)

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

Para probar el mismo debemos ingresar `npm run dev` en la consola, luego de ello debemos dirigirnos a `https://localhost:3000/` y ver como se imprime el texto que ingresamos anteriormente en consola.
