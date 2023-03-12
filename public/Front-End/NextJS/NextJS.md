# NextJS

[NextJS](https://nextjs.org/) es un framework basado en [ReactJs](../ReactJS/ReactJS.md), desarrollado en [TypeScript](../TypeScript/TypeScript.md) que tiene todas las funcionalidades de ReactJs, pero que a su vez agrega mas facilidades, como la de conectarnos y desarrollar un Back-End completo basado en [NodeJS](../../BackEnd/NodeJS/NodeJS.md), mayor facilidad para generar rutas, mejora el rendimiento base de ReactJS, posee una facilidad para generar alta escalabilidad, entre otras.  
Next esta desarrollado por [Vercel](https://vercel.com/), lo cual nos beneficia a la hora de subir nuestro proyecto en desarrollo.

## Guía de Temas

1. [Instalación](#instalación)
2. [SSR vs CSR](#server-side-rendering-vs-client-side-rendering)
3. [Preparación del template](#template)
4. Código
    - [Layout](#head-y-layout)
    - [Styling](#estilos)
    - [Creación de páginas](#páginas)
    - [Links y enrutamiento](#links)
    - [Imágenes](#imágenes)
    - Fetching
      - [Fetching estático](#getstaticprops)
      - [Fetching dinámico](#getserversideprops)
    - Rendering
      -[Páginas dinámicas](#páginas-dinámicas)
      -[Páginas estáticas](#generar-página-estática)
    - [Deploy](#deploy-a-vercel)

---

## Instalación

> Para iniciar con Next lo primero que debemos tener en cuenta es que necesitaremos tener instalado [NodeJS](../../BackEnd/NodeJS/NodeJS.md)

Lo primero que debemos hacer es abrir una terminal en donde queremos iniciar nuestro nuevo proyecto con Next y crear nuestra carpeta con el siguiente comando y seguir las indicaciones que nos aparecen en consola.

```cmd
npx create-next-app@latest
```

Hecho esto podemos empezara a abrir nuestra app con Visual Studio Code para ver que nos generó el comando.

## Server Side Rendering vs Client Side Rendering

Hay dos formas de renderizar una página web, desde el lado del cliente (`Client side rendering`), siendo esta la forma de que utilizan los frameworks como React y Vue para mostrar la información en la misma, y desde el lado del servidor (`Server side rendering`), el cual hace que el servidor se encargue del generar los HTML necesarios para generar todo el contenido de la página.  
Hay una gran diferencia entre estos dos, la principal es la forma en la que la página recibe los datos, ya que en el CSR la página renderiza un HTML básico sin información, quedando de la siguiente manera.

```html
<body>
    <main id="app"></main>
</body>
```

Esto mejora en cuanto a la versatilidad de la página en sí, pero en cuanto al SEO es contraproducente, ya que el mismo solo muestra una etiqueta `main` a los crawlers de Google, en cambio cuando se genera una página con SSR se envía todo el contenido de la página en formato HTML de al siguiente manera.

```html
<body>
    <main>
        <h1>Hola mundo</h1>
    </main>
</body>
```

La ventaja de `NextJs` sobre esto es que nos deja elegir que tipo de rendering usaremos, pero sin limitarnos a utilizar solo uno, sino que pudiendo combinar ambos en el caso que sea necesario el uso de uno o el otro.

## Template

El comando nos generó un template con todos los archivos necesarios para poder iniciar nuestro proyecto, siendo los más importantes los siguientes.

> styles => Carpeta que contiene los estilos generales del proyecto
>
> public => Carpeta que contiene los archivos públicos, en este caso, las imágenes que se usan para generar la página
>
> pages => Carpeta que contiene las rutas que iremos utilizando para crear el proyecto
>
> pages |-> api => Carpeta que contiene nuestro backend

## Head y layout

Como podemos ver en el archivo `index.js`, Next nos importó un modulo llamado `Head`, el mismo contiene los datos necesarios del head de nuestra aplicación, como puede ser el titulo que se muestra en la pestaña (`title`), la descripción de la misma (`description`) y el ícono que se mostrará (`icon`). Esto nos ayudará con el SEO, ya que gracias a este Head podemos cambiar lo que sea necesario cuando cambiemos de página y necesitemos refrescar estos datos.  
Teniendo esto en mente podemos crear un componente que nos ayude con las bases del head de cada página. Para ello crearemos la carpeta `components` y dentro de ella el layout base para todas nuestras páginas, creando un archivo llamado `BaseLayout.jsx` que contendrá nuestro head de la siguiente manera.

```js
import Head from "next/head";       // Importamos el Head desde Next

const BaseLayout = ({       // Creamos nuestro componente
     children,                  // Le pasamos children para poder usar el componente coo contenedor
     title = "NextJS project",              // Indicamos el titulo predeterminado
     desc = "First project with NextJS",    // Indicamos la descripción predeterminada
    }) => {
    return (
        <>
            <Head>                                          {/* Usamos el head */}
                <title>{title}</title>                      {/* Agregamos el titulo en base a la prop */}
                <meta name="description" content={desc} />  {/* Y la descripción */}
                <link rel="icon" href="/favicon.ico" />
            </Head>
            {children}              {/* Indicamos donde tendremos todos los demás componentes */}
        </>
    );
};

export default BaseLayout;
```

Y ahora podemos llevar esto a nuestro `index.js` de la siguiente manera.

```js
import BaseLayout from "../components/BaseLayout/BaseLayout";        // Importamos nuestro layout

const Home = () => {
    return (
        <>
            <BaseLayout>                {/* Lo usamos para encerrar el contenido de la página */}
                <h1>Welcome!</h1>       {/* Indicamos el contenido de la página */}
            </BaseLayout>
        </>
    );
};

export default Home;
```

Con esto armado podemos iniciar nuestra página y ver como vamos avanzando, ademas de poder pasar los parámetros al `BaseLayout` y ver como cambian en tiempo real con el siguiente comando.

```cmd
npm run dev
```

## Estilos

Al iniciar la pagina podemos ver que posee algunos estilos base, los cuales podemos cambiar de una forma particular.  
Los estilos en Next no se paran de la misma manera, hay dos formas de estilizar, la primera es usando [CSS Modules](https://keepcoding.io/blog/css-modules-en-react/), los cuales dividen los estilos en diferentes módulos, como su nombre lo indica, haciendo que cada estilo afecte unicamente al componente que estamos generando.  
Para empezar con CSS Modules vamos a crear un componente nuevo llamado `MainButton.jsx`, en el mismo crearemos un archivo CSS llamado `MainButton.module.css`. Con esto hecho podemos empezar a crear nuestro botón de la siguiente manera.

```jsx
import styles from './MainButton.module.css';       // Importamos los estilos

const MainButton = ({text="Click me!"}) => {
    return (
        <button className={styles.mainButton}>          {/* Llamamos a la clase que vamos a usar */}
            {text}
        </button>
    )
}

export default MainButton
```

Y en el archivo CSS empezamos a colocar nuestros estilos.

```css
.mainButton {
    width: fit-content;
    height: fit-content;
    padding: .7em 1em;
    background-color: #e3e3e3;
    border: 2px solid #2e2e2e;
    color: #2e2e2e;
    font-size: medium;
    font-weight: bold;
    transition: ease all .25s;
    border-radius: 10px;
    cursor: pointer;
}

.mainButton:hover {
    background-color: #2e2e2e;
    border: 2px solid #e3e3e3;
    color: #e3e3e3;
}
```

Como podemos ver, las clases se llaman como propiedad `style`, pero en el CSS no hay cambio alguno.  
Como dije anteriormente, no es la única forma de crear estilizar en Next, sino que también podemos hacer uso de [`Styled JSX`](https://nextjs.org/blog/styling-next-with-styled-jsx), los cuales funcionan teniendo una etiqueta `style` en nuestro archivo.  
Tomando el ejemplo anterior, se podría usar Styled JSX y nos quedaría de la siguiente manera.

```jsx
const MainButton = ({ text = "Click me!" }) => {
    return (
        <button className="mainButton">
        {text}
        <style jsx>{`       
            .mainButton {
            width: fit-content;
            height: fit-content;
            padding: 0.7em 1em;
            background-color: #e3e3e3;
            border: 2px solid #2e2e2e;
            color: #2e2e2e;
            font-size: medium;
            font-weight: bold;
            transition: ease all 0.25s;
            border-radius: 10px;
            cursor: pointer;
            }

            .mainButton:hover {
            background-color: #2e2e2e;
            border: 2px solid #e3e3e3;
            color: #e3e3e3;
            }
        `}</style>
        </button>
    );
};

export default MainButton;
```

Como podemos ver, esta forma de estilizar no es muy organizada, ademas de ocupar mas espacio en el mismo código, pero sigue siendo funcional.  
Para ver nuestro botón correctamente podemos importarlo en nuestro `index` como importaríamos cualquier otro componente en React.

```jsx
import BaseLayout from "../components/BaseLayout/BaseLayout";
import MainButton from "../components/MainButton/MainButton";

const Home = () => {
    return (
        <>
            <BaseLayout>
                <h1>Welcome!</h1>
                <MainButton/>
            </BaseLayout>
        </>
    );
};

export default Home;
```

Por ultimo, también es posible asignar más de un estilo en el componente, utilizando los backticks (``), y pasar estilos como propiedades con el uso de corchetes ([]) de la siguiente manera.

```jsx
import styles from './MainButton.module.css';       // Importamos los estilos

const MainButton = ({text="Click me!", color="blueish"}) => {
    return (
        <button className={`${styles.mainButton} ${styles[color]}`}>          {/* Le pasamos las clases que indicamos en el CSS */}
            {text}
        </button>
    )
}

export default MainButton
```

Y en su respectivo CSS agregamos la clase que le pasaremos como prop.

```css
.blueish {
    background-color: #3438a3;
    border: 2px solid #a12d37;
}

.redish {
    background-color: #a12d37;
    border: 2px solid #3438a3;
}
```

## Páginas

Ya aprendimos como crear componentes y estilizarlos, los cuales usaremos en diferentes páginas, pero aun no tenemos diferentes páginas, es por eso que empezaremos a crear una de prueba, para ver el uso de la enrutación por defecto que trae Next.  
Para crear una nueva ruta debemos ir a la carpeta `pages` que se nos generó cuando creamos el proyecto, y dentro de ella crearemos un archivo llamado `aboutUs.jsx` de la siguiente manera.

```jsx
import MainButton from "../components/MainButton/MainButton";
import BaseLayout from "../components/BaseLayout/BaseLayout";

const aboutUs = () => {
    return (
        <BaseLayout title="About Us" desc="Page about us">
            <div>aboutUs</div>
            <MainButton />
        </BaseLayout>
    );
};

export default aboutUs;
```

Hecho esto podemos ir a la direccion `http://localhost:3000/aboutUs` y ver como se generó la página con nuestro botón antes creado y sus respectivos estilos.  
Otra forma de crear direcciones es crear una carpeta contenedora con el nombre de la direccion que necesitemos, y dentro de la misma crear el archivo `index.jsx`, quedando el mismo de la siguiente manera `/aboutUs/index.jsx`, dando el mismo resultado final.  
El uso de carpetas para la creación de direcciones también ayuda  al ahora de crear diferentes direcciones anidadas, por ejemplo, si queremos crear una dirección privada que contendrá un dashboard podemos crear una carpeta llamada `private` y dentro de la misma el archivo `dashboard.jsx`, teniendo que usar la dirección `http://localhost:3000/private/dashboard` para acceder a la misma.

## Links

Ya tenemos las rutas, pero no podemos ir de una a otra sin escribirlo como URL, así que es lo que debemos cambiar ahora. Para esto Next tiene un componente llamado `Link`, el cual nos crea una redirección a la pagina que necesitemos, quedándonos en `aboutUs` de la siguiente manera.

```jsx
import MainButton from "../components/MainButton/MainButton";
import BaseLayout from "../components/BaseLayout/BaseLayout";
import Link from "next/link";

const aboutUs = () => {
    return (
        <BaseLayout title="About Us" desc="Page about us">
            <div>aboutUs</div>
            <MainButton />
            <Link href={"/"}>Home</Link>
        </BaseLayout>
    );
};

export default aboutUs;
```

Y lo mismo en nuestro `index`.

```jsx
import Link from "next/link";
import BaseLayout from "../components/BaseLayout/BaseLayout";
import MainButton from "../components/MainButton/MainButton";

const Home = () => {
    return (
        <>
            <BaseLayout>
                <h1>Welcome!</h1>
                <MainButton />
                <Link href={'/aboutUs'}>About Us</Link>
            </BaseLayout>
        </>
    );
};

export default Home;
```

Como vemos, la forma en la que se crean los links es similar al router de React, también convirtiéndose en un `<a></a>` en la salida.

> En versiones anteriores a `Next 12.2` era necesario tener un `<a></a>` dentro del componente Link, quedando el mismo de la siguiente manera `<Link href=""><a></a></Link>`

## Imágenes

Uno de los beneficios de utilizar Next es la posibilidad de optimizar las imágenes gracias al componente `Image`. El mismo hace que la carga de imágenes sea mucho más rápida.  
Para utilizar este componente debemos crear una carpeta en nuestro `public` llamada `images` (/public/images), dentro agregaremos la imagen que utilizaremos luego. En nuestro código importaremos el componente de la siguiente manera.

```jsx
import Link from "next/link";
import BaseLayout from "../components/BaseLayout/BaseLayout";
import MainButton from "../components/MainButton/MainButton";
import Image from "next/image"

const Home = () => {
    return (
        <>
            <BaseLayout>
                <Image 
                    src="/main.png"         // Le pasamos la dirección de la imagen 
                    alt="Vercel Logo"          // Agregamos el alt del mismo
                    width={72}          // Ademas debemos indicar el tamaño en pixeles de la imagen para la optimización del render
                    height={16} 
                />
                <h1>Welcome!</h1>
                <MainButton />
                <Link href={'/aboutUs'}>About Us</Link>
            </BaseLayout>
        </>
    );
};

export default Home;
```

De esta forma Next renderiza mejor las imágenes, ayudando a la carga de las mismas.  
Este método es bueno siempre y cuando sepamos el tamaño de nuestra imagen, pudiendo asignar un tamaño en pixeles adecuadamente, pero si desconocemos el tamaño de la misma es posible usar `layout="fill"`. Para hacer uso de la misma es `NECESARIO` envolver el componente Image dentro de un contenedor, al mismo se le deberá colocar la propiedad `position: relative`, ya que la imagen que se genera con el `fill` tiene `position: absolute`. La misma quedaría de la siguiente manera.

```jsx
import Link from "next/link";
import BaseLayout from "../components/BaseLayout/BaseLayout";
import MainButton from "../components/MainButton/MainButton";
import Image from "next/image"
import styles from "./index.module.css";

const Home = () => {
    return (
        <>
            <BaseLayout>
                <div className={styles.mainImageContainer}>         // El contenedor debe tener una posición relative para que pueda funcionar el fill
                    <Image 
                    src="https://picsum.photos/500/500"         // En este caso utilizamos un placeholder de imágenes 
                    alt="Imagen"
                    layout="fill"       // Debemos indicar que llenará el tamaño del componente padre 
                    objectFit="cover"       // Podemos cambiar el object-fit de la misma, pero por defecto sera cover
                    />
                </div>
                <h1>Welcome!</h1>
                <MainButton />
                <Link href={'/aboutUs'}>About Us</Link>
            </BaseLayout>
        </>
    );
};

export default Home;
```

## GetStaticProps

Uno de los beneficios de poder hacer sitios estáticos con Next es la posibilidad de pedir datos a una API o base de datos en el momento en el que se hacen los archivos estáticos, para esto es posible usar `getStaticProps`.  
Esta función genera un pedido a la API durante la compilación de nuestra app, tomando los datos y guardando los datos en formato HTML. Los beneficios que tiene esto es la velocidad del mismo a la hora de generar la vista para el cliente, ya que al tener los datos pre cargados solo tienen que mostrarse, pero esto solo funciona con datos fijos o con cambios mínimos en un largo periodo de tiempo, ya que los mismos no se vuelven a pedir a menos que se vuelva a generar la aplicación estática.  
Para esto tomaremos un ejemplo simple de pedido de datos estáticos a una api de ejemplo.

```jsx
export default function Home({ dataFromDB }) {      // Pasamos los datos que vienen desde GSP como props
  return (
    [...]
  );
}

export async function getStaticProps() {        // Pedimos los datos al final de nuestro código
  try {                                                                         // Envolvemos todo en un try catch
    const data = await fetch("https://jsonplaceholder.typicode.com/users");     // Hacemos el pedido a la API
    const dataFromDB = await data.json();           // Y formateamos la respuesta

    return {
      props: {          // Hacemos un return de la respuesta como prop para poder usarla en el componente
        dataFromDB,
      },
    };
  } catch (err) {
    console.log(err);
  }
}
```

Con esto hecho podemos tener nuestros datos preparados en el momento de la compilación de nuestra app.

## GetServerSideProps

Así como tenemos el pedido de datos estáticos en el momento que se genera la app, también tenemos una forma de pedir los datos en el momento en el que el usuario entra en la misma, a esto se lo llama `getServerSideProps`, ya que los datos se piden desde el servidor. Como su nombre lo dice, la diferencia radica en que el mismo se pide en el momento, pudiendo ver los cambios que se hayan hecho en la base de datos o en la API desde el momento en el que se generó la app, por lo que es mejor para base de datos con actualizaciones constantes o en tiempos mas cortos.  
El mismo solo se diferencia en algunas cosas muy puntuales, pero la base es la misma que GSP.

```jsx
export default function Home({ dataFromDB }) {      // Pasamos los datos que vienen desde GSSP como props
  return (
    [...]
  );
}

export async function getServerSideProps(context) {        // Pedimos los datos al final de nuestro código
  try {                                                                         // Envolvemos todo en un try catch
    const data = await fetch("https://jsonplaceholder.typicode.com/users");     // Hacemos el pedido a la API
    const dataFromDB = await data.json();           // Y formateamos la respuesta

    return {
      props: {          // Hacemos un return de la respuesta como prop para poder usarla en el componente
        dataFromDB,
      },
    };
  } catch (err) {
    console.log(err);
  }
}
```

## Páginas dinámicas

Es posible crear páginas dinámicas en Next, para ello solo es necesario utilizar corchetes ([]) a la hora de crear un nuevo archivo, dentro de los mismos colocaremos lo que vaya a ser dinámico, por ejemplo, si queremos hacer una página que contendrá información sobre uno de los usuarios que pedimos a la API podemos crear el archivo `[user].jsx` en el cual crearemos nuestra página de la siguiente manera.

```jsx
import Link from "next/link";
import Layout from "../components/Layout/Layout";

const UserPage = () => {      // Hay que exportar el componente como tal, es por eso que no usamos _user_ en este caso en particular
  return (
    <Layout>
      <div>
       <h2>nombre</h2>
       <small>email</small>
        <Link href={`http://localhost:3000/`}>
          Go back
        </Link>
      </div>
    </Layout>
  );
};

export default UserPage;
```

Lo que tenemos hecho ahora solamente es la base de nuestra ruta dinámica, pero sin los datos, para ello hay dos formas de pedir los datos dependiendo de que tipo de pedido se haga, estático o del lado del servidor.  
Para hacer un pedido de datos estáticos se utiliza la función `getStaticPaths()` de la siguiente manera.

```jsx
import Link from "next/link";
import Layout from "../components/Layout/Layout";

const UserPage = ({ userData }) => {        // Los datos que pedimos con GSP
  return (
    <Layout>
      <div>
       <h2>{userData.name}</h2>
       <small>{userData.email}</small>
        <Link href={`http://localhost:3000/`}>
          Go back
        </Link>
      </div>
    </Layout>
  );
};

export function getStaticPaths(){
    try{
        const res = await fetch("https://jsonplaceholder.typicode.com/users");     // Hacemos el pedido a la API
        const dataFromApi = await res.json();
        const paths = dataFromApi.map((data)=>({
            params: {user: `${user.id}`}            // Tomamos el ID para generar las rutas dinámicas
        }))

        return{
            paths,          // Devolvemos el path con todas las rutas
            fallback: true      // Y generamos una página 404 cuando no exista la ruta
        }
    } catch (err){
        console.error(err)
    }
}

export async function getStaticProps({ params }) {        // Pedimos los datos en base a los params generados anteriormente
  try {
    const data = await fetch(`https://jsonplaceholder.typicode.com/users/${params.user}`);     // Hacemos el pedido a la API en base al param
    const userData = await data.json();

    return {
      props: {
        userData,
      },
    };
  } catch (err) {
    console.log(err);
  }
}

export default UserPage;
```

Esto nos genera las rutas dinámicas y se piden los datos en base a los parámetros que se envíen por la URL, aunque solamente funciona cuando se genera datos de forma estática, si queremos hacerlo en forma dinámica con SSR se debe hacer de la siguiente manera.  

```jsx
import Link from "next/link";
import Layout from "../components/Layout/Layout";

const UserPage = ({ userData }) => {        // Los datos que pedimos con GSP
  return (
    <Layout>
      <div>
       <h2>{userData.name}</h2>
       <small>{userData.email}</small>
        <Link href={`http://localhost:3000/`}>
          Go back
        </Link>
      </div>
    </Layout>
  );
};

export async function getServerSideProps(context) {
  try {
    const { params } = context;         // Tomamos los parámetros que se envían por URL
    const { user } = params;        // Y hacemos destructuring del user

    const data = await fetch(`https://jsonplaceholder.typicode.com/users/${user}`);     // Hacemos el pedido a la API en base al context
    const userData = await data.json();

    return {
      props: {
        userData,       // Enviamos los datos como lo hacemos normalmente
        user,
      },
    };
  } catch (err) {
    console.log(err);
  }
}

export default UserPage;
```

## Generar página estática

Si nuestro objetivo final es generar una página estática para subirla a un servidor necesitamos indicarlo en el archivo `package.json` como lo indica la documentación oficial. Para ello debemos crear el método `export`, el cual generará todos nuestros archivos estáticos en una carpeta `out`, la cual podremos subir normalmente.  
El script debería quedarnos de la siguiente manera.

```json
  "scripts": {
    // [...]
    "export": "next build && next export"
  },
```

Con esto configurado solo será necesario iniciar el script escribiendo `npm run export` en nuestra consola, pudiendo ver como se genera la carpeta `out` al finalizar.

## Deploy a Vercel

Si la página no será estática lo mejor será hacer nuestro deploy directamente en Vercel, ya que al ser desarrollado por ellos la implantación es mucho mejor que con otros servidores. En el mismo es posible linkear directamente nuestra cuenta de Github y elegir el repo que necesitemos hacer el deploy directamente.
