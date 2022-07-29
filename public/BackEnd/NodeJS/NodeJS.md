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
