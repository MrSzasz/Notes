# TypeScript

[TypeScript](https://github.com/microsoft/TypeScript) es un lenguaje de tipado estático basado en JavaScript, el cual se utiliza mayormente para denotar los tipos de cada valor para evitar errores.

## Instalación

Typescript necesita ser instalado para su utilización, a su vez se necesita `npm` para gestionar el paquete.
Para saber si tiene npm instalado se tiene que abrir [una consola](https://linube.com/ayuda/articulo/174/abrir-una-consola-de-comandos#:~:text=Windows%20y%20Mac.-,En%20Windows,En%20ella%20debes%20escribir%20cmd.) y en el mismo pegar el siguiente comando.

    npm --v

Esto dará como resultado la version actual del mismo, de no ser asi, se instalar con el siguiente comando.

    npm i -g

Luego de instalarlo, el siguiente paso es instalar TypeScript, en la misma consola pegar el siguiente comando.

    npm -g typescript

> Para instalarlo globalmente o sin `-g` para instalarlo solamente para el proyecto en el que se va a utilizar.

En teoría debería haberse instalado TS, pero siempre es mejor asegurarse escribiendo `tsc` en la misma consola, debería aparecer una lista de comandos el mismo compilador.

## Compilador de JS/TS

Para iniciar con el lenguaje se debe crear un archivo con la extension `.ts`, luego en la consola se deberá iniciar TypeScript con el siguiente comando.

    tsc --init

Esto creará un archivo de configuración (***tsconfig.json***), el cual contiene todas las [configuraciones y opciones](https://www.typescriptlang.org/docs/handbook/compiler-options.html) necesarias para el funcionamiento del compilador en el archivo actual.
Luego del mismo se deberá compilar el archivo `ts` en un archivo `js`, esto se realiza pegando el siguiente comando en la consola.

    tsc

> Es posible compilar un solo archivo `ts` en el proyecto, nombrándolo luego del `tsc` => `tsc archivo.ts`

Se creará un archivo `js`, el cual sera la compilación del código escrito en el archivo de TypeScript.

## Coding

Luego de esta introducción e instalación de TS es momento del código, se puede empezar por escribir un simple código de JavaScript en el archivo `ts`.

    function addNumbers(x, y) {
        return x + y;
    }
    console.log(addNumbers(3, 6));

El código es una función normal que suma los parámetros, pero hay un error notable en el mismo, dado a que TS esta hecho para un tipado marcado, es necesario declarar los tipos de variables que se usan, quedando el mismo de la siguiente forma.

```ts

    function addNumbers(x:number, y:number) {
        return x + y;
    }
    console.log(addNumbers(3, 6));

```

Al agregar el tipo de la variable se evitan los futuros problemas al pasar valores que no sean de tipo declarado, es decir *Number*.
Luego de esto, se debe compilar el archivo, el cual se hace escribiendo `tsc` en la consola, si no hay errores lo compilara sin problemas, y el resultado debería ser el siguiente.

```js
    
    "use strict";
    function addNumbers(x, y) {
        return x + y;
    }
    console.log(addNumbers(3, 6));

```

Como es posible observar, el código es básicamente idéntico, se diferencia en el *`"use strict"`* () y en que el tipado de valores puestos en el archivo `ts` ya no se encuentra, pero el mismo funciona a la perfección.

> El archivo `js` ya se puede linkear como cualquier otro `js` a un HTML, y debería funcionar normalmente.

## Tipos

TypeScript no solo funciona en base a los tipos que existen en [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures), sino que agrega nuevos tipos de datos, uno de ellos es el tipo [***`enum`***](https://www.typescriptlang.org/docs/handbook/enums.html).  
***`Enum`*** es un tipo de dato que se comporta como un array, el cual guarda los posibles valores relacionados que se pueden utilizar en un rango, como pueden ser los días en una semana, o las posibles acciones de un click del mouse.

    enum weekDays{
        Monday, //0
        Tuesday, //1
        Wednesday, //2
        Thursday, //3
        Friday, //4
        Saturday, //5
        Sunday //6
    }

    console.log(weekDays.Wednesday)

> La consola mostrará el resultado como un valor numérico (en este caso *2*).

También es posible empezar la lista con un valor a elección, y los siguientes números serán asignados automáticamente en base al mismo.

    enum StatusCodes {
    OK = 200,
    BadRequest = 400,
    Unauthorized, //401
    PaymentRequired, //402
    Forbidden, //403
    NotFound //404
    }

    console.log(statusCode.NotFound);

> La consola mostrará en este caso el numero *404*, ya que es el valor que se le asigna automáticamente.

Por ultimo, también hay que aclarar que es posible asignar un valor de tipo `string`, pero no sera posible que se asignen los siguientes automáticamente, pero al imprimir los valores con `console.log` se verán mas fácilmente, sin tener que ir a ver el valor asignado al numero en cuestión.

    enum Users{
        user = "USER",
        admin = "ADMIN",
        superAdmin = "SUPERADMIN"
    }

    console.log(Users.admin)

> En este caso, la consola mostrará `ADMIN`, en vez de imprimir el valor que tendría según la posición numérica.

Otro tipo de valor asignable es el tipo [***`any`***](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any), el cual declara que el valor asignable puede ser literalmente de cualquier tipo, ya sea `Number`, `string`, `boolean`, etc.  

    let randomValue: any = 10;
    randomValue = 'Luke';   // OK
    randomValue = true;      // OK

La reasignación de datos a las variables no deriva en un error, gracias al tipo `any`, que es lo que sucede al hacer código de JavaScript normalmente.
  
El tipo `any` puede dar algunos errores, para ello se creo el tipo [***`unknown`***](https://www.typescriptlang.org/docs/handbook/2/functions.html#unknown), el cual es similar al tipo anteriormente nombrado, pero evitando que se pueda acceder al mismo, unicamente reasignarle un valor.

    let randomValue: unknown = 10;
    randomValue = true;
    randomValue = "Luke";
    randomValue = {name: "Exodia", parts: 5}


    console.log(randomValue.name); // ERROR 

Esto se "soluciona" de dos formas, asignándole un valor con el método `as`.

    let randomValue: unknown = 10;
    randomValue = true;
    randomValue = "Luke";
    randomValue = "Skywalker";

    (console.log(randomValue as string)) // Skywalker

> También es posible declararlo con una tag (console.log(`<string>`randomValue)

La 2da forma de comprobar es hacer una comprobación directa de `js`, usando un `typeOf`.

    let randomValue: unknown = 10;
    randomValue = true;
    randomValue = "Luke";
    randomValue = "Skywalker";

    if (typeof randomValue === "string") {
        console.log(randomValue.toUpperCase()); // SKYWALKER
    }

> Esta comprobación se realiza luego de la compilación a JavaScript.

Dado que hay ciertos momentos en los que el control de datos que se ingresan al código pueden ser medianamente controlados, se puede usar la `union` (`|`) para declarar dos o mas tipos de datos aceptados.

    let randomValue: number | boolean = 10; // OK
    randomValue = true; // OK
    randomValue = "Luke"; // ERROR

Otra forma de unir tipos es la `intersección` (`&`), la cual en vez de elegir entre uno o el otro, junta ambos tipos. Para el ejemplo del mismo se van a utilizar `Interfaces`, pero, ¿Que son las interfaces?.

---

## Interfaces

Las `interfaces` son un tipo de estructura que definen las características que va a tener un objeto, siendo similar a las clases, pero con datos obligatorios.  
Las interfaces se declaran con la palabra reservada `interface` y el nombre (que comúnmente comienza con una `I`).

    interface IPerson {
        name: string; // OBLIGATORIO
        surname: string; // OBLIGATORIO
        age: number; // OBLIGATORIO
        country?: string; // OPCIONAL
    }

    let person1 : IPerson ={
        name: "Jotaro", 
        surname: Kujo",
        status: "active", // ERROR, no se reconoce porque no esta en la interface
        age: 40,
    }

> Como se ve en el ejemplo, el dato `country` no es necesario (`?:`), pero el resto si.

---

Las interfaces pueden hacer el uso de la intersección, sumando dos tipos de interfaces para crear una nueva variable.

    interface Employee {
        employeeID: number;
        age: number;
    }
    
    interface Manager {
        stockPlan: boolean;
    }
    
    let newManager: Employee & Manager = {
        employeeID: 12345,
        age: 34,
        stockPlan: true
    };

También es posible crear un `type` especifico uniendo ambos, para crear la validación de los datos necesarios.

    interface Employee {
        employeeID: number;
        age: number;
    }

    interface Manager {
        stockPlan: boolean;
    }

    type ManagementEmployee = Employee & Manager;
    
    let newManager: ManagementEmployee = {
        employeeID: 12345,
        age: 34,
        stockPlan: true
    };

> El resultado sigue siendo el mismo, pero el nuevo `type` puede ser utilizado en mas lugares sin la necesidad de repetir la intersección

Habrá momentos en los que sea necesario asignar un valor especifico de una lista de valores, esto es posible gracias a la definición de tipos literales.  
Los tipos literales brindan la posibilidad de que se declare un error si se pasa un valor que no este anteriormente declarado aunque el mismo sea sintácticamente valido.

    type testResult = "pass" | "fail" | "incomplete";

    let myResult: testResult;
    myResult = "incomplete"; // OK   
    myResult = "pass"; // OK 
    myResult = "failure"; // ERROR

> También es posible pasar valores `boolean` y `number` como tipos literales
