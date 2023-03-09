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
3. Back-end
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
npm i wouter react-icons react-hook-form axios react-hot-toast dompurify @types/dompurify @formkit/auto-animate framer-motion uuid
```

> Con esto instalamos `Wouter` para manejar las rutas, `React Hook Form` para gestionar los formularios, `Axios` para hacer la transferencia de datos con el back-end, `React Hot Toast` para generar toasts que informen al usuario, `Dompurify` para purificar los datos ingresados por los usuarios con sus respectivos tipos, `Auto animate` para que se generen las animaciones simples, `Framer Motion` para las animaciones más complejas y `UUID` para generar los ID de los datos que crearemos en el front.

Luego será necesario ir a nuestro back-end para instalar los otros paquetes, podemos hacerlo desde la consola abierta o abrir otra para la carpeta server. Dentro de la misma instalaremos los siguientes paquetes.  

```cmd
npm i express mongoose dotenv cors jsonwebtoken bcrypt
```

> Con esto instalamos Express, Mongoose para conectarnos a la base de datos, Dotenv para las variables de entorno, json Web Token para mantener las sesiones, bcrypt para encriptar las contraseñas y Cors para las políticas de recursos y conexiones.

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
    extend: {
      colors: {                             // Agregamos los colores que usaremos luego en nuestro proyecto.
        "main": "#162446",
        "success": "#22c55e",
        "rejected": "#ef4444",
        "processing": "#eab308",
        "applied": "#3b82f6",
        "later": "#6b7280",
      },
    },
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

Con esto hecho podemos levantar el servidor e iniciar con el código de nuestro proyecto.

## Routes

Es momento de crear nuestras páginas y componentes, pudiendo dividir y ordenar mucho mejor todos los archivos que necesitaremos luego. El directorio desde `src` del front-end debería quedarnos de la siguiente manera (sin incluir los archivos creados por Vite).

```three
src
├── components
│   ├── AddJob
│   │     ├── AddJob.tsx
│   │
│   ├── Form
│   │     ├── Form.tsx
│   │
│   ├── FormErrors
│   │     ├── FormErrors.tsx
│   │
│   ├── JobCard
│   │     ├── JobCard.tsx
│   │
│   ├── JobDetails
│   │     ├── JobDetails.tsx
│   │
│   ├── Navbar
│   │     ├── Navbar.tsx
│   │
│   ├── PopUpModal
│   │     ├── PopUpModal.tsx
│   │
│   ├── Profile
│         ├── Profile.tsx
│   
│
├── helpers
│   ├── errors.ts
│   │
│   ├── requests.ts
│
│
├── interfaces
│   ├── jobsInterfaces.ts
│   
│
├── pages
│   ├── Dashboard
│   │     ├── Dashboard.tsx
│   │
│   ├── Home
│   │     ├── Home.tsx
│   │
│   ├── App.tsx
│   │
│   ├── index.css
│   │
│   ├── main.tsx
│
│
├── .env
│
├── .gitignore
│
├── netlify.toml
```

Separamos las páginas de los componentes para poder tener un mejor orden de todos los archivos que crearemos, a diferencia de Next, en donde si necesitamos dividir las páginas en sus respectivas carpetas.  
En cuanto a las rutas de nuestro back debería quedarnos de la siguiente manera (sin incluir los archivos creados automáticamente).

```three
src
├── controllers
│   ├── jobControllers.js
│   │
│   ├── userControllers.js
│  
│
├── middlewares
│   ├── validateToken.ts
│
│
├── models
│   ├── user.js
│   
│
├── routes
│   ├── jobsRoutes.js
│   │
│   ├── userRoutes.js
│
│
├── .env
│
├── .gitignore
│
├── index.js
```

## Home

Para empezar debemos crear el inicio de nuestra página, en esta misma crearemos un login simple con opción de registro y de usar el mismo como invitado, para ello empezaremos modificando el archivo `Home.tsx` de la siguiente manera.

```tsx
import Form from "../../components/Form/Form";      // Importamos el form que crearemos luego

const Home = () => {
  return (
    <div className="relative grid grid-cols-1 md:grid-cols-3 w-full h-screen">
      <div className="relative hidden md:block col-start-1 col-end-3">
        <img
          className="h-full object-cover object-center"
          src="https://i.imgur.com/twBcBWA.jpg"
        />
        <div className="absolute h-full w-full  backdrop-blur-sm inset-0 grid place-content-center">
          <div className="absolute w-full h-full bg-black opacity-75 -z-10"></div>
          <h1 className="text-5xl">Job Vault</h1>
          <p>
            Welcome to Job Vault, the page that stores and manages all of your
            job applications.
          </p>
        </div>
      </div>
      <div className="md:col-start-3">
        <Form />                        {/* Llamamos al componente que crearemos luego */}
      </div>
    </div>
  );
};

export default Home;
```

Es un Home simple con un estilo básico para no dejar pasar la oportunidad de utilizar Tailwind.

## Form

Como pudimos ver en el Home tenemos el Form, pero no lo creamos aún, es por eso que modificaremos este componente para que quede acorde a lo que necesitamos.

```tsx
import { useState } from "react";
import { Link, useLocation } from "wouter";
import { useForm } from "react-hook-form";
import { Toaster } from "react-hot-toast";
import { FiLogOut } from "react-icons/fi";
import { GoPerson } from "react-icons/go";
import { MdOutlineClose } from "react-icons/md";
import FormErrors from "../FormErrors/FormErrors";
import { UserInterface } from "../../interfaces/jobsInterfaces";     // Importamos las interfaces
import {
  axios_USERS_addData,
  axios_USERS_getData,
} from "../../helpers/requests";                                    // Importamos los helpers que crearemos luego
import { notifyErrorWithToast } from "../../helpers/errors";        // Los handlers de errores

const Form = () => {
  const [registerForm, setRegisterForm] = useState(false);          // Creamos un estado para guardar el tipo de formulario
  const [location, setLocation] = useLocation();                    // Y al location de wouter
  const {
    register,
    handleSubmit,
    formState: { errors },
    watch,
  } = useForm();         // Llamamos al hook del formulario

  const getLoginData = async (data: any): Promise<void> => {        // Creamos la función para traer los datos de la base de datos
    try {
      if (registerForm) {                                   // Si el formulario es de registro
        await axios_USERS_addData(                          // Enviamos datos de usuario al back
          { ...data, jobs: [] }, 
          "users" 
        );

        setLocation("/dashboard");          // Y lo redirigimos al dashboard
      } else {
        await axios_USERS_getData(data, "users");

        setLocation("/dashboard");
      }
    } catch (err) {
      console.log(err);
    }
  };

  const changeFormToRegister = () => {
    setRegisterForm((current) => !current);     // Cambiamos el tipo de formulario
  };

  const handleGuestAccount = () => {                            // Creamos la función para los usuarios sin cuenta
    localStorage.setItem("token", "guest");
    localStorage.setItem("auth", JSON.stringify(true));         // Y guardamos los tokens para los usuarios sin cuenta 
  };

  const ERRORS_TYPES_PASSWORD = {                                   // Creamos el "diccionario" de errores
    required: <FormErrors errorMessage="Insert a password" />,
    maxLength: (
      <FormErrors errorMessage="The password is too long. Maximum length of this field is 21 characters" />
    ),
    minLength: (
      <FormErrors errorMessage="The password is too short. Minimum length of this field is 8 characters" />
    ),
  };

  return (
    <div className="h-full flex flex-col p-8">
      <form
        onSubmit={handleSubmit(getLoginData)}                   // Le pasamos los datos de react hook form
        className="p-8 flex flex-col justify-center h-full"
      >
        <h2 className="text-center pb-8 text-4xl">
          {registerForm ? "Register" : "Sign in"}               // Indicamos que mostrar dependiendo del tipo de formulario
        </h2>
        <div className="relative z-0 w-full mb-6 group">
          <input
            type="text"
            {...register("email", {
              required: true,
              pattern:
                /(?:[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*|"(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])*")@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\[(?:(?:(2(5[0-5]|[0-4][0-9])|1[0-9][0-9]|[1-9]?[0-9]))\.){3}(?:(2(5[0-5]|[0-4][0-9])|1[0-9][0-9]|[1-9]?[0-9])|[a-z0-9-]*[a-z0-9]:(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21-\x5a\x53-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])+)\])/,
            })}             // Indicamos el patrón a validar para que sea un link válido
            id="email"
            className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
            placeholder=" "
          />
          <label
            htmlFor="email"
            className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
          >
            Email address
          </label>
          {
            (errors.email?.type === "required" && (
              <FormErrors errorMessage="Insert a mail" />
            ),
            errors.email?.type === "pattern" && (
              <FormErrors errorMessage="The password is too long. Maximum length of this field is 21 characters" />
            ))      // Mostramos los errores
          }
        </div>
        <div className="relative z-0 w-full mb-6 group">
          <input
            type="password"
            {...register("password", {
              required: true,
              minLength: 8,
              maxLength: 21,
            })}
            minLength={8}
            id="password"
            className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
            placeholder=" "
          />
          <label
            htmlFor="password"
            className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
          >
            Password
          </label>
          {ERRORS_TYPES_PASSWORD[
            errors.password?.type as keyof typeof ERRORS_TYPES_PASSWORD         // Indicamos que error usaremos con la key del diccionario
          ] || null}
        </div>
        {registerForm && (
          <div className="relative z-0 w-full mb-6 group">
            <input
              type="password"
              {...register("repeatPassword", {
                required: true,

                validate: (val: string) => {            // Creamos una validación para indicar si son las mismas contraseñas
                  if (watch("password") != val) { 
                    return false;
                  }
                },
              })}
              id="repeatPassword"
              className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
              placeholder=" "
            />
            <label
              htmlFor="repeatPassword"
              className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
            >
              Confirm password
            </label>
            {errors.repeatPassword?.type === "validate" && (
              <FormErrors errorMessage="The passwords don't match" />
            )}
          </div>
        )}
        <button className="cursor-pointer text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800 flex justify-center items-center gap-4">
          <input
            value={registerForm ? "Register" : "Login"}
            type="submit"
            className="cursor-pointer"
          />
          <FiLogOut />
        </button>
      </form>
      <div className="flex flex-col items-center gap-4">
        {!registerForm && <h2>No account?</h2>}
        <div className="flex flex-col gap-2">
          <button
            onClick={changeFormToRegister}              // Le pasamos la función para cambiar de tipo de formulario
            type="submit"
            className="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800 flex items-center justify-center gap-3"
          >
            {registerForm ? "Cancel" : "Register"}
            {registerForm ? <MdOutlineClose /> : <FiLogOut />}
          </button>
          {!registerForm && (
            <Link
              onClick={handleGuestAccount}              // Le pasamos la función para iniciar como usuario sin cuenta
              href="/dashboard"
              className="text-white bg-teal-700 hover:bg-teal-800 focus:ring-4 focus:outline-none focus:ring-teal-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-teal-600 dark:hover:bg-teal-700 dark:focus:ring-teal-800 flex justify-center items-center gap-3"
            >
              Enter without account
              <GoPerson/>
            </Link>
          )}
        </div>
      </div>
      <Toaster />
    </div>
  );
};

export default Form;
```

## Interfaces

Gracias a que utilizamos TypeScript podemos crear interfaces para manejar los tipos de datos, para ello modificaremos el archivo `jobsInterfaces.ts`. Este archivo se encargará de llevar el registro de todas las interfaces que crearemos para los datos y exportarlas. El archivo nos deberá quedar de la siguiente manera.

```ts
export type statusVariants =      // Los tipos de estado que tendrán nuestros trabajos
  | "success"
  | "rejected"
  | "processing"
  | "applied"
  | "later";

export interface statusColorsVariants {       // Los estados para los colores
  success: string;
  rejected: string;
  processing: string;
  applied: string;
  later: string;
}

export interface JobInterface {       // La interfaz para los trabajos
  id: string;
  title: string;
  link: string;
  description: string;
  status: statusVariants;
  date: string;
  company: string;
  requirements: string;
  extra?: string | null;
}

export interface UserInterface {      // Y para los usuarios
  email: string;
  password: string;
  jobs: [] | JobInterface[];
}

export interface UserDataInterface {      // Además de la interfaz de los datos del usuario desde el back-end
  __v: number;
  _id: string;
  color: string;
  createdAt: string;
  email: string;
  jobs: JobInterface[];
  password: string;
}
```

Con esto hecho podemos pasar a utilizar estas interfaces en otros lados de nuestro proyecto.

## Helpers

Tambien podemos ver en el Form que hacemos uso de los helpers, los cuales son las funciones que nos ayudan con el manejo de datos entre el front-end y el back-end, para ello utilizamos Axios, creando el codigo en el archivo `requests.ts` de la siguiente manera.

```ts
import axios from "axios";                // Importamos Axios
import { JobInterface, UserInterface } from "../interfaces/jobsInterfaces";   // Importamos las interfaces
import { handleRequestErrors, handleUnexpectedRequestErrors } from "./errors";    // Y los handlers de errores
const serverBaseUrl = import.meta.env.URL;        // Y la url que guardaremos en el .env 


/* ============================== JOBS ============================== */


// Traer trabajos de la base de datos

export const axios_JOBS_getData = async (       // Creamos y exportamos la función necesaria
  path: string,
  tokenFromUser: string
) => {
  try {
    const { data } = await axios.get(serverBaseUrl + path, {
      headers: {
        "Authorization": `Bearer ${tokenFromUser}`,           // Enviamos el token
      },
    });
    return data;
  } catch (err) {
    if (axios.isAxiosError(err)) {
      handleRequestErrors(err!);            // Manejamos los errores
    } else {
      handleUnexpectedRequestErrors(err!);
    }
  }
};

// Editar trabajo

export const axios_JOBS_updateData = async (
  dataToUpdate: JobInterface,
  path: string
) => {
  try {
    const { data } = await axios.put(serverBaseUrl + path, dataToUpdate, {     // Le enviamos los datos modificados
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
        "Authorization": `Bearer ${localStorage.getItem("token")}`,
      },
    });
    return data;
  } catch (err) {
    if (axios.isAxiosError(err)) {
      handleRequestErrors(err!);
    } else {
      handleUnexpectedRequestErrors(err!);
    }
  }
};

// Borrar trabajos en la base de datos

export const axios_JOBS_deleteData = async (
  idToDelete: string,
  path: string
) => {
  try {
    const { data } = await axios.delete(serverBaseUrl + path, {
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
        "Authorization": `Bearer ${localStorage.getItem("token")}`,
      },
      data: { jobID: idToDelete }, // Enviamos el ID del trabajo
    });
    return data;
  } catch (err) {
    if (axios.isAxiosError(err)) {
      handleRequestErrors(err!);
    } else {
      handleUnexpectedRequestErrors(err!);
    }
  }
};

// Crear un nuevo trabajo

export const axios_JOBS_addData = async (
  dataFromForm: JobInterface, 
  path: string 
) => {
  try {
    const { data } = await axios.post<JobInterface>(
      serverBaseUrl + path,
      dataFromForm,
      {
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
          "Authorization": `Bearer ${localStorage.getItem("token")}`, 
        },
      }
    );

    return data;
  } catch (err) {
    if (axios.isAxiosError(err)) {
      handleRequestErrors(err!);
    } else {
      handleUnexpectedRequestErrors(err!);
    }
  }
};

/* ============================== USERS ============================== */

// Crea un nuevo usuario

export const axios_USERS_addData = async (
  dataFromForm: UserInterface,
  path: string
) => {
  try {
    const { data } = await axios.post(serverBaseUrl + path, dataFromForm, {
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
      },
    });

    localStorage.setItem("token", data.token);    // Guardamos el token
    localStorage.setItem("auth", data.auth);      // Y le damos autorización

    return data;
  } catch (err) {
    if (axios.isAxiosError(err)) {
      handleRequestErrors(err!);
    } else {
      handleUnexpectedRequestErrors(err!);
    }
  }
};

// Traer datos de usuario de la base de datos

export const axios_USERS_getData = async (
  dataFromUser: UserInterface,
  path: string
) => {
  try {
    const { data } = await axios.get(serverBaseUrl + path, {
      params: { email: dataFromUser.email, password: dataFromUser.password }, 
    });

    localStorage.setItem("token", data.token);
    localStorage.setItem("auth", data.auth);

    return data;
  } catch (err) {
    if (axios.isAxiosError(err)) {
      handleRequestErrors(err!);
    } else {
      handleUnexpectedRequestErrors(err!);
    }
  }
};

// Eliminar un usuario de la base de datos

export const axios_USERS_deleteData = async (
  idToDelete: string,
  path: string
) => {
  try {
    const { data } = await axios.delete(serverBaseUrl + path, {
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
        "Authorization": `Bearer ${localStorage.getItem("token")}`,
      },
      data: { id: idToDelete },
    });
    console.log(data);
    return data;
  } catch (err) {
    if (axios.isAxiosError(err)) {
      handleRequestErrors(err!);
    } else {
      handleUnexpectedRequestErrors(err!);
    }
  }
};
```

## Error Handlers

Como vimos en el archivo anterior, hacemos uso de los handlers de errores, es por eso que debemos crear codigo del mismo en el archivo llamado `errors.ts` dentro de la carpeta de helpers, el cual nos quedará de la siguiente manera.

```tsx
import toast from "react-hot-toast";     // Importamos el toast

const notify = (message: string) =>       // Creamos la función para llamar al toast
  toast.error(message, {
    style: { backgroundColor: "#ef4444", color: "white" },    // Con sus respectivos estilos
  });

export const notifyErrorWithToast = (message: string, err: {}) => {       // Y creamos la función que exportaremos para manejar errores
  toast.error(message, {
    style: { backgroundColor: "#ef4444", color: "white" },
  }); // We catch the error and show the error message
  console.log(err);
};

export const handleRequestErrors = (err: {
  response?: { data?: { popUpMessage?: string } };
}) => {
  if (err.response?.data?.popUpMessage !== "Token not provided") {
    notify(err.response?.data?.popUpMessage!);

    // Generate a new error for the handler in form
    throw new Error(err.response?.data?.popUpMessage);
  }

  throw new Error("Not authenticated");
};

export const handleUnexpectedRequestErrors = (err: {}) => {
  console.log("unexpected error: ", err);
  notify("An unexpected error occurred, please try again later");
  return "An unexpected error occurred, please try again later";
};
```

## Form Errors handler

Además de manejar los errores de las request tambien tenemos un componente que maneja los errores del formulario, este es el componente llamado `FormErrors`, este mismo se encuentra en la carpeta del mismo nombre.  
Creamos este componente para poder reutilizarlo las veces que sea necesario, para ello debemos crear el codifo del mismo, el cual quedará de la siguiente manera.

```tsx
type PropsType_FormErrors = {     // Creamos el type para los props de nuestro componente
  errorMessage: string;
};

const FormErrors = ({ errorMessage }: PropsType_FormErrors) => {      // Le indicamos las props necesarias con su tipo
  return <small className="text-red-500">{errorMessage}</small>;      // Y creamos el componente que se generará para mostrar errores
};

export default FormErrors;
```

## Dashboard

Hecho esto podemos empezar con los componentes que ayudarán a los usuarios a interactiar con la base de datos y manejar sus trabajos. Esto se hará mediante la página llamada `Dashboard`, en la cual crearemos la base para todo nuestro proyecto, quedando la misma de la siguiente manera.

```tsx
import { useState, useEffect } from "react";
import { useLocation } from "wouter";
import { useAutoAnimate } from "@formkit/auto-animate/react";
import { v4 as uuidv4 } from "uuid";
import toast, { Toaster } from "react-hot-toast";
import { AnimatePresence } from "framer-motion";
import { IoMdAdd } from "react-icons/io";
import { IoCloseSharp } from "react-icons/io5";
import { FiSearch } from "react-icons/fi";
import Navbar from "../../components/Navbar/Navbar";
import Profile from "../../components/Profile/Profile";
import JobCard from "../../components/JobCard/JobCard";
import AddJob from "../../components/AddJob/AddJob";
import JobDetails from "../../components/JobDetails/JobDetails";
import PopUpModal from "../../components/PopUpModal/PopUpModal";
import {
  JobInterface,
  UserDataInterface,
} from "../../interfaces/jobsInterfaces";
import {
  axios_JOBS_addData,
  axios_JOBS_deleteData,
  axios_JOBS_getData,
  axios_JOBS_updateData,
} from "../../helpers/requests";
import { notifyErrorWithToast } from "../../helpers/errors";

const Dashboard = () => {
  const [openModal, setOpenModal] = useState<Boolean>(false);           // Creamos el hook para el modal
  const [tokenInLocalStorage, setTokenInLocalStorage] = useState("");   // Creamos el hook para guardar el token localmente
  const [jobDetailsModalComponent, setJobDetailsModalComponent] =
    useState<Boolean>(true);                                            // Creamos el hook que indica el tipo de modal
  const [userTabOpened, setUserTabOpened] = useState<Boolean>(false);   // Creamos el hook para el estado de la pestaña de usuario
  const [jobsFromDB, setJobsFromDB] = useState<Array<JobInterface>>([]);    // Creamos el hook para guardar los trabajos
  const [jobForDetails, setJobForDetails] = useState<JobInterface>();       // Creamos el hook para guardar el trabajo para los detalles
  const [profileInfo, setProfileInfo] = useState<UserDataInterface>();      // Creamos el hook con los datos del usuario
  const [searchQuery, setSearchQuery] = useState("");                       // Creamos el hook con los datos para la busqueda de trabajos
  const [location, setLocation] = useLocation();
  const [jobsContainer] = useAutoAnimate();           // Creamos el hook para generar la animación automatica

  !JSON.parse(localStorage.getItem("auth")!) && setLocation("/");     // Comprobamos que tenga autorización

  const confirmDelete = (jobID: string, closeModal?: boolean) => {    // Creamos el toast para confirmar la eliminación del trabaho
    toast(
      () => (
        <span className="flex flex-col gap-3">
          Do you want to delete this job?
          <div className="flex justify-center items-center gap-3">
            <button
              className="flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg hover:bg-blue-800 focus:ring-4 bg-blue-900 focus:ring-blue-800"
              onClick={() => toast.dismiss("confirmDeleteJobToast")}
            >
              Cancel
            </button>
            <button
              className="flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg hover:bg-red-800 focus:ring-4 bg-red-900 focus:ring-red-800"
              onClick={() => {
                toast.dismiss("confirmDeleteJobToast");
                handleDeleteJob(jobID);
                closeModal && controlModal();
              }}
            >
              Delete
            </button>
          </div>
        </span>
      ),
      {
        duration: 99999999,           // Indicamos la duración para que no se elimine rapidamente
        id: "confirmDeleteJobToast",
        style: {
          backgroundColor: "#1f2937",
          borderRadius: "0.375rem",
          padding: "2rem",
          maxWidth: "64rem",
          color: "#FFFFFF",
          width: "fit-content",
        },
      }
    );
  };

  const controlModal = (jobDetails?: boolean, id?: string) => {       // Creamos la función que controla el modal
    setOpenModal((current) => !current); 
    setJobDetailsModalComponent(jobDetails as boolean); 
    setJobForDetails(jobsFromDB.find((job) => job.id === id));
  };

  const controlUserTab = () => {              // Creamos la función que controla la pestaña de usuario
    setUserTabOpened((current) => !current);
  };

  const hideWarning = () => {       // Creamos la función que oculta la advertencia si no se tiene una cuenta
    document.getElementById("warningGuest")!.classList.add("hidden");
  };

  const handleDeleteJob = async (jobID: string) => {      // Creamos la función para eliminar el trabajo
    if (tokenInLocalStorage === "guest") {               // Comprobamos si se tiene una cuenta
      const arrayWithDeletedJob = jobsFromDB.filter((job) => job.id !== jobID);
      setJobsFromDB(jobsFromDB.filter((job) => job.id !== jobID)); 
      localStorage.setItem("guestJobs", JSON.stringify(arrayWithDeletedJob)); 
      toast.success("Job deleted successfully!", {
        style: { backgroundColor: "#1F2937", color: "#FFFFFF" },
      });
    } else {      // Sino trabajamos con el back-end
      try {
        await axios_JOBS_deleteData(jobID, "jobs"); 
        setJobsFromDB(jobsFromDB.filter((job) => job.id !== jobID)); 
      } catch (err) {
        notifyErrorWithToast(                               // Notificamos el error si lo hay
          "Error deleting job, please try again later",
          err!
        );
      }
    }
  };

  const handleUpdateJob = (id: string, jobForUpdate: JobInterface) => {      // Creamos la función para editar el trabajo
    if (tokenInLocalStorage === "guest") {
      jobsFromDB[jobsFromDB.findIndex((job) => job.id === id)] = jobForUpdate; 
      localStorage.setItem("guestJobs", JSON.stringify(jobsFromDB));
      toast.success("Job updated successfully!", {
        style: {
          backgroundColor: "green",
          color: "white",
        },
      });
    } else {
      try {
        axios_JOBS_updateData(jobForUpdate, "jobs"); 
        jobsFromDB[jobsFromDB.findIndex((job) => job.id === id)] = jobForUpdate; 
      } catch (err) {
        notifyErrorWithToast("Error editing job, please try again later", err!);
      }
    }
  };

  const getJobsFromDatabase = async () => {      // Creamos la función para traer los trabajos
    if (localStorage.getItem("token")! === "guest") {
      const guestJobsInLocalStorage = localStorage.getItem("guestJobs");
      guestJobsInLocalStorage
        ? setJobsFromDB(JSON.parse(guestJobsInLocalStorage))
        : localStorage.setItem("guestJobs", JSON.stringify([]));    // Si no tiene cuenta se guardan en el local storage
    } else {
      try {
        const userData: UserDataInterface = await axios_JOBS_getData(
          "jobs",
          localStorage.getItem("token")!
        );

        setJobsFromDB(userData?.jobs); 
        setProfileInfo(userData); 
      } catch (err) {
        notifyErrorWithToast(
          "Error getting jobs from database, please try again later",
          err!
        );
      }
    }
  };

  const handleAddJob = async (data: JobInterface) => {      // Creamos la función para crear el trabajo
    const timeFormat = new Intl.DateTimeFormat("en-us", {   // Creamos la función para formatear la fecha
      dateStyle: "short",
    });

    const dataToAdd = {                       // Creamos la data del nuevo trabajo
      ...data, 
      date: timeFormat.format(new Date()),    // Con la fecha formateada
      id: uuidv4(),                           // Y el id del nuevo trabajo
    };

    if (tokenInLocalStorage === "guest") {
      jobsFromDB.push(dataToAdd);
      localStorage.setItem("guestJobs", JSON.stringify(jobsFromDB));    // Guardamos el array en el local storage si no tiene cuenta 
      toast.success("Job saved successfully!", {
        style: { backgroundColor: "#1F2937", color: "#FFFFFF" },
      });
    } else {
      try {
        await toast.promise(
          axios_JOBS_addData(
            dataToAdd,
            "jobs"
          ),
          {
            loading: "Loading...",
            success: "Job added successfully",
            error: "Error adding job, please try again later",
          },
          {
            style: { backgroundColor: "#1F2937", color: "#FFFFFF" },
          }
        );

        jobsFromDB.push(dataToAdd);
      } catch (err) {
        notifyErrorWithToast("Error adding job, please try again later", err!);
      }
    }
  };

  useEffect(() => {
    setTokenInLocalStorage(localStorage.getItem("token")!);     // Traemos el token
    getJobsFromDatabase();                                      // Y los trabajos
  }, []);

  return (
    <>
      <Navbar
        controlUserTab={controlUserTab}
        userEmail={profileInfo?.email!}
        userType={tokenInLocalStorage}
      />
      {tokenInLocalStorage == "guest" && (        // Mostramos la advertencia solamente si no tiene cuenta
        <div
          id="warningGuest"
          className="flex bg-red-600 text-white px-8 py-1 justify-between"
        >
          <p>
            You're using this app without an account, your jobs will be saved
            ONLY in this device.
          </p>
          <button onClick={hideWarning} className="w-fit self-start">
            <IoCloseSharp size={25} color="white" />
          </button>
        </div>
      )}
      <div className="relative md:w-1/2 md:mx-auto mx-8 mt-2">
        <input
          type="search"
          name="search"
          id="search"
          placeholder="Search..."
          className="block py-2.5 px-0 text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 w-full"
          onChange={(e) => setSearchQuery(e.target.value)}      // Indicamos que guarde cada vez que se tipee algo
        />
        <span className="absolute right-2 bottom-4">
          <FiSearch />
        </span>
      </div>
      <div className="relative">
        <div
          className="p-8 flex flex-wrap gap-4 w-full items-stretch"
          ref={jobsContainer}
        >
          {jobsFromDB &&
            jobsFromDB
              .filter((job) => {                            // Filtramos los array dependiendo de la busqueda
                return searchQuery.toLowerCase() === ""
                  ? job
                  : job.title.toLowerCase().includes(searchQuery);
              })
              .map((job, i) => (
                <JobCard                              // Creamos una card por cada uno de los trabajos 
                  key={i}
                  job={job}
                  functionModal={controlModal}
                  deleteJobFunction={confirmDelete}
                />
              ))}
          {jobsFromDB.length === 0 && (
            <div className="h-full w-screen grid place-content-center">
              <h2 className="text-xl">
                No saved jobs yet :c <br /> Click + to add a job
              </h2>                                                       // Si no hay trabajos que mostrar lo indicamos en pantalla
            </div>
          )}
        </div>
        <button
          onClick={() => controlModal(false)}
          className="fixed bottom-4 right-4 h-10 w-10 rounded-full bg-main text-2xl transition-all border border-white flex justify-center items-center"
        >
          <IoMdAdd color="white" />
        </button>
        <AnimatePresence>               // Encerramos todo en el componente para animar
          {userTabOpened && (
            <Profile                            // Y le pasamos la pestaña del usuario
              userInfo={profileInfo!}           // Con los datos del mismo
              controlUserTab={controlUserTab}
              userType={tokenInLocalStorage}
            />
          )}
        </AnimatePresence>
      </div>
      <AnimatePresence>
        {openModal ? (
          <PopUpModal modalControls={controlModal}>
            {jobDetailsModalComponent ? (
              <JobDetails
                job={jobForDetails!}
                deleteJobFunction={confirmDelete}
                updateJobFunction={handleUpdateJob}
              />
            ) : (
              <AddJob addJobFunction={handleAddJob} />
            )}
          </PopUpModal>
        ) : null}
      </AnimatePresence>
      <Toaster />
    </>
  );
};

export default Dashboard;
```

## Job Card

La card que generaremos como vista previa para cada uno de los trabajos es una card simple qur generaremos gracias al map del array en el dashboard. El codigo de la misma es el siguiente.

```tsx
import { AiOutlineArrowRight } from "react-icons/ai";
import { HiOutlineTrash } from "react-icons/hi";
import {
  statusColorsVariants,
  JobInterface,
} from "../../interfaces/jobsInterfaces";

type PropsType_JobCard = {
  job: JobInterface;
  functionModal: (arg0: boolean, arg1: string) => void;
  deleteJobFunction: (jobId: string) => void;
};

const JobCard = ({
  job,
  functionModal,
  deleteJobFunction,
}: PropsType_JobCard) => {

  const TEXT_COLORS_VARIANTS: statusColorsVariants = {      // Creamos el diccionario para las vaariantes en los colores
    success: "success-text-style",
    rejected: "rejected-text-style",
    processing: "processing-text-style",
    applied: "applied-text-style",
    later: "later-text-style",
  };

  const BORDER_COLORS_VARIANTS: statusColorsVariants = {    // Creamos el diccionario para las vaariantes en los bordes
    success: "hover:border-success",
    rejected: "hover:border-rejected",
    processing: "hover:border-processing",
    applied: "hover:border-applied",
    later: "hover:border-later",
  };

  return (
    <div
      className={`transition-all max-w-sm rounded-lg max-h-60 bg-gray-800 shadow-sm hover:shadow-2xl border-2 border-gray-800 basis-[100%] ${
        BORDER_COLORS_VARIANTS[job.status]      // Llamamos al borde dependiendo del estado del trabajo
      }`}
    >
      <div className="p-5 h-full flex flex-col justify-between">
        <div className="flex flex-wrap">
          <div className="flex items-center gap-2 w-full">
            <img
              className="h-4"
              src={`https://s2.googleusercontent.com/s2/favicons?domain_url=${job.link}`}     // Traemos el favicon de la página
              alt="web favicon"
            />
            <h5
              className="text-xl font-bold tracking-tight text-gray-900 dark:text-white capitalize"
              style={{
                display: "-webkit-box",
                WebkitLineClamp: 1,
                WebkitBoxOrient: "vertical",
                overflow: "hidden",
              }}                            // Agregamos los estilos para cortar el texto
            >
              {job.title.toLowerCase()}
            </h5>
          </div>
          <small
            className={`${
              TEXT_COLORS_VARIANTS[job.status as keyof statusColorsVariants]
            } pb-3`}
          >
            {job.status}
          </small>
        </div>
        <p
          className="mb-3 font-normal text-gray-700 dark:text-gray-400"
          style={{
            display: "-webkit-box",
            WebkitLineClamp: 3,
            WebkitBoxOrient: "vertical",
            overflow: "hidden",
            cursor: "default",
          }}
        >
          {job.description}
        </p>
        <div className="flex w-full justify-between flex-wrap">
          <button
            onClick={() => {
              functionModal(true, job.id);      // Creamos el boton para abrir los detalles del trabajo
            }}
            className="flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg hover:bg-blue-800 focus:ring-4 bg-blue-900 focus:ring-blue-800"
          >
            Read more
            <AiOutlineArrowRight />
          </button>
          <button
            onClick={() => deleteJobFunction(job.id)}     // Creamos el boton para eliminar el trabajo
            className="flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg hover:bg-red-800 focus:ring-4 bg-red-900 focus:ring-red-800"
          >
            Delete <HiOutlineTrash />
          </button>
        </div>
      </div>
    </div>
  );
};

export default JobCard;
```

## Navbar

Otra cosa que debemos crear en nuestro dashboard es el Navbar, ya que este nos ayudará a controlar la pestaña del perfil de usuario.

```tsx
import { AiOutlineUser } from "react-icons/ai";

type PropsType_Navbar = {
  controlUserTab: () => void;
  userEmail: string;
  userType: string;
};

const Navbar = ({ controlUserTab, userEmail, userType }: PropsType_Navbar) => {
  return (
    <div className="h-16 w-screen bg-main flex justify-between items-center px-4 md:px-8">
      <h2 className="text-xl md:text-3xl">JOB VAULT</h2>
      <div className="flex items-center md:w-fit gap-4 overflow-hidden group/navbar-user">
        <p className="transition-all md:translate-x-[150%] hidden md:block md:opacity-0 group-hover/navbar-user:translate-x-[0] group-hover/navbar-user:opacity-100 z-0">
          {userType === "guest" ? "Guest" : userEmail}    // Mostramos el mail del usuario si es que está registrado
        </p>
        <button
          onClick={controlUserTab}                // Y creamos el botón para abrir la pestaña del usuario
          className="z-10 rounded-full border-2 border-white h-10 w-10 grid place-content-center bg-main"
        >
          <AiOutlineUser size={"1.5em"} />
        </button>
      </div>
    </div>
  );
};

export default Navbar;
```

## Profile

Ahora que tenemos una forma de abrir la pestaña del usuario debemos crearla. Esta nos mostrará los datos del usuario y nos permitirá cerrar sesión o eliminar los datos del mismo. El codigo del mismo será el siguiente.

```tsx
import { useState } from "react";
import { useLocation } from "wouter";
import { toast, Toaster } from "react-hot-toast";
import { useForm } from "react-hook-form";
import { FiLogOut } from "react-icons/fi";
import { IoCloseSharp } from "react-icons/io5";
import { MdOutlineClose, MdOutlineDangerous } from "react-icons/md";
import { AnimatePresence, motion } from "framer-motion";
import FormErrors from "../FormErrors/FormErrors";
import PopUpModal from "../PopUpModal/PopUpModal";
import { notifyErrorWithToast } from "../../helpers/errors";
import { UserDataInterface } from "../../interfaces/jobsInterfaces";
import { axios_USERS_deleteData } from "../../helpers/requests";

type PropsType_Profile = {
  controlUserTab: () => void;
  userInfo: UserDataInterface;
  userType: string;
};

const Profile = ({ controlUserTab, userInfo, userType }: PropsType_Profile) => {
  const [deleteAccountModal, setDeleteAccountModal] = useState(false);
  const [location, setLocation] = useLocation();
  const { register, watch } = useForm();          // Importamos lo necesario del hook para el formulario

  const controlDeleteModal = () => {
    setDeleteAccountModal((current) => !current);
  };

  const handleLogOut = () => {      // Creamos la funcion para el logout
    localStorage.setItem("token", JSON.stringify(null));
    localStorage.setItem("auth", JSON.stringify(false));

    setLocation("/");
  };

  const handleDeleteRequest = () => {        // Creamos la funcion para eliminar al usuario
    try {
      axios_USERS_deleteData(userInfo._id, "users");
      handleLogOut();
    } catch (err) {
      notifyErrorWithToast(
        "Something went wrong deleting your account, please try again later",
        err!
      );
    }
  };

  const handleDeleteAccount = () => {       // Comprobamos que el email sea valido
    userInfo.email === watch("confirmation") && handleDeleteRequest();
  };

  return (
    // ========== Return ============================================================== //

    <motion.div                           // Generamos la animación del componente
      initial={{ x: +200, opacity: 0 }}
      animate={{
        x: 0,
        opacity: 1,
        transition: {
          ease: "linear",
        },
      }}
      exit={{
        x: +200,
        opacity: 0,
        transition: {
          ease: "linear",
        },
      }}
      className="w-screen h-screen md:w-fit md:right-0 md:border-gray-900 md:border-l-4 top-0 bg-gray-900 fixed z-20"
    >
      <div className="absolute md:h-48 w-full bg-main" >
        <button
          className="absolute top-4 right-4 z-10"
          onClick={controlUserTab}                    // Creamos el botón para cerrar la pestaña
        >
          <IoCloseSharp size={25} color="white" />
        </button>
      </div>
      <div className="flex relative flex-col p-8 md:w-fit h-full justify-evenly items-center">
        <div className="z-20 flex flex-col items-center">
          <div className="h-40 w-40 grid place-content-center bg-gray-900 rounded-full z-10 mb-4">
            <div className="relative h-32 w-32 bg-black rounded-full border-2 border-gray-900 grid place-content-center">
              <div className="h-min w-min inset-0 place-content-center text-7xl uppercase">
                <span>{userType === "guest" ? "G" : userInfo.email[0]}</span>             // Mostramos el primer caracter
              </div>
            </div>
          </div>
          <h2 className="text-lg">
            {userType === "guest" ? "Guest" : `${userInfo.email}`}
          </h2>
          <small className="text-gray-600 uppercase w-full">
            {userType === "guest" ? "" : `Created at: ${userInfo.createdAt}`}
          </small>
        </div>
        <button
          onClick={handleLogOut}          // Creamos el botón para el logout
          className="flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg hover:bg-red-800 focus:ring-4 bg-red-900 focus:ring-red-800"
        >
          Log out <FiLogOut />
        </button>
        {userType !== "guest" && (
          <small
            onClick={controlDeleteModal}        // Y la opcion de eliminar cuenta solamente si el usuario tiene una
            className="text-red-800 underline cursor-pointer absolute bottom-4 m-auto w-fit"
          >
            Delete account
          </small>
        )}
      </div>
      <AnimatePresence>
        {deleteAccountModal ? (
          <PopUpModal modalControls={controlDeleteModal}>         // Creamos el modal para la confirmacion de la eliminacion del usuario
            <div className="flex flex-col">
              <div>
                <h3 className="text-3xl underline mb-4">Delete account</h3>
                <p>
                  You'll lose all your saved jobs. Are you sure you want to
                  delete your account?
                </p>
              </div>
              <div className="relative z-0 w-full mb-8 group mt-6">
                <input
                  type="email"
                  {...register("confirmation", {
                    required: true,
                    maxLength: 50,
                  })}
                  id="confirmation"
                  className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
                  placeholder=" "
                  maxLength={50}
                />
                <label
                  htmlFor="confirmation"
                  className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 z-[5] origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
                >
                  Enter your email for confirmation
                </label>
              </div>

              <div className="flex gap-8">
                <button
                  onClick={controlDeleteModal}
                  className="flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg hover:bg-blue-800 focus:ring-4 bg-blue-900 focus:ring-blue-800"
                >
                  Cancel
                  <MdOutlineClose />
                </button>
                <button
                  onClick={handleDeleteAccount}
                  disabled={watch("confirmation") !== userInfo.email}
                  className="disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:bg-red-900 flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg hover:bg-red-800 focus:ring-4 bg-red-900 focus:ring-red-800"
                >
                  <MdOutlineDangerous />
                  Delete account
                </button>
              </div>
            </div>
          </PopUpModal>
        ) : null}
      </AnimatePresence>
      <Toaster />
    </motion.div>
  );
};

export default Profile;
```

## Modal

Vimos que la confirmación del usuario se muestra dentro del componente `PopUpModal`, el cual es el modal que tambien se utiliza para mostrar los datos del trabajo, por lo que será necesario crearlo. Esto lo haremos en el archivo del mismo nombre, quedando de la siguirente manera.

```tsx
import { IoCloseSharp } from "react-icons/io5";
import { motion } from "framer-motion";

type PropsType_PopUpModal = {
  children: React.ReactNode;        // Indicamos que el children es un nodo de React
  modalControls: () => void;
};

const PopUpModal = ({ children, modalControls }: PropsType_PopUpModal) => {
  return (
    <motion.div
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{
        opacity: 0,
      }}
      className="fixed w-screen min-h-screen h-fit py-8 z-[100] inset-0"
      key="popUpModal"
    >
      <div
        onClick={modalControls}     // Creamos el div que estará por detras del modal y que cerrrará el mismo cuando se haga click
        className="absolute inset-0 w-full h-full bg-black opacity-75 -z-10"
      />
      <motion.div
        initial={{ y: "-100" }}
        animate={{
          y: 0,
          transition: {
            duration: 0.5,
            type: "tween",
          },
        }}
        exit={{
          y: "-100",
        }}
        className="relative bg-gray-800 rounded-md p-8 max-w-5xl md:max-w-3xl m-auto max-h-[90vh] overflow-y-auto md:w-1/2"
      >
        <button className="absolute top-4 right-4 z-10" onClick={modalControls}>    // Creamos el botón para cerrar el modal
          <IoCloseSharp size={25} color="white" />
        </button>
        {children}          // Y mostramos dentro del modal todo lo que le pasemos como children
      </motion.div>
    </motion.div>
  );
};

export default PopUpModal;
```

## Job Details

Este modal tambien nos ayudará mostrando los detalles del trabajo, es por eso que debemos crearlo. El archivo del detalle no solo mostrará los deltalles del mismo, sino que nos dejará editarlo, por lo que el codifo nos quedará de la siguienmte manera.

```tsx
import { useState } from "react";
import { AiFillEdit, AiOutlineCheck } from "react-icons/ai";
import { BiLinkExternal } from "react-icons/bi";
import { HiOutlineTrash } from "react-icons/hi";
import DOMPurify from "dompurify";        // Llamamos a dompurify para purificar los datos
import FormErrors from "../FormErrors/FormErrors";
import { JobInterface, statusVariants } from "../../interfaces/jobsInterfaces";

type PropsType_JobDetails = {
  job: JobInterface;
  deleteJobFunction: (jobID: string, modalControl: boolean) => void;
  updateJobFunction: (jobID: string, job: JobInterface) => void;
};

const JobDetails = ({
  job,
  deleteJobFunction,
  updateJobFunction,
}: PropsType_JobDetails) => {
  const [editMode, setEditMode] = useState(false);          // Creamos el estado para ver si se edita o solo se muestra
  const [invalidLink, setInvalidLink] = useState(false);
  const [selectedEditStatus, setSelectedEditStatus] = useState(job.status);
  const [selectedEditTitle, setSelectedEditTitle] = useState(job.title);
  const [selectedEditLink, setSelectedEditLink] = useState(job.link);

  const checkValidLink = () => {      // Creamos la validación del link
    const linkElement = document.querySelector("#editJobLink")?.textContent!;
    const pattern = 
      /[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b([-a-zA-Z0-9()@:%_\+.~#?&//=]*)?/gi; // Con el patrón indicado

    return pattern.test(linkElement);     // Y generamos el test
  };

  const handleDeleteJobOnModal = (jobID: string) => {     // Creamos la función para borrar el trabajo
    deleteJobFunction(jobID, true);
  };

  const handleUpdate = () => {
    if (checkValidLink()) {
      const jobToUpdate: JobInterface = {       // Si el link es valido tomamos los datos a editar
        id: job.id,
        title: (document.querySelector("#editJobTitle") as HTMLInputElement)
          .textContent!,
        link: (document.querySelector("#editJobLink") as HTMLInputElement)
          .textContent!,
        description: (
          document.querySelector("#editJobDescription") as HTMLElement
        ).innerText!,
        status: (document.querySelector("#editJobStatus") as HTMLInputElement)
          .value as statusVariants,
        company: (document.querySelector("#editJobCompany") as HTMLInputElement)
          .textContent!,
        requirements: (
          document.querySelector("#editJobRequirements") as HTMLElement
        ).innerText,
        date: job.date,
        extra:
          (document.querySelector("#editJobExtra") as HTMLElement)?.innerText ||
          null,
      };
      setSelectedEditTitle(jobToUpdate.title);
      setSelectedEditLink(jobToUpdate.link);
      updateJobFunction(job.id, jobToUpdate);
      setEditMode((current) => !current);
      setInvalidLink(false);
    } else {
      setInvalidLink(true);       // Indicamos que el link es invalido
    }
  };

  const TEXT_COLORS_VARIANTS = {
    success: "success-text-style",
    rejected: "rejected-text-style",
    processing: "processing-text-style",
    applied: "applied-text-style",
    later: "later-text-style",
  };

  const editable =
    "block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer";

  const nonEditable =
    "block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer";

  return (
    <div className="grid place-content-stretch items-center h-full">
      {editMode ? (       // Mostramos uno u el otro dependiendo si es editable o no
        <>
          <h3
            dangerouslySetInnerHTML={{
              __html: DOMPurify.sanitize(selectedEditTitle),      // Indicamos que pasaremos datos HTML desde el front-end, pero antes lo purificamos
            }}
            id="editJobTitle"
            contentEditable={editMode}
            className="flex items-center text-3xl uppercase gap-2 border-0 border-b-2 border-gray-300"
          />
          <small
            contentEditable={editMode}
            dangerouslySetInnerHTML={{
              __html: DOMPurify.sanitize(selectedEditLink),
            }}
            id="editJobLink"
            className="text-blue-600 border-0 border-b-2 border-gray-300"
          />
          {invalidLink && (
            <FormErrors errorMessage="Please insert a valid link" />
          )}
        </>
      ) : (
        <a
          href={selectedEditLink}
          target="_blank"
          className="flex items-center text-3xl uppercase gap-2 hover:text-blue-600 w-fit transition-all"
        >
          <h3 contentEditable={editMode}>{selectedEditTitle}</h3>
          <BiLinkExternal size={14} />
        </a>
      )}
      <div className="flex justify-between">
        <small className="text-gray-600 uppercase">
          by{" "}
          <span
            dangerouslySetInnerHTML={{
              __html: DOMPurify.sanitize(job.company),
            }}
            id="editJobCompany"
            contentEditable={editMode}
            className={editMode ? "border-0 border-b-2 border-gray-300" : ""}
          />
        </small>
        <small className="text-gray-500">Added: {job.date}</small>
      </div>
      {editMode ? (
        <select
          id="editJobStatus"
          onChange={() =>
            setSelectedEditStatus(
              (document.getElementById("editJobStatus") as HTMLInputElement)
                .value as statusVariants
            )
          }
          className={`bg-gray-800 text-xs italic w-fit pb-3 pt-2 ${TEXT_COLORS_VARIANTS[selectedEditStatus]}`}
          defaultValue={selectedEditStatus}
        >
          <option value="success" className="success-text-style">
            Success
          </option>
          <option value="rejected" className="rejected-text-style">
            Rejected
          </option>
          <option value="processing" className="processing-text-style">
            Processing
          </option>
          <option value="applied" className="applied-text-style">
            Applied
          </option>
          <option value="later" className="later-text-style">
            Save for later
          </option>
        </select>
      ) : (
        <small className={`${TEXT_COLORS_VARIANTS[selectedEditStatus]} pb-3`}>
          {selectedEditStatus}
        </small>
      )}
      <hr />
      <div className="relative z-0 w-full">
        <h4 className="text-xl uppercase underline pt-4">Description</h4>
        <p
          dangerouslySetInnerHTML={{
            __html: DOMPurify.sanitize(job.description),
          }}
          id="editJobDescription"
          contentEditable={editMode}
          className={`${
            editMode ? editable : nonEditable
          } pb-8 whitespace-pre-line`}
        />
      </div>
      <div className="relative z-0 w-full">
        <h4 className="text-xl uppercase underline">Requirements</h4>
        <p
          dangerouslySetInnerHTML={{
            __html: DOMPurify.sanitize(job.requirements),
          }}
          id="editJobRequirements"
          contentEditable={editMode}
          className={`${
            editMode ? editable : nonEditable
          } pb-8 whitespace-pre-line`}
        />
        {job.extra && (
          <>
            <h4 className="text-xl uppercase underline">Extras</h4>
            <p
              dangerouslySetInnerHTML={{
                __html: DOMPurify.sanitize(job.extra),
              }}
              id="editJobExtra"
              contentEditable={editMode}
              className={`${
                editMode ? editable : nonEditable
              } whitespace-pre-line`}
            />
          </>
        )}
      </div>
      <div className="flex justify-between pt-8">
        {editMode ? (
          <button
            onClick={() => handleUpdate()}
            className="flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg focus:ring-4 hover:bg-green-800 bg-green-900 focus:ring-green-800"
          >
            Done <AiOutlineCheck />
          </button>
        ) : (
          <button
            onClick={() => setEditMode((current) => !current)}
            className="flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg focus:ring-4 hover:bg-blue-800 bg-blue-900 focus:ring-blue-800"
          >
            Edit <AiFillEdit />
          </button>
        )}
        {!editMode && (
          <button
            onClick={() => handleDeleteJobOnModal(job.id)}
            className="flex w-fit items-center gap-2 hover:gap-3 px-3 py-2 text-sm font-medium text-center text-white transition-all rounded-lg hover:bg-red-800 focus:ring-4 bg-red-900 focus:ring-red-800"
          >
            Delete <HiOutlineTrash />
          </button>
        )}
      </div>
    </div>
  );
};

export default JobDetails;
```

## Add Job

Por ultimo nos queda el componente que nos permitirá crear los trabajos. Para ello tambien usaremos el modal. El componente nos permitirá crear los datos para el trabajo y subirlo a la base de datos, por lo que el mismo quedará de la siguiente manera.

```tsx
import { useState } from "react";
import { useForm } from "react-hook-form";
import { Toaster } from "react-hot-toast";
import { HiOutlineTrash } from "react-icons/hi";
import { AiOutlineSend } from "react-icons/ai";
import {
  JobInterface,
  statusColorsVariants,
} from "../../interfaces/jobsInterfaces";
import FormErrors from "../FormErrors/FormErrors";

type PropsType_AddJob = {
  addJobFunction: (data:JobInterface) => Promise<void>;
};

const AddJob = ({ addJobFunction }: PropsType_AddJob) => {
  const [selectedStatus, setSelectedStatus] = useState<string>("later");
  const {
    register,
    formState: { errors },
    handleSubmit,
    reset,
  } = useForm<JobInterface>();

  const TEXT_COLORS_VARIANTS: statusColorsVariants = {
    success: "success-text-style",
    rejected: "rejected-text-style",
    processing: "processing-text-style",
    applied: "applied-text-style",
    later: "later-text-style",
  };

  return (
    <form
      onSubmit={handleSubmit(addJobFunction)}         // Le pasamos el controlador del hook para el form
      className="grid items-center h-full px-8"
    >
      <h3 className="flex items-center text-3xl uppercase gap-2 pb-3 m-auto ">
        Add job
      </h3>
      <div className="relative z-0 w-full mb-6 group">
        <input
          type="text"
          {...register("title", { required: true, maxLength: 50 })}
          id="addTitle"
          className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
          placeholder=" "
          maxLength={50}
        />
        <label
          htmlFor="addTitle"
          className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 z-[5] origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
        >
          Job title
        </label>
        {
          (errors.title?.type === "required" && (
            <FormErrors errorMessage="Insert a title for the job" />      // Manejamos los errores
          ),
          errors.title?.type === "maxLength" && (
            <FormErrors errorMessage="The title is too long" />
          ))
        }
      </div>
      <div className="relative z-0 w-full mb-6 group">
        <input
          type="text"
          {...register("link", {
            required: true,
            pattern:
              /[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b([-a-zA-Z0-9()@:%_\+.~#?&//=]*)?/gi,
          })}
          id="addLink"
          className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
          placeholder=" "
        />
        <label
          htmlFor="addLink"
          className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 z-[5] origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
        >
          Link
        </label>
        {
          (errors.link?.type === "required" && (
            <FormErrors errorMessage="Insert a link of the job" />
          ),
          errors.link?.type === "pattern" && (
            <FormErrors errorMessage="Insert a valid link" />
          ))
        }
      </div>
      <div className="relative z-0 w-full mb-6 group">
        <textarea
          {...register("description", { required: true })}
          id="addDescription"
          className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
          placeholder=" "
          rows={10}
        />
        <label
          htmlFor="addDescription"
          className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-7 scale-75 top-3 z-[5] origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-7"
        >
          Description
        </label>
        {errors.description?.type === "required" && (
          <FormErrors errorMessage="Insert a description for the job" />
        )}
      </div>
      <div className="grid md:grid-cols-2 md:gap-6">
        <div className="relative z-0 w-full mb-6 group">
          <select
            {...register("status", { required: true })}
            id="jobStatus"
            onChange={() =>
              setSelectedStatus(
                (document.getElementById("jobStatus") as HTMLInputElement).value
              )
            }
            className={`block py-2.5 px-0 w-full text-sm bg-gray-800 border-0 border-b-2 appearance-none dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer ${
              TEXT_COLORS_VARIANTS[
                selectedStatus as keyof typeof TEXT_COLORS_VARIANTS
              ]
            }`}
            placeholder=" "
          >
            <option className="later-text-style" value="later">
              Save for later
            </option>
            <option className="applied-text-style" value="applied">
              Applied
            </option>
            <option className="processed-text-style" value="processed">
              Processed
            </option>
            <option className="success-text-style" value="success">
              Success
            </option>
            <option className="rejected-text-style" value="rejected">
              Rejected
            </option>
          </select>
          <label
            htmlFor="jobStatus"
            className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 z-[5] origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
          >
            Status
          </label>
          {errors.status?.type === "required" && (
            <FormErrors errorMessage="Choose a status for the job" />
          )}
        </div>
        <div className="relative z-0 w-full mb-6 group">
          <input
            type="text"
            {...register("company", { required: true })}
            id="addCompany"
            className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
            placeholder=" "
          />
          <label
            htmlFor="addCompany"
            className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 z-[5] origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6"
          >
            Company
          </label>
          {errors.company?.type === "required" && (
            <FormErrors errorMessage="Insert a company name" />
          )}
        </div>
      </div>
      <div className="relative z-0 w-full mb-6 group">
        <textarea
          {...register("requirements", { required: true })}
          id="jobRequirements"
          className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
          placeholder=" "
          rows={10}
        />
        <label
          htmlFor="jobRequirements"
          className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-7 scale-75 top-3 z-[5] origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-7"
        >
          Requirements
        </label>
        {errors.requirements?.type === "required" && (
          <FormErrors errorMessage="Insert the requirements for the job" />
        )}
      </div>
      <div className="relative z-0 w-full mb-6 group">
        <textarea
          {...register("extra")}
          id="jobExtras"
          className="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
          placeholder=" "
          rows={10}
        />
        <label
          htmlFor="jobExtras"
          className="peer-focus:font-medium absolute text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-7 scale-75 top-3 z-[5] origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-7"
        >
          Extra data
        </label>
      </div>
      <div className="flex md:flex-row flex-col gap-4 w-full justify-between">
        <div className="cursor-pointer text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center flex justify-center items-center gap-3">
          <input
            type="button"
            value="Clear"
            className="cursor-pointer"
            onClick={() => reset()}
          />
          <HiOutlineTrash />
        </div>
        <button className="cursor-pointer text-white bg-green-700 hover:bg-green-800 focus:ring-4 focus:outline-none focus:ring-green-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center flex justify-center items-center gap-3">
          <input type="submit" value="Submit" className="cursor-pointer" />
          <AiOutlineSend/>
        </button>
      </div>
      <Toaster />
    </form>
  );
};

export default AddJob;
```

Hecho esto podemos decir que tenemos todo el front-end completamente terminado, el usuario puede interactuar por completo con la página, pudiendo manejar todos los datos guardados en la base de datos.

## Back

## Index

## User model

## User Routes

## Verify Token

## Job Routes

## User Controllers

## Job Controllers

## JWT - JsonWebToken

JsonWebToken nos ayudará a generar tokens para mantener la sesión del usuario en nuestro proyecto, así como su ID para poder pedir los datos en MongoDB. Para ello necesitamos que se cree un token cada vez que el usuario se registra o inicia sesión, por lo que será necesario utilizarlo en nuestro controller de las rutas de usuario.  
Cuando generamos el token necesitaremos una key secreta para encriptar los mismos, la misma debemos crearla en nuestro archivo `.env` y luego pedirla cuando la necesitemos. La misma quedará de la siguiente manera.

```env
JWT_SECRET=<la key que nosotros querramos usar>
```

Con la key declarada podemos empezar a desarrollar el código para crear el token en nuestro controlador, el cual quedaría de la siguiente manera.

```js
const bcrypt = require("bcrypt")
const userModel = require("../models/user")
const jwt = require("jsonwebtoken")         // Requerimos JWT 
const secret = process.env.JWT_SECRET       // Y guardamos nuestra key en una variable

module.exports = {

    // Create a new user on the database

    users_createNewUser: (req, res) => {
        try {
            const user = new userModel(req.body)
            user.save((err, userResult) => {
                if (err) {
                    return res.status(500).json({
                        message: "The email is already in use"
                    })
                }
                const token = jwt.sign({              // Creamos el token con el método sign
                    id: userResult._id                // Y le agregamos el user id al token
                }, secret, {                          // Le pasamos la secret key que creamos
                    expiresIn: 60 * 60 * 24 * 30      // Y le indicamos que expira en 30 días
                })
                res.status(200).json({                // Le indicamos un estado correcto al front
                    auth: true,                       // Indicamos que está autorizado
                    token                             // Y le enviamos le token con la información del usuario
                });
            })
        } catch (err) {
            console.log(err)
            res.status(409).send(err)
        }
    },


    //  Find a user on the database

    users_getUserFromDataBase: (req, res) => {
        try {
            userModel.findOne({
                email: req.query.email
            }, (err, user) => {
                if (err) return res.status(400).send({
                    message: err.message
                })
                bcrypt.compare(req.query.password, user.password, function (error, isMatch) {
                    if (error) {
                        throw error
                    } else if (!isMatch) {
                        res.status(500).send("Password doesn't match!")
                    } else {
                        res.status(200).send(user)
                    }
                })
            })
        } catch (err) {
            console.log(err)
            res.status(409).send(err)
        }
    },

    // Update a user on the database

    users_updateUserOnDatabase: (req, res) => {
        console.log(req.body)
        res.send("hi, put")
    },

    // Delete a user on the database

    users_deleteOneUserOnDatabase: (req, res) => {
        console.log(req.body)
        res.send("hi, delete")
    },
}
```

## Cierre
