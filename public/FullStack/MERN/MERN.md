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
    - [Tailwind](#Tailwind-css)
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
npm i sass wouter react-icons
```

> Con esto instalamos [Sass](../../Front-End/Sass/Sass.md) para los estilos y Wouter para manejar las rutas.

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

Con Nodemon instalado debemos agregar dos scripts importante para el funcionamiento del servidor, para ello nos dirigiremos al archivo `package.json` del back (`server/package.json`). y cambiaremos el apartado `scripts` para que nos quede de la siguiente manera.

```json
"scripts": {
    "run": "node index.js",         // Inicia el proyecto con Node
    "dev": "nodemon index.js"       // Inicia el proyecto con Nodemon
},
```

También es posible cambiar los datos automáticos que nos generó el npm init, por ejemplo el nombre del proyecto, descripción o el autor.

## Tailwind CSS

Para el front lo primero que debemos hacer es configurar Tailwind CSS, para ello debemos instalar ciertas dependencias que necesitaremos en modo de desarrollo. Para ello usaremos el siguiente comando

```cmd
npm install -D tailwindcss postcss autoprefixer
```

Al finalizar usaremos el siguiente.

```cmd
npx tailwindcss init -p
```

Por ultimo debemos agregar los archivos que utilizaremos en el proyecto en la configuración de Tailwind, modificando el archivo `tailwind.config.cjs` de la siguiente manera.

```cjs
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Por ultimo debemos importar los estilos de Tailwind en nuestro `index.css`.

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Con esto hecho podemos levantar el servidor e iniciar con el codigo de nuestro proyecto.

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

Para empezar debemos crear el inicio de nuestra página, en esta misma crearemos un login simple con opcion de registro y de usar el mismo como invitado, para ello empezaremos modificando el archivo `Home.tsx` de la siguiente manera.

```tsx
import Form from "../../components/Form/Form";    // Importamos el componente que utilizaremos

const Home = () => {
  return (
    <div className="relative grid grid-cols-1 md:grid-cols-3 w-full h-screen">
      <div className="relative hidden md:block col-start-1 col-end-3">
        <img
          className="h-full object-cover object-center"
          src="https://picsum.photos/1920/1280"
        />
        <div className="absolute h-full w-full  backdrop-blur-sm inset-0 grid place-content-center">
          <div className="absolute w-full h-full bg-black opacity-75 -z-10"></div>
          <h1 className="text-5xl">TITLE OF THE PAGE</h1>
          <p>
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Ad, ipsum!
          </p>
        </div>
      </div>
      <div className="col-start-3">
        <Form />      // Y lo llamamos
      </div>
    </div>
  );
};

export default Home;
```

Es un Home simple con un estilo basico para no dejar pasar la oportunidad de utilizar Tailwind.

## Form

Con el Home maquetado podemos centrarnos en las bases del formulario de inicio de sesión. Para ello modificaremos el archivo `Form.tsx` que creamos anteriormente, quedando el mismo de la siguiente manera.

```tsx
const Form = () => {
  return (
    <>
      <form className="p-8 grid place-content-center items-center h-full">
        <h1 className="text-center pb-4"> Sign in</h1>
        <div className="relative z-0 w-full mb-6 group">
          <input
            type="email"
            name="loginEmail"
            id="loginEmail"
            className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
            placeholder=" "
            required
          />
          <label
            htmlFor="floating_email"
            className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
          >
            Email address
          </label>
        </div>
        <div className="relative z-0 w-full mb-6 group">
          <input
            type="password"
            name="floating_password"
            id="floating_password"
            className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
            placeholder=" "
            required
          />
          <label
            htmlFor="floating_password"
            className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
          >
            Password
          </label>
        </div>
        <button
          type="submit"
          className="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        >
          Login
        </button>
      </form>
      <div>
        <h2>No account?</h2>
        <button
          type="submit"
          className="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        >
          Enter without account
        </button>
        <button
          type="submit"
          className="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        >
          Register
        </button>
      </div>
    </>
  );
};

export default Form;
```

## Back

## Cierre
