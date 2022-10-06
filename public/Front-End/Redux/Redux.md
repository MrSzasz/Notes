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

Sumado a esto podemos instalar una extensión que nos ayudará con el debugging de Redux, la cual está disponible para [Chrome](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd), [Firefox](https://addons.mozilla.org/en-US/firefox/addon/reduxdevtools/) y [otros navegadores](https://github.com/reduxjs/redux-devtools/tree/main/extension#installation).

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

    const initialState = [{             // Creamos el estado inicial
        id: "hq",
        name: 'scarface',
        desc: 'Tells the story of Cuban refugee Tony Montana (Al Pacino), who arrives penniless in Miami during the Mariel boatlift and becomes a powerful and extremely homicidal drug lord.'
    }];                            

    export const favMovieListSlice = createSlice({      // Exportamos el slice que crearemos
        name: 'favMovieList',                           // Le asignamos un nombre
        initialState,                               // Le pasamos el estado inicial
        reducers:{}                                     // Y los reducers que crearemos luego
    })

    export default favMovieListSlice.reducer;           // Exportamos los reducers

```

Y por ultimo importamos este slice en nuestro store de la siguiente manera

```jsx

    import { configureStore } from '@reduxjs/toolkit'
    import favMovieListSlicer from '../features/movies/favMovieListSlice';      // Importamos el slice

    const store = configureStore({
        reducer:{
            favMovieList: favMovieListSlicer            // Y lo asignamos con el nombre que queremos
        }
    })

    export default store;

```

Con esto hecho tendremos la configuración de nuestro store completo.

## Uso del estado

Con nuestro estado configurado podemos empezar a utilizarlo. Para ello lo llamaremos en nuestro `App.jsx` de la siguiente manera.

```jsx

    import "./App.scss";
    import { useSelector } from "react-redux";      // Importamos la función que llama al estado

    function App() {
        const favMovieListArray = useSelector((state) => state.favMovieList);       // Usamos la función especificando el estado y lo guardamos en una constante
        
        console.log(favMovieListArray);         // Imprimimos la constante en la consola para comprobar que funciona
        
        return (
            <div>
                <h1 className="text-3xl font-bold underline">Hello world!</h1>
            </div>
        );
    }

    export default App;

```

## Agregar datos

Ya podemos llamar los datos, ahora es momento de agregar datos, para ello crearemos la función necesaria en nuestro `favMovieListSlice.js` como un `reducer` de la siguiente manera.

```jsx

    import {
        createSlice
    } from "@reduxjs/toolkit";

    const initialState = [{
        id: "hq"
        name: 'scarface',
        desc: 'Tells the story of Cuban refugee Tony Montana (Al Pacino), who arrives penniless in Miami during the Mariel boatlift and becomes a powerful and extremely homicidal drug lord.'
    }];

    export const favMovieListSlice = createSlice({
        name: 'favMovieList',
        initialState,
        reducers: {
            addMovie: (state, action) => {          // Le asignamos un nombre al reducer
                state.push(action.payload)          // Y usamos push para mandarlos al array
            }
        }
    })


    export const {
        addMovie
    } = favMovieListSlice.actions                   // Exportamos la acción para usarla en otro lado
    export default favMovieListSlice.reducer;

```

Para crear el id de cada uno de nuestros datos de momento utilizaremos [`uuid`](https://www.npmjs.com/package/uuid), el cual instalaremos de la siguiente manera.

```bash

    npm i uuid

```

Luego de esto podemos crear el resto de las funciones para generar la película.

```jsx

    import "./App.scss";
    import $ from "jquery";                                      // Utilizamos jQuery para agilizar la explicación de js
    import { useSelector, useDispatch } from "react-redux";         // Importamos el dispatch para llamar a la acción
    import { addMovie } from "./features/movies/favMovieListSlice";     // Importamos la acción
    import { v4 as uuid } from "uuid";                                  // Importamos uuid

    function App() {
        const favMovieListArray = useSelector((state) => state.favMovieList);

        const dispatch = useDispatch();             // Llamamos al useDispatch y la guardamos en una constante

        const handleSubmit = (e) => {           // Creamos un handleSubmit para obtener y guardar los datos
            e.preventDefault();
            dispatch(                           // Utilizamos el dispatch y le pasamos el objeto como parámetro para guardar
                addMovie({ 
                    id: uuid(),
                    name: $("#movieName").val(),
                    desc: $("#movieDesc").val() 
                })
            );
        };

        return (
            <div className="bg-gray-900 text-white min-h-screen h-fit text-center flex flex-col gap-8 p-4">
                <form
                    className="flex flex-col w-1/4 mx-auto text-black gap-4"
                    onSubmit={handleSubmit}
                >                                           {/* Creamos el form para guardar los datos */}
                    <input
                      className="rounded p-2"
                      type="text"
                      placeholder="movie name"
                      id="movieName"
                      required
                    />
                    <textarea
                      className="rounded p-2"
                      name="desc"
                      id="movieDesc"
                      cols="30"
                      rows="5"
                      placeholder="description"
                    ></textarea>
                    <button
                      className="py-3 px-6 text-white bg-purple-600 rounded w-1/2 mx-auto border-2 border-black transition-all   hover:scale-105"
                      type="submit"
                    >
                    SAVE
                    </button>
                </form>
                <div>                                                           {/* Creamos el div que contendrá nuestra lista */}
                    <h1 className="text-2xl uppercase underline font-bold pb-4">
                    fav movies
                    </h1>
                    <div className="flex justify-center items-center flex-wrap">
                        {favMovieListArray.map((movie, i) => (
                            <div
                              key={i}
                              className="w-1/4 bg-gray-500 flex flex-col justify-center items-center p-4 gap-6 border-2 border-black rounded self-stretch"
                            >
                                <h3 className="font-bold uppercase underline">{movie.name}</h3>
                                <p className="h-full flex items-center">{movie.desc}</p>
                                <button className="py-2 px-4 bg-red-600 rounded min-w-fit w-1/2 mx-auto border-2 border-black transition-all hover:scale-105">
                                    DELETE
                                </button>
                            </div>
                        ))}
                    </div>
                </div>
            </div>
        );
    }

    export default App;

```

Con esto hecho podemos agregar películas y ver como se actualiza en el momento.

## Eliminar datos

Ya tenemos los datos creados y guardados, pero va a ser necesario poder eliminar los datos del array, para esto crearemos otro reducer de la siguiente manera.

```jsx

    [ ... ]             // Resto del código

    export const favMovieListSlice = createSlice({

        name: 'favMovieList',

        initialState,

        reducers: {
            addMovie: (state, action) => {
                state.push(action.payload)
            },

            deleteMovie: (state, action) => {           // Le asignamos el nombre
                const movieInList = state.find(movie => movie.id === action.payload)        // Usamos ".find()" para buscar el id en el array
                state.splice(state.indexOf(movieInList), 1)         // Y buscamos el index para poder usar ".splice()"
            }
        }
    })

    export const {
        addMovie,
        deleteMovie,                // Lo importamos para usarlo luego
    } = favMovieListSlice.actions
    
    export default favMovieListSlice.reducer;

```

Ahora podemos llamarlo en nuestra `App.jsx` y asignarlo al botón correspondiente.

```jsx

    import "./App.scss";
    import $ from "jquery";
    import { useSelector, useDispatch } from "react-redux";
    import { addMovie, deleteMovie } from "./features/movies/favMovieListSlice";        // Importamos el delete
    import { v4 as uuid } from "uuid";

    function App() {
        [ ... ]

        const handleDelete = (id) => {
            dispatch(deleteMovie(id));        // Creamos el dispatch y le pasamos el id
        }

        return (
            <div className="bg-gray-900 text-white min-h-screen h-fit text-center flex flex-col gap-8 p-4">
                [ ... ]
                <div className="flex justify-center items-center flex-wrap">
                    {favMovieListArray.map((movie, i) => (
                        <div
                         key={i}
                         className="w-1/4 bg-gray-500 flex flex-col justify-center items-center p-4 gap-6 border-2 border-black  rounded self-stretch"
                        >
                            <h3 className="font-bold uppercase underline">{movie.name}</h3>
                            <p className="h-full flex items-center">{movie.desc}</p>
                            <button onClick={()=> handleDelete(movie.id)}             // Le pasamos el id de la película
                                    className="py-2 px-4 bg-red-600 rounded min-w-fit w-1/2 mx-auto border-2 border-black transition-all hover:scale-105">
                                DELETE
                            </button>
                        </div>
                    ))}
                </div>
            </div>
        );
    }

    export default App;

```
