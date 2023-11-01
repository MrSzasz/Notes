# Vitest for React Testing

El testing por parte del front para React se puede hacer gracias a [Vitest](https://vitest.dev/), el cual es un framework para testing que nos ayuda a realizar las pruebas necesarias para comprobar el funcionamiento de nuestro código, ya sea probando simples funciones como utilizando diferentes plugins para poder renderizar los componentes del mismo.  

## Guía de Temas

1. [Instalación](#instalaci%C3%B3n)
2. [Código](#coding)
    - [Globales](#globals)
    - [Render](#testing-en-render)
    - [User Interactions](#interacciones-del-usuario)
3. [Testing con UI](#ui-testing)
4. [Fuentes](#fuentes)
5. [Errores](#errores)

---

## Instalación

Para comenzar con el testing deberemos instalar Vitest y jsdom, el cual es el paquete que nos ayudará a renderizar el dom de nuestros componentes, para ello debemos iniciar una consola en nuestro proyecto (para este ejemplo será con NextJs y TypeScript) y usar el siguiente comando para instalar el paquete necesario.

```cmd
npm install vitest jsdom @testing-library/react -D
```

> La flag -D instala el paquete unicamente para desarrollo.

Hecho esto deberemos configurar Vitest, para ello crearemos el archivo `vitest.config.js` en el root de nuestro proyecto, el cual deberá quedar de la siguiente manera.

```js
import { defineConfig } from "vitest/config";

export default defineConfig({
  test: {
    environment: "jsdom"
  },
});
```

Por ultimo debemos configurar el script `test` para que abra Vitest cada vez que lo necesitemos, por lo que deberemos configurar nuestro package.json de la siguiente manera.

```json
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "test": "vitest"
  },
```

Con estas configuraciones básicas ya podremos crear nuestros primeros tests para comprobar que todo funcione.

## Coding

Para probar el funcionamiento de nuestras configuraciones podemos crear un componente simple de React que se encargue de mostrar una prop que le pasemos, quedando el mismo en el directorio `/app/components/CardComponent/CardComponent.tsx` de la siguiente manera.

```tsx
type CardComponentProps = {
  title: string;
};

const CardComponent = ({ title }: CardComponentProps) => {
  return (
    <div>
      <h2>Title: {title}</h2>
    </div>
  );
};

export default CardComponent;
```

Con esto hecho podemos crear el propio test al mismo nivel, llamado `CardComponent.test.tsx`, en el cual crearemos todos nuestros tests relacionado a ese componente en particular. Para comprobar que todo está funcionando podemos crear una función de suma simple y probarla de la siguiente manera.

```tsx
import { describe, expect, test } from "vitest";    // Importamos lo necesario

const add = (a: number, b: number): number => {     // Creamos la función
  return a + b;
};

describe("Test working testing", () => {    // Indicamos el "nombre"
  test("should add two numbers", () => {    // Lo que debería hacer
    const result = add(1, 2);               // Y llamamos a la función, guardando el resultado

    expect(result).toBe(3);         // Indicamos que nos debería llegar como resultado, ya que "toBe" compara con el resultado
  });

  test("should return negative number", () => {     // Indicamos otra instancia de prueba
    const result = add(-10, 2);

    expect(result).toBeLessThan(1);     // E indicamos que el resultado tiene que ser menor a 1
  });
});
```

Hecho esto podemos abrir nuestra consola y escribir el script que creamos anteriormente de la siguiente manera.

```cmd
npm run test
```

> En Visual Studio Code también es posible utiliza `CTRL+K T` para iniciar el test.

Esto nos debería dar como resultado que todos los test pasaron, por lo que podremos ver el funcionamiento del mismo.

## Globals

Cuando tenemos diferentes componentes vamos a tener que importar varias veces las funciones necesarias (`test, expect, etc`), por lo que Vitest nos ayuda a que el código quede mas limpio gracias a la configuración de Globals, el cual permite que utilicemos estos en todos los tests por igual. Para ello debemos agregar estos a `vitest.config.js` de la siguiente manera.

```js
import {
  defineConfig
} from "vitest/config";

export default defineConfig({
  test: {
    environment: "jsdom",
    globals: true
  },
});
```

> Al trabajar con TS debemos cambiar ciertas [configuraciones adicionales](#typescript-no-reconoce-los-tipos)

## Testing en render

Para poder hacer testing de los apartados del render del componente haremos uso del paquete de testing en React que instalamos anteriormente, para ello debemos importar la función de render en nuestro test, junto al componente de la siguiente manera.

```tsx
import { render, screen } from "@testing-library/react";  // Importamos las funciones
import CardComponent from "./CardComponent";    // Y los componentes que utilizaremos

describe("Card Component", () => {
  test("should render the title", () => {     // Indicamos la descripción del test
    render(<CardComponent title="hello" />);  // Y hacemos un render indicando el titulo

    expect(screen.getByText("hello")).toBeDefined();    // Por ultimo lo buscamos en el componente
  });
});
```

Con este test podemos comprobar que un texto puntual que pasemos se esté renderizando correctamente, ya que lo busca en el componente. También podemos buscar lo contrario, es decir, que no se encuentre el mismo, utilizando `toBeNull()` con las mismas bases.

```tsx
import { render, screen } from "@testing-library/react";
import CardComponent from "./CardComponent";  

describe("Card Component", () => {
  test("should render the title", () => {     
    render(<CardComponent title="hello" />);  

    expect(screen.getByText("hello")).toBeDefined();    
  });

  test("shouldn't render 'test'", () => {    
    render(<CardComponent title="hello" />); 

    expect(screen.queryByText(/test/i)).toBeNull();    // Indicamos que busque el texto pero que no exista
  });
});
```

## Interacciones del usuario

También podemos simular los clicks de un usuario, para ello haremos uso de la función `fireEvent` y el método correspondiente al click, pero para ello debemos cambiar un poco nuestro componente. Podemos agregar un botón y un estado que nos muestre un nombre que le pasemos como prop unicamente cuando hacemos click en el botón, por lo que nuestro componente final quedaría de la siguiente manera.

```tsx
import { useState } from "react";   // Importamos lo necesario

type CardComponentProps = {
  title: string;
  name: string;     // Creamos el type para el prop
};

const CardComponent = ({ title, name }: CardComponentProps) => {
  const [visibleAuthor, setVisibleAuthor] = useState<Boolean>(false);   // Creamos el estado iniciándolo en false

  const showAuthor = (): void => {      // Creamos la función para cambiar el estado
    setVisibleAuthor((current) => !current);  // Utilizando el estado actual por el contrario
  };

  return (
    <div>
      <h2>{title}</h2>
      <div>
        {visibleAuthor && <h3>Author: {name}</h3>}    {/* Indicamos que solamente se muestre si es true */}
        <button onClick={showAuthor}>Show</button>    {/* E indicamos que el botón cambiará el estado */}
      </div>
    </div>
  );
};

export default CardComponent;
```

Con esto hecho podemos agregar 3 nuevos tests, que no se muestre el nombre al montarse el componente, que se muestre al hacer click y que se oculte al hacer click otra vez, quedando todos los tests de la siguiente manera.

```tsx
import { fireEvent, render, screen } from "@testing-library/react";
import CardComponent from "./CardComponent";

describe("Card Component", () => {

  beforeEach(() => {              // Indicamos que se tiene que hacer antes de cada test
    render(<CardComponent title="hello" name="Leo" />);   // Es decir, renderizar el componente
  });

  test("should render the title", () => {
    expect(screen.getByText("hello")).toBeDefined();
  });

  test("shouldn't render 'test'", () => {
    render(<CardComponent title="hello" name="leo" />);

    expect(screen.queryByText(/test/i)).toBeNull();
  });

  test("shouldn't render the name on start", () => {    // Indicamos que no tiene que existir al primer render ya que está oculto
    expect(screen.queryByText(/Leo/i)).toBeNull();
  });

  test("should render the name on click", () => {     // Indicamos que debería mostrarse después de un click
    const button = screen.getByText(/Show/i);         // Por lo que buscamos el componente del botón y lo guardamos como una variable

    fireEvent.click(button);    // Utilizamos fireEvent para indicar que se dará un click

    expect(screen.queryByText(/Leo/i)).toBeDefined();     // Y buscamos el texto correspondiente
  });

  test("should render the name on click and hide it on 2nd click", () => {    // Por ultimo indicamos el test para que se oculte
    const button = screen.getByText(/Show/i);

    fireEvent.click(button);    // Damos un primer click

    expect(screen.queryByText(/Leo/i)).toBeDefined();     // Volvemos a comprobar el texto 

    fireEvent.click(button);    // Luego debería ocultarse el texto con el 2do click

    expect(screen.queryByText(/Leo/i)).toBeNull();    // Por lo que buscamos que no exista
  });
});
```

Con estos simples tests tenemos comprobado el funcionamiento base de nuestro componente, desde el inicio hasta la interacción del mismo con el usuario final.

## UI Testing

Vitest nos proporciona un paquete que puede agilizar el testing, ya que nos genera una UI en la que podemos interactuar, podemos ver los test en una lista y a la vez probar cambios directamente en el navegador, para ello debemos instalar el paquete `Vitest UI` de la siguiente manera.

```cmd
npm i @vitest/ui -D
```

Con esto debemos crear (o modificar) un script para pasarle la flag necesaria, quedando en `package.json` de la siguiente manera.

```json
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "test": "vitest",
    "test-ui" : "vitest --ui"
  },
```

Cuando usemos este script se generará una dirección a la cual podemos ir para ver los tests en el mismo, e interactuar cambiando los mismos y volviendo a probar su funcionamiento.

## Fuentes

[Vitest Testing by Fazt Code](https://www.youtube.com/watch?v=Yocj2BB3AQU&list=PLcNjwRlm8ufmw3Ua7x91zGzia7s2MJx0W&index=275)
[Vitest Guide](https://vitest.dev/guide/)
[React Testing Library Guide](https://testing-library.com/docs/)

## Errores

### TypeScript no reconoce los tipos

Para solucionar este error hay que agregar ciertos datos en los archivos de configuraciones, empezando por `vitest.config.js` de la siguiente manera.

```js
/// <reference types="vitest"/>
/// <reference types="Vite/client"/>

import {
  defineConfig
} from "vitest/config";

export default defineConfig({
  test: {
    environment: "jsdom",
    globals: true
  },
});
```

Sumado a eso debemos configurar los tipos en el archivo `tsconfig.json` para que pueda reconocerlo, agregándolo de la siguiente manera.

```ts
{
  "compilerOptions": {
        "types": [
            "vitest/globals" 
        ],
    }
}
```

> Para que funcione se deberá tocar F1 y buscar `TypeScript: Restart TS Server`

### ReferenceError: React is not defined

Para solucionar el error debemos instalar el paquete `@vitejs/plugin-react` con el siguiente comando.

```cmd
npm i @vitejs/plugin-react -D
```

Luego agregar el plugin a nuestra configuración en `vitest.config.js`, quedando el mismo.

```js
/// <reference types="vitest"/>
/// <reference types="Vite/client"/>

import { defineConfig } from "vitest/config";
import react from "@vitejs/plugin-react";


export default defineConfig({
  plugins: [react()],
  test: {
    environment: "jsdom",
    globals: true
  },
});
```
