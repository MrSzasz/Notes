# Python

[Python](https://www.python.org/) es un lenguaje de programación ampliamente utilizado para diferentes motivos, desde la creación de programas de automatización, machine learning, desarrollo de software, ciencia de datos, entre otros. Python es un lenguaje de fácil aprendizaje y adaptación, por lo que esto lo convierte en uno de los lenguajes preferidos para aprender, además de contar con una buena demanda en el ámbito laboral.

## Guía de Temas

1. [Instalación](#instalaci%C3%B3n)
2. [Código](#coding)

---

## Instalación

Para iniciar con Python se deberá descargar el mismo desde su [página web](https://www.python.org/downloads/) y luego instalarlo, dependiendo del sistema operativo que se seleccione. Sumado a esto será necesario tener instalado un IDE, y lo mejor será tener los plugins instalados para que sea mucho mas fácil trabajar con el código de Python.

## Coding

Lo primero que se deberá hacer para crear código de Python es crear un archivo con la extensión `.py`, y el mismo deberemos abrirlo en el editor de código que utilizaremos.  
Para empezar crearemos el archivo llamado `main.py`, en el cual crearemos todo el código del mismo.

### Imprimir

Empezaremos por lo básico, mostrar/imprimir un 'Hello World', esto se realiza con el comando `print()`, el cual muestra en consola lo que se le pase al mismo, en este caso quedaría de la siguiente manera.

```py
# Imprimir "Hello World"

print("Hello World")
```

> Se puede comentar con `# una linea` o con `""" un bloque """`

Hecho esto podemos darle play al código (en VSC el botón se encuentra en la esquina superior derecha si se instala la extensión correspondiente)

### Tipos de datos

En Python existen diferentes tipos de datos que también podemos imprimir, los mismos se comportan de diferentes maneras, por ejemplo, si queremos sumar `a + b` el resultado será `ab`, en cambio si queremos sumar `1 + 2` el resultado será `3`, dado que el primero es un tipo `String (cadena de texto)`, y el segundo un tipo `Int (numero)`. Podemos ver el tipo de dato que es usando el método `type` de la siguiente manera.

```py
# Tipos de datos

print("Tipos de datos")
print(type("Tipos de datos")) # Tipo String (str)

print(127)
print(type(127)) # Tipo Integer/Numero (int)

print(1.99)
print(type(1.99)) # Tipo Float (float)

print(True)
print(type(True)) # Tipo Booleano (bool)
```

También es posible cambiar el tipo de dato, por ejemplo, si queremos que el dato `127` se imprima como una cadena de texto (string) podemos utilizar el método `str()`, el cual recibe un parámetro y lo devuelve como un string, de la siguiente manera.

```py
print(type(127)) # Imprime Int

print(type(str(127))) # Imprime String, ya que lo cambiamos con "str()"
```

Esto nos servirá mas adelante, ya que no dará el mismo resultado imprimir `"1" + "1"` (resultado = "11") a imprimir `1 + 1` (resultado = 2)

### Variables

Como vimos anteriormente podemos imprimir datos escribiéndolos directamente, pero la practica normal de esto es guardarlas en `variables` y estas imprimirlas en pantallas. Las variables se encargan de guardar datos con un nombre en particular, y el dato que se guarda puede cambiar. Para explicar mejor esto crearemos dos variables, la variable `message` que contendrá el mensaje que queremos imprimir en consola, y la variable `my_name`, que contendrá un nombre.

```py
message = "Hello World"

print(message) # Imprime el valor de message

my_name = "Heisenberg"

print(my_name) # Imprime el valor de my_name
```

> Las variables en Python se escriben en minúscula y en `snake_case` (palabras separadas con _), siendo esta la forma estandarizada del mismo.

Como dijimos anteriormente, el valor de una variable puede cambiarse, para ver esto primero imprimiremos el valor de `message`, luego lo cambiaremos y volvemos a imprimirlo.

```py
message = "Hello World"

print(message) # Imprime el primer valor de message

message = "Goodbye world"

print(message) # Imprime el valor cambiado de message
```

El código se ejecuta en orden descendiente, por lo que primero se imprime el valor original de la variable, luego se cambia y al final se imprime el valor por el que se cambió.  
También podemos concatenar diferentes variables para imprimir o crear una variable con la suma de las mismas de la siguiente manera.

```py
message = "Hello from the"

second_message = "console output"

print(message, second_message) # Imprime ambos con un espacio en medio

concat_message = message + second_message

print(concat_message) # Al sumarlos sin tener espacio, imprime todo junto

print("Hello! This is the", second_message) # Junta el string que escribimos con el valor de la variable

first_number = 4

second_number = 2

print(first_number, second_number) # Imprime 4 2, ya que imprime ambos

print(second_number + first_number) # Imprime 6, ya que los suma
```

### Input

En Python también tenemos la posibilidad de escribir datos a medida que se nos pida por consola, esta forma de insertar los datos se utiliza mayormente en pruebas, ya que no es el mejor acercamiento si queremos hacerlo para un usuario final, pero nos sirve para hacer pruebas con diferentes valores en el momento. Para ello usaremos el método `input()` de la siguiente manera.

```py
# Input directo

name = input("Ingresa tu nombre") # Te pide el dato
print(name) # Imprime el dato que le hayamos pasado
```

> También es posible pedir el dato directamente, sin guardarlo en un variable, pasando el input dentro del print.

### Operadores

Como vimos anteriormente, es posible sumar datos, ya sean sumar números o concatenar strings, pero la suma no es la única operación que podemos hacer, hay diferentes operaciones que podemos realizar, como por ejemplo las siguientes.

```py
# Operadores

print(1 + 1) # Suma

print(1 - 1) # Resta

print(2 * 2) # Multiplicación

print(4 / 2) # División

print(5 % 2) # Resto de una división

print(5 // 2) # División redondeada

print(5 ** 2) # Potencia

print(1 + 2 - 3 * 4) # Varias operaciones juntas

print("Hola" + 5) # Error porque son dos tipos diferentes que no se pueden sumar

print("Hola" * 5) # Imprime 5 veces "Hola", siempre que sea un Int y no un Float

print("Hola numero" + str(5)) # Imprime "Hola numero5" ya que los concatena como dos string
```

### Comparadores

Una operación importante que usaremos mucho en nuestro código es la comparación de dos o mas valores, para esto usaremos diferentes operadores, los cuales como resultado nos darán un Bool, de la siguiente manera.

```py
# Comparadores de números

print(1 > 2) # Mayor que

print(1 < 2) # Menor que

print(1 <= 2) # Menor o igual que

print(2 >= 2) # Mayor o igual que 

print(1 == 2) # Iguales

print(1 != 2) # Diferentes


# Comparadores de strings

print("Hola" == "Hola")  # Compara si los strings son iguales

print("Hola" == "Mundo") # Al ser diferente cuenta como False


# Comparadores lógicos

print(3 > 4 and "Hola" == "Adios") # Comprueba que dos (o más) comparaciones sean verdaderas (todas tienen que ser verdaderas)

print(4 > 3 and "Hola" == "Hola") 

print(4 > 3 or "Hola" == "Adios") # Comprueba que mínimo una comparación sea verdadera

print(3 > 4 or "Hola" == "Adios")

print(3 == 3)

print(not(3 == 3)) # Invierte el valor del Boolean, por lo que en este caso queda False
```

### Formateo de datos

Los datos que necesitemos imprimir en consola se pueden formatear cuando se van a utilizar, para ello tenemos varias formas de hacerlo, ya sea utilizando `%` dependiendo del tipo de dato que se necesite, o directamente utilizando `f" "` y pasando las variables dentro de las mismas de la siguiente manera.

```py
# Formateo de variables

name = "Walter Hartwell White"
address_number = 308
address_street = "Negra Arroyo Lane"

print("My name is %s. I live at %d %s, Albuquerque, New Mexico, 87104" % (name, address_number, address_street))

print(f"My name is {name}. I live at {address_number} {address_street}, Albuquerque, New Mexico, 87104")
```

Como podemos ver, en el primer print indicamos que el primer valor (`%s`) es un string, y el 2do (`%d`) es un numero, al final indicamos las variables que se utilizarán en cada espacio en particular.  
En el 2do print vemos como imprimimos el string literal (`f" "`), pasando las variables dentro de los `{}`.

### Slice de strings

Un string tiene una longitud que depende de cuantos caracteres contenga, los mismos se pueden "cortar" para mostrar solamente algunos de estos. Para esto usamos el signo `:`, indicando primero de donde empezará y donde terminará (sin incluir este ultimo), y por ultimo podemos pasarle cuantos saltos hará, de la siguiente manera.

```py
# Slice de strings

my_name = "Heisenberg"

print(my_name[1:2]) # Toma solamente el 2do carácter

print(my_name[1:4]) # Toma desde el 2do carácter hasta el 3ro

print(my_name[2:4]) # Toma el 3er carácter

print(my_name[5:]) # Toma desde el 6to carácter hasta el final

print(my_name[-1]) # Toma solamente el ultimo carácter

print(my_name[-4:]) # Toma desde el 4to carácter (empezando por el ultimo) hasta el final

print(my_name[-4]) # Toma el 4to carácter empezando por el ultimo

print(my_name[0:-1:2]) # Toma los caracteres con saltos de 2

```

> Los espacios (indices) en los lenguajes de programación comienzan desde el 0, en este caso "H" = indice 0, "e" = indice 1, etc.

### Modificadores de strings

Otra cosa que viene con el lenguaje son las funciones que modifican los strings, los cuales pueden ir desde pasarlos a lower case hasta comprobar si el mismo contiene cierto carácter. Probaremos algunos de los mismos de la siguiente manera.

```py
# Modificadores de strings

my_name = "Heisenberg"

print(my_name.capitalize()) # Convierte la primer letra en mayúscula

print(my_name.lower()) # Convierte todo en minúscula

print(my_name.upper()) # Convierte todo en mayúscula

print(my_name.isnumeric()) # Comprueba si es un numero

print(my_name.isupper()) # Comprueba si esta en mayúscula

print(my_name.count("e")) # Cuenta cuantas e tiene el string

print(my_name.count("z")) # Devuelve 0

print(my_name.upper().isupper()) # Se pueden crear cadenas, las cuales se toman en orden (True)
```

## Listas

Las listas son un tipo de dato que se comporta como una "caja" que contiene otros datos (similares a los arrays en JavaScript). Estos pueden contener diferentes tipos de datos, ya sean strings, números, booleans, etc. Para crear una lista tenemos diferentes maneras, se puede utilizar `list()` y pasarle los datos de la lista como parámetro, o directamente crear la lista con `[]`, de la siguiente manera.

```py
# Listas

my_list = list(["Heisenberg", "Walter White", 14, True, 15.5, 14])

my_new_list = ["Heisenberg", "Walter White", 14, True, 15.5, 14]

print(my_list)

print(my_new_list)
```

De ambas formas creamos las mismas listas, y el print es el mismo en ambas.  
Podemos acceder a las listas utilizando `[]` e indicando el indice (lugar que tiene en la lista) del dato que queremos acceder dentro del mismo

```py
my_new_list = ["Heisenberg", "Walter White", 14, True, 15.5, 14]

print(my_new_list[0]) # Accedemos al primer elemento de la lista

print(my_new_list[3]) # Accedemos al 4to elemento de la lista

print(my_new_list[-1]) # Accedemos al ultimo elemento de la lista

print(my_new_list[-3]) # Cuenta 3 elementos desde el ultimo

print(my_new_list[0:2]) # Empieza por el primero hasta el 2do elemento de la lista

print(my_new_list[1:]) # Empieza por el 2do hasta el final de la lista

print(len(my_new_list)) # Indica la longitud de la lista

print(my_new_list.count(14)) # Cuenta cuantos elementos coinciden con el parámetro que pasamos (2)

print(my_new_list.count("Jesse")) # Y en este caso indica 0 ya que no se encuentra en la lista

print(my_list + my_new_list) # Combina ambas listas en una sola
```

También tenemos la posibilidad de modificar una lista, ya sea agregando o quitando datos de la misma, reordenar entre otras cosas, para ello haremos uso de los métodos de la misma de la siguiente manera.

```py
# Listas

my_list = ["Heisenberg", "Walter White", 14, True, 15.5, 14]

my_list.append("Jess") # Agrega un nuevo elemento al final de la lista

print(my_list) ## ['Heisenberg', 'Walter White', 14, True, 15.5, 14, 'Jess']

my_list[6] = "Jesse" # Cambiamos el elemento de la lista que indicamos

print(my_list) ## ['Heisenberg', 'Walter White', 14, True, 15.5, 14, 'Jesse']

my_list.insert(2, "New Mexico") # Agregamos el dato en el indice que indicamos

print(my_list) ## ['Heisenberg', 'Walter White', 'New Mexico', 14, True, 15.5, 14, 'Jesse']

my_list.remove(True) # Eliminamos el elemento que coincida con el dato

print(my_list) ## ['Heisenberg', 'Walter White', 'New Mexico', 14, 15.5, 14, 'Jesse']

del my_list[3] # Elimina el elemento con el indice que indicamos

print(my_list) ## ['Heisenberg', 'Walter White', 'New Mexico', 15.5, 14, 'Jesse']

my_list.pop(4) # Al igual que "del", elimina el elemento con el indice que indicamos, pero también lo devuelve

print(my_list) ## ['Heisenberg', 'Walter White', 'New Mexico', 15.5, 'Jesse']

print(my_list.pop()) ## Jesse

print(my_list.index("New Mexico")) # Devuelve el indice del elemento con el valor que pasamos (2)

my_list.reverse() # Invierte el orden de la lista

print(my_list) ## [15.5, 'New Mexico', 'Walter White', 'Heisenberg']

my_list.clear() # Limpia la lista por completo

print(my_list) ## []

my_list = [5, 2, 6, 71, 1, 24, 125]

my_list.sort() # Ordena la lista de menor a mayor a menos que lo indiquemos como parámetro

print(my_list) ## [1, 2, 5, 6, 24, 71, 125]
```
