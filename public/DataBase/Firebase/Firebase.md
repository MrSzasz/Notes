# Firebase

[Firebase](https://firebase.google.com/) es la plata forma de Google que ayuda con el desarrollo de aplicaciones gracias a los diferentes servicios que ofrece, como puede ser una base de datos, autenticación, comunicación en tiempo real, entre otros. En esta ocasión usaremos Firestore y la plataforma de autenticación de la misma.

## Instalaciones

Para empezar con Firebase es necesario tener una cuenta en Google y luego iniciar un nuevo proyecto en Firebase desde su [consola](https://console.firebase.google.com/), configurando todos los campos necesarios.  
Con esto hecho podemos entrar en la configuración de nuestro proyecto en particular, seleccionando la version web, agregando el nombre de nuestra app, sin agregar el hosting, luego crearemos un nuevo proyecto en [React](../../Front-End/ReactJS/ReactJS.md) e instalamos el paquete necesario de Firebase con el siguiente comando.

```cmd

    npm i firebase

```

Y copiamos el SKD que nos provee Firebase, el cual seria el siguiente.

```js

    import { initializeApp } from "firebase/app";

    const firebaseConfig = {
        apiKey: "<apikey>",
        authDomain: "<domain>",
        projectId: "<project-id>",
        storageBucket: "<storage>",
        messagingSenderId: "<id>",
        appId: "<appid>"
    };

    const app = initializeApp(firebaseConfig);

```

Luego de esto podemos ir a la raíz de nuestro proyecto y crear la carpeta llamada `firebase` y dentro el archivo `config.js`, en la que pegaremos el SDK y lo modificaremos para poder agregar las variables de entorno, quedando de la siguiente manera.

```js

    import { initializeApp } from "firebase/app";

    const firebaseConfig = {
        apiKey: import.meta.env.VITE_APP_APIKEY,                    // Keys que luego reemplazaremos en .env
        authDomain: import.meta.env.VITE_APP_AUTHDOMAIN,
        projectId: import.meta.env.VITE_APP_PROJECTID,
        storageBucket: import.meta.env.VITE_APP_STORAGEBUCKET,
        messagingSenderId: import.meta.env.VITE_APP_MESSAGINGSENDERID,
        appId: import.meta.env.VITE_APP_APPID
    };

    const app = initializeApp(firebaseConfig);

    export default function getFirestoreApp() { 
        return app
    }

```

> Usamos `import.meta.env.VITE` porque la app en cuestión esta hecha con Vite

Ademas, debemos crear estas mismas variables en nuestro archivo `.env` para que sean ocultas, de la siguiente manera.

```env

    VITE_APP_APIKEY=<apikey>
    VITE_APP_AUTHDOMAIN=<domain>
    VITE_APP_PROJECTID=<project-id>
    VITE_APP_STORAGEBUCKET=<storage>
    VITE_APP_MESSAGINGSENDERID=<id>
    VITE_APP_APPID=1:<appid>

```

> IMPORTANTE agregar el `.env` al archivo `.gitignore`

Luego de esto debemos ir a nuestro `main.jsx` e importar la configuración de Firebase.

```jsx

    import React from "react";
    import ReactDOM from "react-dom/client";
    import App from "./App";
    import "./index.scss";
    import getFirestoreApp from "./firebase/config";        // Importamos la configuración 

    getFirestoreApp();          // Y la inicializamos

    ReactDOM.createRoot(document.getElementById("root")).render(
        <App />
    );

```

Con esto tendremos nuestra conexión con Firebase completa, el ultimo paso será crear la base de datos desde la [consola del proyecto](https://console.firebase.google.com/), accediendo a compilación |-> Firestore, creamos la base de datos y le asignamos el modo de prueba, dejando el host predeterminado.

> IMPORTANTE, el modo de prueba tiene una duración de 30 días que permite leer y escribir en la base de datos, luego debemos cambiarlo como sea que lo necesitemos

## (C)RUD - Create

Ahora tenemos nuestra base de datos completa, pero será necesario crear los datos para empezar a utilizarla. Para ello tenemos dos formas, manualmente desde la misma consola o configurando nuestra subida de datos automática. Para ello empezaremos creando un botón en nuestra `App.jsx` con la función necesaria para subir los datos de la siguiente manera

```jsx

    import { addDoc, collection, getFirestore } from "firebase/firestore";      // Importamos lo necesario

    const App = () => {

        const handleLoadDB = async () => {      // Creamos la función para subir los datos
            const data = [                      // Pasamos los datos que subiremos
                {
                    name: "Jack",
                    lastName: "Skellington",
                },
                {
                    name: "Sally",
                    lastName: "Skellington",
                }
            ];

            const db = await getFirestore();        // Traemos la base de datos

            await data.forEach((name) => {          // Subiremos uno por uno los datos dentro de nuestro array
                addDoc(
                        collection(db, "users"),         // Traemos la colección, pasando db y el nombre de la colección como parámetros
                        { ...name }         // Y le pasamos los datos a subir
                    )
                    .then(console.log('done'))      // Por cada objeto subido imprimimos una confirmación
            });
        };

        return (
            <div>
                <button onClick={handleLoadDB}>load data</button>
            </div>
        );
    };

    export default App;

```

> Si la colección no existe, se creará en el momento, además de ello se creará un id único por cada dato que se suba

## C(R)UD - Read

Ahora que tenemos los datos subidos podemos pedirlos, para ello crearemos un nuevo componente llamado `LoadedData.jsx` de la siguiente manera.

```jsx

    import { collection, getDocs, getFirestore } from "firebase/firestore";         // Importamos lo necesario
    import { useEffect, useState } from "react";

    const LoadedData = () => {
        const [dataFromDB, setDataFromDB] = useState([]);       // Creamos un estado para guardar los datos

        const getProductsFromFirebase = async () => {       // Creamos la función para pedir los datos
            const db = getFirestore();                  // Llamamos a la base de datos

            const queryCollection = collection(db, "users");        // Creamos la colección pasando el nombre de la misma

            await getDocs(queryCollection)          // Traemos los datos en base a la colección
                .then((res) =>
                    setDataFromDB(res.docs.map((item) => ({ ...item.data(), id: item.id })))        // Guardamos los datos en nuestro array
            );
        };

        useEffect(() => {
            getProductsFromFirebase();      // Los datos se pedirán una vez que cargue la página
        }, []);

        return (
            <div>
                {dataFromDB.length === 0 ? (
                    <h1>Loading...</h1>             // Si no hay datos mostrará la carga
                ) : (
                    dataFromDB.map((data) => {      // Si hay datos los itera y crea una card por cada dato
                        <div key={data.id}>
                            <h2>{data.name}</h2>
                            <h3>{data.lastName}</h3>
                        </div>;
                    })
                )}
            </div>
        );
    };

    export default LoadedData;

```

También es posible filtrar los datos de la siguiente manera.

```jsx

    import {
        collection,
        getDocs,
        getFirestore,
        query,
        where,
    } from "firebase/firestore";                // Importamos lo necesario
    import { useEffect, useState } from "react";

    const LoadedData = () => {
        const [dataFromDB, setDataFromDB] = useState([]);

        const getProductsFromFirebase = async () => {
            const db = getFirestore();

            const queryCollection = collection(db, "users");

            const queryCollectionFiltered = query(      // Creamos la query
                queryCollection,
                where("name", "==", "Jack")             // Y le pasamos las condiciones que necesitemos
            );

            await getDocs(queryCollectionFiltered).then((res) =>            // Pedimos los datos en base a la query filtrada
                setDataFromDB(res.docs.map((item) => ({ ...item.data(), id: item.id })))
            );
        };

        useEffect(() => {
            getProductsFromFirebase();
        }, []);

        return (
            <div>
                {dataFromDB.length === 0 ? (
                    <h1>Loading...</h1>
                ) : (
                    dataFromDB.map((data) => {
                        <div key={data.id}>
                            <h2>{data.name}</h2>
                            <h3>{data.lastName}</h3>
                        </div>;
                    })
                )}
            </div>
        );
    };

    export default LoadedData;

```

> Hay mas formas de filtrar y ordenar, las cuales pueden verse [aquí](https://firebase.google.com/docs/firestore/query-data/order-limit-data?hl=es&authuser=0)

Si necesitamos traer un solo dato podemos usar `getDoc`.

```jsx

    import { doc, getDoc, getFirestore } from "firebase/firestore";         // Importamos lo necesario

    const LoadedData = () => {
        const handleGet = async () => {
            const db = await getFirestore();

            const userInDB = await getDoc(doc(db, "users", "xocIDMNEqTKR4A0HjCasg"));       // Pasamos la base de datos, la colección y el ID del objeto

            userInDB.exists()                   // Comprobamos si existe
            ? console.log(userInDB.data())      // Si hay, lo muestra en consola
            : console.error("Not found");       // Sino, indica el error
        };

        return (
            <div>
                <button onClick={handleGet}>get user</button>
            </div>
        );
    };

    export default LoadedData;

```

## CR(U)D - Update

Es momento de editar nuestro datos, para ello podemos hacerlo con la función `update()` de Firebase.

```jsx

    import { doc, getFirestore, updateDoc } from "firebase/firestore";          // Importamos lo necesario

    const LoadedData = () => {
        const handleUpdate = async () => {      // Creamos la función
            const db = await getFirestore();
            const dataRef = doc(db, "users", "xocIDMNEqTKR4A0HjCasg");      // Buscamos el dato, pasando la base de datos, la colección y el ID del objeto 

            await updateDoc(dataRef, {      // Le pasamos el objeto
                name: "Jackie",             // Y elegimos que queremos cambiar del mismo
            });
        };

        return (
            <div>
                <button onClick={handleUpdate}>update</button>
            </div>
        );
    };

    export default LoadedData;

```

## CRU(D) - Delete

Por ultimo podemos borrar los datos de la base de datos. Hay diferentes formas de borrar documentos, pero la misma documentación de Firebase indica que es mejor borrarlo desde la misma consola del proyecto, más allá de ello podemos hacerlo con `deleteDoc()`.

```jsx

    import { deleteDoc, doc, getFirestore } from "firebase/firestore";

    const LoadedData = () => {
        const handleDelete = async () => {
            const db = await getFirestore();

            await deleteDoc(doc(db, "users", "xocIDMNEqTKR4A0HjCasg"));         // Le pasamos el objeto que pedimos con "doc"
        };

        return (
            <div>
                <button onClick={handleDelete}>delete</button>
            </div>
        );
    };

    export default LoadedData;

```

También podemos borrar un campo especifico de un objeto de la siguiente manera.

```jsx

    import { deleteDoc, doc, getFirestore } from "firebase/firestore";

    const LoadedData = () => {
        const handleDelete = async () => {
            const db = await getFirestore();

            const dataRef = doc(db, "users", "xocIDMNEqTKR4A0HjCasg");          // Traemos el objeto

            await updateDoc(dataRef, {
                name: deleteField()             // Eliminamos el field indicado
            });
        };

        return (
            <div>
                <button onClick={handleDelete}>delete</button>
            </div>
        );
    };

    export default LoadedData;

```

Con esto hecho tendremos configurado el CRUD completo de Firebase.
