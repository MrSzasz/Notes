# NextJS

[NextJS](https://nextjs.org/) es un framework basado en [ReactJs](../ReactJS/ReactJS.md), desarrollado en [TypeScript](../TypeScript/TypeScript.md) que tiene todas las funcionalidades de ReactJs, pero que a su vez agrega mas facilidades, como la de conectarnos y desarrollar un Back-End completo basado en [NodeJS](../../BackEnd/NodeJS/NodeJS.md), mayor facilidad para generar rutas, mejora el rendimiento base de ReactJS, posee una facilidad para generar alta escalabilidad, entre otras.  
Next esta desarrollado por [Vercel](https://vercel.com/), lo cual nos beneficia a la hora de subir nuestro proyecto en desarrollo.

## Instalación

> Para iniciar con Next lo primero que debemos tener en cuenta es que necesitaremos tener instalado [NodeJS](../../BackEnd/NodeJS/NodeJS.md)

Lo primero que debemos hacer es abrir una terminal en donde queremos iniciar nuestro nuevo proyecto con Next y crear nuestra carpeta con el siguiente comando y seguir las indicaciones que nos aparecen en consola.

```cmd

    npx create-next-app@latest

```

Hecho esto podemos empezara a abrir nuestra app con Visual Studio Code para ver que nos generó el comando.

## Template

El comando nos generó un template con todos los archivos necesarios para poder iniciar nuestro proyecto, siendo los más importantes los siguientes.

> styles => Carpeta que contiene los estilos generales del proyecto
>
> public => Carpeta que contiene los archivos públicos, en este caso, las imágenes que se usan para generar la página
>
> pages => Carpeta que contiene las rutas que iremos utilizando para crear el proyecto
>
> pages |-> api => Carpeta que contiene nuestro backend

## Head

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

    import BaseLayout from "../components/BaseLayout/baseLayout";        // Importamos nuestro layout

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

    import BaseLayout from "../components/BaseLayout/baseLayout";
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
Además de esto podemos crear carpetas para anidar paginas, un ejemplo rápido de esto seria crear la carpeta `/users/mainUser.jsx`, para la que deberíamos ir a la direccion `http://localhost:3000/users/mainUser` para poder ver lo que tenemos generado en la misma.

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
    import BaseLayout from "../components/BaseLayout/baseLayout";
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
