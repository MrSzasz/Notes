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
En el archivo que creamos iniciamos jQuery y creamos un `console.log` para ver si todo esta funcionando bien.

```js

    $(document).ready(function () {
        console.log("Hola Mundo, con jQuery");
    });

```

> El archivo js con jQuery siempre utiliza `document.ready` al iniciar el código, ya que indica que se realizan las acciones solamente cuando termine de cargar la página

En VSC hay una extensión llamada [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer), la cual nos ayuda brindándonos un servidor para poder probar nuestro proyecto, y es el que usaremos actualmente para probar si todo funciona.

## Selectores

Con esto hecho podemos empezar a ver como seleccionar elementos en el HTML, empezamos creando 3 botones para ver las diferentes manera de interactuar con los mismos.

```HTML

    <main>
        <button>
            Primer botón
        </button>
        <button class="btn">
            Segundo botón
        </button>
        <button class="btn" id="btnID">
            Tercer botón
        </button>
        <ul>
            <li>1</li>
            <li data-position="2nd">2</li>
            <li>3</li>
            <li>4</li>
        </ul>
    </main>

```

En nuestro archivo js podemos hacer uso de los selectores de jQuery. Los selectores empiezan siempre con el símbolo `$` (dólar), seguido por un paréntesis (`()`) en el cual pondremos un string de lo que querramos seleccionar en el HTML.

```js

    $(document).ready(function () {
        $('button').html('Estos son botones')       // Al no indicar un punto (.) o un numeral (#) toma todos los elementos del tipo button
    });

```

Esta linea de código toma todos los elementos de tipo `button` de la pagina y cambia su contenido HTML (en este caso el texto) por el texto que le pasamos como parámetro, si no le pasamos nada simplemente los obtiene, lo que nos da la oportunidad de guardarlo en una variable y utilizarlo para otras cosas.  
Hay varias formas de usar los [selectores](https://www.w3schools.com/jquery/jquery_ref_selectors.asp), pero en este caso veremos los mas comunes siendo estos los siguientes.

```js

    $(document).ready(function () {
        // $('button').html('Estos son botones')
        $(".btn").html("seleccionado con clase")        // Seleccionamos en base a su clase
        $("#btnID").html("seleccionado con ID")         // Seleccionamos en base a su ID
        $("ul li[data-position='2nd']").html("este es el item con valor 2")         // Seleccionamos el item con el data que creamos en el HTML
        $("ul li:first").html("este es el primer item")         // Seleccionamos el primer li que encontramos
        $("ul li:last").html("este es el primer item")          // Seleccionamos el ultimo li que encontramos 
    });

```

> En el caso de los `ul li` estamos indicando que solo tomaremos los `li` que estén dentro de un elemento `ul`

## Eventos

Ahora podemos agregar eventos a los botones para que podamos interactuar con los mismos. Empezamos con el evento más básico, un evento `click` para, como su nombre lo indica, detectar cuando el usuario hizo un click en nuestro botón.

```js

    $(document).ready(function () {
        $(".btn").click(() => {
            alert("Soy una alerta!");
        });
    });

```

Con esto lo que hacemos es que se envíe una alerta cada vez que hacemos click en el botón que tiene la clase `btn`, usando el evento `click`, el cual es solo uno de los tantos [eventos de jQuery](https://api.jquery.com/category/events/), pero es uno de los mas utilizados junto al `dblclick`, el cual solo se inicia cuando se hace doble click sobre el elemento seleccionado.  

## CSS

También es posible manipular los estilos y combinarlos con los eventos, haciendo que cambie el estilo dependiendo de lo que hagamos. Por ejemplo, crearemos un simple `p` y dos botones para cambiarle el color a la fuente.

```HTML

    <main>
        <p id="text">Hola soy un párrafo</p>
        <button id="rojo">rojo</button>
        <button id="azul">azul</button>
        <button id="varios">color y upper</button>
    </main>

```

Y ahora podemos seleccionarlo en nuestro js, agregando los eventos correspondientes.

```js

    $(document).ready(function () {

        let textP = $("#text")      // Seleccionamos el elemento y lo guardamos en una variable
        
        $("#rojo").click(() => {
            textP.css("color", "red")       // Cambiamos el CSS del elemento al hace click
        });
        
        $("#azul").click(() => {
            textP.css("color", "blue")
        });
        
        $("#varios").click(() => {
            textP.css({         // Para pasar mas de un modificador lo hacemos en forma de objeto 
                "color": "blue",
                "text-transform": "uppercase"        // Transformamos el texto a mayúsculas
            });
        });
    });

```
