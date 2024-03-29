# Python

[Python](https://www.python.org/) es un lenguaje de programación ampliamente utilizado para diferentes motivos, desde la creación de programas de automatización, machine learning, desarrollo de software, ciencia de datos, entre otros. Python es un lenguaje de fácil aprendizaje y adaptación, por lo que esto lo convierte en uno de los lenguajes preferidos para aprender, además de contar con una buena demanda en el ámbito laboral.

## Guía de Temas

1. [Instalación](#instalaci%C3%B3n)
2. [Código](#coding)
    - [Print](#imprimir)
    - [Tipos de datos](#tipos-de-datos)
    - [Variables](#variables)
    - [Inputs](#input)
    - [Operadores matemáticos](#operadores)
    - [Operadores de comparación](#comparadores)
    - [Formateo de datos](#formateo-de-datos)
    - [Manejo de strings](#slice-de-strings)
    - [Listas](#listas)
    - [Tuplas](#tuples)
    - [Sets](#sets)
    - [Diccionarios](#diccionarios)
    - [Condicionales](#condicionales)
    - [Loops](#loops)
    - [Funciones](#funciones)
    - [Clases](#clases)
    - [Errores](#manejo-de-errores-exceptions)
    - [Modularización](#módulos)
    - [Manejo de fechas](#dates)
    - [List comprehension](#list-comprehension)
    - [Funciones anónimas / lambdas](#lambdas)
    - [Funciones de orden superior](#high-order-functions--closures)
    - [Manejo de archivos](#file-handling)
    - [Expresiones regulares](#regex)
3. [Referencias](#referencias)

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

Sumado a esto es posible asignar diferentes variables en una sola linea, o asignar el mismo valor a diferentes variables de la siguiente manera.

```py
x, y, z = 1, 2, 3

print(x) ## 1

print(y) ## 2

print(z) ## 3

a = b = c = "alphabet"

print(a) ## alphabet

print(b) ## alphabet

print(c) ## alphabet
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

### Listas

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

### Tuples

Las tuplas son similares a las listas en su forma, con la diferencia que se utilizan `()` en vez de `[]`, pero su mayor diferencia es que las tuplas son inmutables, es decir, no se puede cambiar el contenido de las mismas, solo se puede acceder. Para ver como funciona esto podemos crear una tupla e intentar modificarlo de la siguiente manera.

```py
# Tuplas

my_tuple = tuple() # Declaramos la tupla

my_second_tuple = () # Declaramos la tupla

my_tuple = ("Heisenberg", "Walter White", 14, True, 15.5, 14) # Asignamos los valores a la tupla

my_second_tuple = ("Heisenberg", "Walter White", 14, True, 15.5, 14)

print(my_tuple) ## ('Heisenberg', 'Walter White', 14, True, 15.5, 14)

print(my_second_tuple) ## ('Heisenberg', 'Walter White', 14, True, 15.5, 14)

print(my_tuple.count(14)) ## 2

print(my_tuple.count(2)) ## 0

print(my_tuple.index(True)) ## 3

my_tuple.append("Jess") # Error, no se puede agregar un valor a la tupla

del my_tuple # Elimina la tupla Y ADEMAS la variable

print(my_tuple) # Error, la variable "my_tuple" fue eliminada con el "del" anterior
```

### Sets

Los sets, al igual que las tuplas, comparten similitudes con las listas, pero a diferencia de estas los sets se inician con `{}` y además estas no tienen un orden, por lo que no se puede acceder con el indice del dato en particular (`[0]`), pero a su vez esto ayuda a que los elementos del mismo no se repitan. Podemos ver el funcionamiento de las mismas de la siguiente manera.

```py
# Sets

my_set = set() # Creamos el set

my_second_set = {"Heisenberg", "Walter White", 14, True, 15.5} # Creamos el set

my_set = {"Jesse", "Hank", 24, False, 11.5} # Le asignamos los valores al set

print(my_set) ## {False, 'Jesse', 24, 11.5, 'Hank'}

print(my_second_set) ## {True, 'Walter White', 15.5, 14, 'Heisenberg'}

my_set.add("Skyler") # Añade un valor al set

print(my_set.union(my_second_set)) # Junta los dos sets sin modificar el original

print(my_set) ## {False, 'Jesse', 'Skyler', 24, 11.5, 'Hank'}

my_set.add("Skyler") # No se puede añadir el mismo elemento porque ya existe en el set

print(my_set) ## {False, 'Jesse', 'Skyler', 24, 11.5, 'Hank'}

print("Hank" in my_set) # Imprime True, ya que existe el valor en el set

my_set.remove("Hank") # Quita el valor del set

print("Hank" in my_set) # Imprime False, ya que no existe el valor en el set

print(my_set) ## {False, 'Jesse', 24, 11.5, 'Skyler'}

my_set.update({"Junior", 155}) # Agrega el valor que le asignamos al set

print(my_set) ## {False, 'Jesse', 'Junior', 24, 11.5, 155, 'Skyler'}

print(my_second_set) ## {True, 'Heisenberg', 'Walter White', 14, 15.5}

my_set.update(my_second_set) # Unimos ambos sets

print(my_set) ## {False, True, 'Jesse', 'Heisenberg', 'Junior', 11.5, 14, 15.5, 24, 'Walter White', 155, 'Skyler'}

print(my_set.difference(my_second_set)) # Imprime los valores que no se encuentran en el set
```

### Diccionarios

Otro tipo similar a los anteriores nombrados son los dictionaries (también similares a los objetos de JavaScript), estos a diferencia de las listas poseen un esquema `"key":"value"` (`"clave":"valor"`), a los cuales se puede acceder mediante las keys de las mismas. La mayoría de los métodos disponibles se repiten, quedando los mismos de la siguiente manera.

```py
# Diccionarios

my_dict = dict() # Creamos el diccionario

my_second_dict = {"name": "Jesse",
                  "last_name": "Pinkman",
                  "age": 24,
                  "numbers": {4, 2, 4}
                  } # Creamos el diccionario

my_dict = {"name": "Walter",
           "last_name": "White",
           "age": 52,
           "numbers": {1, 2, 4}
           } # Le asignamos los valores al diccionario

print(my_dict) ## {'name': 'Walter', 'last_name': 'White', 'age': 52, 'numbers': {1, 2, 4}}

print(my_second_dict) ## {'name': 'Jesse', 'last_name': 'Pinkman', 'age': 24, 'numbers': {2, 4}}

print(my_dict["age"]) # Accedemos al valor con la key correspondiente

# print(my_dict["address"]) # Error, porque no existe la key

my_dict["address"] = "308 Negra Arroyo Lane, Albuquerque, New Mexico. 87104" # Creamos la key con su valor correspondiente

print(my_dict) ## {'name': 'Walter', 'last_name': 'White', 'age': 52, 'numbers': {1, 2, 4}, 'address': '308 Negra Arroyo Lane, Albuquerque, New Mexico. 87104'}

print(my_dict["address"]) ## 308 Negra Arroyo Lane, Albuquerque, New Mexico. 87104

del my_dict["address"] # Eliminamos la key y su valor

print(my_dict) ## {'name': 'Walter', 'last_name': 'White', 'age': 52, 'numbers': {1, 2, 4}}

print("Walter" in my_dict) # False, ya que lo que comprueba es que exista la key en el diccionario

print("name" in my_dict) ## True

print("address" in my_dict) ## False

print("Walter" in my_dict["name"]) # True, ya que el valor existe para esa key

print(my_dict.items()) # Imprime una lista con los items (key:value) en el diccionario

print(my_dict.keys()) # Imprime una lista solo de las keys del diccionario

print(my_dict.values()) # Imprime una lista solo de los valores del diccionario

my_dict.clear() # Limpia el diccionario por completo

print(my_dict) ## {}

my_new_dict = my_second_dict.fromkeys(my_second_dict) # Crea un nuevo diccionario en base a las keys que le pasamos, con valor "None"

print(my_new_dict) ## {'name': None, 'last_name': None, 'age': None, 'numbers': None}

my_new_dict = my_second_dict.fromkeys(my_second_dict, "same value") # Al pasarle un 2do parámetro, lo agrega como valor a todas las keys

print(my_new_dict) ## {'name': 'same value', 'last_name': 'same value', 'age': 'same value', 'numbers': 'same value'}
```

> Es posible unir dos diccionarios / actualizar usando `dict.update(data)`

### Condicionales

Los condicionales se utilizan para ejecutar cierto bloque de código solamente cuando una condición se cumpla, por ejemplo, si queremos enviarle un resultado al usuario solamente cuando tenga permisos para ello utilizamos los condicionales. Los mismos se basan en los booleans `True` y `False`.  
La comprobación se realiza con el uso de `if` o `elif`, los cuales marcan un "camino" que tomará el código dependiendo de si el mismo es verdadero o falso. Podemos ver el funcionamiento de las mismas de la siguiente manera.

```py
# Condicionales

my_true_condition = True

my_false_condition = False

if my_true_condition: # Si la condición es verdadera
    print("La condición es verdadera") # Se realiza la acción

if my_false_condition:
    print("La condición es falsa") # Es False, así que no se realizar la condición

my_number = 120

if my_number < 0: # Si el numero es menor a 0
    print("Mi numero es negativo") # Imprime esto
elif my_number >= 1: # En cambio si el numero es mayor o igual a 1 
    print("Mi numero es positivo") # Imprime esto
else: # Si no entra en ninguna de las dos comprobaciones anteriores
    print("Este no es un numero valido") # Imprime esto
   
my_sum = 6 + 9

if my_sum == 9: # Si el resultado es 9
    print("Nine")
else: 
    print(my_sum) ## 15
    
if my_sum > 0 and my_number > 0: # Comprueba que ambos sean verdaderos
    print("Son positivos")
else:
    print("Son negativos")
    
if my_number > 0 or my_number > 0: # Comprueba que al menos uno sea verdadero
    print("Uno es positivo")
else:
    print("Son negativos")
    
if not my_number == 120: # Invierte la comprobación
    print("Solo se imprime si es diferente a 120")
else: 
    print("El numero es 120")
    
if not my_number != 120: # Invierte la comprobación
    print("El numero es 120")
else: 
    print("Solo se imprime si es diferente a 120")

my_empty_string = ""

my_not_empty_string = "Texto"

if my_empty_string: # La cadena vacía equivale a False
    print("La cadena tiene un valor")
    
if my_not_empty_string: # La cadena equivale a True
    print("La cadena tiene un valor")
    
if my_empty_string == "": # Comprueba que la cadena esté vacía
    print("La cadena no tiene un valor")
```

### Loops

Los loops (ciclos) son pedazos de código que se encargan de repetir cada vez que una condición se cumpla, por ejemplo, si queremos que cierto código se imprima solamente cuando el numero sea mejor a 10, podemos usar un `while` e indicar que se sume el valor hasta llegar a 10, o si queremos iterar por los valores de una lista podemos utilizar un `for`, quedándonos de la siguiente manera.

```py
# Loops

my_first_num = 0

while my_first_num < 10: # El loop siempre se ejecuta si la condición es True
    print(f"Vuelta numero {my_first_num + 1}")
    my_first_num += 1 # Y aumentamos el valor del numero para que no se cree un loop infinito


my_second_num = 0

while my_second_num < 10:
    print(f"Vuelta numero {my_second_num + 1}")
    my_second_num += 1
else: # Se imprime justo al finalizar el ciclo
    print("Fin del ciclo")


my_third_num = 0

while my_third_num < 10:
    if my_third_num % 2 == 0: # Comprueba si la condición en el loop es True
        print(f"{my_third_num} es numero par") # E imprime lo siguiente
    else: # En cambio si es False
        print(f"{my_third_num} es numero impar") # Imprime esto
    my_third_num += 1


my_fourth_num = 0

while my_fourth_num < 10:
    print(my_fourth_num)
    if my_fourth_num == 5:
        break # Si el numero en el loop es 5 termina el ciclo
    my_fourth_num += 1
else: # Y no imprime el final, ya que el break lo rompe por completo
    print("Fin del ciclo")



my_list = [1, 14, 516, 7, 132, 751, -13, 15, 1892]

for num in my_list: # Itera por cada uno de los valores de la lista
    print(num) # E imprime el valor correspondiente en cada ciclo


for num in my_list:
    print(num)
else: # Al igual que en el While, se imprime al finalizar el ciclo
    print("Fin del ciclo")


for num in my_list:
    print(num)
    if num > 600:
        break # El break funciona en ambas situaciones
else:
    print("Fin del ciclo")


for num in my_list:
    if num > 500:
        continue # El continue salta la ejecución, pero no termina el ciclo
    print(num)
else:
    print("Fin del ciclo")
```

### Funciones

Las funciones son uno de los temas mas importantes en todos los lenguajes de programación, estos son bloques de código que se pueden llamar para realizar cierta acción sin tener la necesidad de repetir todo el código una y otra vez. Python como otros lenguajes de programación ya vienen con ciertas funciones integradas (como por ejemplo `print()`), pero nosotros podemos crear nuestras propias funciones de la siguiente manera.

```py
# Funciones

def sum_values(param_1, param_2): # Definimos la función con "def"
    print(param_1 + param_2) # Indicamos que realiza la función
    
sum_values(1, 5) # Llamamos a la función con sus parámetros

sum_values(11, 61) ## 72

# sum_values() => Error, necesita dos parámetros pero no le pasamos ninguno

sum_values(1.4, 5.16) ## 6.5600000000000005

sum_values("Hola", ", como estas") ## Hola, como estas

sum_values("Hola", "44") ## Hola44
    
    
def say_my_name(name, last_name, alias = "Heisenberg"): # Podemos agregar valores por defecto por si no se pasan los parámetros
    print(f"{name} {last_name}, {alias}")
    
say_my_name("Walter", "White") ## Walter White, Heisenberg

say_my_name(last_name = "Pinkman", name = "Jesse", alias = "Cap'n Cook") ## Jesse Pinkman, Cap'n Cook

    
def sum_values_and_return(param_1, param_2):
    return param_1 + param_2 # La función realiza el calculo y devuelve el valor

sum_values_and_return(1, 6) # No sucede nada porque no se esta utilizando el valor

return_with_variable = sum_values_and_return(22, 9) # Guarda el valor de la suma en una variable

print(return_with_variable) ## 31

print(sum_values_and_return(155, 15)) ## 170


def print_all(*params): # Indicamos que puede recibir multiples parámetros
    for param in params: # Con cada una de los parámetros
        print(param) # Imprime el parámetro, uno por uno
        
print_all("Walter", "White") # Imprime ambos en diferentes lineas

print_all("Walter", "White", "Jesse", "Pinkman")
```

### Clases

Las clases son similares a las funciones, con la diferencia que estas nos sirven para crear diferentes objetos que contengan las mismas características, por ejemplo, si creamos una clase Animal podemos indicar que el mismo puede hacer sonidos, pero que no puede tener ciertas acciones como hacer matemáticas complejas, esto nos ayuda a mantener un control dentro de lo que podemos cuando creamos diferentes objetos. Para ver esto usamos la palabra reservada `class` de la siguiente manera.

```py
# Clases

class Person: # Creamos la clase con CamelCase
    def __init__(self, name, last_name, alias = "Heisenberg"): # Pasamos los parámetros que necesitaremos junto al __init__ y el self obligatorio
        self.full_name = f"{name} {last_name}, \"{alias}\"" # Creamos un dato que será publico
        self.__name = name # Y el dato que será privado con "__"
        
    def get_name(self): # Podemos indicar un "getter" para acceder al nombre sin modificarlo
        print(f"{self.__name}")
        
    def say_my_name(self): # Una función que tome los parámetros que le pasamos
        print(f"{self.full_name}")
        
    def say_hi(self): # Y una función normal
        print("Hi")
        
person_1 = Person("Walter", "White") # Creamos la persona

person_1.say_my_name() ## Walter White, "Heisenberg"

# print(person_1.__name) => Error, no se puede acceder al dato porque es privado

person_1.full_name = "Heisenberg" # Podemos cambiar el valor del dato publico, aunque no es lo recomendado

person_1.say_my_name() ## Heisenberg

person_1.say_hi() ## "Hi"


person_2 = Person(alias = "Cap'n Cook", name = "Jesse", last_name = "Pinkman") # Podemos cambiar el orden de los parámetros

person_2.say_my_name() ## Jesse Pinkman, "Cap'n Cook"
```

### Manejo de errores (Exceptions)

Cuando un código de Python falla, normalmente el error detiene toda la ejecución, lo que puede llevar a una mala experiencia para el usuario, o mismamente para fallas en el código por completo, es por eso que podemos manejar los errores gracias a los bloques `try/except`, los cuales toman esos errores y se encargan de la solución de los mismos, sin detener el flujo de código. Para ello debemos crear el bloque de la siguiente manera.

```py
# Excepciones

message = "Hello, world!"

try: # Creamos el bloque try para que intente un código
    raise Exception() # Genera un error manualmente
    print(message)
except: # Si el código falla seguirá por este bloque
    print("Hubo un error en el primer ejemplo")
    
    
try:
    print(message)
except:
    print("Hubo un error en el 2do ejemplo")
else: # Este bloque solo se ejecutará si el código no falló
    print("El ejemplo 2 se completó sin errores")


try:
    print(message)
except:
    print("Hubo un error en el 3er ejemplo")
else:
    print("El ejemplo 3 se completó sin errores")
finally: # Se ejecuta siempre al finalizar, independientemente si hubo o no un error
    print("Fin del ejemplo 3")
   
    
try:
    raise Exception()
    print(message)
except:
    print("Hubo un error en el 4to ejemplo")
else:
    print("El ejemplo 4 se completó sin errores")
finally:
    print("Fin del ejemplo 4")
   
    
try:
    raise ValueError() # Genera un error del tipo ValueError
    print(message)
except TypeError: # Se ejecuta solamente si es el tipo de error correspondiente
    print("Hubo un error de tipo TypeError")
except ValueError:
    print("Hubo un error de tipo ValueError")
   
    
try:
    raise Exception("Esto es un mensaje de error") # Le indicamos el mensaje de error
    print(message)
except Exception as err: # Si no sabemos el tipo de error imprimimos todos los errores
    print(err)
```

### Módulos

Python viene cargado con diferentes módulos, es decir, con diferentes "porciones" de código, funciones, métodos, todo lo que nos ayuda a realizar ciertas acciones, pero que no siempre son necesarias, por lo que se separa en otros ficheros para agilizar el código. Estos módulos de código pueden utilizarse con la palabra reservada `import`, o podemos crear nuestros propios módulos para agilizar el código. Para ver mejor esto lo haremos creando un archivo llamado `module_functions.py`, el cual utilizaremos para crear una función de la siguiente manera.

```py
# Funciones para exportar

def say_my_name(name, last_name):
    print(f"My name is {name} {last_name}")
    
def print_all_this(*values):
    for value in values:
        print(value)
```

Ahora podemos utilizar estas funciones en nuestro archivo `main.py` de la siguiente manera.

```py
# Módulos

import module_functions # Importamos el modulo completo

module_functions.print_all_this("This", "is", "a", "Normal", "Text") # Y llamamos la función necesaria tomando de base el modulo

print(dir(module_functions)) # Imprime todas las variables que contiene el módulo

from module_functions import say_my_name # Importamos solamente la función que usaremos

say_my_name("Walter", "White") # Y la llamamos normalmente


from module_functions import sum_two_values as default_sum_function # Podemos asignarle un nombre/alias personalizado

default_sum_function(1, 52) # Y lo llamamos de esa forma

# sum_two_values() => Error, no existe la función con ese nombre

import math # Importamos el modulo que viene con Python

print(math.pi) # Y lo utilizamos en base al nombre del modulo

from math import pow # O podemos importar solamente lo que necesitaremos

print(pow(2, 15)) # E utilizarlo solo para ello, sin sobrecargar nuestro código
```

### Dates

Python nos ofrece un modulo para trabajar con fechas, ya sea usando dia y hora, o ambos por separado, ademas de poder sumar y restar franjas de tiempo entre estos. Para esto debemos utilizar el modulo llamado `datetime`, pudiendo usar del mismo `datetime` para trabajar con ambos de la siguiente manera.

```py
# Dates

from datetime import datetime # Importamos datetime desde datetime

now = datetime.now() # Creamos la variable con la fecha y hora actual

print(f"{now.year}/{now.month}/{now.day} - {now.hour}:{now.minute}:{now.second} ({now.timestamp()})") # Podemos tomar solo lo que necesitamos de la variable

custom_datetime = datetime(1922, 12, 15) # Ademas de poder crear nuestra propia fecha
custom_datetime_with_time = datetime(1941, 2, 2, 13, 20, 13) # Y agregarle el tiempo del mismo

print(custom_datetime) ## 1922-12-15 00:00:00
print(custom_datetime_with_time) ## 1941-02-02 13:20:13

datetime_diff = now - custom_datetime # Ademas podemos restar las fechas para ver el tiempo que paso entre una y otra
print(datetime_diff) ## 36683 days, 13:37:28.570086
```

Ademas de esto también podemos trabajar solamente con el apartado de fecha usando el modulo `date` que contiene `datetime` de la siguiente manera.

```py
# Dates

from datetime import date # Importamos date desde datetime

date_now = date.today() # Tomamos la fecha actual
custom_date = date(1999, 7, 22) # O podemos crear nuestra propia fecha

print(f"{custom_date.year}/{custom_date.month}/{custom_date.day}") ## 1999/7/22
print(date_now) ## 2023-05-22
print(custom_date) ## 1999-07-22

date_diff = now.date() - custom_date # De la misma forma podemos operar con los datos
print(date_diff) ## 8705 days, 0:00:00
```

O si necesitamos solamente trabajar con el tiempo podemos utilizar el modulo `time` de `datetime` de la siguiente manera.

```py
# Dates

from datetime import time # Importamos time desde datetime

time_now = time() # Toma una hora vacía, ya que no es posible tomar la hora actual de la misma manera que los anteriores
custom_time = time(12, 11, 41) # Pero podemos crear nuestra propia hora

print(f"{custom_time.hour}h {custom_time.minute}m {custom_time.second}s") ## 12h 11m 41s
print(time_now) ## 00:00:00
print(custom_time) ## 12:11:41

# time_diff = time_now - custom_time
# print(time_diff) => Error, no es posible realizar esta acción
```

Y por ultimo tenemos el modulo `timedelta`, el cual nos ayuda con calcular los rangos entre dos tiempos, pudiendo ver el rango que hay entre dos cantidades de la siguiente manera.

```py
# Dates 

from datetime import timedelta # Importamos timedelta desde datetime

time_start = timedelta(150, 100, hours = 20, minutes = 128) # Indicamos el tiempo de inicio en cantidad
time_end = timedelta(240, 120, hours = 200, minutes = 12) # Y el tiempo de finalización también en cantidad

print(time_end - time_start) ## 97 days, 10:04:20
```

### List comprehension

Cuando queremos copiar una lista y crear una nueva modificando los valores que le pasaremos podemos hacer uso del `list comprehension`, el cual nos permite crear una nueva lista ya sea con los mismos valores o modificando los mismos con lo que necesitemos, como podemos ver en el siguiente ejemplo.

```py
# List comprehension

my_main_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] # Creamos nuestra base

print(f"My main list: {my_main_list}") ## My main list: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

my_new_list = [i for i in my_main_list] # Iteramos por la lista

print(f"My new list: {my_new_list}") ## My new list: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

my_range_list = [i for i in range(10)] # Creamos lo mismo pero con un rango

print(range(10)) ## range(0, 10)

print(f"My range list: {my_range_list}") ## My range list: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

my_modified_list = [i + 5 for i in my_main_list] # Le sumamos 5 a cada uno de los elementos en la lista original

print(f"My modified list: {my_modified_list}") ## My modified list: [5, 6, 7, 8, 9, 10, 11, 12, 13, 14]

def mult_by_self(number): # Creamos una función que multiplique por el mismo numero
    return number * number 

my_mult_list = [mult_by_self(i) for i in my_main_list] # Y la utilizamos para modificar la lista

print(f"My mult list: {my_mult_list}") ## My mult list: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

my_even_list = [i for i in my_main_list if i % 2 == 0] # Solo toma los números que cumplen con la condición

print(my_even_list) ## [0, 2, 4, 6, 8]
```

Este resultado también se puede obtener con un `for`, sin ser tan optimo, pero el mismo quedaría de la siguiente manera.

```py
my_main_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] # Creamos nuestra base

my_for_list = [] # Creamos la lista vacía

for i in my_main_list: # Y usamos un for para recorrer la lista original
    my_for_list.append(mult_by_self(i))
    
print(f"My for list: {my_for_list}") ## My for list: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### Lambdas

Hay veces que necesitaremos crear funciones simples o mismamente funciones dentro de otras funciones. Para esto podemos hacer uso de las `lambdas` (funciones anónimas), las cuales nos permiten crear funciones simples, guardando las mismas en una variable si es necesario. Para esto haremos uso de la palabra reservada `lambda` de la siguiente manera.

```py
# Lambdas

sum_two_values = lambda val_1, val_2: val_1 + val_2 # Suma dos valores

print(sum_two_values(5, 6)) ## 11

sum_ten_and_multiply = lambda val_1, val_2: (val_1 * val_2) + 10 # Multiplica dos valores y le suma 10

print(sum_ten_and_multiply(15, 2)) ## 40

def new_sum(value):
    return lambda val_1, val_2: val_1 + val_2 + value # Suma dos valores con la lambda y le agrega el valor que indicamos como parámetro

print(new_sum(7)(12, 8)) # Primero le pasamos el parámetro de la función, y luego los parámetros de la lambda
```

### High order functions & closures

Las funciones de orden superior son aquellas funciones que contienen funciones dentro de las mismas. Estas funciones pueden tener algunas funciones mas simples dentro, lo que ayuda con el orden de ejecución y practicidad del código. Además es posible pasar funciones como parámetros a estas funciones, o utilizar lambdas, coom podemos ver a continuación.

```py
# High order functions

def sum_two_plus_ten(value): # Creamos la función
    return value + 10 # Y su return

def sum_all(value_1, value_2):
    return sum_two_plus_ten(value_1 + value_2) # Llamamos a la función dentro de la otra función
    
print(sum_all(7, 10)) ## 27



def sum_all_with_inside_functions(value_1, value_2):
    def sum_all_and_add_ten(value): # Creamos la función dentro de la otra función
        return value + 10 # Retornamos el valor de la misma
    
    return sum_all_and_add_ten(value_1 + value_2) # Y retornamos el valor final

print(sum_all_with_inside_functions(7, 20)) ## 37



def do_something_with_two_values(value_1, value_2, func): # Creamos la función a la que le pasaremos otra función como parámetro
    return func(value_1, value_2) # Y devolveremos el valor final de esa función 

print(do_something_with_two_values(15, 20, sum_all)) ## 45
```

Dentro de Python vienen algunas funciones de orden superior para usar, estas funcionan de la misma manera, se le pasa una función como parámetro de la siguiente manera.

```py
# High order functions

list_of_numbers = [1, 16, 22, 18, 29, 2, 55]


def multiply_by_two(value): # Creamos la función que usaremos para el map
    return value * 2

new_list_multiplied = map(multiply_by_two, list_of_numbers) # El mismo itera por cada item y lo pasa como parámetro de la función

print(list(new_list_multiplied)) ## [2, 32, 44, 36, 58, 4, 110]

new_list_multiplied_with_lambda = map(lambda number: number * 2, list_of_numbers) # Podemos hacerlo con una lambda en vez de crear la función fuera

print(list(new_list_multiplied_with_lambda)) ## [2, 32, 44, 36, 58, 4, 110]



def greater_than_twenty(number): # Creamos el filtro que devuelve un boolean
    if number > 20:
        return True
    else:
        return False
    
    # return number > 20  => Es lo mismo pero simplificado


filtered_list = filter(greater_than_twenty, list_of_numbers) # Le pasamos la función como filtro

print(list(filtered_list)) ## [22, 29, 55]

filtered_list_with_lambda = filter(lambda number: number > 15, list_of_numbers) # Podemos llegar a lo mismo si utilizamos una lambda

print(list(filtered_list_with_lambda)) ## [16, 22, 18, 29, 55]



from functools import reduce # Importamos reduce


def sum_two(val1, val2): # Creamos la función para sumar los valores
    return val1 + val2

print(reduce(sum_two, list_of_numbers)) # Suma todos los valores que tenga la lista

print(reduce(lambda val1, val2: val1 + val2, list_of_numbers)) ## 143

print(reduce(lambda val1, val2: val1 - val2, list_of_numbers)) ## -141
```

Por ultimo tenemos los `closures`, los cuales funcionan como funciones de orden superior ya que son funciones dentro de funciones, pero las mismas devuelven funciones en su return, de la siguiente manera.

```py
## Closures


def sum_twenty(first_value): # Creamos una función para abarcar la otra
    def new_sum(value):
        return value + 20 + first_value
    return new_sum # Y retornamos esta función por completo

print(sum_twenty(1)) ## <function>

result_from_sum_twenty = sum_twenty(1) # Guarda la función en una variable

print(result_from_sum_twenty(15)) ## 36

print((sum_twenty(1))(15)) # Podemos llamarlo sin guardarlo, pasando los parámetros por separado
```

### File handling

Una de las funcionalidades mas útiles que nos ofrece Python es la posibilidad de trabajar con archivos, en este caso con archivos de texto (`.txt`) y de datos (`.json`). Para hacer esto haremos uso de dos módulos, `os` y `json`. Empezaremos creando la carpeta `/files` y dentro de la misma el archivo `text.txt`, el cual contendrá el siguiente texto.

```txt
Hola esta es una prueba
del texto y el modulo
para editar archivos txt
```

Con esto hecho podemos crear las funciones que utilizaremos para modificar el mismo de la siguiente manera.

```py
import os # Importamos el modulo para controlar el os


def read_file(filename): # Creamos la función para leer el archivo
    try:
        with open(filename, 'r') as file: # Usamos "open" con la flag "r" para abrir el archivo en solo lectura
            print(file.read()) # E imprimimos contenido
            file.close() # Como buena practica, cerramos el archivo cuando terminamos de utilizarlo
    except Exception as err:
        print(f"Error! {err.args[1]}") # Si hay un error, lo imprimimos
        
# read_file('./files/text.txt')


def read_file_by_line(filename): # Creamos la función para leer linea por linea
    try:
        with open(filename, 'r') as file:
            for line in file.readlines(): # Y utilizamos la función para ir linea por linea
                print(line) # Imprimiendo cada una por separado
    except Exception as err:
        print(f"Error! {err.args[1]}")


# read_file_by_line('./files/text.txt')

def write_file(filename, data):
    try:
        with open(filename, 'w') as file: # Lo abrimos en modo escritura
            file.write(data) # Si no existe el archivo, lo crea, si existe lo sobre escribe
            file.close()
        print("file written successfully at /files/" + filename)
    except Exception as err:
        print(f"Error! {err.args[1]}")

# write_file('./files/text.txt', "Este texto es nuevo") => Sobre escribe el archivo anterior
# write_file('./files/new_text.txt', "Este archivo es nuevo") => Crea un nuevo archivo


def append_to_file(filename, data):
    try:
        with open(filename, 'a') as file: # Lo abrimos en modo edición
            file.write(data) # Si existe, agrega el texto, sino lo crea
        print("data written successfully")
    except Exception as err:
        print(f"Error! {err.args[1]}")

# append_to_file('./files/text.txt', "Este texto es agregado") => Agrega al final del texto
# append_to_file('./files/new_text.txt', "Este texto es nuevo") => Crea un nuevo archivo

def delete_file(filename):
    try:
        os.remove(filename) # Utilizamos el modulo os para eliminar el archivo
        print("file deleted successfully!")
    except Exception as err:
        print(f"Error! {err.args[1]}")

delete_file('./files/text.txt')
```

También es posible manipular archivos JSON con el modulo correspondiente de la siguiente manera.

```py
import json # Importamos el modulo


my_dict = { # Creamos un diccionario
    "name": "Joseph",
    "last_name": "Joestar",
    "age": 91,
    "abilities": ["Hamon", "Stand"]
}


def write_json(filename, data):
    try:
        with open(filename, 'w') as file: # Abrimos el archivo en modo escritura
            json.dump(data, file) # Usamos dump para agregar data al archivo, si no existe lo crea
    except Exception as err:
        print(f"Error! {err.args[1]}")

# write_json('./files/data.json', {"data":"yes"}) # Si existe, sobre escribe los datos



def write_json_with_indent(filename, data, indent):
    try:
        with open(filename, 'w') as file:
            json.dump(data, file, indent=indent) # Podemos indentar el archivo con los espacios que querramos
    except Exception as err:
        print(f"Error! {err.args[1]}")
        

write_json_with_indent('./files/data.json', my_dict, 4)
        
        
            
def read_json(filename):
    try:
        with open(filename, 'r') as file: # Abrimos el archivo en modo solo lectura
            return json.load(file) # Y devolvemos los datos
    except Exception as err:
        return f"Error! {err.args[1]}"
                

print(read_json('./files/data.json')) ## {'name': 'Joseph', 'last_name': 'Joestar', 'age': 91, 'abilities': ['Hamon', 'Stand']}

        
        
def add_data_to_json(filename, data):
    try:
        json_from_file = read_json(filename) # Traemos los datos del JSON
        json_from_file.update(data) # Le agregamos los datos nuevos
        write_json(filename, json_from_file) # Y lo sobre escribimos
    except Exception as err:
        print(f"Error! {err.args[1]}")

add_data_to_json('./files/data.json', {"status": "alive"})
print(read_json('./files/data.json')) ## {'name': 'Joseph', 'last_name': 'Joestar', 'age': 91, 'abilities': ['Hamon', 'Stand'], 'status': 'alive'}
```

### RegEx

Python nos ofrece la posibilidad de comprobar ciertos patrones en nuestros strings, para eso se hace uso de las expresiones regulares y el modulo `re` de la siguiente manera.

```py
# regEx

import re # Importamos el modulo


my_string = "Hello, world! This is a test from Python for RegEx, with some Python code. You can test this right here" # Creamos el string para comprobar

match = re.match("Hello, world!", my_string, re.I) # Creamos el match

print(match) ## <Match>

print(match.span()) ## (0, 13)

start, end = match.span() # Le asignamos nombres a los valores

print(my_string[start:end]) # Imprimimos el match en el string


def match_RE(str_to_match, matching_string): # Podemos hacer lo mismo ordenado en una función
    match = re.match(matching_string, str_to_match, re.I) # Devuelve el match o None
    # if match != None:
    if match:
        start, end = match.span()
        print(f"Matching from {start} to {end}: '{str_to_match[start:end]}'") # Si existe imprimimos el match
    else:
        print("Not matching") # Sino imprimimos que no existe

match_RE(my_string, "Hello") ## Matching from 0 to 5: 'Hello'

match_RE(my_string, "Hello, worlds!") ## Not matching

match_RE(my_string, "This is a test") # Solo imprime si se encuentra desde el principio



def search_RE(str_to_match, matching_string):
    search = re.search(matching_string, str_to_match, re.I) # Busca el match en todo el string
    if search:
        start, end = search.span()
        print(f"Found on {start} to {end}: '{str_to_match[start:end]}'")
    else:
        print("No matching string")
        
search_RE(my_string, "This is a test") ## Found on 14 to 28: 'This is a test'

search_RE(my_string, "Python") # Devuelve solamente el primer match

search_RE(my_string, "JavaScript") ## No matching string



def find_all_RE(str_to_match, matching_string):
    matches = re.findall(matching_string, str_to_match, re.I) # Busca todas las veces que se encuentra en el string
    if len(matches) != 0:
        print(matches) # Y devuelve una lista
    else:
        print("No matching string found")
    
find_all_RE(my_string, "Python") ## ['Python', 'Python']

find_all_RE(my_string, "this") # Es independiente del Case por la flag "re.I"

find_all_RE(my_string, "Js") ## Not matching string found


print(my_string.split(" ")) # Divide el string con el match que le pasamos y lo devuelve como lista

print(my_string.split("!")) ## ['Hello, world', ' This is a test from Python for RegEx, with some Python code. You can test this right here']

print(my_string.split("twt")) # Devuelve la lista con un solo objeto dentro



print(re.sub(" ", ", ", my_string, flags=re.I)) # Reemplaza todos los matches que encuentra

print(re.sub(" ", ", ", my_string, 2 ,re.I)) # Reemplaza solamente los primeros 2 matches

print(re.sub("this", "repl", my_string, 2 ,re.I)) # Sin importar el Case

print(re.sub("twt", "repl", my_string, 2 ,re.I)) # Devuelve el string original si no encuentra matches para reemplazar
```

## Referencias

[Curso Python para principiantes by MoureDev](https://youtu.be/Kp4Mvapo5kc)

[Curso Python intermedio by MoureDev](https://youtu.be/TbcEqkabAWU)

[W3School - Python](https://www.w3schools.com/python)
