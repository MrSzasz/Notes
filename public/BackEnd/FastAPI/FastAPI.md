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

## Configuración de url

Con esto hecho podemos empezar a crear nuestra primer petición básica al servidor, es decir, una petición al directorio raíz. Para eso haremos uso de la clase `app` que creamos anteriormente indicando la respuesta que tendrá de la siguiente manera.

```py
from fastapi import FastAPI

app = FastAPI()

@app.get('/') # Usamos el método GET para la primer request
async def root():
    return "hello world!" # Y devolvemos la respuesta
```

Como podemos ver, tenemos nuestra respuesta a la petición, pero para ver el mismo en funcionamiento debemos levantar el servidor. Esto lo haremos gracias a `uvicorn`, usando la consola de la siguiente manera.

```cmd
uvicorn main:app --reload
```

> uvicorn se instala automáticamente si utilizamos [all] con la instalación de FastAPI, `main` hace referencia al nombre del archivo, `app` de la variable y `--reload` es para que recargue cada vez que hagamos algún cambio.

Ahora podemos dirigirnos a `http://127.0.0.1:8000/` y ver como nos devuelve lo que indicamos anteriormente.

## Routes

Como vimos anteriormente podemos crear una respuesta para la petición del servidor, pero podemos crear respuestas para diferentes request de la siguiente manera.

```py
from fastapi import FastAPI

app = FastAPI()

@app.get('/')
async def root():
    return "hello world!"

@app.get('/users') # Creamos la respuesta de la dirección
async def users():
    return {"name": "John",}
```

Pero esto no es lo correcto a la hora de crear respuestas, ya que las mismas estarían todas en el mismo archivo, lo que nos ayudaría a la hora de mantener todo el código ordenado y limpio, es por eso que lo dividiremos en diferentes rutas, empezando por crear la carpeta llamada `routes`, y dentro de la misma crearemos el archivo llamado `users.py`, el cual usaremos para crear nuestras rutas de usuarios de la siguiente manera.

```py
from fastapi import APIRouter # Importamos APIRouter para crear las rutas

router = APIRouter(prefix='/users') # Y lo usamos pasando la base de la url

@router.get('/') # Esto se traduce en "/users" por el prefix que agregamos anteriormente
async def users():
    return {"name": "John"} 
```

Con esto hecho debemos importarlo en nuestro `main.py` para que lo tome como una ruta valida, quedándonos de la siguiente manera.

```py
from fastapi import FastAPI
from routes import users # Importamos la ruta

app = FastAPI()

app.include_router(users.router) # Y utilizamos el método necesario para validarlo como una ruta

@app.get('/')
async def root():
    return "hello world!"
```

Con esto ya estaría funcionando nuestra nueva ruta, podemos probarla de la misma forma que probamos nuestra ruta anterior, pero con `/users` al final.  
Ademas de esto podemos crear varias rutas para pedir diferentes datos, por ejemplo, podemos crear una ruta para recibir todos los productos de una base de datos, para ello crearemos el archivo llamado `products.py` dentro de la carpeta `routes`, el cual nos quedará de la siguiente manera.

```py
from fastapi import APIRouter

router = APIRouter(prefix="/products") # Agregamos el prefix correspondiente 

product_list = ["apple", "orange", "banana", "grapes"] # Creamos nuestra lista de productos

@router.get("/")
async def get_products():
    return product_list # Y la devolvemos como respuesta
```

Lo que nos queda por hacer es importar la nueva ruta en el archivo main.

```py
from fastapi import FastAPI
from routes import users, products # Importamos ambas rutas

app = FastAPI()

# Routes

app.include_router(users.router) # Y las configuramos
app.include_router(products.router)

@app.get('/')
async def root():
    return "hello world!"
```

Con esto hecho podemos interactuar con ambas rutas sin la necesidad de crear varias rutas en el mismo archivo, o tener que levantar diferentes servidores por cada una de las llamadas a la API que necesitemos hacer

## Request - GET

Hasta ahora hicimos solamente un request del tipo `GET` a nuestra API, pero no es la única. Para probar esto podemos empezar por agregar una lista de usuarios a nuestro archivo `users.py` con su respectivo modelo, con la cual interactuaremos con los diferentes métodos.

```py
from fastapi import APIRouter
from pydantic import BaseModel # Importamos el modelo

router = APIRouter(prefix='/users')

class User(BaseModel): # Y lo creamos como una clase, con todos los datos que contendrá el mismo
    id: int
    name: str
    last_name: str
    age: int

users_db = [
    {
        "id": 1,
        "name": "John",
        "last_name": "Kuwait",
        "age": 18,
    },
    {
        "id": 2,
        "name": "Stephen",
        "last_name": "Kuwait",
        "age": 59,
    },
    {
        "id": 3,
        "name": "Katherine",
        "last_name": "Kuwait",
        "age": 44,
    },
]


@router.get('/')
async def get_all_users(): # Creamos la función para devolver todos los usuarios
    return users_db
```

Pero `GET` no solamente puede devolver todos los usuarios, sino que también podemos devolver uno solo dependiendo del id que le pasemos por diferentes parámetros, esto podemos hacerlo de diferentes formas, por medio del `body`, por medio de la `query` o por medio del `path`. Para empezar podemos usar el `path` de la siguiente manera.

```py
from fastapi import APIRouter, Request
from pydantic import BaseModel

router = APIRouter(prefix='/users')

class User(BaseModel):
    id: int
    name: str
    last_name: str
    age: int

users_db = [...]

@router.get('/{user_id}') # Indicamos que tomaremos el id como path
async def get_one_user_by_path(user_id: int): # Y le pasamos el tipo de dato que recibirá
    try:
        get_user_from_db = filter(lambda user: user["id"] == user_id, users_db) # Buscamos el usuario en la lista
        return list(get_user_from_db)[0] # Y si se encuentra se devuelve el mismo
    except:
        return "Error! User not found" # Sino devolvemos un mensaje de error
```

> Para probar deberemos ir a `/users/2`, indicando que el id será "2"

El otro método para  el id sería en base a la query del mismo, el cual tomará la misma base, quedándonos de la siguiente manera.

```py
from fastapi import APIRouter
from pydantic import BaseModel

router = APIRouter(prefix='/users')

class User(BaseModel):
    id: int
    name: str
    last_name: str
    age: int

users_db = [...]

@router.get('/')
async def get_user_by_query(user_id: int): # Indicamos la query que se recibirá
    try:
        get_user_from_db = filter(lambda user: user["id"] == user_id, users_db)
        return list(get_user_from_db)[0]
    except:
        return "Error! User not found"
```

> Para probar el funcionamiento deberemos ir a `/users?user_id=3` pasando el id que usaremos

Por ultimo podemos tomar los datos que le pasemos por el body con formato `json` usando el paquete `Request` de `FastAPI` de la siguiente manera.

```py
from fastapi import APIRouter, Request # Importamos el modulo necesario
from pydantic import BaseModel

router = APIRouter(prefix='/users')

class User(BaseModel):
    id: int
    name: str
    last_name: str
    age: int


users_db = [...]

@router.get('/')
async def get_all_users(req: Request): # Tomamos la request con su respectivo tipo
    data = await req.json() # Lo guardamos en una variable esperando por el mismo
    try:
        get_user_from_db = filter(lambda user: user["id"] == data["id"], users_db)
        return list(get_user_from_db)[0]
    except:
        return "Error! User not found"
```

> Para que esto funcione debemos pasar `{"id": 3}` como body de la request

## Referencias

[Curso Python para backend by MoureDev](https://youtu.be/_y9qQZXE24A)

[FastAPI guía oficial](https://fastapi.tiangolo.com/lo/tutorial/)
