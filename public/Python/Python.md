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
