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
