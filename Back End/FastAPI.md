# FastAPI

Base on Starlette > a lightweight ASGI(Asynchronous Server Gateway Interface).\
Base on Pydantic > a data validation/management framework.\
Need ASGI server, like Uvicorn or Hypercorn.\
Produce OpenAPI(swagger) and JSON schema document automatically.

https://fastapi.tiangolo.com/alternatives/

# Usage

## Install

    pip install fastapi[all]
    or
    pip install fastapi
    pip install uvicorn[standard]

## first-step

* in main.py

        from fastapi import FastAPI
        app = FastAPI()

        @app.get("/")
        async def root():
        return {"message": "Hello World"}

* start

        uvicorn main:app --reload
    --reload: use in developement enviroment, auto-reload when update code.

* API document\
http://127.0.0.1:8000/docs\
http://127.0.0.1:8000/redoc\
http://127.0.0.1:8000/openapi.json

https://fastapi.tiangolo.com/tutorial/first-steps/

## params

* basic

        from fastapi import FastAPI
        app = FastAPI()

        @app.get("/items/{item_id}")
        async def read_item(item_id: int):
        return {"item_id": item_id}

* pydantic DTO(Data Transfer Object)

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

* Path convertor

        from fastapi import FastAPI

        app = FastAPI()

        @app.get("/files/{file_path:path}")
        async def read_file(file_path: str):
            return {"file_path": file_path}

* query params\
If not default value, the params should be needy.\
http://127.0.0.1:8000/items/?skip=0&limit=10

        from fastapi import FastAPI

        app = FastAPI()

        fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}]

        @app.get("/items/")
        async def read_item(skip: int = 0, limit: int = 10):
            return fake_items_db[skip : skip + limit]

https://fastapi.tiangolo.com/tutorial/path-params/
https://fastapi.tiangolo.com/zh/tutorial/query-params/

## CORS

https://fastapi.tiangolo.com/tutorial/cors/

# Referrence

https://fastapi.tiangolo.com/\
https://github.com/tiangolo/fastapi/tree/22528373bba6a654323de416ad5c867cbadb81bb\
https://www.starlette.io/\
https://www.uvicorn.org/\
https://pydantic-docs.helpmanual.io/