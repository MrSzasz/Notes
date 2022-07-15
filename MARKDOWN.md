# MARKDOWN

Markdown es un lenguaje de marcado utilizado para escribir textos con un formato visible y adaptado para varias webs, el mismo tiene su propia sintaxis y reglas como todo lenguaje.

El mismo se comienza creando un archivo con la extension .md, y contiene ciertos elementos para otorgarle diseño y funcionalidades, siendo estos los siguientes:

<br>

## = Headings =

Los textos de heading se escriben con #, denotando la importancia del mismo en relación a la cantidad de # que posea adelante, siendo # el de mayor tamaño e importancia y ##### el de menor tamaño e importancia visual.

> Las lineas de markdown deben tener una separación de una linea entre headings
>
> Es posible agregar IDs a los headings agregando el id deseado entre {} y empezando con un #.

CÓDIGO:

```md

    # Heading {#title}
 
    ## SubHeading

```

<br>

SALIDA:

<h1 id="title"> Heading </h1>
  
<h2> SubHeading </h2>

<br><br>

## Breaks

Los saltos entre lineas se realizan con la etiqueta `<br>` , la cual agrega una linea vacía entre el elemento en cuestión y el siguiente.

CÓDIGO:

```html

    Hola este <br> es el ejemplo.

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Hola este <br> &nbsp;&nbsp;&nbsp;&nbsp;es el ejemplo.

<br><br>

### Estilos

Hay diferentes estilos de texto que se pueden aplicar para darle un énfasis a las palabras importantes como pueden ser el texto **en negrita**, *en cursiva* y ~~tachado~~.

CÓDIGO:

```md

    ** texto en negrita **
    * texto en cursiva *
    *** texto en cursiva y negrita ***
    ~~ texto tachado ~~

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;**texto en negrita**<br>
&nbsp;&nbsp;&nbsp;&nbsp;*texto en cursiva*<br>
&nbsp;&nbsp;&nbsp;&nbsp;***texto en cursiva y negrita***<br>
&nbsp;&nbsp;&nbsp;&nbsp;~~texto tachado~~<br>

<br><br>

### Bloques

Se pueden agregar bloques de texto para citar una fuente o agregar un elemento con un formato diferente.

CÓDIGO:

```md

    > Esto es un bloque de texto

```

<br>

SALIDA:

> Esto es un bloque de texto

<br>

### Listas

Es posible agregar dos tipos de listas a los markdowns, las listas ordenadas (enumeradas) y las desordenadas (sin números).
Las listas ordenadas tienen que respetar el orden sintáctico en el que se escribió.

CÓDIGO:

```md

    1. primero
    2. segundo

```

<br>

SALIDA:

1. primero
2. segundo

<br>

En cambio las listas desordenadas pueden tener diferentes puntos, independientemente de que sean consecutivos.

> Es posible usar ``` + * - ``` para marcar los bullets, pero no pueden mezclarse

CÓDIGO:

```md

    - MarkDown 
    - List 

```

<br>

SALIDA:

- MarkDown
- List


<br>

Es posible agregar listas de tareas a la misma, con marcas en las que estén completadas

CÓDIGO:

```md

- [x] Hecho
- [ ] Por hacer

```

<br>

SALIDA:

- [x] Hecho
- [ ] Por hacer

<br><br>

### Bloques de CÓDIGO

Son utilizados para denotar bloques especiales de CÓDIGO, los mismos se marcan al iniciar una linea con ``` TAB ``` o con 4 espacios para darle diseño, y entre ``` para mostrar unicamente el CÓDIGO en linea.

> El CÓDIGO entre backticks puede tener un formato, escribiéndose luego de los primeros 3 (`)

CÓDIGO:

```json
    {
        "lenguaje":"markdown",
        "archivo":"readme.md"
    }
```

<br>

SALIDA:

```json
{
    "lenguaje" : "markdown",
    "archivo" : "readme.md"
}
```

<br><br>

### Imágenes y links

Es posible agregar imágenes o links externos al documento, citándolos o llamando a un archivo en la carpeta.

> Los links pueden ser agregados sin texto dentro de `<https://github.com/>`, ademas de poder contener IDs para la navegación, citándolos con #.

CÓDIGO:

```md

    ![petit](link)
    
    Documentación oficial de [MarkDown](link)

```

<br>

SALIDA:

![petit](https://i.imgur.com/jPc865A.jpg)

Documentación oficial de [Markdown](https://www.markdownguide.org/getting-started/)

<br><br>

### Division de textos

Se puede separar/dividir textos con una linea horizontal, marcándolos con `---`, `***` o `___` quedando un ejemplo como el siguiente.

> Al igual que los Headings, debe haber una linea vacía antes y después de las lineas divisoras.

---

<br><br>

### Tablas

Las tablas se pueden utilizar para marcar el contenido del texto en una forma ordenada visualmente, creando filas y columnas en las mismas

CÓDIGO:

```md

    | Syntax      | Ejemplo     |
    | ----------- | ----------- |
    | CÓDIGO      | Ejemplo     |

```

<br>

SALIDA:

| Syntax      | Ejemplo     |
| ----------- | ----------- |
| CÓDIGO      | Ejemplo     |

> Se puede cambiar la posición del texto con `:---` para iniciar en la izquierda, `:---:` para centrar el texto y `---:` para iniciar a la derecha, todos en la 2da linea de la tabla.

<br><br>

### Referencias

Se pueden agregar referencias con un numero sobre el texto para ir a cierto punto del texto.

CÓDIGO:

```md

    Este es mi texto, y este[^1] mi referencia.
    [^1]: Automáticamente te dirige aca

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Este es mi texto, y este[^1] mi referencia.

&nbsp;&nbsp;&nbsp;&nbsp;[^1]: Automáticamente te dirige aca, aunque no se note por la cercanía

<br><br>

### Definiciones

Es posible agregar definiciones, marcando el nombre del mismo visualmente.

CÓDIGO:

```md

    Nombre
     : Definición del mismo

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Nombre
&nbsp;&nbsp;&nbsp;&nbsp; : Definición

 <br><br>

### Palabras destacadas

Se pueden destacar palabras para remarcar visualmente su importancia

CÓDIGO:

```md

    Estas palabras ==son muy importantes==

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Estas palabras ==son muy importantes==

<br><br>

### Posición numeral

Es posible agregar números por sobre o debajo de la altura normal del texto

CÓDIGO:

```md

    El numero UNO^1^ es superior al numero DOS~2~

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;El numero UNO^1^ es superior al numero DOS~2~

<br><br>

### HTML

Es posible agregar CÓDIGO HTML para agregar elementos propios de este lenguaje, también asi agregar estilos a los mismos

CÓDIGO:

```html

    <em> Hola en cursiva y en <span style="color:purple">VIOLETA</span> </em>

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;<em>Hola en cursiva y en <span style="color:purple">VIOLETA</span></em>

<br><br>

Estas son las bases de MarkDown, tiene sus limitaciones como todo lenguaje, pero aun asi con el agregado del HTML es posible crear desde un simple README hasta un libro completo, ¡unicamente limitado por la creatividad del editor!

## LINKS IMPORTANTES

> [Dillinger](https://dillinger.io/), editor de markdown online, con previsualización automática.<br>
> [MarkDownGuide](https://www.markdownguide.org/), guía sobre todo lo básico de markdown, desde la sintaxis hasta ciertas herramientas.<br>
> [Guía de emojis en GitHub](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md), con tablas de emojis y su equivalente en CÓDIGO.<br>
> [Buscador de emojis](https://emojipedia.org/), enciclopedia de emojis con servicio de búsqueda.
