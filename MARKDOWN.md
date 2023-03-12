# MARKDOWN

Markdown es un lenguaje de marcado utilizado para escribir textos con un formato visible y adaptado para varias webs, el mismo tiene su propia sintaxis y reglas como todo lenguaje. Los archivos de Markdown utilizan la extension `.md`.

## Guía de Temas

- [Títulos](#headings)
- [Line Breaks](#breaks)
- [Styling](#estilos)
- [Bloques](#bloques)
- [Listas](#listas)
- [Código](#bloques-de-código)
- [Multimedia](#imágenes-y-links)
- [Lineas divisoras](#division-de-textos)
- [Tablas](#tablas)
- [Referencias](#referencias)
- [Definiciones](#definiciones)
- [Destacados](#palabras-destacadas)
- [Numeración](#posición-numeral)
- [HTML](#html)
- [Referencias](#links-importantes)

---

## Headings

Los textos de heading se escriben con #, denotando la importancia del mismo en relación a la cantidad de # que posea adelante, siendo # el de mayor tamaño e importancia y ##### el de menor tamaño e importancia visual.

> Las lineas de markdown deben tener una separación de una linea entre headings
>
> Es posible agregar IDs a los headings agregando el id deseado entre {} y empezando con un #.

CÓDIGO:

```md
# Heading {#title}
 
## SubHeading
```

SALIDA:

<h1 id="title"> Heading </h1>
  
<h2> SubHeading </h2>

---

## Breaks

Los saltos entre lineas se realizan con la etiqueta `<br>` , la cual agrega una linea vacía entre el elemento en cuestión y el siguiente.

CÓDIGO:

```html
Hola este <br> es el ejemplo.
```

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Hola este <br> &nbsp;&nbsp;&nbsp;&nbsp;es el ejemplo.

> También es posible agregar dos espacios al final de una linea para hacer el salto

---

## Estilos

Hay diferentes estilos de texto que se pueden aplicar para darle un énfasis a las palabras importantes como pueden ser el texto **en negrita**, *en cursiva* y ~~tachado~~.

CÓDIGO:

```md
** texto en negrita **
* texto en cursiva *
*** texto en cursiva y negrita ***
~~ texto tachado ~~
```

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;**texto en negrita**<br>
&nbsp;&nbsp;&nbsp;&nbsp;*texto en cursiva*<br>
&nbsp;&nbsp;&nbsp;&nbsp;***texto en cursiva y negrita***<br>
&nbsp;&nbsp;&nbsp;&nbsp;~~texto tachado~~<br>

---

## Bloques

Se pueden agregar bloques de texto para citar una fuente o agregar un elemento con un formato diferente.

CÓDIGO:

```md
> Esto es un bloque de texto
```

SALIDA:

> Esto es un bloque de texto

## Listas

Es posible agregar dos tipos de listas a los markdowns, las listas ordenadas (enumeradas) y las desordenadas (sin números).
Las listas ordenadas tienen que respetar el orden sintáctico en el que se escribió.

CÓDIGO:

```md
1. primero
2. segundo
```

SALIDA:

1. primero
2. segundo

En cambio las listas desordenadas pueden tener diferentes puntos, independientemente de que sean consecutivos.

> Es posible usar ``` + * - ``` para marcar los bullets, pero no pueden mezclarse

CÓDIGO:

```md
- MarkDown 
- List 
```

SALIDA:

- MarkDown
- List

Es posible agregar listas de tareas a la misma, con marcas en las que estén completadas

CÓDIGO:

```md
- [x] Hecho
- [ ] Por hacer
```

SALIDA:

- [x] Hecho
- [ ] Por hacer

---

## Bloques de CÓDIGO

Son utilizados para denotar bloques especiales de CÓDIGO, los mismos se marcan al iniciar una linea con ``` TAB ``` o con 4 espacios para darle diseño, y entre ``` para mostrar unicamente el CÓDIGO en linea.

> El CÓDIGO entre backticks puede tener un formato, escribiéndose luego de los primeros 3 (`)

CÓDIGO:

```json
{
    "lenguaje":"markdown",
    "archivo":"readme.md"
}
```

SALIDA:

```json
{
    "lenguaje" : "markdown",
    "archivo" : "readme.md"
}
```

---

## Imágenes y links

Es posible agregar imágenes o links externos al documento, citándolos o llamando a un archivo en la carpeta.

> Los links pueden ser agregados sin texto dentro de `<https://github.com/>`, ademas de poder contener IDs para la navegación, citándolos con #.

CÓDIGO:

```md
![petit](link)

Documentación oficial de [MarkDown](link)
```

SALIDA:

![petit](https://i.imgur.com/jPc865A.jpg)

Documentación oficial de [Markdown](https://www.markdownguide.org/getting-started/)

---

## Division de textos

Se puede separar/dividir textos con una linea horizontal, marcándolos con `---`, `***` o `___` quedando un ejemplo como el siguiente.

> Al igual que los Headings, debe haber una linea vacía antes y después de las lineas divisoras.

---

---

## Tablas

Las tablas se pueden utilizar para marcar el contenido del texto en una forma ordenada visualmente, creando filas y columnas en las mismas

CÓDIGO:

```md
| Syntax      | Ejemplo     |
| ----------- | ----------- |
| CÓDIGO      | Ejemplo     |
```

SALIDA:

| Syntax      | Ejemplo     |
| ----------- | ----------- |
| CÓDIGO      | Ejemplo     |

> Se puede cambiar la posición del texto con `:---` para iniciar en la izquierda, `:---:` para centrar el texto y `---:` para iniciar a la derecha, todos en la 2da linea de la tabla.

---

## Referencias

Se pueden agregar referencias con un numero sobre el texto para ir a cierto punto del texto.

CÓDIGO:

```md
Este es mi texto, y este[^1] mi referencia.
[^1]: Automáticamente te dirige aca
```

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Este es mi texto, y este[^1] mi referencia.

&nbsp;&nbsp;&nbsp;&nbsp;[^1]: Automáticamente te dirige aca, aunque no se note por la cercanía

---

## Definiciones

Es posible agregar definiciones, marcando el nombre del mismo visualmente.

CÓDIGO:

```md
Nombre
 : Definición del mismo
```

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Nombre
&nbsp;&nbsp;&nbsp;&nbsp; : Definición

 ---

## Palabras destacadas

Se pueden destacar palabras para remarcar visualmente su importancia

CÓDIGO:

```md
Estas palabras ==son muy importantes==
```

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;Estas palabras ==son muy importantes==

---

## Posición numeral

Es posible agregar números por sobre o debajo de la altura normal del texto

CÓDIGO:

```md
El numero UNO^1^ es superior al numero DOS~2~
```

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;El numero UNO^1^ es superior al numero DOS~2~

---

## HTML

Es posible agregar CÓDIGO HTML para agregar elementos propios de este lenguaje, también asi agregar estilos a los mismos

CÓDIGO:

```html
<em> Hola en cursiva y en <span style="color:purple">VIOLETA</span> </em>
```

SALIDA:

&nbsp;&nbsp;&nbsp;&nbsp;<em>Hola en cursiva y en <span style="color:purple">VIOLETA</span></em>

---

Estas son las bases de MarkDown, tiene sus limitaciones como todo lenguaje, pero aun asi con el agregado del HTML es posible crear desde un simple README hasta un libro completo, ¡unicamente limitado por la creatividad del editor!

## LINKS IMPORTANTES

- [Dillinger](https://dillinger.io/), editor de markdown online, con previsualización automática.
- [MarkDownGuide](https://www.markdownguide.org/), guía sobre todo lo básico de markdown, desde la sintaxis hasta ciertas herramientas.
- [Guía de emojis en GitHub](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md), con tablas de emojis y su equivalente en CÓDIGO.
- [Buscador de emojis](https://emojipedia.org/), enciclopedia de emojis con servicio de búsqueda.
