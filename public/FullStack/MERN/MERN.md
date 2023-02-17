# MERN

MERN es la abreviatura para el stack de tecnologías para proyectos full-stack conformadas por MongoDB, Express, ReactJs y NodeJs. Este es uno de los stacks más utilizados actualmente junto a MEVN (VueJS) y MEAN (Angular).  
En esta guía iniciaremos un proyecto full-stack con MERN, el cual se encargará de guardar usuarios y sus datos, además de utilizar TypeScript para el tipado de React.  
El proyecto se irá subiendo al siguiente [repositorio](https://github.com/MrSzasz/MERN-Job-List).

## ⚠ Pre requisitos ⚠

*IMPORTANTE*  
Para iniciar este proyecto es necesario tener conocimientos en [ReactJS](../../Front-End/ReactJS/ReactJS.md) y en [NodeJS](../../BackEnd/NodeJS/NodeJS.md), además de MongoDB y Express, los cuales se encuentran explicados en las notas de NodeJS. Sumado a esto se utilizará [TypeScript](../../Front-End/TypeScript/TypeScript.md) junto a React.

## Guía de Temas

1. [Configuración del proyecto](#configuración-del-proyecto)
    - [Paquetes](#instalación-de-paquetes)
    - [Scripts](#configuración-de-packagejson)
2. Front-end
    - [Material UI](#material-ui)
    - [Rutas](#routes)
. [Final](#cierre)

---

## Configuración del proyecto

Para comenzar con nuestro proyecto debemos crear una carpeta que contenga nuestro front y nuestro back, para ello crearemos la carpeta raíz (`MERN-Job-List`). Dentro de la misma debemos abrir nuestra consola (escribir `cmd` en la barra de navegación) e iniciamos un proyecto de React con Vite, utilizando el siguiente comando.

```cmd
npm create vite@latest
```

Configuramos el proyecto con React TypeScript y llamamos `client` a la carpeta del proyecto.  
Hecho esto podemos empezar con la carpeta `server`, la cual contendrá todo nuestro back, luego entramos en ella y, al igual que con la carpeta raíz, abrimos la consola dentro de la nueva carpeta. Dentro de la misma configuraremos automáticamente nuestro entorno con el siguiente comando.

```cmd
npm init -y
```

Con esto hecho podemos abrir el proyecto en VSC o el editor de preferencia.

## Instalación de paquetes

Nuestro proximo paso será instalar los paquetes necesarios para el funcionamiento, empezando con el front. Para ello abrimos la consola en el proyecto y nos dirigimos a la carpeta del cliente (`cd /client`), y dentro de esta instalaremos los siguiente paquetes.

```cmd
npm i sass wouter @mui/material @emotion/react @emotion/styled @fontsource/roboto @mui/icons-material
```

> Con esto instalamos [Sass](../../Front-End/Sass/Sass.md) para los estilos, Wouter para manejar las rutas, y MaterialUI con sus iconos y fuente.

Luego será necesario ir a nuestro back para instalar los otros paquetes, podemos hacerlo desde la consola abierta o abrir otra para la carpeta server. Dentro de la misma instalaremos los siguientes paquetes.  

```cmd
npm i express mongoose dotenv cors 
```

> Con esto instalamos Express, Mongoose para conectarnos a la base de datos, Dotenv para las variables de entorno y Cors para las políticas de recursos y conexiones.

También será necesario instalar Nodemon para poder tener nuestro servidor en escucha para los cambios que hagamos, instalándolo como dependencia de desarrollo de la siguiente manera.

```cmd
npm i nodemon -D
```

## Configuración de `package.json`

Con Nodemon instalado debemos agregar dos scripts importante para el funcionamiento del servidor, para ello nos dirigiremos al archivo `package.json`. y cambiaremos el apartado `scripts` para que nos quede de la siguiente manera.

```json
"scripts": {
    "run": "node index.js",         // Inicia el proyecto con Node
    "dev": "nodemon index.js"       // Inicia el proyecto con Nodemon
},
```

También es posible cambiar los datos automáticos que nos generó el npm init, por ejemplo el nombre del proyecto, descripción o el autor.

## Material UI

Para el front lo primero que debemos hacer es configurar MaterialUI, para ello nos dirigiremos al archivo `main.tsx`, en este debemos importar las fuentes de la misma, y el normalizador de css de la siguiente manera.

```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import '@fontsource/roboto/300.css';        // Importamos las fuentes
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';
import App from "./App";
import { CssBaseline } from "@mui/material";        // Y el baseline de CSS

ReactDOM.createRoot(document.getElementById("root") as HTMLElement).render(
  <React.StrictMode>
    <CssBaseline/>      // El cual colocamos antes de nuestra App
    <App />
  </React.StrictMode>
);
```

## Routes

Es momento de crear nuestas páginas y componentes, pudiendo dividir y ordenar mucho mejor todos los archivos que necesitaremos luego. El directorio desde `src` deberia quedarnos de la siguiente manera.

```three
src
├── components
│   ├── Form
│   │     ├── Form.tsx
│   │
│   ├── Navbar
│         ├── Navbar.tsx
│   
|
├── pages
    ├── Dashboard
    │     ├── Dashboard.tsx
    │
    ├── Profile
    │     ├── Profile.tsx
    │
    ├── Home
          ├── Home.tsx
```

Separamos las páginas de los componentes para poder tener un mejor orden de todos los archivos que crearemos, a diferencia de Next, en donde si necesitamos dividir las páginas en sus respectivas carpetas.

## Home

Para empezar debemos crear el inicio de nuestra página, en esta misma crearemos un login simple con opcion de registro y de usar el mismo como invitado, para ello empezaremos modificando el archivo `Home.tsx` de la siguiente manera

```tsx
import Grid from "@mui/material/Grid";            // Importamos el componente Grid
import Form from "../../components/Form/Form";    // Y el componente del formulario

const Home = () => {
  return (
    <Grid container height={"100svh"}>        // Creamos el grid que contendrá todo nuestro componente
      <Grid
        item          // Y el item dentro del grid
        sx={{
          display: { xs: "none", sm: "none", md: "block" },             // Que será visible solo en pantallas md
          backgroundImage: "url('https://picsum.photos/1280/720')",     // Y tendrá la imagen de fondo
          backgroundPosition: "center",
          backgroundSize: "cover",
        }}
        md={7}          // Y en tamaño mediano tomará 7 columnas
      />
      <Grid 
        item xs={12} 
        md={5}
      >
        <Form />      // Llamamos al form
      </Grid>
    </Grid>
  );
};

export default Home;

```

## Back

## Cierre
