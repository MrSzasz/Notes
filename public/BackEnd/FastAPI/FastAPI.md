# FastAPI

[FastAPI](https://fastapi.tiangolo.com/lo/) es un framework para Python el cual nos ayuda a la hora de construir entornos backend para nuestros proyectos, siendo uno de los más simples para aprender y aplicar. El mismo es utilizado por empresas como Netflix, Microsoft y Uber para sus servicios, demostrando la practicidad y beneficios que este tiene para lidiar con páginas de alto trafico.

## Guía de Temas

1. [Instalación](#instalaci%C3%B3n)
2. [Configuración](#configuración)

3. [Referencias](#referencias)

---

## Instalación

Para iniciar con FastAPI será necesario crear una carpeta para poder manejar todo nuestro backend, a esta carpeta la llamaremos `api`. Hecho esto desde nuestra consola abriremos la misma e instalaremos los paquetes necesarios de la siguiente manera.

```cmd
pip install "fastapi[all]"
```

Con la flag `[all]` se descargarán todas las dependencias de FastAPI, esto también incluye `uvicorn`, la dependencia que se utiliza para crear y levantar el servidor.  

## Configuración

Lo primero que se deberá hacer para crear código de back es crear un archivo llamado `main.py`, el mismo contendrá toda nuestra lógica de back.  
Para empezar con este debemos configurar el entorno y crear la clase `app` con FastAPI de la siguiente manera.

```py
from fastapi import FastAPI # Importamos fastapi

app = FastAPI() # Creamos la variable para usar en el servidor
```

## Peticiones - Get

Con esto hecho podemos empezar a crear nuestra primer petición básica al servidor, es decir, una petición GET al directorio raíz. Para eso haremos uso de la clase `app` que creamos anteriormente indicando la respuesta que tendrá de la siguiente manera.

```py
from fastapi import FastAPI

app = FastAPI()

@app.get('/')
async def root():
    return "hello world!"
```

Como podemos ver, tenemos nuestra respuesta a la petición, pero para ver el mismo en funcionamiento debemos levantar el servidor. Esto lo haremos gracias a `uvicorn`, usando la consola de la siguiente manera.

```cmd
uvicorn main:app --reload
```

> uvicorn se instala automáticamente si utilizamos [all] con la instalación de FastAPI, `main` hace referencia al nombre del archivo, `app` de la variable y `--reload` es para que recargue cada vez que hagamos algún cambio.

Ahora podemos dirigirnos a `http://127.0.0.1:8000/` y ver como nos devuelve lo que indicamos anteriormente.

## Referencias

[Curso Python para backend by MoureDev](https://youtu.be/_y9qQZXE24A)

[FastAPI guía oficial](https://fastapi.tiangolo.com/lo/tutorial/)
