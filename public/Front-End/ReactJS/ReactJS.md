# React JS

[ReactJS](https://reactjs.org/) es una librería de JavaScript diseñada con el fin de crear interfaces de usuario dinámicas mucho mas rápidas, la cual fue creada por Facebook y es utilizada, mas allá de sus respectivas paginas web, en una gran variedad mas como puede ser Uber, Pinterest, Netflix entre otros.  
React esta basado en componentes, lo que lo hace escalable y altamente reutilizable  

## NodeJS

Para iniciar debemos tener instalado [NodeJS](https://nodejs.org/en/), para saber si lo tenemos instalado deberemos abrir [la terminal](https://linube.com/ayuda/articulo/174/abrir-una-consola-de-comandos#:~:text=Windows%20y%20Mac.-,En%20Windows,En%20ella%20debes%20escribir%20cmd.) y escribir el siguiente comando.

```cmd

    node -v

```

Si sale la version es que esta instalado correctamente, de no ser así deberemos ir a la [página de node](https://nodejs.org/en/) e instalar la version LTS, ya que es la mas estable.

## Instalación React

Para crear un proyecto de React hay dos formas principales, la forma clásica usando [`npx create-react-app`](https://reactjs.org/docs/create-a-new-react-app.html#create-react-app) y la forma más actual con [`ViteJS`](https://vitejs.dev/guide/#scaffolding-your-first-vite-project).  

### Create-React-App

Para instalar React de la forma clásica abriremos nuestra terminal en el escritorio (o abrimos la terminar y escribimos `cd Desktop`), y escribimos el siguiente comando.

```cmd

    npx create-react-app nombre-de-mi-proyecto

```

> El nombre del proyecto puede ser cualquiera siempre y cuando no tenga espacios de por medio.

Esto creara una carpeta con todos los archivos necesarios para nuestro proyecto, la cual deberemos abrir con nuestro editor de código preferido (en este proyecto usaremos [Visual Studio Code](https://code.visualstudio.com/)).  
Si vemos el peso total de nuestra carpeta ronda aproximadamente los 200MB/250MB por todas las dependencias instaladas.

### ViteJS

El proyecto creado de la anterior forma suele ser mas pesado porque contiene muchas mas dependencias de las que se usan normalmente, es por ello que actualmente es mas usado `ViteJs` para la creación de las mismas. Para comenzar haremos lo mismo, abriremos la consola en el escritorio pero esta vez el comando sera diferente, ya que nos guiara por las opciones a medida que vayamos eligiendo que proyecto crear.

```cmd

    npm create vite@latest

```

> Tal vez nos pida instalar el paquete para crear el proyecto, el cual aceptamos

Primeramente deberemos escribir el nombre de nuestro proyecto, luego con las flechas de dirección seleccionamos `react` y la variante `react` normal (también es posible usar `react-ts` para tener configurado [TypeScript](../TypeScript/TypeScript.md) en el mismo). Hecho esto deberemos entrar en la carpeta que se creó con `cd nombre-de-mi-proyecto` y ejecutar el comando `npm install`, el cual instalará todas las dependencias necesarias para el proyecto.  
Al terminar podemos notar que el peso del mismo ronda los 30MB/35MB, una gran diferencia a comparación de los 200MB de la forma clásica.  
Para este proyecto usaremos esta ultima forma como base, es por eso que deberemos abrir esta carpeta en VSC par poder seguir con el mismo.

## Coding

Al abrir el proyecto podemos ver las carpetas y archivos que nos creo Vite, dando un repaso por ellos podemos explicar los siguientes.

- ***node_modules***: Son los archivos de las dependencias necesarias para la creación de nuestro proyecto, esta misma no hay que tocar.

- ***public***: Esta es la carpeta en la que se encuentran los archivos públicos del Front End

- ***src***: Es la carpeta en la que crearemos todos nuestros componentes y archivos de React

- ***.gitignore***: Es el archivo que contiene los datos de que carpetas o archivos no se deben subir a los repositorios

- ***index.html***: Es el index base en el cual se basará nuestra aplicación

- ***package-lock.json***: Es el archivo que contiene los datos detallados de los paquetes necesarios para el funcionamiento de nuestra aplicación

- ***package.json***: Contiene los datos de la aplicación, los scripts y las dependencias de las mismas

- ***vite.config.js***: Archivo de configuración de ViteJS

Aunque los archivos ya vienen creados y listos para su uso, para una mejor comprensión de los mismos eliminaremos la carpeta `src` y la crearemos nosotros desde cero.

## Archivos básicos

Para comenzar completamente desde cero podemos hablar del archivo `index.html`, el cual es el archivo HTML que contiene nuestra futura aplicación, la misma es una base normal de HTML pero tiene dos puntos clave que veremos a continuación. Comenzamos creando nuestra base HTML normal (en VSC si escribimos el símbolo de exclamación `"!"` y damos ENTER tendremos automáticamente creado el código base).  
Dentro del `body` tendremos un div con el id `root`, el cual usaremos como lienzo para toda nuestra aplicación, y también un script que sera donde tendremos toda la lógica de programación.

```HTML

    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>React-WEB</title>
    </head>

    <body>
    
        <div id="root"></div>       <!-- DIV base que contendrá nuestra aplicación -->

        <script type="module" src="./src/main.jsx"></script>        <!-- Importamos el modulo que crearemos próximamente -->

    </body>

    </html>

```

Hecho esto debemos crear nuestra nueva carpeta `src` en la cual crearemos nuestro archivo `main.jsx` (o `index.js` si se usa `create-react-app`).  
En este archivo es donde tendremos nuestra raíz para la aplicación. Hay que saber que React crea las interfaces en JavaScript y luego las "construye" con un comando para que podamos subirlas a nuestro host, y para esto se usa una forma diferente de escribir el código llamada [`jsx`](https://reactjs.org/docs/introducing-jsx.html), la cual se podría tomar como una combinación entre JavaScript y HTML, lo cual veremos en unos instantes.  
Para empezar deberemos importar la librería de React (librería base) y [ReactDOM](https://es.reactjs.org/docs/react-dom.html) (librería para controlar el DOM en el navegador) en nuestro archivo `main.jsx`, para ello las importaremos en las dos primeras lineas de la siguiente forma.

```jsx

    import React from "react";      // Importamos la base de React
    import ReactDOM from "react-dom/client";        // Importamos ReactDOM para el cliente

```

Obviamente nuestra aplicación no funcionara si no importamos React anteriormente, pero luego debemos declarar en donde se crearan las mismas, es por eso que debemos llamar al DIV que creamos con el id `root` y usar los métodos de React y ReactDOM para generar la interfaz de la siguiente forma.

```jsx

    import React from "react";
    import ReactDOM from "react-dom/client";

    const mainDiv = document.getElementById("root");        // Primero tomamos el elemento DIV del HTML 
    const root = ReactDOM.createRoot(mainDiv);      // Creamos la constante raíz y usamos el método para crear la raíz en base al elemento
    root.render();      // Método que utilizamos para renderizar nuestra aplicación

```

> La forma corta que usaremos de ese código será `const root = ReactDOM.createRoot(document.getElementById("root")).render();`

Acá podemos probar por primera vez nuestra aplicación, pasando un elemento dentro del método `render()`.

```jsx

    const root = ReactDOM.createRoot(document.getElementById("root")).render(<h1>Hola, mundo!</h1>);

```

Luego abrimos la [consola de VSC](https://damiandeluca.com.ar/como-usar-la-terminal-integrada-de-visual-studio-code) y escribimos el siguiente comando.

```cmd

    npm run dev

```

Este comando iniciará nuestra app en el servidor, nos dará una dirección con el puerto que se esté usando, el cual pegaremos en nuestro navegador preferido para ver como se genera nuestra página.  
Aquí mismo podemos ver nuestro primer `Hola, mundo` generado con React, el cual se actualizará automáticamente cada vez que actualicemos nuestro archivo de React.  

## Componentes

Pero la forma en la que creamos nuestro primer componente no es la mejor, dado que al escribir mas y mas código se hará difícil de controlar, es por esto que debemos modularizar los componentes de nuestro proyecto. Para ello comenzamos con el componente principal, en el cual importaremos todos los demás componentes.  
En nuestra carpeta `src` creamos un archivo llamado `App.jsx`.

> TODOS los componentes de React deben de estar escritos con PascalCase, es decir, SI O SI deben empezar con mayúsculas, sino React no los tomara como un componente valido

Este será el componente principal de nuestra aplicación, aquí es donde importaremos los otros componentes a medida que vayamos armándolo. Dentro del mismo debemos crear nuestra aplicación base de la siguiente forma.

```jsx

    const App = () => {         // Creamos el componente, empezando con mayúsculas
        return (        // Creamos el return de la función para retornar el contenido del componente
            <h1>Hola, mundo!</h1>       // El contenido del componente en formato JSX
        )
    }

    export default App      // Exportamos el componente para su uso en otro lado

```

> En VSC si se escribe `rafce` se genera automáticamente el componente con el nombre del archivo en cuestión

Esta es una de las formas de escribir el componente, pero también puede ser escrita como una función normal

```jsx

    function App() {
        return (
            <h1>Hola, mundo!</h1>
        )
    }

```

> Esta se genera automáticamente escribiendo `rfce`

O como una clase, la cual es la forma clásica de crear componentes para React, aunque actualmente no se utiliza tanto, pero hay muchos proyectos que siguen teniendo este formato.

```jsx

    import React, { Component } from 'react'         // En este caso si es importante tener React y el componente importados

    export class App extends Component {        // Se crea la clase en vez de crear la función
        render() {
            return (
                <h1>Hola, mundo!</h1>
            )
        }
    }

    export default App

```

> Esta se genera automáticamente con con el comando `rce`

Por comodidad en el proyecto usaremos la primer forma de creación de componentes (`rafce`).  
Como se puede observar, el componente es prácticamente una sintaxis HTML, dado que solo tenemos un `h1` que vamos a exportar, pero este mismo debemos llevarlo al main para que sea la base de todo.

```jsx

    import React from "react";
    import ReactDOM from "react-dom/client";
    import App from "../src/App";       // Importamos el componente principal

    const root = ReactDOM.createRoot(document.getElementById("root")).render(
        <App />         // Usamos el componente principal como parámetro para la raíz
    );

```

Como se puede ver, el componente tiene una forma de llamarse particular, esta sintaxis es propia de JSX, la cual genera los componentes como si fueran etiquetas HTML, las cuales se cierran en la misma, sin necesidad de tener una etiqueta de cierre como tal, a esto se lo llama `Self-closing tag`, dado a que no necesitan un tag de cierre (a menos que tengamos componentes hijos, lo cual veremos mas adelante).
Hecho esto tenemos nuestra base de React configurada, esto es todo lo que se crea automáticamente con ambas herramientas, ya sea con `npx` o `Vite`.
