# Testing

El testing es una disciplina que se encarga de, como su nombre lo dice, hacer las pruebas en el código para comprobar su correcto funcionamiento. Los tests también se encargan de tener en cuenta los diferentes errores que puedan surgir en el código, como puede ser que no se envíe correctamente un dato y como se afronta el mismo.  

## Guía de Temas

1. [Tipos de test](#tipos-de-test)
    - [Unitarias](#pruebas-unitarias)
    - [Integración](#pruebas-de-integración)
    - [End-To-End](#pruebas-end-to-end)
2. [TDD](#test-driven-development)

---

## Tipos de Test

Los tests que se pueden lograr en un proyecto pueden variar dependiendo de que acciones se utilicen y cual es el fin de las mismas, estas pueden ser pruebas unitarias (Unit testing), pruebas de integración (Integration testing) y pruebas End-To-End, cada una con su respectivo nivel de carga de código y velocidad.

### Pruebas unitarias

Las pruebas unitarias son las pruebas que se encargan de probar una pequeña porción de código, ya sea una función o un render de un componente particular, por lo que es la prueba más rápida de lograr, pero la que menos porción de proyecto puede abarcar.

### Pruebas de integración

Este tipo de pruebas se realizan para poder comprobar que dos o mas porciones de código funcionan cuando se "juntan", es decir, que pueden probar una porción de código en la que se hizo una prueba unitaria (ejemplo, base de datos) con otra porción complementaria (ejemplo, mostrar los datos de la base de datos).  
Mayormente estas pruebas se hacen cuando un grupo de trabajo se dividen las tareas, por lo que cada uno puede tener su porción de código testeado y funcional, pero se deben cumplir los tests de integración en conjunto.

### Pruebas End-To-End

Son las pruebas en las que se puede "simular" el usuario final, con diferentes interacciones del mismo, entrada y salida de datos, movimientos, entre otros. Es por este motivo que este tipo de pruebas son las que más tiempo llevan para completar, siendo de las más costosas de lograr.  
En este tipos de pruebas se pueden llegar a comprobar que las bases de datos entreguen los datos necesarios o que incluso se puedan enviar datos a traves de formularios.

## Test Driven Development

El TDD o Test Driven Development es el modelo que marca una guía en el desarrollo en base a las pruebas, es decir, que lo primero que se tiene que idear son las pruebas, luego de tener estas el desarrollo se hace en pequeños bloques con el único fin de hacer funcionar estas pruebas, pasando luego a pulir y mejorar el código.  
El TDD se divide en 3 etapas:

| STEP     | DESC                                                                               |
|----------|------------------------------------------------------------------------------------|
| RED      | Solo la prueba escrita, por lo que sin código el resultado es rojo (red)           |
| GREEN    | Se crea el código necesario unicamente para lograr que pase la prueba              |
| REFACTOR | El código se mejora, para volver a probarse con el fin de que siga pasando el test |

Las diferentes etapas se generan en un "loop", dado que con cada refactorización se tiene que comprobar que el código siga funcionando, es decir, que siga en la etapa GREEN.
