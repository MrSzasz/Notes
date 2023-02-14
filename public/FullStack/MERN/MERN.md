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
npm i sass react-router-dom @mui/material @emotion/react @emotion/styled
```

> Con esto instalamos [Sass](../../Front-End/Sass/Sass.md) para los estilos, React-router-dom para las rutas de React, y MaterialUI.

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

## Cierre
