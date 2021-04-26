# FastAPI

Base on Starlette > a lightweight ASGI(Asynchronous Server Gateway Interface).\
Base on Pydantic > a data validation/management framework.\
Need ASGI server, like Uvicorn or Hypercorn.\
Produce OpenAPI(swagger) and JSON schema document automatically.

https://fastapi.tiangolo.com/alternatives/

# Usage

## Install

```bash
pip install fastapi[all]
# or
pip install fastapi
pip install uvicorn[standard]
```

## first step

in main.py

```python
from fastapi import FastAPI
app = FastAPI()

@app.get("/")
async def root():
return {"message": "Hello World"}
```

start\
--reload: use in developement enviroment, auto-reload when update code.

```bash
uvicorn main:app --reload
```

API document\
http://127.0.0.1:8000/docs \
http://127.0.0.1:8000/redoc \
http://127.0.0.1:8000/openapi.json

https://fastapi.tiangolo.com/tutorial/first-steps/

## params

### basic

```python
from fastapi import FastAPI
app = FastAPI()

@app.get("/items/{item_id}")
async def read_item(item_id: int):
return {"item_id": item_id}
```

### pydantic DTO(Data Transfer Object)

```python
from enum import Enum
from fastapi import FastAPI

class ModelName(str, Enum):
    alexnet = "alexnet"
    resnet = "resnet"
    lenet = "lenet"

app = FastAPI()

@app.get("/models/{model_name}")
async def get_model(model_name: ModelName):
if model_name == ModelName.alexnet:
    return {"model_name": model_name, "message": "Deep Learning FTW!"}

if model_name.value == "lenet":
    return {"model_name": model_name, "message": "LeCNN all the images"}

return {"model_name": model_name, "message": "Have some residuals"}
```

### Path convertor

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/files/{file_path:path}")
async def read_file(file_path: str):
    return {"file_path": file_path}
```

### query params
If not default value, the params should be needy.\
http://127.0.0.1:8000/items/?skip=0&limit=10

```python
from fastapi import FastAPI

app = FastAPI()

fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}]

@app.get("/items/")
async def read_item(skip: int = 0, limit: int = 10):
    return fake_items_db[skip : skip + limit]
```

https://fastapi.tiangolo.com/tutorial/path-params/ \
https://fastapi.tiangolo.com/zh/tutorial/query-params/

## Validation

### Query params

Generic validations and metadata:

* alias
* title
* description
* deprecated

Validations specific for strings:

* min_length
* max_length
* regex

```python
from typing import Optional
from fastapi import FastAPI, Query

app = FastAPI()

@app.get("/items/")
async def read_items(
    q: Optional[str] = Query(
        None,
        title="Query string",
        description="Query string for the items to search in the database that have a good match",
        alias="item-query",
        min_length=3,
        max_length=50,
        regex="^fixedquery$"
        )
    ):
    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}
    if q:
        results.update({"q": q})
    return results
```

if deprecated, show in document.

```python
@app.get("/items/")
async def read_items(
    q: Optional[str] = Query(
        None,
        deprecated=True
        )
    ):
    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}
    if q:
        results.update({"q": q})
    return results
```
### Path params

Operator
* gt: greater than
* ge: greater than or equal
* lt: less than
* le: less than or equal

```python
from fastapi import FastAPI, Path

app = FastAPI()

@app.get("/items/{item_id}")
async def read_items(
    *,
    item_id: int = Path(..., title="The ID of the item to get", gt=0, le=1000),
    q: str,
):
    results = {"item_id": item_id}
    if q:
        results.update({"q": q})
    return results
```

Python won't do anything with that *, but it will know that all the following parameters should be called as keyword arguments (key-value pairs), also known as kwargs. Even if they don't have a default value.

https://fastapi.tiangolo.com/tutorial/query-params-str-validations/
https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/

## Request

### Request Body

```python
from typing import Optional
from fastapi import FastAPI
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    description: Optional[str] = None
    price: float
    tax: Optional[float] = None

app = FastAPI()

@app.post("/items/")
async def create_item(item: Item):
    return item
```
### Embed a single body parameter

```python
# item: Item = Body(..., embed=True)
from typing import Optional
from fastapi import Body, FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: Optional[str] = None
    price: float
    tax: Optional[float] = None

@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Item = Body(..., embed=True)):
    results = {"item_id": item_id, "item": item}
    return results

# expect body
{
    "item": {
        "name": "Foo",
        "description": "The pretender",
        "price": 42.0,
        "tax": 3.2
    }
}
# not
{
    "name": "Foo",
    "description": "The pretender",
    "price": 42.0,
    "tax": 3.2
}
```

### Fields

```python
from typing import Optional
from fastapi import Body, FastAPI
from pydantic import BaseModel, Field

app = FastAPI()

class Item(BaseModel):
    name: str
    description: Optional[str] = Field(
        None, title="The description of the item", max_length=300
    )
    price: float = Field(..., gt=0, description="The price must be greater than zero")
    tax: Optional[float] = None


@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Item = Body(..., embed=True)):
    results = {"item_id": item_id, "item": item}
    return results
```

## Response

### Response Model

```python
from typing import Optional
from fastapi import FastAPI
from pydantic import BaseModel, EmailStr

app = FastAPI()

class UserIn(BaseModel):
    username: str
    password: str
    email: EmailStr
    full_name: Optional[str] = None

class UserOut(BaseModel):
    username: str
    email: EmailStr
    full_name: Optional[str] = None

@app.post("/user/", response_model=UserOut)
async def create_user(user: UserIn):
    return user
```

Default value and response_model_exclude_unset 

```python
from typing import List, Optional
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: Optional[str] = None
    price: float
    tax: float = 10.5
    tags: List[str] = []

items = {
    "foo": {"name": "Foo", "price": 50.2},
    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},
    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []},
}

@app.get("/items/{item_id}", response_model=Item, response_model_exclude_unset=True)
async def read_item(item_id: str):
    return items[item_id]
```

response_model_include and response_model_exclude

```python
from typing import Optional
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    description: Optional[str] = None
    price: float
    tax: float = 10.5

items = {
    "foo": {"name": "Foo", "price": 50.2},
    "bar": {"name": "Bar", "description": "The Bar fighters", "price": 62, "tax": 20.2},
    "baz": {
        "name": "Baz",
        "description": "There goes my baz",
        "price": 50.2,
        "tax": 10.5,
    },
}

@app.get(
    "/items/{item_id}/name",
    response_model=Item,
    response_model_include={"name", "description"},
)
async def read_item_name(item_id: str):
    return items[item_id]

@app.get("/items/{item_id}/public", response_model=Item, response_model_exclude={"tax"})
async def read_item_public_data(item_id: str):
    return items[item_id]
```

https://fastapi.tiangolo.com/tutorial/response-model/

## Schema Extra

https://fastapi.tiangolo.com/tutorial/schema-extra-example/

## Middleware

https://fastapi.tiangolo.com/tutorial/middleware/

## CORS

https://fastapi.tiangolo.com/tutorial/cors/

# Referrence

https://fastapi.tiangolo.com/\
https://github.com/tiangolo/fastapi/tree/22528373bba6a654323de416ad5c867cbadb81bb\
https://www.starlette.io/\
https://www.uvicorn.org/\
https://pydantic-docs.helpmanual.io/