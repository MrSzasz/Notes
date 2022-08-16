# jQuery

[`jQuery`](https://jquery.com/) es una biblioteca de JavaScript creada en el año 2006, la cual es una "compilación" de funciones de JavaScript que ayuda con la integración entre diferentes navegadores. Actualmente hay paginas que siguen usando jQuery, y nunca viene mal aprenderlo, es por eso que empecé a tomar notas en esta guía.

## Instalación

Para empezar a usar jQuery en nuestro proyecto debemos [instalarlo](https://jquery.com/download/), para lo cual existen diferentes formas de hacerlo. Podemos hacer uso de `npm` (npm i jquery) o en su defecto, usar un [`CDN`](https://developer.mozilla.org/es/docs/Glossary/CDN), que es la manera en la que vamos a trabajar con nuestro proyecto.  
Para ello debemos crear nuestro archivo base en HTML (en VSC podemos escribir `!` (signo de exclamación) y nos creará automáticamente la base de nuestro HTML) y al final del body agregar el link al CDN.

```HTML

    <body>

        <script src="https://code.jquery.com/jquery-3.6.0.min.js"
            integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4=" crossorigin="anonymous"></script>
    </body>

```

## Coding

Hecho esto podemos empezar a probar nuestro jQuery. Para ello crearemos un archivo `.js` que importaremos debajo de la importación de jQuery.
