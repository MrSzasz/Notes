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
    User(id=1,
         name="John",
         last_name="Kuwait",
         age=18,),
    User(id=2,
         name="Stephen",
         last_name="Smith",
         age=48,),
    User(id=3,
         name="Katherine",
         last_name="Powell",
         age=24,),
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

async def search_user_in_db(user_id: int): # Creamos la función que buscará el usuario
    found_user = filter( # Filtramos la lista
            lambda user: user.id == user_id, users_db) # Tomando de base el ID que le pasamos como parámetro
    try:
        return list(found_user)[0] # Si lo encuentra devolvemos el usuario
    except:
        return "Error! User not found" # Sino devolvemos un error

@router.get('/{user_id}') # Indicamos que tomaremos el id como path
async def get_one_user_by_path(user_id: int): # Y le pasamos el tipo de dato que recibirá
    user_in_db = await search_user_in_db(user_id) # Usamos la función para buscar el usuario
    if type(user_in_db) != str: # Si lo encuentra devuelve el usuario
        return user_in_db 
    else:
        return "Error! User not found" # Sino mostramos el error
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

async def search_user_in_db(user_id: int):
    found_user = filter(
            lambda user: user.id == user_id, users_db)
    try:
        return list(found_user)[0]
    except:
        return "Error! User not found"

@router.get('/')
async def get_user_by_query(id: int): # Indicamos la query que se recibirá
    user_in_db = await search_user_in_db(id)
    if type(user_in_db) != str:
        return user_in_db 
    else:
        return "Error! User not found"
```

> Para probar el funcionamiento deberemos ir a `/users?id=3` pasando el id que usaremos

## Request - POST

Podemos agregar un nuevo usuario usando el método POST, el cual comúnmente se utiliza para agregar un nuevo dato en una API, por lo que lo utilizaremos de la siguiente manera.

```py
# [...] => Resto del código

@router.post('/') 
async def create_new_user(user: User): # Indicamos que se pasará un dato tipo User por el body
    user_in_db = await search_user_in_db(user.id) # Buscamos el usuario en la base de datos
    if type(user_in_db) == str: # Si no lo encuentra
        users_db.append(user) # Agrega el usuario a la base de datos
        return user # Y lo devuelve
    else:
        return "Error! User is already in database" # Sino indica que ya se encuentra el usuario
```

## Request - PUT

Con el método PUT podemos editar un elemento de nuestro array, para ello debemos buscar el mismo en la base de datos y reemplazarlo con los datos que se nos envían por medio del body, quedando el mismo de la siguiente manera.

```py
# [...]

async def search_user_index(user_id_for_find): # Creamos la función para buscar el índice
    user_index = [index for index, user_in_db in enumerate(
            users_db) if user_in_db.id == user_id_for_find]
    return user_index[0] # Y retornamos el indice

@router.put('/') # Indicamos el método
async def edit_user(user: User): # Y los datos que recibiremos del body
    user_in_db = await search_user_in_db(user.id) # Buscamos si el usuario se encuentra en la base de datos
    if type(user_in_db) != str: # Si se encuentra
        user_index = await search_user_index(user.id) # Guardamos el indice
        users_db[user_index] = user # Reemplazamos el usuario con los datos que recibimos
        return user # Y retornamos el usuario editado
    else:
        return "User not found" # Si no lo encuentra devolvemos el mensaje de error
```

## Request - DELETE

Por ultimo lo que podemos hacer es utilizar el método DELETE para eliminar un usuario de la base de datos, tomando de base las funciones que creamos anteriormente de la siguiente manera.

```py
# [...]

@router.delete('/{user_id}') # Indicamos el método y el path
async def delete_user(user_id: int):
    user_in_db = await search_user_in_db(user_id) 
    if type(user_in_db) != str:
        user_index = await search_user_index(user_id)
        del users_db[user_index] # Eliminamos el usuario con el indice que encontró
        return "User deleted successfully" # Y devolvemos un mensaje para indicar que se eliminó correctamente
    else:
        return "User not found"
```

## Status codes

Sumado a esto, no solamente deberemos enviar una respuesta de error como string, también debemos indicarle al usuario que tipo de error tuvo por parte del código de estado, para esto usamos los módulos `status` (contiene los códigos de estado más comunes) y `Response` (respuesta que daremos al usuario) por parte de FastAPI de la siguiente manera

```py
from fastapi import APIRouter, status, Response # Importamos los módulos necesarios
from pydantic import BaseModel

# [...] 

#  ==================== Functions ====================

async def search_user_in_db(user_id: int):
    found_user = filter(
        lambda user: user.id == user_id, users_db)
    try:
        return list(found_user)[0]
    except:
        return "Error! User not found"
    
async def search_user_index(user_id_for_find):
    user_index = [index for index, user_in_db in enumerate(
            users_db) if user_in_db.id == user_id_for_find]
    return user_index[0]


#  ==================== Responses ====================

@router.get('/')
async def get_all_users():
    return users_db


@router.get('/{user_id}', status_code=status.HTTP_302_FOUND) # Indicamos el status code que enviaremos si al respuesta fue correcta
async def get_one_user(user_id: int, res : Response): # Utilizamos el módulo para indicar el tipo de respuesta
    user_in_db = await search_user_in_db(user_id)
    if type(user_in_db) != str:
        return user_in_db
    else:
        res.status_code = status.HTTP_404_NOT_FOUND # Y devolvemos la respuesta de que el usuario no fue encontrado
        return "Error! User not found"

# =========================

@router.post('/', status_code=status.HTTP_201_CREATED) # Indicamos la respuesta que indica que se creó el usuario
async def create_new_user(user: User, res: Response):
    user_in_db = await search_user_in_db(user.id)
    if type(user_in_db) == str:
        users_db.append(user)
        return user
    else:
        res.status_code = status.HTTP_409_CONFLICT # O que no se pudo crear por un conflicto
        return "Error! User is already in database"

# =========================

@router.put('/')
async def edit_user(user: User, res: Response):
    user_in_db = await search_user_in_db(user.id)
    if type(user_in_db) != str:
        user_index = await search_user_index(user.id)
        users_db[user_index] = user
        return user
    else:
        res.status_code = status.HTTP_404_NOT_FOUND
        return "User not found"

# =========================

@router.delete('/{user_id}') # Al no indicar nada, se toma de base el código de estado 200
async def delete_user(user_id: int, res: Response):
    user_in_db = await search_user_in_db(user_id)
    if type(user_in_db) != str:
        user_index = await search_user_index(user_id)
        del users_db[user_index]
        return "User deleted successfully"
    else:
        res.status_code = status.HTTP_404_NOT_FOUND
        return "User not found"

# =========================
```

> El modulo `status` nos ayuda a la hora de indicarnos que significa cada código, pudiendo indicar solamente el nombre del estado (NOT FOUND, CREATED, etc) y lo autocompleta con el código correspondiente

## Referencias

[Curso Python para backend by MoureDev](https://youtu.be/_y9qQZXE24A)

[FastAPI guía oficial](https://fastapi.tiangolo.com/lo/tutorial/)
