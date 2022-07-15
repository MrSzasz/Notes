# NOTAS

¡Hola! Bienvenidos a mis notas, en esta voy a dejar por escrito todo mi camino hacia ser Full-Stack Developer.

Principalmente desarrollaré el README, el cual se encarga de dar una introducción al documento, el mismo esta escrito en el lenguaje MarkDown, el cual es un lenguaje de marcado.

El mismo se comienza creando un archivo con la extension .md (Normalmente README.md), el cual luego se utiliza con sus propio tipado para darle un estilo particular, siendo estos los siguientes:
<br>

### = Headings =

Los textos de heading se escriben con #, denotando la importancia del mismo en relación a la cantidad de # que posea adelante, siendo # el de mayor tamaño e importancia y ##### el de menor tamaño e importancia visual.

> Las lineas de markdown deben tener una separación de una linea entre headings

> Es posible agregar IDs a los headings agregando el id deseado entre {} y empezando con un #.

CODIGO:

```md

    # Heading {#title}
 
    ## SubHeading

```

<br>

SALIDA:

<h1 id="title"> Heading </h1>
  
<h2> SubHeading </h2>


<br><br>

### Breaks

Los saltos entre lineas se realizan con la etiqueta `<br>` , la cual agrega una linea vacia entre el elemento en cuestion y el siguiente.

CODIGO: 


```html

    Hola este <br> es el ejemplo.

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Hola este <br> &nbsp;&nbsp;&nbsp;&nbsp;es el ejemplo.

<br><br>

### Estilos

Hay diferentes estilos de texto que se pueden aplicar para darle un enfasis a las palabras importantes como pueden ser el texto **en negrita**, *en cursiva* y ~~tachado~~.

CODIGO:

```

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

CODIGO:

```md

    > Esto es un bloque de texto

```

<br>

SALIDA:

> Esto es un bloque de texto

<br>

### Listas

Es posible agregar dos tipos de listas a los markdowns, las listas ordenadas (enumeradas) y las desordenadas (sin numeros).
Las listas ordenadas tienen que respetar el orden sintactico en el que se escribio.

CODIGO:

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

CODIGO:

```md

    - MarkDown 
    - List 

```

<br>

SALIDA:

- MarkDown
- List


<br>

Es posible agregar listas de tareas a la misma, con marcas en las que esten completadas

CODIGO:

```

- [x] Hecho
- [ ] Por hacer

```

<br>

SALIDA:

- [x] Hecho
- [ ] Por hacer

<br><br>

### Bloques de codigo

Son utilizados para denotar bloques especiales de codigo, los mismos se marcan al iniciar una linea con ``` TAB ``` o con 4 espacios para darle diseño, y entre ``` para mostrar unicamente el codigo en linea.


> El codigo entre backsticks puede tener un formato, escribiendose luego de los primeros 3 (`) 

CODIGO:

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

### Imagenes y links

Es posible agregar imagenes o links externos al documento, citandolos o llamando a un archivo en la carpeta.

> Los links pueden ser agregados sin texto dentro de `<https://github.com/>`, ademas de poder contener IDs para la navegacion, citandolos con #.

CODIGO:

```

    ![petit](link)
    
    Documentacion oficial de [MarkDown](link)

```

<br>

SALIDA:

![petit](https://i.imgur.com/jPc865A.jpg)

Documentacion oficial de [Markdown](https://www.markdownguide.org/getting-started/) 

<br><br>

### Division de textos

Se puede separar/dividir textos con una linea horizontal, marcandolos con `---`, `***` o `___` quedando un ejemplo como el siguiente.

> Al igual que los Headings, debe haber una linea vacia antes y despues de las lineas divisoras.

---

<br><br>

### Tablas

Las tablas se pueden utilizar para marcar el contenido del texto en una forma ordenada visualmente, creando filas y columnas en las mismas

CODIGO:

```

    | Syntax      | Ejemplo     |
    | ----------- | ----------- |
    | Codigo      | Ejemplo     |

```

<br>

SALIDA:

| Syntax      | Ejemplo     |
| ----------- | ----------- |
| Codigo      | Ejemplo     |

> Se puede cambiar la posicion del texto con `:---` para iniciar en la izquierda, `:---:` para centrar el texto y `---:` para iniciar a la derecha, todos en la 2da linea de la tabla.

<br><br>

### Referencias

Se pueden agregar referencias con un numero sobre el texto para ir a cierto punto del texto.

CODIGO:

```

    Este es mi texto, y este[^1] mi referencia.
    [^1]: Automaticamente te dirige aca

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Este es mi texto, y este[^1] mi referencia.

&nbsp;&nbsp;&nbsp;&nbsp;[^1]: Automaticamente te dirige aca, aunque no se note por la cercania

<br><br>

### Definiciones

Es posible agregar definiciones, marcando el nombre del mismo visualmente.

CODIGO:

```

    Nombre
     : Definicion del mismo

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Nombre
&nbsp;&nbsp;&nbsp;&nbsp; : Definicion

 <br><br>

### Palabras destacadas

Se pueden destacar palabras para remarcar visualmente su importancia

CODIGO:

```

    Estas palabras ==son muy importantes==

```
<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Estas palabras ==son muy importantes==

<br><br>

### Posicion numeral

Es posible agregar numeros por sobre o debajo de la altura normal del texto

CODIGO:

```

    El numero UNO^1^ es superior al numero DOS~2~

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;El numero UNO^1^ es superior al numero DOS~2~

<br><br>

### HTML

Es posible agregar codigo HTML para agregar elementos propios de este lenguaje, tambien asi agregar estilos a los mismos

CODIGO:

```

    <em> Hola en cursiva y en <span style="color:purple">VIOLETA</span> </em>

```

<br>

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;<em>Hola en cursiva y en <span style="color:purple">VIOLETA</span></em> 

<br><br>

Estas son las bases de MarkDown, tiene sus limitaciones como todo lenguaje, pero aun asi con el agregado del HTML es posible crear desde un simple README hasta un libro completo, ¡unicamente limitado por la creatividad del editor!


## LINKS IMPORTANTES

> [Dilinger](https://dillinger.io/), editor de markdown online, con previsualizacion automarica.<br>
> [MarkDownGuide](https://www.markdownguide.org/), guia sobre todo lo basico de markdown, desde la sintaxis hasta ciertas herramientas.<br>
> [Guia de emojis en GitHub](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md), con tablas de emojis y su equivalente en codigo.<br>
> [Buscador de emojis](https://emojipedia.org/), enciclopedia de emojis con servicio de busqueda.
