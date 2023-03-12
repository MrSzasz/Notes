# TypeScript

[TypeScript](https://github.com/microsoft/TypeScript) es un lenguaje de tipado estático basado en JavaScript, el cual se utiliza mayormente para denotar los tipos de cada valor para evitar errores. Se dice que TypeScript es un superset de Javascript, dado que al final el código escrito en el archivo `.ts` se compila a un archivo normal `.js`, independientemente de si este termina funcionando o no.

## Guía de temas

1. [Instalación](#instalación)
2. [Compilación](#compilador-de-jsts)
3. Código de TypeScript
    - [Post compilación](#coding)
    - [Tipos](#tipos)
    - [Interfaces](#interfaces)
    - [Intersecciones](#intersecciones)
    - [Literales](#literales)
    - [Array y tuples](#arrays)
    - [Datos de solo lectura](#readonly)
    - [Funciones y void](#funciones)
    - [Clases y su privacidad](#clases)
    - [Tipos genéricos](#generic-types)
    - [Selección de datos](#selección-de-datos)

---

## Instalación

Typescript necesita ser instalado para su utilización, a su vez se necesita `npm` para gestionar el paquete.
Para saber si tiene npm instalado se tiene que abrir [una consola](https://linube.com/ayuda/articulo/174/abrir-una-consola-de-comandos#:~:text=Windows%20y%20Mac.-,En%20Windows,En%20ella%20debes%20escribir%20cmd.) y en el mismo pegar el siguiente comando.

```cmd
npm --v
```

Esto dará como resultado la version actual del mismo, de no ser asi, se instalar con el siguiente comando.

```cmd
npm i -g
```

Luego de instalarlo, el siguiente paso es instalar TypeScript, en la misma consola pegar el siguiente comando.

```cmd
npm i typescript -g
```

> El flag `-g` indica que el mismo se instalará globalmente, si queremos instalarlo en un solo proyecto deberemos abrir la consola en el mismo e instalarlo sin esta flag.

En teoría debería haberse instalado TS, pero siempre es mejor asegurarse escribiendo `tsc -v` en la misma consola, el cual debería mostrar la version instalada del mismo.

## Compilador de JS/TS

Para iniciar con el lenguaje se debe crear un archivo con la extension `.ts`, luego en la consola se deberá iniciar TypeScript con el siguiente comando.

```cmd
tsc --init
```

Esto creará un archivo de configuración (***tsconfig.json***), el cual contiene todas las [configuraciones y opciones](https://www.typescriptlang.org/docs/handbook/compiler-options.html) necesarias para el funcionamiento del compilador en el archivo actual.
Luego del mismo se deberá compilar el archivo `ts` en un archivo `js`, esto se realiza pegando el siguiente comando en la consola.

```cmd
tsc
```

> Es posible compilar un solo archivo `ts` en el proyecto, nombrándolo luego del `tsc` => `tsc archivo.ts`

Se creará un archivo `js`, el cual sera la compilación del código escrito en el archivo de TypeScript.

## Coding

Luego de esta introducción e instalación de TS es momento del código, se puede empezar por escribir un simple código de JavaScript en el archivo `ts`.

```ts
function addNumbers(x, y) {
    return x + y;
}
console.log(addNumbers(3, 6));
```

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
***`Enum`*** es un tipo de dato que se comporta como un array/clase, el cual guarda los posibles valores relacionados que se pueden utilizar en un rango, como pueden ser los días en una semana, o las posibles acciones de un click del mouse.

```ts
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
```

> La consola mostrará el resultado como un valor numérico (en este caso *2*).

Como los arrays normales, los `enum` comienzan en 0, pero es posible empezar la lista con un valor a elección, y los siguientes números serán asignados automáticamente en base al mismo.

```ts
enum StatusCodes {
    OK = 200,
    BadRequest = 400,
    Unauthorized, //401
    PaymentRequired, //402
    Forbidden, //403
    NotFound //404
}

console.log(statusCode.NotFound);
```

> La consola mostrará en este caso el numero *404*, ya que es el valor que se le asigna automáticamente.

Por ultimo, también hay que aclarar que es posible asignar un valor de tipo `string`, pero no sera posible que se asignen los siguientes automáticamente, pero al imprimir los valores con `console.log` se verán mas fácilmente, sin tener que ir a ver el valor asignado al numero en cuestión.

```ts
enum Users{
    user = "USER",
    admin = "ADMIN",
    superAdmin = "SUPERADMIN"
}

console.log(Users.admin)
```

> En este caso, la consola mostrará `ADMIN`, en vez de imprimir el valor que tendría según la posición numérica.

Otro tipo de valor asignable es el tipo [***`any`***](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any), el cual declara que el valor asignable puede ser literalmente de cualquier tipo, ya sea `Number`, `string`, `boolean`, etc.  

```ts
let randomValue: any = 10;
randomValue = 'Luke';   // OK
randomValue = true;      // OK
```

La reasignación de datos a las variables no deriva en un error, gracias al tipo `any`, que es lo que sucede al hacer código de JavaScript normalmente.
  
El tipo `any` puede dar algunos errores, para ello se creo el tipo [***`unknown`***](https://www.typescriptlang.org/docs/handbook/2/functions.html#unknown), el cual es similar al tipo anteriormente nombrado, pero evitando que se pueda acceder al mismo, unicamente reasignarle un valor.

```ts
let randomValue: unknown = 10;
randomValue = true;
randomValue = "Luke";
randomValue = {name: "Exodia", parts: 5}

console.log(randomValue.name); // ERROR 
```

Esto se "soluciona" de dos formas, asignándole un valor con el método `as`.  
El método `as` sirve para forzar el tipo de valor, siempre y cuando sea correcto.

```ts
let randomValue: unknown = 10;
randomValue = true;
randomValue = "Luke";
randomValue = "Skywalker";

console.log(randomValue as string) // Skywalker
```

Cuando no se declara el valor inicial como `unknown`, es posible reasignarlo como tal posteriormente.

```ts
let randomValue: unknown = 10;
randomValue = true;
randomValue = "Luke";
randomValue = "Skywalker";
let randomValueForError = 19;

console.log(randomValue as string) // Skywalker
console.log(randomValueForError as string) // ERROR, 19 no es un string
console.log(((randomValueForError) as unknown) as string) // OK, ya que primero se declara como UNKNOWN
```

> También es posible declararlo con una tag (console.log(`<string>`randomValue)

La 2da forma de comprobar es hacer una comprobación directa de `js`, usando un `typeOf`.

```ts
let randomValue: unknown = 10;
randomValue = true;
randomValue = "Luke";
randomValue = "Skywalker";

if (typeof randomValue === "string") {
    console.log(randomValue.toUpperCase()); // SKYWALKER
}
```

> Esta comprobación se realiza luego de la compilación a JavaScript.

Dado que hay ciertos momentos en los que el control de datos que se ingresan al código pueden ser medianamente controlados, se puede usar la `union` (`|`) para declarar dos o mas tipos de datos aceptados.

```ts
let randomValue: number | boolean = 10; // OK
randomValue = true; // OK
randomValue = "Luke"; // ERROR
```

Otra forma de unir tipos es la `intersección` (`&`), la cual en vez de elegir entre uno o el otro, junta ambos tipos. Para el ejemplo del mismo se van a utilizar `Interfaces`, pero, ¿Que son las interfaces?.

---

## Interfaces

Las `interfaces` son un tipo de estructura que definen las características que va a tener un objeto, siendo similar a las clases, pero con datos obligatorios.
Las interfaces se declaran con la palabra reservada `interface` y el nombre.

```ts
interface Character {
    name: string; // OBLIGATORIO
    surname: string; // OBLIGATORIO
    age: number; // OBLIGATORIO
    country?: string; // OPCIONAL
}

let person1 : Character ={
    name: "Jotaro", 
    surname: "Kujo",
    status: "active", // ERROR, no se reconoce porque no esta en la interface
    age: 40,
}
```

> Como se ve en el ejemplo, el dato `country` no es necesario (`?:`), pero el resto si.

También es posible crear interfaces que requieran funciones con ciertos nombres predefinidos.

```ts
interface Fly {
    fly(): void;
    // fly: () => void      // Es otra forma de declarar las funciones
}

let action: Fly = {
    fly: function () {
        console.log("I believe I can fly");
    },
};

action.fly();
```

Sumado a esto es posible editar las interfaces simplemente volviendo a declarar una interface con el mismo nombre de la siguiente manera

```ts
interface Fly {
    species: string
}
```

Las interfaces pueden juntarse para no repetir las mismas propiedades si una ya las tiene, dando asi un mejor flow a la hora de escribir el código. Esto es posible hacerlo con la palabra reservada `extends`, extendiendo todas las propiedades anteriormente nombradas.

```ts
interface Character {
    name: string; // OBLIGATORIO
    surname: string; // OBLIGATORIO
    age: number; // OBLIGATORIO
    country?: string; // OPCIONAL
}

interface FirstAppearance extends Character {
    chapter: string;
    publisher: string;
    year: number;
}

let person1: FirstAppearance = {
    name: "Jotaro",
    surname: "Kujo",
    age: 40,
    country: "Japan",
    chapter: "114 'Jotaro Kujo (1)'",
    publisher: "Weekly Shōnen Jump",
    year: 1989,
};
```

## Intersecciones

Las interfaces pueden hacer el uso de la intersección, el mismo es el método utilizado para combinar dos tipos de interfaces, dando como resultado una nueva de la siguiente manera.

```ts
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
```

También es posible crear un `type` especifico uniendo ambos, para crear la validación de los datos necesarios.

```ts
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
```

> El resultado sigue siendo el mismo, pero el nuevo `type` puede ser utilizado en mas lugares sin la necesidad de repetir la intersección, lo cual se explicará a continuación

## Literales

Habrá momentos en los que sea necesario asignar un valor especifico de una lista de valores, esto es posible gracias a la definición de tipos literales.  
Los tipos literales brindan la posibilidad de que se declare un error si se pasa un valor que no este anteriormente declarado aunque el mismo sea sintácticamente valido.

```ts
type testResult = "pass" | "fail" | "incomplete";

let myResult: testResult;
myResult = "incomplete"; // OK   
myResult = "pass"; // OK 
myResult = "failure"; // ERROR
```

> También es posible pasar valores `boolean` y `number` como tipos literales

## Arrays

Como todos los otros datos, los arrays también tienen que declarar los tipos que contendrán, evitando que se agreguen tipos indeseados.

```ts
const numbers : number[] = [1, 2, 3, 4, 5] // OK

const vowels : string[] = ["a", "e", "i", "o", "u"] // OK

const surelyVowels : string[] = ["a", 3, 1, 0, "u"] // ERROR, no se puede pasar un number como valor
```

Sumado a esto, hay un tipo especial de array que se caracteriza por tener una longitud definida de valores, con su tipo marcado en cada uno de ellos, los cuales se conocen como `tuples`.

```ts
const life : [number, string] = [1, "UP"]  // OK

const wrong : [number, string, number] = [4, "GET", "ME"] // ERROR, no es de tipo number

const missingNo : [string, number] = ["404"] // ERROR, falta un dato
```

> Los `tuples` tienen que contener sus datos como fueron asignados, en orden y cantidad, sino da ERROR como resultado

También existe la posibilidad de nombrar `tuples` para tener un mejor contexto de los mismos, y generar un `destructuring` de sus datos.

```ts
const persona : [nombre: string, apellido: string, edad: number] = ["Lara", "Croft", 26]

const [primerNombre, primerApellido, edadActual] = persona;

console.log(primerApellido) // "CROFT", el valor dado por el destructuring
```

## ReadOnly

Es posible declarar arrays que sean solo para lectura, es decir, que no se puedan modificar. Esto se logra gracias a la palabra reservada `readonly`.

```ts
const numbers : number[] = [1, 2, 3, 4, 5]

const codes : readonly number[] = [200, 400, 404, 500]

numbers.push(4)

codes.push(403) // ERROR, no se puede modificar un array con readonly
```

> `readonly` también es aplicable a los `tuples`, dotando a los mismos de una capa mas de comprobación

Los objetos en `ts` también tienen su sintaxis definida, la cual cambia un poco a como es en `js`.

```ts
const house: { address: string, city: string, price: number, pets: boolean, website: string, weekly?: boolean} = {
    address: '39 Niagara Street',
    city: 'Toronto',
    pets: true,
    price: 4000,
    website: "https://rentals.ca/toronto/niagara-west"
};
```

> Cuando se declara una variable con el símbolo `?` significa que el mismo puede ser omitido, ya que no es obligatorio

Si no se sabe la cantidad exacta de valores que contendrá un objeto es posible definir todos sus valores, independientemente de la cantidad.

```ts
const namesAndAge: { [index : string]: number} = {}

namesAndAge.Alucard = 598;
namesAndAge.SerasVictoria = 19;
namesAndAge.IntegraFairbrookWingatesHellsing = 22 
```

## Funciones

Las funciones en `ts` también pueden tener los tipos de entrada y salida marcados, su sintaxis base es la misma que en `js`, solo que se le agrega que tipo de dato vamos a pasar como parámetro (dentro de los paréntesis) y que tipo de dato retornara (luego de los paréntesis), esto también aplica para las funciones anónimas y las arrow functions.

```ts
function suma(a: number, b: number): number {
    console.log(a + b);
    return a + b;
}

let anonSuma = function(c: number, d: number): number {
    console.log(c + d);
    return c + d;
}

let arrowSuma = (e: number, f: number): number => e + f;

console.log(arrowSuma(5,7))
```

Sumado a esto, es posible crear funciones que no retornen ningún valor explicito, a esto se le llama `void`.

```ts
function sayMyName(name : string) : void {
    if (name.toLowerCase() === "heisenberg"){
        console.log("You're goddamn right")
    }
    else{
        console.log(":gun:")
    }
}

sayMyName("heisenberg");
```

## Clases

Algo muy característico de la OOP son las clases, estas mismas pueden ser utilizadas en `ts`, pero su implementación cambia ligeramente, ya que ademas de que se tienen que declarar los tipos de las propiedades, también se tiene que declarar el tipo de dato que se utilizará en los métodos.

```ts

class CardsDeck {
    conName: string;
    conCardsQty: number;
    conBrand: string;

    constructor(name: string, cardsQty: number, brand: string) {
        this.conName = name;
        this.conCardsQty = cardsQty;
        this.conBrand = brand;
    }

    giveMeOne(max = this.conCardsQty): number {
            let yourCard: number = Math.floor(Math.random() * (max - 1 + 1) + 1); // método para retornar un numero al azar
            return yourCard;
    }
}

const black = new CardsDeck("Samurai", 56, "Bicycle");
    
console.log(black.giveMeOne());
```

Las clases pueden tener sus propiedades con 3 etiquetas, `public` (la que se usa normalmente, pudiendo acceder y modificarlas desde cualquier lado), `private` (solo pueden acceder y modificarse en la misma clase) y por ultimo `protected` (solo pueden acceder y modificarse en la misma clase o cuando viene de una clase padre).

```ts
class Person {
    private conName: string; // Solo en la clase
    public conSurname: string; // Desde cualquier lado
    protected conWorking: boolean; // Solo en la clase y al heredarse

    constructor(name: string, surname: string) {
        this.conName = name;
        this.conSurname = surname;
        this.conWorking = true;
    }

    public getConName(): string {
        return this.conName;
    }
}

class Employee extends Person {
    conId: number;

    constructor(id: number, name: string, surname: string) {
        super(name, surname);
        this.conId = id;
    }

    isWorker(): string {
        if (this.conWorking) {
            return "Es un empleado modelo";
        } else {
            return "No es posible llegar a este error sin modificar el código >:(";
        }
    }
}

let first = new Employee(1523, "Walter", "White");

console.log(first.conName); //ERROR, no se puede acceder desde fuera
console.log(first.getConName()); // Walter
console.log(first.isWorker()); // Es un empleado modelo
```

> Es posible agregar `readonly` para evitar la reasignación de datos (`private readonly conName: string`)

En las clases es posible incluir interfaces con la palabra reservada `implements`.

```ts
interface Character {
    name: string;
    surname: string;
    age: number;
    country?: string;
}

class Person implements Character{
    name: string;
    surname: string;
    age: number; 

    constructor(name: string, surname: string, age: number) {
        this.name = name;
        this.surname = surname;
        this.age = age;
    }

    public getData(): string {
        return `${this.name} ${this.surname}, ${this.age} años`;
    }
}

let first = new Person("Walter", "White", 52);

console.log(first.getData());
```

Es posible crear clases que sirvan unicamente como bases para crear otras bases, a estas se las conoce como `abstract`, y se las implementa nuevamente con el uso de la palabra reservada `extends`.

```ts
abstract class Animal {
    type: string;
    name: string;
    
    constructor(type: string, name: string) {
        this.type = type;
        this.name = name;
    }

    abstract makeNoise(): string;
}

class Cat extends Animal {
    makeNoise(): string {
        return "meow";
    }
}

let white = new Animal("dog", "White"); // ERROR, las clases abstractas no se pueden llamar, solo usar en otras clases
let black = new Cat("feline", "Black");

console.log(black.makeNoise()); // meow
```

## Generic types

Hay veces que necesitamos crear funciones o interfaces bases pero sin tener del todo claro que tipo de datos vamos a usar desde un principio, para eso se utilizan los `generic types`, los cuales sirven para crear tipos que se declararan en su uso y pueden reutilizarse.

```ts
interface savedData<T>{
    name: string;
    id: number;
    data: T;
}

const person1 : savedData<object> = {
    name: "Luci",
    id: 616,
    data: {age: "unknown", status: "alive"}
}
```

> Es posible declarar un tipo default agregando = al generic `<T = string>`

Ademas, es posible declarar los tipos de variables que se pueden usar desde un inicio, evitando poder pasar un tipo indeseado cuando se use.

```ts
interface savedData<T extends object | string> {
    name: string;
    id: number;
    data: T;
}

const person1 : savedData<object> = {
    name: "Lucy",
    id: 616,
    data: {age: "unknown", status: "alive"}
}

const person2 : savedData<string> = {
    name: "white shadow",
    id: 111,
    data: "unknown"
}

const person3 : savedData<number> = {  // ERROR, number no es un tipo que se haya declarado en el generic
    name: "test",
    id: 7357,
    data: 0
}
```

## Selección de datos

Hay veces que necesitamos pasar solamente algunos datos de una interface, sin que todos sean obligatorios, para ello podemos usar la palabra reservada `Partial`, el cual evita que sean obligatorios.

```ts
interface savedData<T> {
    name: string;
    id: number;
    data: T;
}

const person1 : Partial<savedData<object>> = {
    name: "Lucy",
    data: {age: "unknown", status: "alive"} // Falta el ID, pero al ser Partial deja de ser necesario
}
```

Para el efecto contrario se utiliza `Required`.

```ts
interface Person{
    name: string;
    surname: string;
    code?: number;
}

let newPerson : Required<Person> = {
    name: "James",
    surname: "Bond"
} // ERROR, falta code ya que el Required lo convirtió en obligatorio
```

`Record` se utiliza para marcar como deben de ser estructurados los datos que se pasaran a un objeto.

```ts
const errors : Record<number, string> ={
    204: "No content",
    400: "Bad request",
    404: "Not found"
}
```

> También es posible llegar al mismo resultado usando `{[key: number]: string}`

Es posible eliminar un dato necesario de una interface, para ello se utiliza `Omit`, el cual evita usar el valor que se declare en el mismo.

```ts
interface savedData {
    name: string;
    id: number;
    data: object;
}

const person1 : Omit<savedData, "name" | "id" > = {
    name: "Lucy", // ERROR, Omit elimino este valor asi que no puede ser aplicado
    id: 616,  // ERROR, Omit elimino este valor asi que no puede ser aplicado
    data: {age: "unknown", status: "alive"}
}
```

Al contrario de este existe `Pick`, el cual solo declara los valores elegidos.

```ts
interface savedData {
    name: string;
    id: number;
    data: object;
}

const person1 : Pick<savedData, "name"> = {
    name: "Lucy",
    id: 616,  // ERROR, solo se eligió el valor name para declararse
}
```
