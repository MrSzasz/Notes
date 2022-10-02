# Redux

[Redux](https://redux.js.org/) es una herramienta de gestión de estados framework agnostic (es decir, que se puede usar con diferentes frameworks), la cual nos ayuda a manejar mejor los estados, evitando los problemas a futuro junto al debugging.  
Para esta guía crearemos un proyecto básico en el que podremos agregar películas a una lista de películas favoritas y de películas vistas.

## Instalación

Para este caso usaremos Redux con [React](../ReactJS/ReactJS.md), para ello comenzaremos creando un nuevo proyecto de React, ya sea con `create-react-app` o con `vite`, luego de ello abriremos nuestro proyecto en el editor de código.  

> Para este proyecto vamos a usar [Tailwind](https://tailwindcss.com/)

Luego de esto, empezaremos con la instalación de [Redux Toolkit](https://redux-toolkit.js.org/), el cual nos ayudará a configurar Redux en nuestro proyecto. Para ello abriremos la consola y usaremos el comando que nos proporciona la [documentación](https://redux-toolkit.js.org/tutorials/quick-start#install-redux-toolkit-and-react-redux).

```npm

    npm i @reduxjs/toolkit react-redux

```

## Store

Para empezar a usar Redux es necesario crear nuestro `store`, que será donde guardaremos todos nuestros estados. Para ello debemos crear una carpeta dentro de `src` llamada `app` y dentro de ella un archivo llamado `store.js`, y dentro del mismo crearemos nuestro store con el siguiente código.

```jsx

    import { configureStore } from '@reduxjs/toolkit'       // Importamos lo necesario de Redux

    const store = configureStore({          // Creamos nuestra store
        reducer: {},
    })

    export default store;       // La exportamos

```

Con nuestra store creada debemos indicarle a nuestra app cual será el store que usaremos, para ello iremos a nuestra `main.jsx` (o `index.js` en caso de haber usado `create-react-app`) y allí usaremos el `Provider` que nos facilita Redux de la siguiente manera.

```jsx

    import "./index.scss";
    import React from "react";
    import ReactDOM from "react-dom/client";
    import App from "./App";
    import { Provider } from "react-redux";         // Importamos el provider de Redux
    import store from "./app/store";            // Importamos la store que creamos anteriormente

    ReactDOM.createRoot(document.getElementById("root")).render(
        <React.StrictMode>
            <Provider store={store}>        {/* Usamos el provider para envolver nuestra app y le pasamos la store como prop */}
                <App />
            </Provider>
        </React.StrictMode>
    );

```

## Slice

Luego de crear nuestro store será necesario crear nuestro `slice`, es decir, nuestro modificador de estados. Para ello crearemos una carpeta `features` dentro de la carpeta `src`, dentro de la misma crearemos la carpeta `movies` y por ultimo el archivo `favMovieListSlice.js` en la que tendremos nuestro slice.  

> Una forma fácil de hacer esto sería escribir `features/movies/favMovieListSlice.js` dentro de `src`

Hecho esto agregamos el código en nuestro archivo

```jsx

    import { createSlice } from "@reduxjs/toolkit";         // Importamos lo necesario para crear el slice

    export const favMovieListSlice = createSlice({      // Exportamos el slice que crearemos
        name: 'favMovieList',                           // Le asignamos un nombre
        initialState: [],                               // El estado inicial
        reducers:{}                                     // Y los reducers que crearemos luego
    })

    export default favMovieListSlice.reducer;           // Exportamos los reducers

```

Y por ultimo importamos este slice en nuestro store de la siguiente manera

```jsx

    import { configureStore } from '@reduxjs/toolkit'
    import favMovieListSlicer from '../features/movies/favMovieListSlice';      // Importamos el slice

    const store = configureStore({
        favMovieList: favMovieListSlicer            // Y lo asignamos con el nombre que queremos
    })

    export default store;

```

Con esto hecho tendremos la configuración de nuestro store completo.
