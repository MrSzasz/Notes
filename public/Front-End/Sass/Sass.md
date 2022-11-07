# Sass

[Sass](https://sass-lang.com/) es un pre procesador de CSS el cual agrega diferentes 'super poderes' a nuestras hojas de estilo, pudiendo agregar funcionalidades que tienen otros lenguajes como pueden ser los condicionales y las variables.

## Instalación

Hay varias maneras de comenzar a utilizar Sass, pero la forma más fácil con Visual Studio Code es instalar la extensión de [Live Sass Compiler](https://marketplace.visualstudio.com/items?itemName=glenn2223.live-sass), la cual compila automáticamente todo el código escrito en Sass automáticamente a código CSS, unicamente haciendo click en el icono que se nos habilita.
Esta forma sirve cuando vamos a utilizar la compilación de Sass, pero al utilizar un framework como React podemos instalar Sass con su comando de la siguiente manera.

```cmd
npm i sass
```

Unicamente con esto podemos crear nuestros archivos de Sass sin tener que compilarlos, ya que lo podrá detectar de la misma manera.

## Utilización

Luego de la instalación podemos empezar a crear nuestro archivo de Sass, para ello se puede utilizar dos tipos de extensiones, `.scss` o `.sass`, ambos se basan en el estilo de `.css`, cambiando la sintaxis que se tiene que utilizar en los mismos.

> `.scss`, el más utilizado actualmente dado su parecido con CSS clásico

```scss
body{
    background-color: #1e1e1e;
    color: white
}
```

> `.sass`, el que más difiere del CSS clásico, igualmente aceptado

```sass
body
    background: #1e1e1e
    color: white
```

Cuando escribamos nuestro código y lo compilemos podremos ver que automáticamente nuestra extensión nos devolverá un archivo `.css`, este archivo CSS será nuestro archivo de estilos que utilizaremos para linkear a nuestro archivo principal.

> Al crear nuestro código con un framework NO ES NECESARIO la compilación de Sass, simplemente linkeamos el archivo `.scss` como lo haríamos con nuestro archivo de estilos normalmente

## Variables

Aunque las variables existen en CSS puro, Sass las agrega de una forma un poco más directa, para el uso de las mismas se puede ver una comparación en la forma que se escriben pero particularmente en la forma en la que se llaman, sin la necesidad de utilizar `var()` para las mismas, quedando de la siguiente manera

```scss

$bg-color: #1e1e1e;
$primary-color: #8132a8;
$secondary-color: #325fa8;
$font: #fefefe;

body {
    background-color: $bg-color;
}
```

A diferencia de CSS puro, el cual quedaría de la siguiente manera.

```css
:root {
    --bg-color: #1e1e1e;
    --primary-color: #8132a8;
    --secondary-color: #325fa8;
    --font: #fefefe;
}
    
body {
    background-color: var(--bg-color);
}
```

## Nesting

Uno de los 'poderes' que agrega Sass a nuestros estilos es la posibilidad de hacer un nesting con las propiedades del código sin necesidad de tener que escribir todo el indicador en una sola linea, agregando una mejor legibilidad y comprensión.

> `css`

```css
header {
    width: 100%;
    height: 30%;
}

header nav {
    background-color: var(--bg-color);
}

header nav ul {
    background-color: var(--primary-color);
    color: var(--font);
}

header nav ul:hover {
    background-color: var(--secondary-color);
}
```

> `.scss`

```scss
header {
    width: 100%;
    height: 30%;
        
    nav {
        background-color: $bg-color;

        ul {
            background-color: $primary-color;
            color: $font;

            &:hover {
                background-color: $secondary-color;
            }
        }
    }
}
```

Como podemos ver, el nesting nos ayuda mucho a la hora de visualizar mucho mejor como están organizados los padres e hijos de los elementos en cuestión, además de poder agregar los modificadores como el hover directamente en el mismo nivel.

## Módulos

Sass nos permite separar nuestro código en módulos para tener un mejor orden del mismo, para ello será necesario crear un archivo que comience con un `_` y luego el nombre del archivo en cuestión, como podría ser `_header.scss`, en el que pondremos todo el código que utilizaremos para modificar el header, y en nuestro archivo principal de Sass lo llamaremos con `@use` de la siguiente manera

```scss
@use 'header';

body {
    background-color: $bg-color;
}
```

> SIEMPRE se debe agregar un `_` al inicio del archivo, para que el compilador no lo tome como un archivo separado

## Mixins

Los mixins son porciones de código que se reutilizaran en otro lugar, siendo este similar a lo que pasa con las funciones, ademas de tener una sintaxis similar. También es posible pasar parámetros o tener parámetros base como tienen las funciones.  
Para usar las mismas será necesario utilizar `@mixin` y luego declarar la porción de código en cuestión de la siguiente manera.

```scss
@mixin mainBgImg($link, $size: cover){
    background-image: url($link);
    background-position: center;
    background-size: $size;
    background-repeat: no-repeat;
}

@include mainBgImg("https://i.kym-cdn.com/photos/images/newsfeed/001/584/180/0c2.jpg")
```

Como podemos ver, para llamarlo luego debemos pasar los parámetros necesarios, pero los que tienen un valor declarado se pueden ignorar.
