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

<!-- pages -->
<!-- links/anchors -->