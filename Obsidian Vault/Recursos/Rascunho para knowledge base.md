
**

# First Steps[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#first-steps)

The simplest FastAPI file could look like this:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/first-steps/#__tabbed_1_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

@app.get("/")

async def root():

    return {"message": "Hello World"}

  

Copy that to a file main.py.

Run the live server:

fastapi dev main.py

  

 FastAPI  Starting development server 🚀

  

            Searching for package file structure from directories

            with __init__.py files

            Importing from /home/user/code/awesomeapp

  

  module  🐍 main.py

  

    code  Importing the FastAPI app object from the module with

            the following code:

  

            from main import app

  

     app  Using import string: main:app

  

  server  Server started at http://127.0.0.1:8000

  server  Documentation at http://127.0.0.1:8000/docs

  

     tip  Running in development mode, for production use:

            fastapi run

  

            Logs:

  

    INFO  Will watch for changes in these directories:

            ['/home/user/code/awesomeapp']

    INFO  Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C

            to quit)

    INFO  Started reloader process [383138] using WatchFiles

    INFO  Started server process [383153]

    INFO  Waiting for application startup.

    INFO  Application startup complete.

  

[restart ↻](https://fastapi.tiangolo.com/tutorial/first-steps/#)

In the output, there's a line with something like:

INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)

  

That line shows the URL where your app is being served, in your local machine.

### Check it[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#check-it)

Open your browser at [http://127.0.0.1:8000](http://127.0.0.1:8000/).

You will see the JSON response as:

{"message": "Hello World"}

  

### Interactive API docs[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#interactive-api-docs)

Now go to [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).

You will see the automatic interactive API documentation (provided by [Swagger UI](https://github.com/swagger-api/swagger-ui)):

![Swagger UI](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_OjjrpdytaCrv49NsQMuUqcb2r4ke_E4Kad9yY3xn79Z3EHptO88oC9VOhLiM7LXZQjzFbjo4k_9FW4f-aaTgHjjejnRZM8pDLV-WcO3o5AM-t-nNkwmNuOHyrfw73lgp6coEGg?key=f9HbvYiRp_Cr6j6NlCUV7A)

### Alternative API docs[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#alternative-api-docs)

And now, go to [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc).

You will see the alternative automatic documentation (provided by [ReDoc](https://github.com/Rebilly/ReDoc)):

![ReDoc](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdcffUe3_YnxeCr_uFFjBBeZvDZvnWHq6MrykwpIAY2l4Fc8vYo3oj3NYl5QzJe2lkH9-sHI6hJPwgoAZfufwIFAAtBR7UcljPzltpth_OYiIaIy343U1Kcr-fYgYuEghnoZH5OAA?key=f9HbvYiRp_Cr6j6NlCUV7A)

### OpenAPI[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#openapi)

FastAPI generates a "schema" with all your API using the OpenAPI standard for defining APIs.

#### "Schema"[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#schema)

A "schema" is a definition or description of something. Not the code that implements it, but just an abstract description.

#### API "schema"[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#api-schema)

In this case, [OpenAPI](https://github.com/OAI/OpenAPI-Specification) is a specification that dictates how to define a schema of your API.

This schema definition includes your API paths, the possible parameters they take, etc.

#### Data "schema"[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#data-schema)

The term "schema" might also refer to the shape of some data, like a JSON content.

In that case, it would mean the JSON attributes, and data types they have, etc.

#### OpenAPI and JSON Schema[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#openapi-and-json-schema)

OpenAPI defines an API schema for your API. And that schema includes definitions (or "schemas") of the data sent and received by your API using JSON Schema, the standard for JSON data schemas.

#### Check the openapi.json[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#check-the-openapijson)

If you are curious about how the raw OpenAPI schema looks like, FastAPI automatically generates a JSON (schema) with the descriptions of all your API.

You can see it directly at: [http://127.0.0.1:8000/openapi.json](http://127.0.0.1:8000/openapi.json).

It will show a JSON starting with something like:

{

    "openapi": "3.1.0",

    "info": {

        "title": "FastAPI",

        "version": "0.1.0"

    },

    "paths": {

        "/items/": {

            "get": {

                "responses": {

                    "200": {

                        "description": "Successful Response",

                        "content": {

                            "application/json": {

  
  
  

...

  

#### What is OpenAPI for[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#what-is-openapi-for)

The OpenAPI schema is what powers the two interactive documentation systems included.

And there are dozens of alternatives, all based on OpenAPI. You could easily add any of those alternatives to your application built with FastAPI.

You could also use it to generate code automatically, for clients that communicate with your API. For example, frontend, mobile or IoT applications.

## Recap, step by step[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#recap-step-by-step)

### Step 1: import FastAPI[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#step-1-import-fastapi)

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/first-steps/#__tabbed_2_1)

from fastapi import FastAPI

  

  

app = FastAPI()

  
  

@app.get("/")

async def root():

    return {"message": "Hello World"}

  

FastAPI is a Python class that provides all the functionality for your API.

Technical Details

FastAPI is a class that inherits directly from Starlette.

You can use all the [Starlette](https://www.starlette.io/) functionality with FastAPI too.

### Step 2: create a FastAPI "instance"[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#step-2-create-a-fastapi-instance)

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/first-steps/#__tabbed_3_1)

from fastapi import FastAPI

  

  

app = FastAPI()

  

  
  

@app.get("/")

async def root():

    return {"message": "Hello World"}

  

Here the app variable will be an "instance" of the class FastAPI.

This will be the main point of interaction to create all your API.

### Step 3: create a path operation[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#step-3-create-a-path-operation)

#### Path[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#path)

"Path" here refers to the last part of the URL starting from the first /.

So, in a URL like:

https://example.com/items/foo

  

...the path would be:

/items/foo

  

Info

A "path" is also commonly called an "endpoint" or a "route".

While building an API, the "path" is the main way to separate "concerns" and "resources".

#### Operation[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#operation)

"Operation" here refers to one of the HTTP "methods".

One of:

- POST
    
- GET
    
- PUT
    
- DELETE
    

...and the more exotic ones:

- OPTIONS
    
- HEAD
    
- PATCH
    
- TRACE
    

In the HTTP protocol, you can communicate to each path using one (or more) of these "methods".

---

When building APIs, you normally use these specific HTTP methods to perform a specific action.

Normally you use:

- POST: to create data.
    
- GET: to read data.
    
- PUT: to update data.
    
- DELETE: to delete data.
    

So, in OpenAPI, each of the HTTP methods is called an "operation".

We are going to call them "operations" too.

#### Define a path operation decorator[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#define-a-path-operation-decorator)

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/first-steps/#__tabbed_4_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

  

@app.get("/")

  

async def root():

    return {"message": "Hello World"}

  

The @app.get("/") tells FastAPI that the function right below is in charge of handling requests that go to:

- the path /
    
- using a get operation
    

@decorator Info

That @something syntax in Python is called a "decorator".

You put it on top of a function. Like a pretty decorative hat (I guess that's where the term came from).

A "decorator" takes the function below and does something with it.

In our case, this decorator tells FastAPI that the function below corresponds to the path / with an operation get.

It is the "path operation decorator".

You can also use the other operations:

- @app.post()
    
- @app.put()
    
- @app.delete()
    

And the more exotic ones:

- @app.options()
    
- @app.head()
    
- @app.patch()
    
- @app.trace()
    

Tip

You are free to use each operation (HTTP method) as you wish.

FastAPI doesn't enforce any specific meaning.

The information here is presented as a guideline, not a requirement.

For example, when using GraphQL you normally perform all the actions using only POST operations.

### Step 4: define the path operation function[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#step-4-define-the-path-operation-function)

This is our "path operation function":

- path: is /.
    
- operation: is get.
    
- function: is the function below the "decorator" (below @app.get("/")).
    

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/first-steps/#__tabbed_5_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

@app.get("/")

  

async def root():

  

   return {"message": "Hello World"}

  

This is a Python function.

It will be called by FastAPI whenever it receives a request to the URL "/" using a GET operation.

In this case, it is an async function.

---

You could also define it as a normal function instead of async def:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/first-steps/#__tabbed_6_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

@app.get("/")

  

def root():

  

   return {"message": "Hello World"}

  

Note

If you don't know the difference, check the [Async: "In a hurry?"](https://fastapi.tiangolo.com/async/#in-a-hurry).

### Step 5: return the content[¶](https://fastapi.tiangolo.com/tutorial/first-steps/#step-5-return-the-content)

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/first-steps/#__tabbed_7_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

@app.get("/")

async def root():

  

   return {"message": "Hello World"}

  

You can return a dict, list, singular values as str, int, etc.

You can also return Pydantic models (you'll see more about that later).

There are many other objects and models that will be automatically converted to JSON (including ORMs, etc). Try using your favorite ones, it's highly probable that they are already supported.

# Path Parameters[¶](https://fastapi.tiangolo.com/tutorial/path-params/#path-parameters)

You can declare path "parameters" or "variables" with the same syntax used by Python format strings:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_1_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

  

@app.get("/items/{item_id}")

  

async def read_item(item_id):

  

   return {"item_id": item_id}

  

The value of the path parameter item_id will be passed to your function as the argument item_id.

So, if you run this example and go to [http://127.0.0.1:8000/items/foo](http://127.0.0.1:8000/items/foo), you will see a response of:

{"item_id":"foo"}

  

## Path parameters with types[¶](https://fastapi.tiangolo.com/tutorial/path-params/#path-parameters-with-types)

You can declare the type of a path parameter in the function, using standard Python type annotations:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_2_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

  

async def read_item(item_id: int):

  

   return {"item_id": item_id}

  

In this case, item_id is declared to be an int.

Check

This will give you editor support inside of your function, with error checks, completion, etc.

## Data conversion[¶](https://fastapi.tiangolo.com/tutorial/path-params/#data-conversion)

If you run this example and open your browser at [http://127.0.0.1:8000/items/3](http://127.0.0.1:8000/items/3), you will see a response of:

{"item_id":3}

  

Check

Notice that the value your function received (and returned) is 3, as a Python int, not a string "3".

So, with that type declaration, FastAPI gives you automatic request "parsing".

## Data validation[¶](https://fastapi.tiangolo.com/tutorial/path-params/#data-validation)

But if you go to the browser at [http://127.0.0.1:8000/items/foo](http://127.0.0.1:8000/items/foo), you will see a nice HTTP error of:

{

  "detail": [

    {

      "type": "int_parsing",

      "loc": [

        "path",

        "item_id"

      ],

      "msg": "Input should be a valid integer, unable to parse string as an integer",

      "input": "foo",

      "url": "https://errors.pydantic.dev/2.1/v/int_parsing"

    }

  ]

}

  

because the path parameter item_id had a value of "foo", which is not an int.

The same error would appear if you provided a float instead of an int, as in: [http://127.0.0.1:8000/items/4.2](http://127.0.0.1:8000/items/4.2)

Check

So, with the same Python type declaration, FastAPI gives you data validation.

Notice that the error also clearly states exactly the point where the validation didn't pass.

This is incredibly helpful while developing and debugging code that interacts with your API.

## Documentation[¶](https://fastapi.tiangolo.com/tutorial/path-params/#documentation)

And when you open your browser at [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs), you will see an automatic, interactive, API documentation like:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfp8V-XeUWJDER6SbbQ-loaD9SvbmdtZojGJTTTtkS1mZKetZonQJ-n3EITwJbNlZbtOExdR77JAlLcydTYEws3u3Tw7ai-pUGHJhbR-iIZdQRc8vsCzYEikgmQnonH7dEKFGAYfg?key=f9HbvYiRp_Cr6j6NlCUV7A)

Check

Again, just with that same Python type declaration, FastAPI gives you automatic, interactive documentation (integrating Swagger UI).

Notice that the path parameter is declared to be an integer.

## Standards-based benefits, alternative documentation[¶](https://fastapi.tiangolo.com/tutorial/path-params/#standards-based-benefits-alternative-documentation)

And because the generated schema is from the [OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.1.0.md) standard, there are many compatible tools.

Because of this, FastAPI itself provides an alternative API documentation (using ReDoc), which you can access at [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc):

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXejy1WWqpxOzHktBLaPuzzHDjQ6cXd_i8292fUNP3sMrz88CMfwBYswz7LnAIx6rkj_W-HeSbq57gPdpJrZYZAq2hYDfASJdSAWaHjDWKQyTNTgBCbfk-CJW5Bg9Fbz0WpFKQrJ?key=f9HbvYiRp_Cr6j6NlCUV7A)

The same way, there are many compatible tools. Including code generation tools for many languages.

## Pydantic[¶](https://fastapi.tiangolo.com/tutorial/path-params/#pydantic)

All the data validation is performed under the hood by [Pydantic](https://docs.pydantic.dev/), so you get all the benefits from it. And you know you are in good hands.

You can use the same type declarations with str, float, bool and many other complex data types.

Several of these are explored in the next chapters of the tutorial.

## Order matters[¶](https://fastapi.tiangolo.com/tutorial/path-params/#order-matters)

When creating path operations, you can find situations where you have a fixed path.

Like /users/me, let's say that it's to get data about the current user.

And then you can also have a path /users/{user_id} to get data about a specific user by some user ID.

Because path operations are evaluated in order, you need to make sure that the path for /users/me is declared before the one for /users/{user_id}:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_3_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

  

@app.get("/users/me")

  

async def read_user_me():

    return {"user_id": "the current user"}

  
  

  

@app.get("/users/{user_id}")

  

async def read_user(user_id: str):

    return {"user_id": user_id}

  

Otherwise, the path for /users/{user_id} would match also for /users/me, "thinking" that it's receiving a parameter user_id with a value of "me".

Similarly, you cannot redefine a path operation:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_4_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

  

@app.get("/users")

  

async def read_users():

    return ["Rick", "Morty"]

  
  

  

@app.get("/users")

  

async def read_users2():

    return ["Bean", "Elfo"]

  

The first one will always be used since the path matches first.

## Predefined values[¶](https://fastapi.tiangolo.com/tutorial/path-params/#predefined-values)

If you have a path operation that receives a path parameter, but you want the possible valid path parameter values to be predefined, you can use a standard Python Enum.

### Create an Enum class[¶](https://fastapi.tiangolo.com/tutorial/path-params/#create-an-enum-class)

Import Enum and create a sub-class that inherits from str and from Enum.

By inheriting from str the API docs will be able to know that the values must be of type string and will be able to render correctly.

Then create class attributes with fixed values, which will be the available valid values:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_5_1)

from enum import Enum

  

  

from fastapi import FastAPI

  
  

  

class ModelName(str, Enum):

  

   alexnet = "alexnet"

  

   resnet = "resnet"

  

   lenet = "lenet"

  

  
  

app = FastAPI()

  
  

@app.get("/models/{model_name}")

async def get_model(model_name: ModelName):

    if model_name is ModelName.alexnet:

        return {"model_name": model_name, "message": "Deep Learning FTW!"}

  

    if model_name.value == "lenet":

        return {"model_name": model_name, "message": "LeCNN all the images"}

  

    return {"model_name": model_name, "message": "Have some residuals"}

  

Info

[Enumerations (or enums) are available in Python](https://docs.python.org/3/library/enum.html) since version 3.4.

Tip

If you are wondering, "AlexNet", "ResNet", and "LeNet" are just names of Machine Learning models.

### Declare a path parameter[¶](https://fastapi.tiangolo.com/tutorial/path-params/#declare-a-path-parameter)

Then create a path parameter with a type annotation using the enum class you created (ModelName):

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_6_1)

from enum import Enum

  

from fastapi import FastAPI

  
  

class ModelName(str, Enum):

    alexnet = "alexnet"

    resnet = "resnet"

    lenet = "lenet"

  
  

app = FastAPI()

  
  

@app.get("/models/{model_name}")

  

async def get_model(model_name: ModelName):

  

   if model_name is ModelName.alexnet:

        return {"model_name": model_name, "message": "Deep Learning FTW!"}

  

    if model_name.value == "lenet":

        return {"model_name": model_name, "message": "LeCNN all the images"}

  

    return {"model_name": model_name, "message": "Have some residuals"}

  

### Check the docs[¶](https://fastapi.tiangolo.com/tutorial/path-params/#check-the-docs)

Because the available values for the path parameter are predefined, the interactive docs can show them nicely:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfnYnsECBAh0TKWsAK-IJEdcXbmhAPs06rPax2bEqEC1oF4FEJHp4WxJ1zo5Ka92y3dirQuB0_dOAre6aZHjJ8DqFw-i0fWGjLm27hsD8qpLBwmaEX_uf0mvBYnKSV6NNiczCQsCQ?key=f9HbvYiRp_Cr6j6NlCUV7A)

### Working with Python enumerations[¶](https://fastapi.tiangolo.com/tutorial/path-params/#working-with-python-enumerations)

The value of the path parameter will be an enumeration member.

#### Compare enumeration members[¶](https://fastapi.tiangolo.com/tutorial/path-params/#compare-enumeration-members)

You can compare it with the enumeration member in your created enum ModelName:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_7_1)

from enum import Enum

  

from fastapi import FastAPI

  
  

class ModelName(str, Enum):

    alexnet = "alexnet"

    resnet = "resnet"

    lenet = "lenet"

  
  

app = FastAPI()

  
  

@app.get("/models/{model_name}")

async def get_model(model_name: ModelName):

  

   if model_name is ModelName.alexnet:

  

       return {"model_name": model_name, "message": "Deep Learning FTW!"}

  

    if model_name.value == "lenet":

        return {"model_name": model_name, "message": "LeCNN all the images"}

  

    return {"model_name": model_name, "message": "Have some residuals"}

  

#### Get the enumeration value[¶](https://fastapi.tiangolo.com/tutorial/path-params/#get-the-enumeration-value)

You can get the actual value (a str in this case) using model_name.value, or in general, your_enum_member.value:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_8_1)

from enum import Enum

  

from fastapi import FastAPI

  
  

class ModelName(str, Enum):

    alexnet = "alexnet"

    resnet = "resnet"

    lenet = "lenet"

  
  

app = FastAPI()

  
  

@app.get("/models/{model_name}")

async def get_model(model_name: ModelName):

    if model_name is ModelName.alexnet:

        return {"model_name": model_name, "message": "Deep Learning FTW!"}

  

  

   if model_name.value == "lenet":

  

       return {"model_name": model_name, "message": "LeCNN all the images"}

  

    return {"model_name": model_name, "message": "Have some residuals"}

  

Tip

You could also access the value "lenet" with ModelName.lenet.value.

#### Return enumeration members[¶](https://fastapi.tiangolo.com/tutorial/path-params/#return-enumeration-members)

You can return enum members from your path operation, even nested in a JSON body (e.g. a dict).

They will be converted to their corresponding values (strings in this case) before returning them to the client:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_9_1)

from enum import Enum

  

from fastapi import FastAPI

  
  

class ModelName(str, Enum):

    alexnet = "alexnet"

    resnet = "resnet"

    lenet = "lenet"

  
  

app = FastAPI()

  
  

@app.get("/models/{model_name}")

async def get_model(model_name: ModelName):

    if model_name is ModelName.alexnet:

  

       return {"model_name": model_name, "message": "Deep Learning FTW!"}

  

  

    if model_name.value == "lenet":

  

       return {"model_name": model_name, "message": "LeCNN all the images"}

  

  

  

   return {"model_name": model_name, "message": "Have some residuals"}

  

In your client you will get a JSON response like:

{

  "model_name": "alexnet",

  "message": "Deep Learning FTW!"

}

  

## Path parameters containing paths[¶](https://fastapi.tiangolo.com/tutorial/path-params/#path-parameters-containing-paths)

Let's say you have a path operation with a path /files/{file_path}.

But you need file_path itself to contain a path, like home/johndoe/myfile.txt.

So, the URL for that file would be something like: /files/home/johndoe/myfile.txt.

### OpenAPI support[¶](https://fastapi.tiangolo.com/tutorial/path-params/#openapi-support)

OpenAPI doesn't support a way to declare a path parameter to contain a path inside, as that could lead to scenarios that are difficult to test and define.

Nevertheless, you can still do it in FastAPI, using one of the internal tools from Starlette.

And the docs would still work, although not adding any documentation telling that the parameter should contain a path.

### Path convertor[¶](https://fastapi.tiangolo.com/tutorial/path-params/#path-convertor)

Using an option directly from Starlette you can declare a path parameter containing a path using a URL like:

/files/{file_path:path}

  

In this case, the name of the parameter is file_path, and the last part, :path, tells it that the parameter should match any path.

So, you can use it with:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-params/#__tabbed_10_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

  

@app.get("/files/{file_path:path}")

  

async def read_file(file_path: str):

    return {"file_path": file_path}

  

Tip

You could need the parameter to contain /home/johndoe/myfile.txt, with a leading slash (/).

In that case, the URL would be: /files//home/johndoe/myfile.txt, with a double slash (//) between files and home.

## Recap[¶](https://fastapi.tiangolo.com/tutorial/path-params/#recap)

With FastAPI, by using short, intuitive and standard Python type declarations, you get:

- Editor support: error checks, autocompletion, etc.
    
- Data "parsing"
    
- Data validation
    
- API annotation and automatic documentation
    

And you only have to declare them once.

That's probably the main visible advantage of FastAPI compared to alternative frameworks (apart from the raw performance).

# Query Parameters[¶](https://fastapi.tiangolo.com/tutorial/query-params/#query-parameters)

When you declare other function parameters that are not part of the path parameters, they are automatically interpreted as "query" parameters.

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/query-params/#__tabbed_1_1)

from fastapi import FastAPI

  

app = FastAPI()

  

fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}]

  
  

@app.get("/items/")

  

async def read_item(skip: int = 0, limit: int = 10):

  

   return fake_items_db[skip : skip + limit]

  

The query is the set of key-value pairs that go after the ? in a URL, separated by & characters.

For example, in the URL:

http://127.0.0.1:8000/items/?skip=0&limit=10

  

...the query parameters are:

- skip: with a value of 0
    
- limit: with a value of 10
    

As they are part of the URL, they are "naturally" strings.

But when you declare them with Python types (in the example above, as int), they are converted to that type and validated against it.

All the same process that applied for path parameters also applies for query parameters:

- Editor support (obviously)
    
- Data "parsing"
    
- Data validation
    
- Automatic documentation
    

## Defaults[¶](https://fastapi.tiangolo.com/tutorial/query-params/#defaults)

As query parameters are not a fixed part of a path, they can be optional and can have default values.

In the example above they have default values of skip=0 and limit=10.

So, going to the URL:

http://127.0.0.1:8000/items/

  

would be the same as going to:

http://127.0.0.1:8000/items/?skip=0&limit=10

  

But if you go to, for example:

http://127.0.0.1:8000/items/?skip=20

  

The parameter values in your function will be:

- skip=20: because you set it in the URL
    
- limit=10: because that was the default value
    

## Optional parameters[¶](https://fastapi.tiangolo.com/tutorial/query-params/#optional-parameters)

The same way, you can declare optional query parameters, by setting their default to None:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params/#__tabbed_2_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

  

async def read_item(item_id: str, q: str | None = None):

  

   if q:

        return {"item_id": item_id, "q": q}

    return {"item_id": item_id}

  

🤓 Other versions and variants

In this case, the function parameter q will be optional, and will be None by default.

Check

Also notice that FastAPI is smart enough to notice that the path parameter item_id is a path parameter and q is not, so, it's a query parameter.

## Query parameter type conversion[¶](https://fastapi.tiangolo.com/tutorial/query-params/#query-parameter-type-conversion)

You can also declare bool types, and they will be converted:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params/#__tabbed_4_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

  

async def read_item(item_id: str, q: str | None = None, short: bool = False):

  

   item = {"item_id": item_id}

    if q:

        item.update({"q": q})

    if not short:

        item.update(

            {"description": "This is an amazing item that has a long description"}

        )

    return item

  

🤓 Other versions and variants

In this case, if you go to:

http://127.0.0.1:8000/items/foo?short=1

  

or

http://127.0.0.1:8000/items/foo?short=True

  

or

http://127.0.0.1:8000/items/foo?short=true

  

or

http://127.0.0.1:8000/items/foo?short=on

  

or

http://127.0.0.1:8000/items/foo?short=yes

  

or any other case variation (uppercase, first letter in uppercase, etc), your function will see the parameter short with a bool value of True. Otherwise as False.

## Multiple path and query parameters[¶](https://fastapi.tiangolo.com/tutorial/query-params/#multiple-path-and-query-parameters)

You can declare multiple path parameters and query parameters at the same time, FastAPI knows which is which.

And you don't have to declare them in any specific order.

They will be detected by name:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params/#__tabbed_6_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

  

@app.get("/users/{user_id}/items/{item_id}")

  

async def read_user_item(

  

   user_id: int, item_id: str, q: str | None = None, short: bool = False

  

):

    item = {"item_id": item_id, "owner_id": user_id}

    if q:

        item.update({"q": q})

    if not short:

        item.update(

            {"description": "This is an amazing item that has a long description"}

        )

    return item

  

🤓 Other versions and variants

## Required query parameters[¶](https://fastapi.tiangolo.com/tutorial/query-params/#required-query-parameters)

When you declare a default value for non-path parameters (for now, we have only seen query parameters), then it is not required.

If you don't want to add a specific value but just make it optional, set the default as None.

But when you want to make a query parameter required, you can just not declare any default value:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/query-params/#__tabbed_8_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

  

@app.get("/items/{item_id}")

  

async def read_user_item(item_id: str, needy: str):

  

   item = {"item_id": item_id, "needy": needy}

    return item

  

Here the query parameter needy is a required query parameter of type str.

If you open in your browser a URL like:

http://127.0.0.1:8000/items/foo-item

  

...without adding the required parameter needy, you will see an error like:

{

  "detail": [

    {

      "type": "missing",

      "loc": [

        "query",

        "needy"

      ],

      "msg": "Field required",

      "input": null,

      "url": "https://errors.pydantic.dev/2.1/v/missing"

    }

  ]

}

  

As needy is a required parameter, you would need to set it in the URL:

http://127.0.0.1:8000/items/foo-item?needy=sooooneedy

  

...this would work:

{

    "item_id": "foo-item",

    "needy": "sooooneedy"

}

  

And of course, you can define some parameters as required, some as having a default value, and some entirely optional:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params/#__tabbed_9_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

async def read_user_item(

  

   item_id: str, needy: str, skip: int = 0, limit: int | None = None

  

):

    item = {"item_id": item_id, "needy": needy, "skip": skip, "limit": limit}

    return item

  

🤓 Other versions and variants

In this case, there are 3 query parameters:

- needy, a required str.
    
- skip, an int with a default value of 0.
    
- limit, an optional int.
    

# Request Body[¶](https://fastapi.tiangolo.com/tutorial/body/#request-body)

When you need to send data from a client (let's say, a browser) to your API, you send it as a request body.

A request body is data sent by the client to your API. A response body is the data your API sends to the client.

Your API almost always has to send a response body. But clients don't necessarily need to send request bodies all the time, sometimes they only request a path, maybe with some query parameters, but don't send a body.

To declare a request body, you use [Pydantic](https://docs.pydantic.dev/) models with all their power and benefits.

Info

To send data, you should use one of: POST (the more common), PUT, DELETE or PATCH.

Sending a body with a GET request has an undefined behavior in the specifications, nevertheless, it is supported by FastAPI, only for very complex/extreme use cases.

As it is discouraged, the interactive docs with Swagger UI won't show the documentation for the body when using GET, and proxies in the middle might not support it.

## Import Pydantic's BaseModel[¶](https://fastapi.tiangolo.com/tutorial/body/#import-pydantics-basemodel)

First, you need to import BaseModel from pydantic:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body/#__tabbed_1_1)

from fastapi import FastAPI

  

from pydantic import BaseModel

  

  
  

class Item(BaseModel):

    name: str

    description: str | None = None

    price: float

    tax: float | None = None

  
  

app = FastAPI()

  
  

@app.post("/items/")

async def create_item(item: Item):

    return item

  

🤓 Other versions and variants

## Create your data model[¶](https://fastapi.tiangolo.com/tutorial/body/#create-your-data-model)

Then you declare your data model as a class that inherits from BaseModel.

Use standard Python types for all the attributes:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body/#__tabbed_3_1)

from fastapi import FastAPI

from pydantic import BaseModel

  
  

  

class Item(BaseModel):

  

   name: str

  

   description: str | None = None

  

   price: float

  

   tax: float | None = None

  

  
  

app = FastAPI()

  
  

@app.post("/items/")

async def create_item(item: Item):

    return item

  

🤓 Other versions and variants

The same as when declaring query parameters, when a model attribute has a default value, it is not required. Otherwise, it is required. Use None to make it just optional.

For example, this model above declares a JSON "object" (or Python dict) like:

{

    "name": "Foo",

    "description": "An optional description",

    "price": 45.2,

    "tax": 3.5

}

  

...as description and tax are optional (with a default value of None), this JSON "object" would also be valid:

{

    "name": "Foo",

    "price": 45.2

}

  

## Declare it as a parameter[¶](https://fastapi.tiangolo.com/tutorial/body/#declare-it-as-a-parameter)

To add it to your path operation, declare it the same way you declared path and query parameters:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body/#__tabbed_5_1)

from fastapi import FastAPI

from pydantic import BaseModel

  
  

class Item(BaseModel):

    name: str

    description: str | None = None

    price: float

    tax: float | None = None

  
  

app = FastAPI()

  
  

@app.post("/items/")

  

async def create_item(item: Item):

  

   return item

  

🤓 Other versions and variants

...and declare its type as the model you created, Item.

## Results[¶](https://fastapi.tiangolo.com/tutorial/body/#results)

With just that Python type declaration, FastAPI will:

- Read the body of the request as JSON.
    
- Convert the corresponding types (if needed).
    
- Validate the data.
    

- If the data is invalid, it will return a nice and clear error, indicating exactly where and what was the incorrect data.
    

- Give you the received data in the parameter item.
    

- As you declared it in the function to be of type Item, you will also have all the editor support (completion, etc) for all of the attributes and their types.
    

- Generate [JSON Schema](https://json-schema.org/) definitions for your model, you can also use them anywhere else you like if it makes sense for your project.
    
- Those schemas will be part of the generated OpenAPI schema, and used by the automatic documentation UIs.
    

## Automatic docs[¶](https://fastapi.tiangolo.com/tutorial/body/#automatic-docs)

The JSON Schemas of your models will be part of your OpenAPI generated schema, and will be shown in the interactive API docs:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdiC4oPU9a06ayvY_0N-FYxpjNdm0D9Zbr4iopjbahK8T5Os6CtytgC6C9FsZLe2Mk3yjVTych_U6FKmoas8fhnZImSUYtB4yYcaGG6Dg8nyHZW562ii2RU4piyXi-xz3g4NwEsxQ?key=f9HbvYiRp_Cr6j6NlCUV7A)

And will also be used in the API docs inside each path operation that needs them:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdoDXpeMzEx9LCbnCad00CorcWcMWbxNHABMH-WzrVnCv3kHXzKR7wvtqIPdrw-A67VUh5mTP2B53IyrC3iHgxTgRc0ib5QurS0rpb56uK-sFjA-sG-k8GiBvXzWM3xqwuBG85nbw?key=f9HbvYiRp_Cr6j6NlCUV7A)

## Editor support[¶](https://fastapi.tiangolo.com/tutorial/body/#editor-support)

In your editor, inside your function you will get type hints and completion everywhere (this wouldn't happen if you received a dict instead of a Pydantic model):

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcw2CfTOyieMIxU6J8jrG7L-mEuBgG0mB3QbYWlM0kMQSS7kvtw_3pSKJTGkauQd8ZsSfwt_sAcr-NI0q7BUGfycJrx-LxeUsreaynkv5SxQ8uyuH52zQqyMiAKkvLHj1sGNcdQpA?key=f9HbvYiRp_Cr6j6NlCUV7A)

You also get error checks for incorrect type operations:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfpgPhteCRI9rRtF-7iU1bwbMOIY4hXAwMZj-WUIh9pnRj0IBcHLUlIElpPTuprGQkO-dDsA9t4lCFdXQdQ9X-ZDjONFPKJe44E-K3_piU84rluUjtkCqHpIAof8z0Iz29lXdXK?key=f9HbvYiRp_Cr6j6NlCUV7A)

This is not by chance, the whole framework was built around that design.

And it was thoroughly tested at the design phase, before any implementation, to ensure it would work with all the editors.

There were even some changes to Pydantic itself to support this.

The previous screenshots were taken with [Visual Studio Code](https://code.visualstudio.com/).

But you would get the same editor support with [PyCharm](https://www.jetbrains.com/pycharm/) and most of the other Python editors:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe8uH99CAWBVHdEhDZNImL8t8jhEmhmbWwWLhSHTE6sEtX2_MoHvxikLHDI4SEe_lkW5Ma05cTUR17xwJxeEpbSt5tlC-disljqOqXaDSD98eLixqNnZlSqL7VpMt-4MLLx6aNtkg?key=f9HbvYiRp_Cr6j6NlCUV7A)

Tip

If you use [PyCharm](https://www.jetbrains.com/pycharm/) as your editor, you can use the [Pydantic PyCharm Plugin](https://github.com/koxudaxi/pydantic-pycharm-plugin/).

It improves editor support for Pydantic models, with:

- auto-completion
    
- type checks
    
- refactoring
    
- searching
    
- inspections
    

## Use the model[¶](https://fastapi.tiangolo.com/tutorial/body/#use-the-model)

Inside of the function, you can access all the attributes of the model object directly:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body/#__tabbed_7_1)

from fastapi import FastAPI

from pydantic import BaseModel

  
  

class Item(BaseModel):

    name: str

    description: str | None = None

    price: float

    tax: float | None = None

  
  

app = FastAPI()

  
  

@app.post("/items/")

async def create_item(item: Item):

    item_dict = item.dict()

    if item.tax is not None:

        price_with_tax = item.price + item.tax

        item_dict.update({"price_with_tax": price_with_tax})

    return item_dict

  

🤓 Other versions and variants

## Request body + path parameters[¶](https://fastapi.tiangolo.com/tutorial/body/#request-body-path-parameters)

You can declare path parameters and request body at the same time.

FastAPI will recognize that the function parameters that match path parameters should be taken from the path, and that function parameters that are declared to be Pydantic models should be taken from the request body.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body/#__tabbed_9_1)

from fastapi import FastAPI

from pydantic import BaseModel

  
  

class Item(BaseModel):

    name: str

    description: str | None = None

    price: float

    tax: float | None = None

  
  

app = FastAPI()

  
  

  

@app.put("/items/{item_id}")

  

async def update_item(item_id: int, item: Item):

  

   return {"item_id": item_id, **item.dict()}

  

🤓 Other versions and variants

## Request body + path + query parameters[¶](https://fastapi.tiangolo.com/tutorial/body/#request-body-path-query-parameters)

You can also declare body, path and query parameters, all at the same time.

FastAPI will recognize each of them and take the data from the correct place.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body/#__tabbed_11_1)

from fastapi import FastAPI

from pydantic import BaseModel

  
  

class Item(BaseModel):

    name: str

    description: str | None = None

    price: float

    tax: float | None = None

  
  

app = FastAPI()

  
  

@app.put("/items/{item_id}")

  

async def update_item(item_id: int, item: Item, q: str | None = None):

  

   result = {"item_id": item_id, **item.dict()}

    if q:

        result.update({"q": q})

    return result

  

🤓 Other versions and variants

The function parameters will be recognized as follows:

- If the parameter is also declared in the path, it will be used as a path parameter.
    
- If the parameter is of a singular type (like int, float, str, bool, etc) it will be interpreted as a query parameter.
    
- If the parameter is declared to be of the type of a Pydantic model, it will be interpreted as a request body.
    

# Query Parameters and String Validations[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#query-parameters-and-string-validations)

FastAPI allows you to declare additional information and validation for your parameters.

Let's take this application as example:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_1_1)

from fastapi import FastAPI

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: str | None = None):

  

   results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

The query parameter q is of type str | None, that means that it's of type str but could also be None, and indeed, the default value is None, so FastAPI will know it's not required.

Note

FastAPI will know that the value of q is not required because of the default value = None.

Having str | None will allow your editor to give you better support and detect errors.

## Additional validation[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#additional-validation)

We are going to enforce that even though q is optional, whenever it is provided, its length doesn't exceed 50 characters.

### Import Query and Annotated[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#import-query-and-annotated)

To achieve that, first import:

- Query from fastapi
    
- Annotated from typing
    

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_3_1)

from typing import Annotated

  

  

  

from fastapi import FastAPI, Query

  

  

app = FastAPI()

  
  

@app.get("/items/")

async def read_items(q: Annotated[str | None, Query(max_length=50)] = None):

    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

Info

FastAPI added support for Annotated (and started recommending it) in version 0.95.0.

If you have an older version, you would get errors when trying to use Annotated.

Make sure you [Upgrade the FastAPI version](https://fastapi.tiangolo.com/deployment/versions/#upgrading-the-fastapi-versions) to at least 0.95.1 before using Annotated.

## Use Annotated in the type for the q parameter[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#use-annotated-in-the-type-for-the-q-parameter)

Remember I told you before that Annotated can be used to add metadata to your parameters in the [Python Types Intro](https://fastapi.tiangolo.com/python-types/#type-hints-with-metadata-annotations)?

Now it's the time to use it with FastAPI. 🚀

We had this type annotation:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_5_1)

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_5_2)

q: str | None = None

  

What we will do is wrap that with Annotated, so it becomes:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_6_1)

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_6_2)

q: Annotated[str | None] = None

  

Both of those versions mean the same thing, q is a parameter that can be a str or None, and by default, it is None.

Now let's jump to the fun stuff. 🎉

## Add Query to Annotated in the q parameter[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#add-query-to-annotated-in-the-q-parameter)

Now that we have this Annotated where we can put more information (in this case some additional validation), add Query inside of Annotated, and set the parameter max_length to 50:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_7_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: Annotated[str | None, Query(max_length=50)] = None):

  

   results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

Notice that the default value is still None, so the parameter is still optional.

But now, having Query(max_length=50) inside of Annotated, we are telling FastAPI that we want it to have additional validation for this value, we want it to have maximum 50 characters. 😎

Tip

Here we are using Query() because this is a query parameter. Later we will see others like Path(), Body(), Header(), and Cookie(), that also accept the same arguments as Query().

FastAPI will now:

- Validate the data making sure that the max length is 50 characters
    
- Show a clear error for the client when the data is not valid
    
- Document the parameter in the OpenAPI schema path operation (so it will show up in the automatic docs UI)
    

## Alternative (old): Query as the default value[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#alternative-old-query-as-the-default-value)

Previous versions of FastAPI (before 0.95.0) required you to use Query as the default value of your parameter, instead of putting it in Annotated, there's a high chance that you will see code using it around, so I'll explain it to you.

Tip

For new code and whenever possible, use Annotated as explained above. There are multiple advantages (explained below) and no disadvantages. 🍰

This is how you would use Query() as the default value of your function parameter, setting the parameter max_length to 50:

[Python 3.10+ - non-Annotated](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_9_1)

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: str | None = Query(default=None, max_length=50)):

  

   results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

As in this case (without using Annotated) we have to replace the default value None in the function with Query(), we now need to set the default value with the parameter Query(default=None), it serves the same purpose of defining that default value (at least for FastAPI).

So:

q: str | None = Query(default=None)

  

...makes the parameter optional, with a default value of None, the same as:

q: str | None = None

  

But the Query version declares it explicitly as being a query parameter.

Then, we can pass more parameters to Query. In this case, the max_length parameter that applies to strings:

q: str | None = Query(default=None, max_length=50)

  

This will validate the data, show a clear error when the data is not valid, and document the parameter in the OpenAPI schema path operation.

### Query as the default value or in Annotated[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#query-as-the-default-value-or-in-annotated)

Keep in mind that when using Query inside of Annotated you cannot use the default parameter for Query.

Instead, use the actual default value of the function parameter. Otherwise, it would be inconsistent.

For example, this is not allowed:

q: Annotated[str, Query(default="rick")] = "morty"

  

...because it's not clear if the default value should be "rick" or "morty".

So, you would use (preferably):

q: Annotated[str, Query()] = "rick"

  

...or in older code bases you will find:

q: str = Query(default="rick")

  

### Advantages of Annotated[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#advantages-of-annotated)

Using Annotated is recommended instead of the default value in function parameters, it is better for multiple reasons. 🤓

The default value of the function parameter is the actual default value, that's more intuitive with Python in general. 😌

You could call that same function in other places without FastAPI, and it would work as expected. If there's a required parameter (without a default value), your editor will let you know with an error, Python will also complain if you run it without passing the required parameter.

When you don't use Annotated and instead use the (old) default value style, if you call that function without FastAPI in other places, you have to remember to pass the arguments to the function for it to work correctly, otherwise the values will be different from what you expect (e.g. QueryInfo or something similar instead of str). And your editor won't complain, and Python won't complain running that function, only when the operations inside error out.

Because Annotated can have more than one metadata annotation, you could now even use the same function with other tools, like [Typer](https://typer.tiangolo.com/). 🚀

## Add more validations[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#add-more-validations)

You can also add a parameter min_length:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_11_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

async def read_items(

  

   q: Annotated[str | None, Query(min_length=3, max_length=50)] = None,

  

):

    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

## Add regular expressions[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#add-regular-expressions)

You can define a regular expression pattern that the parameter should match:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_13_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

async def read_items(

    q: Annotated[

  

       str | None, Query(min_length=3, max_length=50, pattern="^fixedquery$")

  

   ] = None,

):

    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

This specific regular expression pattern checks that the received parameter value:

- ^: starts with the following characters, doesn't have characters before.
    
- fixedquery: has the exact value fixedquery.
    
- $: ends there, doesn't have any more characters after fixedquery.
    

If you feel lost with all these "regular expression" ideas, don't worry. They are a hard topic for many people. You can still do a lot of stuff without needing regular expressions yet.

Now you know that whenever you need them you can use them in FastAPI.

### Pydantic v1 regex instead of pattern[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#pydantic-v1-regex-instead-of-pattern)

Before Pydantic version 2 and before FastAPI 0.100.0, the parameter was called regex instead of pattern, but it's now deprecated.

You could still see some code using it:

[Pydantic v1](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_15_1)

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_16_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

async def read_items(

    q: Annotated[

  

       str | None, Query(min_length=3, max_length=50, regex="^fixedquery$")

  

   ] = None,

):

    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

But know that this is deprecated and it should be updated to use the new parameter pattern. 🤓

## Default values[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#default-values)

You can, of course, use default values other than None.

Let's say that you want to declare the q query parameter to have a min_length of 3, and to have a default value of "fixedquery":

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_17_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: Annotated[str, Query(min_length=3)] = "fixedquery"):

  

   results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

Note

Having a default value of any type, including None, makes the parameter optional (not required).

## Required parameters[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#required-parameters)

When we don't need to declare more validations or metadata, we can make the q query parameter required just by not declaring a default value, like:

q: str

  

instead of:

q: str | None = None

  

But we are now declaring it with Query, for example like:

[Annotated](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_19_1)

q: Annotated[str | None, Query(min_length=3)] = None

  

So, when you need to declare a value as required while using Query, you can simply not declare a default value:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_20_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: Annotated[str, Query(min_length=3)]):

  

   results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

### Required, can be None[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#required-can-be-none)

You can declare that a parameter can accept None, but that it's still required. This would force clients to send a value, even if the value is None.

To do that, you can declare that None is a valid type but simply do not declare a default value:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_22_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: Annotated[str | None, Query(min_length=3)]):

  

   results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

## Query parameter list / multiple values[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#query-parameter-list-multiple-values)

When you define a query parameter explicitly with Query you can also declare it to receive a list of values, or said in another way, to receive multiple values.

For example, to declare a query parameter q that can appear multiple times in the URL, you can write:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_24_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: Annotated[list[str] | None, Query()] = None):

  

   query_items = {"q": q}

    return query_items

  

🤓 Other versions and variants

Then, with a URL like:

http://localhost:8000/items/?q=foo&q=bar

  

you would receive the multiple q query parameters' values (foo and bar) in a Python list inside your path operation function, in the function parameter q.

So, the response to that URL would be:

{

  "q": [

    "foo",

    "bar"

  ]

}

  

Tip

To declare a query parameter with a type of list, like in the example above, you need to explicitly use Query, otherwise it would be interpreted as a request body.

The interactive API docs will update accordingly, to allow multiple values:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfGd9jl0a7lAIWBgah5QNq2VAxgeBTEqjhDCnNbGfKhFifEYPWecWh61ZoUmtiF9X8ZvIAcRk8WJCVbOSqmu-ALe-szblaPQYnZMkCwDQzW1b1Lp4dlxGwhdseFzVhyoljzOoYwjQ?key=f9HbvYiRp_Cr6j6NlCUV7A)

### Query parameter list / multiple values with defaults[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#query-parameter-list-multiple-values-with-defaults)

You can also define a default list of values if none are provided:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_26_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: Annotated[list[str], Query()] = ["foo", "bar"]):

  

   query_items = {"q": q}

    return query_items

  

🤓 Other versions and variants

If you go to:

http://localhost:8000/items/

  

the default of q will be: ["foo", "bar"] and your response will be:

{

  "q": [

    "foo",

    "bar"

  ]

}

  

#### Using just list[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#using-just-list)

You can also use list directly instead of list[str]:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_28_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: Annotated[list, Query()] = []):

  

   query_items = {"q": q}

    return query_items

  

🤓 Other versions and variants

Note

Keep in mind that in this case, FastAPI won't check the contents of the list.

For example, list[int] would check (and document) that the contents of the list are integers. But list alone wouldn't.

## Declare more metadata[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#declare-more-metadata)

You can add more information about the parameter.

That information will be included in the generated OpenAPI and used by the documentation user interfaces and external tools.

Note

Keep in mind that different tools might have different levels of OpenAPI support.

Some of them might not show all the extra information declared yet, although in most of the cases, the missing feature is already planned for development.

You can add a title:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_30_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

async def read_items(

  

   q: Annotated[str | None, Query(title="Query string", min_length=3)] = None,

  

):

    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

And a description:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_32_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

async def read_items(

    q: Annotated[

        str | None,

        Query(

            title="Query string",

  

           description="Query string for the items to search in the database that have a good match",

  

           min_length=3,

        ),

    ] = None,

):

    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

## Alias parameters[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#alias-parameters)

Imagine that you want the parameter to be item-query.

Like in:

http://127.0.0.1:8000/items/?item-query=foobaritems

  

But item-query is not a valid Python variable name.

The closest would be item_query.

But you still need it to be exactly item-query...

Then you can declare an alias, and that alias is what will be used to find the parameter value:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_34_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

  

async def read_items(q: Annotated[str | None, Query(alias="item-query")] = None):

  

   results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

## Deprecating parameters[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#deprecating-parameters)

Now let's say you don't like this parameter anymore.

You have to leave it there a while because there are clients using it, but you want the docs to clearly show it as deprecated.

Then pass the parameter deprecated=True to Query:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_36_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

async def read_items(

    q: Annotated[

        str | None,

        Query(

            alias="item-query",

            title="Query string",

            description="Query string for the items to search in the database that have a good match",

            min_length=3,

            max_length=50,

            pattern="^fixedquery$",

  

           deprecated=True,

  

       ),

    ] = None,

):

    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

The docs will show it like this:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdIjbh71hpQ8FJjP588AD65fx9VvWIFFKgUvSnqWU7NPh5-_6hRdpV84IzpBRkHVKITMl7HNWAO1DAkSBj_Q5r-Geaeb4d-10cbp_GwMn1lDMY0nM5ZY_VDwIndy5V7IyhHH-OOCw?key=f9HbvYiRp_Cr6j6NlCUV7A)

## Exclude parameters from OpenAPI[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#exclude-parameters-from-openapi)

To exclude a query parameter from the generated OpenAPI schema (and thus, from the automatic documentation systems), set the parameter include_in_schema of Query to False:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_38_1)

from typing import Annotated

  

from fastapi import FastAPI, Query

  

app = FastAPI()

  
  

@app.get("/items/")

async def read_items(

  

   hidden_query: Annotated[str | None, Query(include_in_schema=False)] = None,

  

):

    if hidden_query:

        return {"hidden_query": hidden_query}

    else:

        return {"hidden_query": "Not found"}

  

🤓 Other versions and variants

## Custom Validation[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#custom-validation)

There could be cases where you need to do some custom validation that can't be done with the parameters shown above.

In those cases, you can use a custom validator function that is applied after the normal validation (e.g. after validating that the value is a str).

You can achieve that using [Pydantic's AfterValidator](https://docs.pydantic.dev/latest/concepts/validators/#field-after-validator) inside of Annotated.

Tip

Pydantic also has [BeforeValidator](https://docs.pydantic.dev/latest/concepts/validators/#field-before-validator) and others. 🤓

For example, this custom validator checks that the item ID starts with isbn- for an ISBN book number or with imdb- for an IMDB movie URL ID:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_40_1)

import random

from typing import Annotated

  

from fastapi import FastAPI

  

from pydantic import AfterValidator

  

  

app = FastAPI()

  

data = {

    "isbn-9781529046137": "The Hitchhiker's Guide to the Galaxy",

    "imdb-tt0371724": "The Hitchhiker's Guide to the Galaxy",

    "isbn-9781439512982": "Isaac Asimov: The Complete Stories, Vol. 2",

}

  
  

  

def check_valid_id(id: str):

  

   if not id.startswith(("isbn-", "imdb-")):

  

       raise ValueError('Invalid ID format, it must start with "isbn-" or "imdb-"')

  

   return id

  

  
  

@app.get("/items/")

async def read_items(

  

   id: Annotated[str | None, AfterValidator(check_valid_id)] = None,

  

):

    if id:

        item = data.get(id)

    else:

        id, item = random.choice(list(data.items()))

    return {"id": id, "name": item}

  

🤓 Other versions and variants

Info

This is available with Pydantic version 2 or above. 😎

Tip

If you need to do any type of validation that requires communicating with any external component, like a database or another API, you should instead use FastAPI Dependencies, you will learn about them later.

These custom validators are for things that can be checked with only the same data provided in the request.

### Understand that Code[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#understand-that-code)

The important point is just using AfterValidator with a function inside Annotated. Feel free to skip this part. 🤸

---

But if you're curious about this specific code example and you're still entertained, here are some extra details.

#### String with value.startswith()[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#string-with-valuestartswith)

Did you notice? a string using value.startswith() can take a tuple, and it will check each value in the tuple:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#__tabbed_42_1)

# Code above omitted 👆

  

def check_valid_id(id: str):

  

   if not id.startswith(("isbn-", "imdb-")):

  

       raise ValueError('Invalid ID format, it must start with "isbn-" or "imdb-"')

    return id

  

# Code below omitted 👇

  

👀 Full file preview

🤓 Other versions and variants

#### A Random Item[¶](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/#a-random-item)

With data.items() we get an iterable object with tuples containing the key and value for each dictionary item.

We convert this iterable object into a proper list with list(data.items()).

Then with random.choice() we can get a random value from the list, so, we get a tuple with (id, name). It will be something like ("imdb-tt0371724", "The Hitchhiker's Guide to the Galaxy").

Then we assign those two values of the tuple to the variables id and name.

So, if the user didn't provide an item ID, they will still receive a random suggestion.

# Path Parameters and Numeric Validations[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#path-parameters-and-numeric-validations)

In the same way that you can declare more validations and metadata for query parameters with Query, you can declare the same type of validations and metadata for path parameters with Path.

## Import Path[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#import-path)

First, import Path from fastapi, and import Annotated:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_1_1)

from typing import Annotated

  

  

  

from fastapi import FastAPI, Path, Query

  

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

async def read_items(

    item_id: Annotated[int, Path(title="The ID of the item to get")],

    q: Annotated[str | None, Query(alias="item-query")] = None,

):

    results = {"item_id": item_id}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

Info

FastAPI added support for Annotated (and started recommending it) in version 0.95.0.

If you have an older version, you would get errors when trying to use Annotated.

Make sure you [Upgrade the FastAPI version](https://fastapi.tiangolo.com/deployment/versions/#upgrading-the-fastapi-versions) to at least 0.95.1 before using Annotated.

## Declare metadata[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#declare-metadata)

You can declare all the same parameters as for Query.

For example, to declare a title metadata value for the path parameter item_id you can type:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_3_1)

from typing import Annotated

  

from fastapi import FastAPI, Path, Query

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

async def read_items(

  

   item_id: Annotated[int, Path(title="The ID of the item to get")],

  

   q: Annotated[str | None, Query(alias="item-query")] = None,

):

    results = {"item_id": item_id}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

Note

A path parameter is always required as it has to be part of the path. Even if you declared it with None or set a default value, it would not affect anything, it would still be always required.

## Order the parameters as you need[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#order-the-parameters-as-you-need)

Tip

This is probably not as important or necessary if you use Annotated.

Let's say that you want to declare the query parameter q as a required str.

And you don't need to declare anything else for that parameter, so you don't really need to use Query.

But you still need to use Path for the item_id path parameter. And you don't want to use Annotated for some reason.

Python will complain if you put a value with a "default" before a value that doesn't have a "default".

But you can re-order them, and have the value without a default (the query parameter q) first.

It doesn't matter for FastAPI. It will detect the parameters by their names, types and default declarations (Query, Path, etc), it doesn't care about the order.

So, you can declare your function as:

[Python 3.8 non-Annotated](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_5_1)

Tip

Prefer to use the Annotated version if possible.

[Python 3.8+ - non-Annotated](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_6_1)

from fastapi import FastAPI, Path

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

  

async def read_items(q: str, item_id: int = Path(title="The ID of the item to get")):

  

   results = {"item_id": item_id}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

But keep in mind that if you use Annotated, you won't have this problem, it won't matter as you're not using the function parameter default values for Query() or Path().

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_8_1)

from typing import Annotated

  

from fastapi import FastAPI, Path

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

async def read_items(

    q: str, item_id: Annotated[int, Path(title="The ID of the item to get")]

):

    results = {"item_id": item_id}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

## Order the parameters as you need, tricks[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#order-the-parameters-as-you-need-tricks)

Tip

This is probably not as important or necessary if you use Annotated.

Here's a small trick that can be handy, but you won't need it often.

If you want to:

- declare the q query parameter without a Query nor any default value
    
- declare the path parameter item_id using Path
    
- have them in a different order
    
- not use Annotated
    

...Python has a little special syntax for that.

Pass *, as the first parameter of the function.

Python won't do anything with that *, but it will know that all the following parameters should be called as keyword arguments (key-value pairs), also known as kwargs. Even if they don't have a default value.

[Python 3.8+ - non-Annotated](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_10_1)

from fastapi import FastAPI, Path

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

  

async def read_items(*, item_id: int = Path(title="The ID of the item to get"), q: str):

  

   results = {"item_id": item_id}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

### Better with Annotated[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#better-with-annotated)

Keep in mind that if you use Annotated, as you are not using function parameter default values, you won't have this problem, and you probably won't need to use *.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_12_1)

from typing import Annotated

  

from fastapi import FastAPI, Path

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

async def read_items(

  

   item_id: Annotated[int, Path(title="The ID of the item to get")], q: str

  

):

    results = {"item_id": item_id}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

## Number validations: greater than or equal[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#number-validations-greater-than-or-equal)

With Query and Path (and others you'll see later) you can declare number constraints.

Here, with ge=1, item_id will need to be an integer number "greater than or equal" to 1.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_14_1)

from typing import Annotated

  

from fastapi import FastAPI, Path

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

async def read_items(

  

   item_id: Annotated[int, Path(title="The ID of the item to get", ge=1)], q: str

  

):

    results = {"item_id": item_id}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

## Number validations: greater than and less than or equal[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#number-validations-greater-than-and-less-than-or-equal)

The same applies for:

- gt: greater than
    
- le: less than or equal
    

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_16_1)

from typing import Annotated

  

from fastapi import FastAPI, Path

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

async def read_items(

  

   item_id: Annotated[int, Path(title="The ID of the item to get", gt=0, le=1000)],

  

   q: str,

):

    results = {"item_id": item_id}

    if q:

        results.update({"q": q})

    return results

  

🤓 Other versions and variants

## Number validations: floats, greater than and less than[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#number-validations-floats-greater-than-and-less-than)

Number validations also work for float values.

Here's where it becomes important to be able to declare gt and not just ge. As with it you can require, for example, that a value must be greater than 0, even if it is less than 1.

So, 0.5 would be a valid value. But 0.0 or 0 would not.

And the same for lt.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_18_1)

from typing import Annotated

  

from fastapi import FastAPI, Path, Query

  

app = FastAPI()

  
  

@app.get("/items/{item_id}")

async def read_items(

    *,

    item_id: Annotated[int, Path(title="The ID of the item to get", ge=0, le=1000)],

    q: str,

  

   size: Annotated[float, Query(gt=0, lt=10.5)],

  

):

    results = {"item_id": item_id}

    if q:

        results.update({"q": q})

    if size:

        results.update({"size": size})

    return results

  

🤓 Other versions and variants

## Recap[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#recap)

With Query, Path (and others you haven't seen yet) you can declare metadata and string validations in the same ways as with [Query Parameters and String Validations](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/).

And you can also declare numeric validations:

- gt: greater than
    
- ge: greater than or equal
    
- lt: less than
    
- le: less than or equal
    

# Query Parameter Models[¶](https://fastapi.tiangolo.com/tutorial/query-param-models/#query-parameter-models)

If you have a group of query parameters that are related, you can create a Pydantic model to declare them.

This would allow you to re-use the model in multiple places and also to declare validations and metadata for all the parameters at once. 😎

Note

This is supported since FastAPI version 0.115.0. 🤓

## Query Parameters with a Pydantic Model[¶](https://fastapi.tiangolo.com/tutorial/query-param-models/#query-parameters-with-a-pydantic-model)

Declare the query parameters that you need in a Pydantic model, and then declare the parameter as Query:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_1_1)

from typing import Annotated, Literal

  

from fastapi import FastAPI, Query

from pydantic import BaseModel, Field

  

app = FastAPI()

  
  

  

class FilterParams(BaseModel):

  

   limit: int = Field(100, gt=0, le=100)

  

   offset: int = Field(0, ge=0)

  

   order_by: Literal["created_at", "updated_at"] = "created_at"

  

   tags: list[str] = []

  

  
  

@app.get("/items/")

  

async def read_items(filter_query: Annotated[FilterParams, Query()]):

  

   return filter_query

  

🤓 Other versions and variants

FastAPI will extract the data for each field from the query parameters in the request and give you the Pydantic model you defined.

## Check the Docs[¶](https://fastapi.tiangolo.com/tutorial/query-param-models/#check-the-docs)

You can see the query parameters in the docs UI at /docs:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd_S8Kbd32uOXphS4WnvdklVglhJLjGkFI-X3FRK9gSSm7qZESZpCpEFFLvGDYfvX58Tl0QxSArdcHHHCR8ImVCDJX_qIUCkPOQC4UZfLmV-bdlFhbuaMS-egtMdKkl4F3MOt25pg?key=f9HbvYiRp_Cr6j6NlCUV7A)

## Forbid Extra Query Parameters[¶](https://fastapi.tiangolo.com/tutorial/query-param-models/#forbid-extra-query-parameters)

In some special use cases (probably not very common), you might want to restrict the query parameters that you want to receive.

You can use Pydantic's model configuration to forbid any extra fields:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_3_1)

from typing import Annotated, Literal

  

from fastapi import FastAPI, Query

from pydantic import BaseModel, Field

  

app = FastAPI()

  
  

class FilterParams(BaseModel):

  

   model_config = {"extra": "forbid"}

  

  

    limit: int = Field(100, gt=0, le=100)

    offset: int = Field(0, ge=0)

    order_by: Literal["created_at", "updated_at"] = "created_at"

    tags: list[str] = []

  
  

@app.get("/items/")

async def read_items(filter_query: Annotated[FilterParams, Query()]):

    return filter_query

  

🤓 Other versions and variants

If a client tries to send some extra data in the query parameters, they will receive an error response.

For example, if the client tries to send a tool query parameter with a value of plumbus, like:

https://example.com/items/?limit=10&tool=plumbus

  

They will receive an error response telling them that the query parameter tool is not allowed:

{

    "detail": [

        {

            "type": "extra_forbidden",

            "loc": ["query", "tool"],

            "msg": "Extra inputs are not permitted",

            "input": "plumbus"

        }

    ]

}

  

  

  
**

# Path Parameters and Numeric Validations[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#path-parameters-and-numeric-validations "Permanent link")

In the same way that you can declare more validations and metadata for query parameters with `Query`, you can declare the same type of validations and metadata for path parameters with `Path`.

## Import Path[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#import-path "Permanent link")

First, import `Path` from `fastapi`, and import `Annotated`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_1_1)

`from typing import Annotated from fastapi import FastAPI, Path, Query app = FastAPI() @app.get("/items/{item_id}") async def read_items(     item_id: Annotated[int, Path(title="The ID of the item to get")],    q: Annotated[str | None, Query(alias="item-query")] = None, ):     results = {"item_id": item_id}    if q:        results.update({"q": q})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_2_4)

Info

FastAPI added support for `Annotated` (and started recommending it) in version 0.95.0.

If you have an older version, you would get errors when trying to use `Annotated`.

Make sure you [Upgrade the FastAPI version](https://fastapi.tiangolo.com/deployment/versions/#upgrading-the-fastapi-versions) to at least 0.95.1 before using `Annotated`.

## Declare metadata[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#declare-metadata "Permanent link")

You can declare all the same parameters as for `Query`.

For example, to declare a `title` metadata value for the path parameter `item_id` you can type:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_3_1)

`from typing import Annotated from fastapi import FastAPI, Path, Query app = FastAPI() @app.get("/items/{item_id}") async def read_items(     item_id: Annotated[int, Path(title="The ID of the item to get")],    q: Annotated[str | None, Query(alias="item-query")] = None, ):     results = {"item_id": item_id}    if q:        results.update({"q": q})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_4_4)

Note

A path parameter is always required as it has to be part of the path. Even if you declared it with `None` or set a default value, it would not affect anything, it would still be always required.

## Order the parameters as you need[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#order-the-parameters-as-you-need "Permanent link")

Tip

This is probably not as important or necessary if you use `Annotated`.

Let's say that you want to declare the query parameter `q` as a required `str`.

And you don't need to declare anything else for that parameter, so you don't really need to use `Query`.

But you still need to use `Path` for the `item_id` path parameter. And you don't want to use `Annotated` for some reason.

Python will complain if you put a value with a "default" before a value that doesn't have a "default".

But you can re-order them, and have the value without a default (the query parameter `q`) first.

It doesn't matter for **FastAPI**. It will detect the parameters by their names, types and default declarations (`Query`, `Path`, etc), it doesn't care about the order.

So, you can declare your function as:

[Python 3.8 non-Annotated](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_5_1)

Tip

Prefer to use the `Annotated` version if possible.

[Python 3.8+ - non-Annotated](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_6_1)

`from fastapi import FastAPI, Path app = FastAPI() @app.get("/items/{item_id}") async def read_items(q: str, item_id: int = Path(title="The ID of the item to get")):     results = {"item_id": item_id}    if q:        results.update({"q": q})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_7_1)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_7_2)

But keep in mind that if you use `Annotated`, you won't have this problem, it won't matter as you're not using the function parameter default values for `Query()` or `Path()`.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_8_1)

`from typing import Annotated from fastapi import FastAPI, Path app = FastAPI() @app.get("/items/{item_id}") async def read_items(     q: str, item_id: Annotated[int, Path(title="The ID of the item to get")] ):     results = {"item_id": item_id}    if q:        results.update({"q": q})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_9_1)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_9_2)

## Order the parameters as you need, tricks[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#order-the-parameters-as-you-need-tricks "Permanent link")

Tip

This is probably not as important or necessary if you use `Annotated`.

Here's a **small trick** that can be handy, but you won't need it often.

If you want to:

- declare the `q` query parameter without a `Query` nor any default value
- declare the path parameter `item_id` using `Path`
- have them in a different order
- not use `Annotated`

...Python has a little special syntax for that.

Pass `*`, as the first parameter of the function.

Python won't do anything with that `*`, but it will know that all the following parameters should be called as keyword arguments (key-value pairs), also known as `kwargs`. Even if they don't have a default value.

[Python 3.8+ - non-Annotated](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_10_1)

`from fastapi import FastAPI, Path app = FastAPI() @app.get("/items/{item_id}") async def read_items(*, item_id: int = Path(title="The ID of the item to get"), q: str):     results = {"item_id": item_id}    if q:        results.update({"q": q})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_11_1)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_11_2)

### Better with `Annotated`[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#better-with-annotated "Permanent link")

Keep in mind that if you use `Annotated`, as you are not using function parameter default values, you won't have this problem, and you probably won't need to use `*`.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_12_1)

`from typing import Annotated from fastapi import FastAPI, Path app = FastAPI() @app.get("/items/{item_id}") async def read_items(     item_id: Annotated[int, Path(title="The ID of the item to get")], q: str ):     results = {"item_id": item_id}    if q:        results.update({"q": q})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_13_1)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_13_2)

## Number validations: greater than or equal[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#number-validations-greater-than-or-equal "Permanent link")

With `Query` and `Path` (and others you'll see later) you can declare number constraints.

Here, with `ge=1`, `item_id` will need to be an integer number "`g`reater than or `e`qual" to `1`.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_14_1)

`from typing import Annotated from fastapi import FastAPI, Path app = FastAPI() @app.get("/items/{item_id}") async def read_items(     item_id: Annotated[int, Path(title="The ID of the item to get", ge=1)], q: str ):     results = {"item_id": item_id}    if q:        results.update({"q": q})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_15_1)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_15_2)

## Number validations: greater than and less than or equal[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#number-validations-greater-than-and-less-than-or-equal "Permanent link")

The same applies for:

- `gt`: `g`reater `t`han
- `le`: `l`ess than or `e`qual

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_16_1)

`from typing import Annotated from fastapi import FastAPI, Path app = FastAPI() @app.get("/items/{item_id}") async def read_items(     item_id: Annotated[int, Path(title="The ID of the item to get", gt=0, le=1000)],    q: str, ):     results = {"item_id": item_id}    if q:        results.update({"q": q})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_17_1)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_17_2)

## Number validations: floats, greater than and less than[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#number-validations-floats-greater-than-and-less-than "Permanent link")

Number validations also work for `float` values.

Here's where it becomes important to be able to declare `gt` and not just `ge`. As with it you can require, for example, that a value must be greater than `0`, even if it is less than `1`.

So, `0.5` would be a valid value. But `0.0` or `0` would not.

And the same for `lt`.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_18_1)

`from typing import Annotated from fastapi import FastAPI, Path, Query app = FastAPI() @app.get("/items/{item_id}") async def read_items(     *,    item_id: Annotated[int, Path(title="The ID of the item to get", ge=0, le=1000)],    q: str,    size: Annotated[float, Query(gt=0, lt=10.5)], ):     results = {"item_id": item_id}    if q:        results.update({"q": q})    if size:        results.update({"size": size})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_19_1)[](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#__tabbed_19_2)

## Recap[¶](https://fastapi.tiangolo.com/tutorial/path-params-numeric-validations/#recap "Permanent link")

With `Query`, `Path` (and others you haven't seen yet) you can declare metadata and string validations in the same ways as with [Query Parameters and String Validations](https://fastapi.tiangolo.com/tutorial/query-params-str-validations/).

And you can also declare numeric validations:

- `gt`: `g`reater `t`han
- `ge`: `g`reater than or `e`qual
- `lt`: `l`ess `t`han
- `le`: `l`ess than or `e`qual


# Query Parameter Models[¶](https://fastapi.tiangolo.com/tutorial/query-param-models/#query-parameter-models "Permanent link")

If you have a group of **query parameters** that are related, you can create a **Pydantic model** to declare them.

This would allow you to **re-use the model** in **multiple places** and also to declare validations and metadata for all the parameters at once. 😎

Note

This is supported since FastAPI version `0.115.0`. 🤓

## Query Parameters with a Pydantic Model[¶](https://fastapi.tiangolo.com/tutorial/query-param-models/#query-parameters-with-a-pydantic-model "Permanent link")

Declare the **query parameters** that you need in a **Pydantic model**, and then declare the parameter as `Query`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_1_1)

`from typing import Annotated, Literal from fastapi import FastAPI, Query from pydantic import BaseModel, Field app = FastAPI() class FilterParams(BaseModel):     limit: int = Field(100, gt=0, le=100)    offset: int = Field(0, ge=0)    order_by: Literal["created_at", "updated_at"] = "created_at"    tags: list[str] = [] @app.get("/items/") async def read_items(filter_query: Annotated[FilterParams, Query()]):     return filter_query`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_2_4)[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_2_5)

**FastAPI** will **extract** the data for **each field** from the **query parameters** in the request and give you the Pydantic model you defined.

## Check the Docs[¶](https://fastapi.tiangolo.com/tutorial/query-param-models/#check-the-docs "Permanent link")

You can see the query parameters in the docs UI at `/docs`:

![](https://fastapi.tiangolo.com/img/tutorial/query-param-models/image01.png)

## Forbid Extra Query Parameters[¶](https://fastapi.tiangolo.com/tutorial/query-param-models/#forbid-extra-query-parameters "Permanent link")

In some special use cases (probably not very common), you might want to **restrict** the query parameters that you want to receive.

You can use Pydantic's model configuration to `forbid` any `extra` fields:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_3_1)

`from typing import Annotated, Literal from fastapi import FastAPI, Query from pydantic import BaseModel, Field app = FastAPI() class FilterParams(BaseModel):     model_config = {"extra": "forbid"}     limit: int = Field(100, gt=0, le=100)    offset: int = Field(0, ge=0)    order_by: Literal["created_at", "updated_at"] = "created_at"    tags: list[str] = [] @app.get("/items/") async def read_items(filter_query: Annotated[FilterParams, Query()]):     return filter_query`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_4_4)[](https://fastapi.tiangolo.com/tutorial/query-param-models/#__tabbed_4_5)

If a client tries to send some **extra** data in the **query parameters**, they will receive an **error** response.

For example, if the client tries to send a `tool` query parameter with a value of `plumbus`, like:

`https://example.com/items/?limit=10&tool=plumbus`

They will receive an **error** response telling them that the query parameter `tool` is not allowed:

`{     "detail": [        {            "type": "extra_forbidden",            "loc": ["query", "tool"],            "msg": "Extra inputs are not permitted",            "input": "plumbus"        }    ] }`


# Body - Multiple Parameters[¶](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#body-multiple-parameters "Permanent link")

Now that we have seen how to use `Path` and `Query`, let's see more advanced uses of request body declarations.

## Mix `Path`, `Query` and body parameters[¶](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#mix-path-query-and-body-parameters "Permanent link")

First, of course, you can mix `Path`, `Query` and request body parameter declarations freely and **FastAPI** will know what to do.

And you can also declare body parameters as optional, by setting the default to `None`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_1_1)

`from typing import Annotated from fastapi import FastAPI, Path from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None @app.put("/items/{item_id}") async def update_item(     item_id: Annotated[int, Path(title="The ID of the item to get", ge=0, le=1000)],    q: str | None = None,    item: Item | None = None, ):     results = {"item_id": item_id}    if q:        results.update({"q": q})    if item:        results.update({"item": item})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_2_4)

Note

Notice that, in this case, the `item` that would be taken from the body is optional. As it has a `None` default value.

## Multiple body parameters[¶](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#multiple-body-parameters "Permanent link")

In the previous example, the _path operations_ would expect a JSON body with the attributes of an `Item`, like:

`{     "name": "Foo",    "description": "The pretender",    "price": 42.0,    "tax": 3.2 }`

But you can also declare multiple body parameters, e.g. `item` and `user`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_3_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None class User(BaseModel):     username: str    full_name: str | None = None @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item, user: User):     results = {"item_id": item_id, "item": item, "user": user}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_4_1)

In this case, **FastAPI** will notice that there is more than one body parameter in the function (there are two parameters that are Pydantic models).

So, it will then use the parameter names as keys (field names) in the body, and expect a body like:

`{     "item": {        "name": "Foo",        "description": "The pretender",        "price": 42.0,        "tax": 3.2    },    "user": {        "username": "dave",        "full_name": "Dave Grohl"    } }`

Note

Notice that even though the `item` was declared the same way as before, it is now expected to be inside of the body with a key `item`.

**FastAPI** will do the automatic conversion from the request, so that the parameter `item` receives its specific content and the same for `user`.

It will perform the validation of the compound data, and will document it like that for the OpenAPI schema and automatic docs.

## Singular values in body[¶](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#singular-values-in-body "Permanent link")

The same way there is a `Query` and `Path` to define extra data for query and path parameters, **FastAPI** provides an equivalent `Body`.

For example, extending the previous model, you could decide that you want to have another key `importance` in the same body, besides the `item` and `user`.

If you declare it as is, because it is a singular value, **FastAPI** will assume that it is a query parameter.

But you can instruct **FastAPI** to treat it as another body key using `Body`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_5_1)

`from typing import Annotated from fastapi import Body, FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None class User(BaseModel):     username: str    full_name: str | None = None @app.put("/items/{item_id}") async def update_item(     item_id: int, item: Item, user: User, importance: Annotated[int, Body()] ):     results = {"item_id": item_id, "item": item, "user": user, "importance": importance}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_6_2)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_6_3)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_6_4)

In this case, **FastAPI** will expect a body like:

`{     "item": {        "name": "Foo",        "description": "The pretender",        "price": 42.0,        "tax": 3.2    },    "user": {        "username": "dave",        "full_name": "Dave Grohl"    },    "importance": 5 }`

Again, it will convert the data types, validate, document, etc.

## Multiple body params and query[¶](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#multiple-body-params-and-query "Permanent link")

Of course, you can also declare additional query parameters whenever you need, additional to any body parameters.

As, by default, singular values are interpreted as query parameters, you don't have to explicitly add a `Query`, you can just do:

`q: Union[str, None] = None`

Or in Python 3.10 and above:

`q: str | None = None`

For example:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_7_1)

`from typing import Annotated from fastapi import Body, FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None class User(BaseModel):     username: str    full_name: str | None = None @app.put("/items/{item_id}") async def update_item(     *,    item_id: int,    item: Item,    user: User,    importance: Annotated[int, Body(gt=0)],    q: str | None = None, ):     results = {"item_id": item_id, "item": item, "user": user, "importance": importance}    if q:        results.update({"q": q})    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_8_2)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_8_3)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_8_4)

Info

`Body` also has all the same extra validation and metadata parameters as `Query`,`Path` and others you will see later.

## Embed a single body parameter[¶](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#embed-a-single-body-parameter "Permanent link")

Let's say you only have a single `item` body parameter from a Pydantic model `Item`.

By default, **FastAPI** will then expect its body directly.

But if you want it to expect a JSON with a key `item` and inside of it the model contents, as it does when you declare extra body parameters, you can use the special `Body` parameter `embed`:

`item: Item = Body(embed=True)`

as in:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_9_1)

`from typing import Annotated from fastapi import Body, FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None @app.put("/items/{item_id}") async def update_item(item_id: int, item: Annotated[Item, Body(embed=True)]):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_10_1)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_10_2)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_10_3)[](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#__tabbed_10_4)

In this case **FastAPI** will expect a body like:

`{     "item": {        "name": "Foo",        "description": "The pretender",        "price": 42.0,        "tax": 3.2    } }`

instead of:

`{     "name": "Foo",    "description": "The pretender",    "price": 42.0,    "tax": 3.2 }`

## Recap[¶](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#recap "Permanent link")

You can add multiple body parameters to your _path operation function_, even though a request can only have a single body.

But **FastAPI** will handle it, give you the correct data in your function, and validate and document the correct schema in the _path operation_.

You can also declare singular values to be received as part of the body.

And you can instruct **FastAPI** to embed the body in a key even when there is only a single parameter declared.

# Body - Fields[¶](https://fastapi.tiangolo.com/tutorial/body-fields/#body-fields "Permanent link")

The same way you can declare additional validation and metadata in _path operation function_ parameters with `Query`, `Path` and `Body`, you can declare validation and metadata inside of Pydantic models using Pydantic's `Field`.

## Import `Field`[¶](https://fastapi.tiangolo.com/tutorial/body-fields/#import-field "Permanent link")

First, you have to import it:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_1_1)

`from typing import Annotated from fastapi import Body, FastAPI from pydantic import BaseModel, Field app = FastAPI() class Item(BaseModel):     name: str    description: str | None = Field(        default=None, title="The description of the item", max_length=300    )    price: float = Field(gt=0, description="The price must be greater than zero")    tax: float | None = None @app.put("/items/{item_id}") async def update_item(item_id: int, item: Annotated[Item, Body(embed=True)]):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_2_4)

Warning

Notice that `Field` is imported directly from `pydantic`, not from `fastapi` as are all the rest (`Query`, `Path`, `Body`, etc).

## Declare model attributes[¶](https://fastapi.tiangolo.com/tutorial/body-fields/#declare-model-attributes "Permanent link")

You can then use `Field` with model attributes:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_3_1)

`from typing import Annotated from fastapi import Body, FastAPI from pydantic import BaseModel, Field app = FastAPI() class Item(BaseModel):     name: str    description: str | None = Field(        default=None, title="The description of the item", max_length=300    )    price: float = Field(gt=0, description="The price must be greater than zero")    tax: float | None = None @app.put("/items/{item_id}") async def update_item(item_id: int, item: Annotated[Item, Body(embed=True)]):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/body-fields/#__tabbed_4_4)

`Field` works the same way as `Query`, `Path` and `Body`, it has all the same parameters, etc.

Technical Details

Actually, `Query`, `Path` and others you'll see next create objects of subclasses of a common `Param` class, which is itself a subclass of Pydantic's `FieldInfo` class.

And Pydantic's `Field` returns an instance of `FieldInfo` as well.

`Body` also returns objects of a subclass of `FieldInfo` directly. And there are others you will see later that are subclasses of the `Body` class.

Remember that when you import `Query`, `Path`, and others from `fastapi`, those are actually functions that return special classes.

Tip

Notice how each model's attribute with a type, default value and `Field` has the same structure as a _path operation function's_ parameter, with `Field` instead of `Path`, `Query` and `Body`.

## Add extra information[¶](https://fastapi.tiangolo.com/tutorial/body-fields/#add-extra-information "Permanent link")

You can declare extra information in `Field`, `Query`, `Body`, etc. And it will be included in the generated JSON Schema.

You will learn more about adding extra information later in the docs, when learning to declare examples.

# Body - Nested Models[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#body-nested-models "Permanent link")

With **FastAPI**, you can define, validate, document, and use arbitrarily deeply nested models (thanks to Pydantic).

## List fields[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#list-fields "Permanent link")

You can define an attribute to be a subtype. For example, a Python `list`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_1_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: list = [] @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_2_1)

This will make `tags` be a list, although it doesn't declare the type of the elements of the list.

## List fields with type parameter[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#list-fields-with-type-parameter "Permanent link")

But Python has a specific way to declare lists with internal types, or "type parameters":

### Import typing's `List`[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#import-typings-list "Permanent link")

In Python 3.9 and above you can use the standard `list` to declare these type annotations as we'll see below. 💡

But in Python versions before 3.9 (3.6 and above), you first need to import `List` from standard Python's `typing` module:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_3_1)

`from typing import List, Union from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: Union[str, None] = None    price: float    tax: Union[float, None] = None    tags: List[str] = [] @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_4_2)

### Declare a `list` with a type parameter[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#declare-a-list-with-a-type-parameter "Permanent link")

To declare types that have type parameters (internal types), like `list`, `dict`, `tuple`:

- If you are in a Python version lower than 3.9, import their equivalent version from the `typing` module
- Pass the internal type(s) as "type parameters" using square brackets: `[` and `]`

In Python 3.9 it would be:

`my_list: list[str]`

In versions of Python before 3.9, it would be:

`from typing import List my_list: List[str]`

That's all standard Python syntax for type declarations.

Use that same standard syntax for model attributes with internal types.

So, in our example, we can make `tags` be specifically a "list of strings":

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_5_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: list[str] = [] @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_6_2)

## Set types[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#set-types "Permanent link")

But then we think about it, and realize that tags shouldn't repeat, they would probably be unique strings.

And Python has a special data type for sets of unique items, the `set`.

Then we can declare `tags` as a set of strings:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_7_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set() @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_8_2)

With this, even if you receive a request with duplicate data, it will be converted to a set of unique items.

And whenever you output that data, even if the source had duplicates, it will be output as a set of unique items.

And it will be annotated / documented accordingly too.

## Nested Models[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#nested-models "Permanent link")

Each attribute of a Pydantic model has a type.

But that type can itself be another Pydantic model.

So, you can declare deeply nested JSON "objects" with specific attribute names, types and validations.

All that, arbitrarily nested.

### Define a submodel[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#define-a-submodel "Permanent link")

For example, we can define an `Image` model:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_9_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Image(BaseModel):     url: str    name: str class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set()    image: Image | None = None @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_10_1)[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_10_2)

### Use the submodel as a type[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#use-the-submodel-as-a-type "Permanent link")

And then we can use it as the type of an attribute:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_11_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Image(BaseModel):     url: str    name: str class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set()    image: Image | None = None @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_12_1)[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_12_2)

This would mean that **FastAPI** would expect a body similar to:

`{     "name": "Foo",    "description": "The pretender",    "price": 42.0,    "tax": 3.2,    "tags": ["rock", "metal", "bar"],    "image": {        "url": "http://example.com/baz.jpg",        "name": "The Foo live"    } }`

Again, doing just that declaration, with **FastAPI** you get:

- Editor support (completion, etc.), even for nested models
- Data conversion
- Data validation
- Automatic documentation

## Special types and validation[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#special-types-and-validation "Permanent link")

Apart from normal singular types like `str`, `int`, `float`, etc. you can use more complex singular types that inherit from `str`.

To see all the options you have, checkout [Pydantic's Type Overview](https://docs.pydantic.dev/latest/concepts/types/). You will see some examples in the next chapter.

For example, as in the `Image` model we have a `url` field, we can declare it to be an instance of Pydantic's `HttpUrl` instead of a `str`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_13_1)

`from fastapi import FastAPI from pydantic import BaseModel, HttpUrl app = FastAPI() class Image(BaseModel):     url: HttpUrl    name: str class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set()    image: Image | None = None @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_14_1)[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_14_2)

The string will be checked to be a valid URL, and documented in JSON Schema / OpenAPI as such.

## Attributes with lists of submodels[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#attributes-with-lists-of-submodels "Permanent link")

You can also use Pydantic models as subtypes of `list`, `set`, etc.:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_15_1)

`from fastapi import FastAPI from pydantic import BaseModel, HttpUrl app = FastAPI() class Image(BaseModel):     url: HttpUrl    name: str class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set()    images: list[Image] | None = None @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_16_1)[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_16_2)

This will expect (convert, validate, document, etc.) a JSON body like:

`{     "name": "Foo",    "description": "The pretender",    "price": 42.0,    "tax": 3.2,    "tags": [        "rock",        "metal",        "bar"    ],    "images": [        {            "url": "http://example.com/baz.jpg",            "name": "The Foo live"        },        {            "url": "http://example.com/dave.jpg",            "name": "The Baz"        }    ] }`

Info

Notice how the `images` key now has a list of image objects.

## Deeply nested models[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#deeply-nested-models "Permanent link")

You can define arbitrarily deeply nested models:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_17_1)

`from fastapi import FastAPI from pydantic import BaseModel, HttpUrl app = FastAPI() class Image(BaseModel):     url: HttpUrl    name: str class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set()    images: list[Image] | None = None class Offer(BaseModel):     name: str    description: str | None = None    price: float    items: list[Item] @app.post("/offers/") async def create_offer(offer: Offer):     return offer`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_18_1)[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_18_2)

Info

Notice how `Offer` has a list of `Item`s, which in turn have an optional list of `Image`s

## Bodies of pure lists[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#bodies-of-pure-lists "Permanent link")

If the top level value of the JSON body you expect is a JSON `array` (a Python `list`), you can declare the type in the parameter of the function, the same as in Pydantic models:

`images: List[Image]`

or in Python 3.9 and above:

`images: list[Image]`

as in:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_19_1)

`from fastapi import FastAPI from pydantic import BaseModel, HttpUrl app = FastAPI() class Image(BaseModel):     url: HttpUrl    name: str @app.post("/images/multiple/") async def create_multiple_images(images: list[Image]):     return images`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_20_1)

## Editor support everywhere[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#editor-support-everywhere "Permanent link")

And you get editor support everywhere.

Even for items inside of lists:

![](https://fastapi.tiangolo.com/img/tutorial/body-nested-models/image01.png)

You couldn't get this kind of editor support if you were working directly with `dict` instead of Pydantic models.

But you don't have to worry about them either, incoming dicts are converted automatically and your output is converted automatically to JSON too.

## Bodies of arbitrary `dict`s[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#bodies-of-arbitrary-dicts "Permanent link")

You can also declare a body as a `dict` with keys of some type and values of some other type.

This way, you don't have to know beforehand what the valid field/attribute names are (as would be the case with Pydantic models).

This would be useful if you want to receive keys that you don't already know.

---

Another useful case is when you want to have keys of another type (e.g., `int`).

That's what we are going to see here.

In this case, you would accept any `dict` as long as it has `int` keys with `float` values:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_21_1)

`from fastapi import FastAPI app = FastAPI() @app.post("/index-weights/") async def create_index_weights(weights: dict[int, float]):     return weights`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-nested-models/#__tabbed_22_1)

Tip

Keep in mind that JSON only supports `str` as keys.

But Pydantic has automatic data conversion.

This means that, even though your API clients can only send strings as keys, as long as those strings contain pure integers, Pydantic will convert them and validate them.

And the `dict` you receive as `weights` will actually have `int` keys and `float` values.

## Recap[¶](https://fastapi.tiangolo.com/tutorial/body-nested-models/#recap "Permanent link")

With **FastAPI** you have the maximum flexibility provided by Pydantic models, while keeping your code simple, short and elegant.

But with all the benefits:

- Editor support (completion everywhere!)
- Data conversion (a.k.a. parsing / serialization)
- Data validation
- Schema documentation
- Automatic docs

# Declare Request Example Data[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#declare-request-example-data "Permanent link")

You can declare examples of the data your app can receive.

Here are several ways to do it.

## Extra JSON Schema data in Pydantic models[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#extra-json-schema-data-in-pydantic-models "Permanent link")

You can declare `examples` for a Pydantic model that will be added to the generated JSON Schema.

[Pydantic v2](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_1_1)[Pydantic v1](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_1_2)

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_2_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None     model_config = {        "json_schema_extra": {            "examples": [                {                    "name": "Foo",                    "description": "A very nice Item",                    "price": 35.4,                    "tax": 3.2,                }            ]        }    } @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_3_1)

That extra info will be added as-is to the output **JSON Schema** for that model, and it will be used in the API docs.

[Pydantic v2](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_6_1)[Pydantic v1](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_6_2)

In Pydantic version 2, you would use the attribute `model_config`, that takes a `dict` as described in [Pydantic's docs: Configuration](https://docs.pydantic.dev/latest/api/config/).

You can set `"json_schema_extra"` with a `dict` containing any additional data you would like to show up in the generated JSON Schema, including `examples`.

Tip

You could use the same technique to extend the JSON Schema and add your own custom extra info.

For example you could use it to add metadata for a frontend user interface, etc.

Info

OpenAPI 3.1.0 (used since FastAPI 0.99.0) added support for `examples`, which is part of the **JSON Schema** standard.

Before that, it only supported the keyword `example` with a single example. That is still supported by OpenAPI 3.1.0, but is deprecated and is not part of the JSON Schema standard. So you are encouraged to migrate `example` to `examples`. 🤓

You can read more at the end of this page.

## `Field` additional arguments[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#field-additional-arguments "Permanent link")

When using `Field()` with Pydantic models, you can also declare additional `examples`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_7_1)

`from fastapi import FastAPI from pydantic import BaseModel, Field app = FastAPI() class Item(BaseModel):     name: str = Field(examples=["Foo"])    description: str | None = Field(default=None, examples=["A very nice Item"])    price: float = Field(examples=[35.4])    tax: float | None = Field(default=None, examples=[3.2]) @app.put("/items/{item_id}") async def update_item(item_id: int, item: Item):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_8_1)

## `examples` in JSON Schema - OpenAPI[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#examples-in-json-schema-openapi "Permanent link")

When using any of:

- `Path()`
- `Query()`
- `Header()`
- `Cookie()`
- `Body()`
- `Form()`
- `File()`

you can also declare a group of `examples` with additional information that will be added to their **JSON Schemas** inside of **OpenAPI**.

### `Body` with `examples`[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#body-with-examples "Permanent link")

Here we pass `examples` containing one example of the data expected in `Body()`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_9_1)

`from typing import Annotated from fastapi import Body, FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None @app.put("/items/{item_id}") async def update_item(     item_id: int,    item: Annotated[        Item,        Body(            examples=[                {                    "name": "Foo",                    "description": "A very nice Item",                    "price": 35.4,                    "tax": 3.2,                }            ],        ),    ], ):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_10_1)[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_10_2)[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_10_3)[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_10_4)

### Example in the docs UI[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#example-in-the-docs-ui "Permanent link")

With any of the methods above it would look like this in the `/docs`:

![](https://fastapi.tiangolo.com/img/tutorial/body-fields/image01.png)

### `Body` with multiple `examples`[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#body-with-multiple-examples "Permanent link")

You can of course also pass multiple `examples`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_11_1)

`from typing import Annotated from fastapi import Body, FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None @app.put("/items/{item_id}") async def update_item(     *,    item_id: int,    item: Annotated[        Item,        Body(            examples=[                {                    "name": "Foo",                    "description": "A very nice Item",                    "price": 35.4,                    "tax": 3.2,                },                {                    "name": "Bar",                    "price": "35.4",                },                {                    "name": "Baz",                    "price": "thirty five point four",                },            ],        ),    ], ):     results = {"item_id": item_id, "item": item}    return results`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_12_1)[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_12_2)[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_12_3)[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_12_4)

When you do this, the examples will be part of the internal **JSON Schema** for that body data.

Nevertheless, at the time of writing this, Swagger UI, the tool in charge of showing the docs UI, doesn't support showing multiple examples for the data in **JSON Schema**. But read below for a workaround.

### OpenAPI-specific `examples`[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#openapi-specific-examples "Permanent link")

Since before **JSON Schema** supported `examples` OpenAPI had support for a different field also called `examples`.

This **OpenAPI-specific** `examples` goes in another section in the OpenAPI specification. It goes in the **details for each _path operation_**, not inside each JSON Schema.

And Swagger UI has supported this particular `examples` field for a while. So, you can use it to **show** different **examples in the docs UI**.

The shape of this OpenAPI-specific field `examples` is a `dict` with **multiple examples** (instead of a `list`), each with extra information that will be added to **OpenAPI** too.

This doesn't go inside of each JSON Schema contained in OpenAPI, this goes outside, in the _path operation_ directly.

### Using the `openapi_examples` Parameter[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#using-the-openapi_examples-parameter "Permanent link")

You can declare the OpenAPI-specific `examples` in FastAPI with the parameter `openapi_examples` for:

- `Path()`
- `Query()`
- `Header()`
- `Cookie()`
- `Body()`
- `Form()`
- `File()`

The keys of the `dict` identify each example, and each value is another `dict`.

Each specific example `dict` in the `examples` can contain:

- `summary`: Short description for the example.
- `description`: A long description that can contain Markdown text.
- `value`: This is the actual example shown, e.g. a `dict`.
- `externalValue`: alternative to `value`, a URL pointing to the example. Although this might not be supported by as many tools as `value`.

You can use it like this:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_13_1)

``from typing import Annotated from fastapi import Body, FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None @app.put("/items/{item_id}") async def update_item(     *,    item_id: int,    item: Annotated[        Item,        Body(            openapi_examples={                "normal": {                    "summary": "A normal example",                    "description": "A **normal** item works correctly.",                    "value": {                        "name": "Foo",                        "description": "A very nice Item",                        "price": 35.4,                        "tax": 3.2,                    },                },                "converted": {                    "summary": "An example with converted data",                    "description": "FastAPI can convert price `strings` to actual `numbers` automatically",                    "value": {                        "name": "Bar",                        "price": "35.4",                    },                },                "invalid": {                    "summary": "Invalid data is rejected with an error",                    "value": {                        "name": "Baz",                        "price": "thirty five point four",                    },                },            },        ),    ], ):     results = {"item_id": item_id, "item": item}    return results``

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_14_1)[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_14_2)[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_14_3)[](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#__tabbed_14_4)

### OpenAPI Examples in the Docs UI[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#openapi-examples-in-the-docs-ui "Permanent link")

With `openapi_examples` added to `Body()` the `/docs` would look like:

![](https://fastapi.tiangolo.com/img/tutorial/body-fields/image02.png)

## Technical Details[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#technical-details "Permanent link")

Tip

If you are already using **FastAPI** version **0.99.0 or above**, you can probably **skip** these details.

They are more relevant for older versions, before OpenAPI 3.1.0 was available.

You can consider this a brief OpenAPI and JSON Schema **history lesson**. 🤓

Warning

These are very technical details about the standards **JSON Schema** and **OpenAPI**.

If the ideas above already work for you, that might be enough, and you probably don't need these details, feel free to skip them.

Before OpenAPI 3.1.0, OpenAPI used an older and modified version of **JSON Schema**.

JSON Schema didn't have `examples`, so OpenAPI added its own `example` field to its own modified version.

OpenAPI also added `example` and `examples` fields to other parts of the specification:

- [`Parameter Object` (in the specification)](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#parameter-object) that was used by FastAPI's:
    - `Path()`
    - `Query()`
    - `Header()`
    - `Cookie()`
- [`Request Body Object`, in the field `content`, on the `Media Type Object` (in the specification)](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md#media-type-object) that was used by FastAPI's:
    - `Body()`
    - `File()`
    - `Form()`

Info

This old OpenAPI-specific `examples` parameter is now `openapi_examples` since FastAPI `0.103.0`.

### JSON Schema's `examples` field[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#json-schemas-examples-field "Permanent link")

But then JSON Schema added an [`examples`](https://json-schema.org/draft/2019-09/json-schema-validation.html#rfc.section.9.5) field to a new version of the specification.

And then the new OpenAPI 3.1.0 was based on the latest version (JSON Schema 2020-12) that included this new field `examples`.

And now this new `examples` field takes precedence over the old single (and custom) `example` field, that is now deprecated.

This new `examples` field in JSON Schema is **just a `list`** of examples, not a dict with extra metadata as in the other places in OpenAPI (described above).

Info

Even after OpenAPI 3.1.0 was released with this new simpler integration with JSON Schema, for a while, Swagger UI, the tool that provides the automatic docs, didn't support OpenAPI 3.1.0 (it does since version 5.0.0 🎉).

Because of that, versions of FastAPI previous to 0.99.0 still used versions of OpenAPI lower than 3.1.0.

### Pydantic and FastAPI `examples`[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#pydantic-and-fastapi-examples "Permanent link")

When you add `examples` inside a Pydantic model, using `schema_extra` or `Field(examples=["something"])` that example is added to the **JSON Schema** for that Pydantic model.

And that **JSON Schema** of the Pydantic model is included in the **OpenAPI** of your API, and then it's used in the docs UI.

In versions of FastAPI before 0.99.0 (0.99.0 and above use the newer OpenAPI 3.1.0) when you used `example` or `examples` with any of the other utilities (`Query()`, `Body()`, etc.) those examples were not added to the JSON Schema that describes that data (not even to OpenAPI's own version of JSON Schema), they were added directly to the _path operation_ declaration in OpenAPI (outside the parts of OpenAPI that use JSON Schema).

But now that FastAPI 0.99.0 and above uses OpenAPI 3.1.0, that uses JSON Schema 2020-12, and Swagger UI 5.0.0 and above, everything is more consistent and the examples are included in JSON Schema.

### Swagger UI and OpenAPI-specific `examples`[¶](https://fastapi.tiangolo.com/tutorial/schema-extra-example/#swagger-ui-and-openapi-specific-examples "Permanent link")

Now, as Swagger UI didn't support multiple JSON Schema examples (as of 2023-08-26), users didn't have a way to show multiple examples in the docs.

To solve that, FastAPI `0.103.0` **added support** for declaring the same old **OpenAPI-specific** `examples` field with the new parameter `openapi_examples`. 🤓

# Extra Data Types[¶](https://fastapi.tiangolo.com/tutorial/extra-data-types/#extra-data-types "Permanent link")

Up to now, you have been using common data types, like:

- `int`
- `float`
- `str`
- `bool`

But you can also use more complex data types.

And you will still have the same features as seen up to now:

- Great editor support.
- Data conversion from incoming requests.
- Data conversion for response data.
- Data validation.
- Automatic annotation and documentation.

## Other data types[¶](https://fastapi.tiangolo.com/tutorial/extra-data-types/#other-data-types "Permanent link")

Here are some of the additional data types you can use:

- `UUID`:
    - A standard "Universally Unique Identifier", common as an ID in many databases and systems.
    - In requests and responses will be represented as a `str`.
- `datetime.datetime`:
    - A Python `datetime.datetime`.
    - In requests and responses will be represented as a `str` in ISO 8601 format, like: `2008-09-15T15:53:00+05:00`.
- `datetime.date`:
    - Python `datetime.date`.
    - In requests and responses will be represented as a `str` in ISO 8601 format, like: `2008-09-15`.
- `datetime.time`:
    - A Python `datetime.time`.
    - In requests and responses will be represented as a `str` in ISO 8601 format, like: `14:23:55.003`.
- `datetime.timedelta`:
    - A Python `datetime.timedelta`.
    - In requests and responses will be represented as a `float` of total seconds.
    - Pydantic also allows representing it as a "ISO 8601 time diff encoding", [see the docs for more info](https://docs.pydantic.dev/latest/concepts/serialization/#custom-serializers).
- `frozenset`:
    - In requests and responses, treated the same as a `set`:
        - In requests, a list will be read, eliminating duplicates and converting it to a `set`.
        - In responses, the `set` will be converted to a `list`.
        - The generated schema will specify that the `set` values are unique (using JSON Schema's `uniqueItems`).
- `bytes`:
    - Standard Python `bytes`.
    - In requests and responses will be treated as `str`.
    - The generated schema will specify that it's a `str` with `binary` "format".
- `Decimal`:
    - Standard Python `Decimal`.
    - In requests and responses, handled the same as a `float`.
- You can check all the valid Pydantic data types here: [Pydantic data types](https://docs.pydantic.dev/latest/usage/types/types/).

## Example[¶](https://fastapi.tiangolo.com/tutorial/extra-data-types/#example "Permanent link")

Here's an example _path operation_ with parameters using some of the above types.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_1_1)

`from datetime import datetime, time, timedelta from typing import Annotated from uuid import UUID from fastapi import Body, FastAPI app = FastAPI() @app.put("/items/{item_id}") async def read_items(     item_id: UUID,    start_datetime: Annotated[datetime, Body()],    end_datetime: Annotated[datetime, Body()],    process_after: Annotated[timedelta, Body()],    repeat_at: Annotated[time | None, Body()] = None, ):     start_process = start_datetime + process_after    duration = end_datetime - start_process    return {        "item_id": item_id,        "start_datetime": start_datetime,        "end_datetime": end_datetime,        "process_after": process_after,        "repeat_at": repeat_at,        "start_process": start_process,        "duration": duration,    }`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_2_4)

Note that the parameters inside the function have their natural data type, and you can, for example, perform normal date manipulations, like:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_3_1)

`from datetime import datetime, time, timedelta from typing import Annotated from uuid import UUID from fastapi import Body, FastAPI app = FastAPI() @app.put("/items/{item_id}") async def read_items(     item_id: UUID,    start_datetime: Annotated[datetime, Body()],    end_datetime: Annotated[datetime, Body()],    process_after: Annotated[timedelta, Body()],    repeat_at: Annotated[time | None, Body()] = None, ):     start_process = start_datetime + process_after    duration = end_datetime - start_process    return {        "item_id": item_id,        "start_datetime": start_datetime,        "end_datetime": end_datetime,        "process_after": process_after,        "repeat_at": repeat_at,        "start_process": start_process,        "duration": duration,    }`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/extra-data-types/#__tabbed_4_4)

 Back to top

[

Previous

Declare Request Example Data



](https://fastapi.tiangolo.com/tutorial/schema-extra-example/)[

Next

Cookie Parameters

](https://fastapi.tiangolo.com/tutorial/cookie-params/)

The FastAPI trademark is owned by [@tiangolo](https://tiangolo.com/) and is registered in the US and across other regions

Made with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)

[](https://github.com/fastapi/fastapi "github.com")[](https://discord.gg/VQjSZaeJmf "discord.gg")[](https://twitter.com/fastapi "twitter.com")[](https://www.linkedin.com/company/fastapi "www.linkedin.com")[](https://tiangolo.com/ "tiangolo.com")


# Cookie Parameters[¶](https://fastapi.tiangolo.com/tutorial/cookie-params/#cookie-parameters "Permanent link")

You can define Cookie parameters the same way you define `Query` and `Path` parameters.

## Import `Cookie`[¶](https://fastapi.tiangolo.com/tutorial/cookie-params/#import-cookie "Permanent link")

First import `Cookie`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_1_1)

`from typing import Annotated from fastapi import Cookie, FastAPI app = FastAPI() @app.get("/items/") async def read_items(ads_id: Annotated[str | None, Cookie()] = None):     return {"ads_id": ads_id}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_2_4)

## Declare `Cookie` parameters[¶](https://fastapi.tiangolo.com/tutorial/cookie-params/#declare-cookie-parameters "Permanent link")

Then declare the cookie parameters using the same structure as with `Path` and `Query`.

You can define the default value as well as all the extra validation or annotation parameters:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_3_1)

`from typing import Annotated from fastapi import Cookie, FastAPI app = FastAPI() @app.get("/items/") async def read_items(ads_id: Annotated[str | None, Cookie()] = None):     return {"ads_id": ads_id}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/cookie-params/#__tabbed_4_4)

Technical Details

`Cookie` is a "sister" class of `Path` and `Query`. It also inherits from the same common `Param` class.

But remember that when you import `Query`, `Path`, `Cookie` and others from `fastapi`, those are actually functions that return special classes.

Info

To declare cookies, you need to use `Cookie`, because otherwise the parameters would be interpreted as query parameters.

## Recap[¶](https://fastapi.tiangolo.com/tutorial/cookie-params/#recap "Permanent link")

Declare cookies with `Cookie`, using the same common pattern as `Query` and `Path`.

# Header Parameters[¶](https://fastapi.tiangolo.com/tutorial/header-params/#header-parameters "Permanent link")

You can define Header parameters the same way you define `Query`, `Path` and `Cookie` parameters.

## Import `Header`[¶](https://fastapi.tiangolo.com/tutorial/header-params/#import-header "Permanent link")

First import `Header`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_1_1)

`from typing import Annotated from fastapi import FastAPI, Header app = FastAPI() @app.get("/items/") async def read_items(user_agent: Annotated[str | None, Header()] = None):     return {"User-Agent": user_agent}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_2_4)

## Declare `Header` parameters[¶](https://fastapi.tiangolo.com/tutorial/header-params/#declare-header-parameters "Permanent link")

Then declare the header parameters using the same structure as with `Path`, `Query` and `Cookie`.

You can define the default value as well as all the extra validation or annotation parameters:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_3_1)

`from typing import Annotated from fastapi import FastAPI, Header app = FastAPI() @app.get("/items/") async def read_items(user_agent: Annotated[str | None, Header()] = None):     return {"User-Agent": user_agent}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_4_4)

Technical Details

`Header` is a "sister" class of `Path`, `Query` and `Cookie`. It also inherits from the same common `Param` class.

But remember that when you import `Query`, `Path`, `Header`, and others from `fastapi`, those are actually functions that return special classes.

Info

To declare headers, you need to use `Header`, because otherwise the parameters would be interpreted as query parameters.

## Automatic conversion[¶](https://fastapi.tiangolo.com/tutorial/header-params/#automatic-conversion "Permanent link")

`Header` has a little extra functionality on top of what `Path`, `Query` and `Cookie` provide.

Most of the standard headers are separated by a "hyphen" character, also known as the "minus symbol" (`-`).

But a variable like `user-agent` is invalid in Python.

So, by default, `Header` will convert the parameter names characters from underscore (`_`) to hyphen (`-`) to extract and document the headers.

Also, HTTP headers are case-insensitive, so, you can declare them with standard Python style (also known as "snake_case").

So, you can use `user_agent` as you normally would in Python code, instead of needing to capitalize the first letters as `User_Agent` or something similar.

If for some reason you need to disable automatic conversion of underscores to hyphens, set the parameter `convert_underscores` of `Header` to `False`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_5_1)

`from typing import Annotated from fastapi import FastAPI, Header app = FastAPI() @app.get("/items/") async def read_items(     strange_header: Annotated[str | None, Header(convert_underscores=False)] = None, ):     return {"strange_header": strange_header}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_6_2)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_6_3)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_6_4)

Warning

Before setting `convert_underscores` to `False`, bear in mind that some HTTP proxies and servers disallow the usage of headers with underscores.

## Duplicate headers[¶](https://fastapi.tiangolo.com/tutorial/header-params/#duplicate-headers "Permanent link")

It is possible to receive duplicate headers. That means, the same header with multiple values.

You can define those cases using a list in the type declaration.

You will receive all the values from the duplicate header as a Python `list`.

For example, to declare a header of `X-Token` that can appear more than once, you can write:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_7_1)

`from typing import Annotated from fastapi import FastAPI, Header app = FastAPI() @app.get("/items/") async def read_items(x_token: Annotated[list[str] | None, Header()] = None):     return {"X-Token values": x_token}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_8_2)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_8_3)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_8_4)[](https://fastapi.tiangolo.com/tutorial/header-params/#__tabbed_8_5)

If you communicate with that _path operation_ sending two HTTP headers like:

`X-Token: foo X-Token: bar`

The response would be like:

`{     "X-Token values": [        "bar",        "foo"    ] }`

## Recap[¶](https://fastapi.tiangolo.com/tutorial/header-params/#recap "Permanent link")

Declare headers with `Header`, using the same common pattern as `Query`, `Path` and `Cookie`.

And don't worry about underscores in your variables, **FastAPI** will take care of converting them.

# Cookie Parameter Models[¶](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#cookie-parameter-models "Permanent link")

If you have a group of **cookies** that are related, you can create a **Pydantic model** to declare them. 🍪

This would allow you to **re-use the model** in **multiple places** and also to declare validations and metadata for all the parameters at once. 😎

Note

This is supported since FastAPI version `0.115.0`. 🤓

Tip

This same technique applies to `Query`, `Cookie`, and `Header`. 😎

## Cookies with a Pydantic Model[¶](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#cookies-with-a-pydantic-model "Permanent link")

Declare the **cookie** parameters that you need in a **Pydantic model**, and then declare the parameter as `Cookie`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_1_1)

`from typing import Annotated from fastapi import Cookie, FastAPI from pydantic import BaseModel app = FastAPI() class Cookies(BaseModel):     session_id: str    fatebook_tracker: str | None = None    googall_tracker: str | None = None @app.get("/items/") async def read_items(cookies: Annotated[Cookies, Cookie()]):     return cookies`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_2_4)

**FastAPI** will **extract** the data for **each field** from the **cookies** received in the request and give you the Pydantic model you defined.

## Check the Docs[¶](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#check-the-docs "Permanent link")

You can see the defined cookies in the docs UI at `/docs`:

![](https://fastapi.tiangolo.com/img/tutorial/cookie-param-models/image01.png)

Info

Have in mind that, as **browsers handle cookies** in special ways and behind the scenes, they **don't** easily allow **JavaScript** to touch them.

If you go to the **API docs UI** at `/docs` you will be able to see the **documentation** for cookies for your _path operations_.

But even if you **fill the data** and click "Execute", because the docs UI works with **JavaScript**, the cookies won't be sent, and you will see an **error** message as if you didn't write any values.

## Forbid Extra Cookies[¶](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#forbid-extra-cookies "Permanent link")

In some special use cases (probably not very common), you might want to **restrict** the cookies that you want to receive.

Your API now has the power to control its own cookie consent. 🤪🍪

You can use Pydantic's model configuration to `forbid` any `extra` fields:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_3_1)

`from typing import Annotated, Union from fastapi import Cookie, FastAPI from pydantic import BaseModel app = FastAPI() class Cookies(BaseModel):     model_config = {"extra": "forbid"}     session_id: str    fatebook_tracker: Union[str, None] = None    googall_tracker: Union[str, None] = None @app.get("/items/") async def read_items(cookies: Annotated[Cookies, Cookie()]):     return cookies`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/cookie-param-models/#__tabbed_4_4)

If a client tries to send some **extra cookies**, they will receive an **error** response.

Poor cookie banners with all their effort to get your consent for the API to reject it. 🍪

For example, if the client tries to send a `santa_tracker` cookie with a value of `good-list-please`, the client will receive an **error** response telling them that the `santa_tracker` cookie is not allowed:

`{     "detail": [        {            "type": "extra_forbidden",            "loc": ["cookie", "santa_tracker"],            "msg": "Extra inputs are not permitted",            "input": "good-list-please",        }    ] }`

# Header Parameter Models[¶](https://fastapi.tiangolo.com/tutorial/header-param-models/#header-parameter-models "Permanent link")

If you have a group of related **header parameters**, you can create a **Pydantic model** to declare them.

This would allow you to **re-use the model** in **multiple places** and also to declare validations and metadata for all the parameters at once. 😎

Note

This is supported since FastAPI version `0.115.0`. 🤓

## Header Parameters with a Pydantic Model[¶](https://fastapi.tiangolo.com/tutorial/header-param-models/#header-parameters-with-a-pydantic-model "Permanent link")

Declare the **header parameters** that you need in a **Pydantic model**, and then declare the parameter as `Header`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_1_1)

`from typing import Annotated from fastapi import FastAPI, Header from pydantic import BaseModel app = FastAPI() class CommonHeaders(BaseModel):     host: str    save_data: bool    if_modified_since: str | None = None    traceparent: str | None = None    x_tag: list[str] = [] @app.get("/items/") async def read_items(headers: Annotated[CommonHeaders, Header()]):     return headers`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_2_4)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_2_5)

**FastAPI** will **extract** the data for **each field** from the **headers** in the request and give you the Pydantic model you defined.

## Check the Docs[¶](https://fastapi.tiangolo.com/tutorial/header-param-models/#check-the-docs "Permanent link")

You can see the required headers in the docs UI at `/docs`:

![](https://fastapi.tiangolo.com/img/tutorial/header-param-models/image01.png)

## Forbid Extra Headers[¶](https://fastapi.tiangolo.com/tutorial/header-param-models/#forbid-extra-headers "Permanent link")

In some special use cases (probably not very common), you might want to **restrict** the headers that you want to receive.

You can use Pydantic's model configuration to `forbid` any `extra` fields:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_3_1)

`from typing import Annotated from fastapi import FastAPI, Header from pydantic import BaseModel app = FastAPI() class CommonHeaders(BaseModel):     model_config = {"extra": "forbid"}     host: str    save_data: bool    if_modified_since: str | None = None    traceparent: str | None = None    x_tag: list[str] = [] @app.get("/items/") async def read_items(headers: Annotated[CommonHeaders, Header()]):     return headers`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_4_4)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_4_5)

If a client tries to send some **extra headers**, they will receive an **error** response.

For example, if the client tries to send a `tool` header with a value of `plumbus`, they will receive an **error** response telling them that the header parameter `tool` is not allowed:

`{     "detail": [        {            "type": "extra_forbidden",            "loc": ["header", "tool"],            "msg": "Extra inputs are not permitted",            "input": "plumbus",        }    ] }`

## Disable Convert Underscores[¶](https://fastapi.tiangolo.com/tutorial/header-param-models/#disable-convert-underscores "Permanent link")

The same way as with regular header parameters, when you have underscore characters in the parameter names, they are **automatically converted to hyphens**.

For example, if you have a header parameter `save_data` in the code, the expected HTTP header will be `save-data`, and it will show up like that in the docs.

If for some reason you need to disable this automatic conversion, you can do it as well for Pydantic models for header parameters.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_5_1)

`from typing import Annotated from fastapi import FastAPI, Header from pydantic import BaseModel app = FastAPI() class CommonHeaders(BaseModel):     host: str    save_data: bool    if_modified_since: str | None = None    traceparent: str | None = None    x_tag: list[str] = [] @app.get("/items/") async def read_items(     headers: Annotated[CommonHeaders, Header(convert_underscores=False)], ):     return headers`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_6_2)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_6_3)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_6_4)[](https://fastapi.tiangolo.com/tutorial/header-param-models/#__tabbed_6_5)

Warning

Before setting `convert_underscores` to `False`, bear in mind that some HTTP proxies and servers disallow the usage of headers with underscores.# Response Model - Return Type[¶](https://fastapi.tiangolo.com/tutorial/response-model/#response-model-return-type "Permanent link")

You can declare the type used for the response by annotating the _path operation function_ **return type**.

You can use **type annotations** the same way you would for input data in function **parameters**, you can use Pydantic models, lists, dictionaries, scalar values like integers, booleans, etc.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_1_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: list[str] = [] @app.post("/items/") async def create_item(item: Item) -> Item:     return item @app.get("/items/") async def read_items() -> list[Item]:     return [        Item(name="Portal Gun", price=42.0),        Item(name="Plumbus", price=32.0),    ]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_2_2)

FastAPI will use this return type to:

- **Validate** the returned data.
    - If the data is invalid (e.g. you are missing a field), it means that _your_ app code is broken, not returning what it should, and it will return a server error instead of returning incorrect data. This way you and your clients can be certain that they will receive the data and the data shape expected.
- Add a **JSON Schema** for the response, in the OpenAPI _path operation_.
    - This will be used by the **automatic docs**.
    - It will also be used by automatic client code generation tools.

But most importantly:

- It will **limit and filter** the output data to what is defined in the return type.
    - This is particularly important for **security**, we'll see more of that below.

## `response_model` Parameter[¶](https://fastapi.tiangolo.com/tutorial/response-model/#response_model-parameter "Permanent link")

There are some cases where you need or want to return some data that is not exactly what the type declares.

For example, you could want to **return a dictionary** or a database object, but **declare it as a Pydantic model**. This way the Pydantic model would do all the data documentation, validation, etc. for the object that you returned (e.g. a dictionary or database object).

If you added the return type annotation, tools and editors would complain with a (correct) error telling you that your function is returning a type (e.g. a dict) that is different from what you declared (e.g. a Pydantic model).

In those cases, you can use the _path operation decorator_ parameter `response_model` instead of the return type.

You can use the `response_model` parameter in any of the _path operations_:

- `@app.get()`
- `@app.post()`
- `@app.put()`
- `@app.delete()`
- etc.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_3_1)

`from typing import Any from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: list[str] = [] @app.post("/items/", response_model=Item) async def create_item(item: Item) -> Any:     return item @app.get("/items/", response_model=list[Item]) async def read_items() -> Any:     return [        {"name": "Portal Gun", "price": 42.0},        {"name": "Plumbus", "price": 32.0},    ]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_4_2)

Note

Notice that `response_model` is a parameter of the "decorator" method (`get`, `post`, etc). Not of your _path operation function_, like all the parameters and body.

`response_model` receives the same type you would declare for a Pydantic model field, so, it can be a Pydantic model, but it can also be, e.g. a `list` of Pydantic models, like `List[Item]`.

FastAPI will use this `response_model` to do all the data documentation, validation, etc. and also to **convert and filter the output data** to its type declaration.

Tip

If you have strict type checks in your editor, mypy, etc, you can declare the function return type as `Any`.

That way you tell the editor that you are intentionally returning anything. But FastAPI will still do the data documentation, validation, filtering, etc. with the `response_model`.

### `response_model` Priority[¶](https://fastapi.tiangolo.com/tutorial/response-model/#response_model-priority "Permanent link")

If you declare both a return type and a `response_model`, the `response_model` will take priority and be used by FastAPI.

This way you can add correct type annotations to your functions even when you are returning a type different than the response model, to be used by the editor and tools like mypy. And still you can have FastAPI do the data validation, documentation, etc. using the `response_model`.

You can also use `response_model=None` to disable creating a response model for that _path operation_, you might need to do it if you are adding type annotations for things that are not valid Pydantic fields, you will see an example of that in one of the sections below.

## Return the same input data[¶](https://fastapi.tiangolo.com/tutorial/response-model/#return-the-same-input-data "Permanent link")

Here we are declaring a `UserIn` model, it will contain a plaintext password:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_5_1)

`from fastapi import FastAPI from pydantic import BaseModel, EmailStr app = FastAPI() class UserIn(BaseModel):     username: str    password: str    email: EmailStr    full_name: str | None = None # Don't do this in production! @app.post("/user/") async def create_user(user: UserIn) -> UserIn:     return user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_6_1)

Info

To use `EmailStr`, first install [`email-validator`](https://github.com/JoshData/python-email-validator).

Make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install it, for example:

`$ pip install email-validator`

or with:

`$ pip install "pydantic[email]"`

And we are using this model to declare our input and the same model to declare our output:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_7_1)

`from fastapi import FastAPI from pydantic import BaseModel, EmailStr app = FastAPI() class UserIn(BaseModel):     username: str    password: str    email: EmailStr    full_name: str | None = None # Don't do this in production! @app.post("/user/") async def create_user(user: UserIn) -> UserIn:     return user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_8_1)

Now, whenever a browser is creating a user with a password, the API will return the same password in the response.

In this case, it might not be a problem, because it's the same user sending the password.

But if we use the same model for another _path operation_, we could be sending our user's passwords to every client.

Danger

Never store the plain password of a user or send it in a response like this, unless you know all the caveats and you know what you are doing.

## Add an output model[¶](https://fastapi.tiangolo.com/tutorial/response-model/#add-an-output-model "Permanent link")

We can instead create an input model with the plaintext password and an output model without it:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_9_1)

`from typing import Any from fastapi import FastAPI from pydantic import BaseModel, EmailStr app = FastAPI() class UserIn(BaseModel):     username: str    password: str    email: EmailStr    full_name: str | None = None class UserOut(BaseModel):     username: str    email: EmailStr    full_name: str | None = None @app.post("/user/", response_model=UserOut) async def create_user(user: UserIn) -> Any:     return user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_10_1)

Here, even though our _path operation function_ is returning the same input user that contains the password:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_11_1)

`from typing import Any from fastapi import FastAPI from pydantic import BaseModel, EmailStr app = FastAPI() class UserIn(BaseModel):     username: str    password: str    email: EmailStr    full_name: str | None = None class UserOut(BaseModel):     username: str    email: EmailStr    full_name: str | None = None @app.post("/user/", response_model=UserOut) async def create_user(user: UserIn) -> Any:     return user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_12_1)

...we declared the `response_model` to be our model `UserOut`, that doesn't include the password:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_13_1)

`from typing import Any from fastapi import FastAPI from pydantic import BaseModel, EmailStr app = FastAPI() class UserIn(BaseModel):     username: str    password: str    email: EmailStr    full_name: str | None = None class UserOut(BaseModel):     username: str    email: EmailStr    full_name: str | None = None @app.post("/user/", response_model=UserOut) async def create_user(user: UserIn) -> Any:     return user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_14_1)

So, **FastAPI** will take care of filtering out all the data that is not declared in the output model (using Pydantic).

### `response_model` or Return Type[¶](https://fastapi.tiangolo.com/tutorial/response-model/#response_model-or-return-type "Permanent link")

In this case, because the two models are different, if we annotated the function return type as `UserOut`, the editor and tools would complain that we are returning an invalid type, as those are different classes.

That's why in this example we have to declare it in the `response_model` parameter.

...but continue reading below to see how to overcome that.

## Return Type and Data Filtering[¶](https://fastapi.tiangolo.com/tutorial/response-model/#return-type-and-data-filtering "Permanent link")

Let's continue from the previous example. We wanted to **annotate the function with one type**, but we wanted to be able to return from the function something that actually includes **more data**.

We want FastAPI to keep **filtering** the data using the response model. So that even though the function returns more data, the response will only include the fields declared in the response model.

In the previous example, because the classes were different, we had to use the `response_model` parameter. But that also means that we don't get the support from the editor and tools checking the function return type.

But in most of the cases where we need to do something like this, we want the model just to **filter/remove** some of the data as in this example.

And in those cases, we can use classes and inheritance to take advantage of function **type annotations** to get better support in the editor and tools, and still get the FastAPI **data filtering**.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_15_1)

`from fastapi import FastAPI from pydantic import BaseModel, EmailStr app = FastAPI() class BaseUser(BaseModel):     username: str    email: EmailStr    full_name: str | None = None class UserIn(BaseUser):     password: str @app.post("/user/") async def create_user(user: UserIn) -> BaseUser:     return user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_16_1)

With this, we get tooling support, from editors and mypy as this code is correct in terms of types, but we also get the data filtering from FastAPI.

How does this work? Let's check that out. 🤓

### Type Annotations and Tooling[¶](https://fastapi.tiangolo.com/tutorial/response-model/#type-annotations-and-tooling "Permanent link")

First let's see how editors, mypy and other tools would see this.

`BaseUser` has the base fields. Then `UserIn` inherits from `BaseUser` and adds the `password` field, so, it will include all the fields from both models.

We annotate the function return type as `BaseUser`, but we are actually returning a `UserIn` instance.

The editor, mypy, and other tools won't complain about this because, in typing terms, `UserIn` is a subclass of `BaseUser`, which means it's a _valid_ type when what is expected is anything that is a `BaseUser`.

### FastAPI Data Filtering[¶](https://fastapi.tiangolo.com/tutorial/response-model/#fastapi-data-filtering "Permanent link")

Now, for FastAPI, it will see the return type and make sure that what you return includes **only** the fields that are declared in the type.

FastAPI does several things internally with Pydantic to make sure that those same rules of class inheritance are not used for the returned data filtering, otherwise you could end up returning much more data than what you expected.

This way, you can get the best of both worlds: type annotations with **tooling support** and **data filtering**.

## See it in the docs[¶](https://fastapi.tiangolo.com/tutorial/response-model/#see-it-in-the-docs "Permanent link")

When you see the automatic docs, you can check that the input model and output model will both have their own JSON Schema:

![](https://fastapi.tiangolo.com/img/tutorial/response-model/image01.png)

And both models will be used for the interactive API documentation:

![](https://fastapi.tiangolo.com/img/tutorial/response-model/image02.png)

## Other Return Type Annotations[¶](https://fastapi.tiangolo.com/tutorial/response-model/#other-return-type-annotations "Permanent link")

There might be cases where you return something that is not a valid Pydantic field and you annotate it in the function, only to get the support provided by tooling (the editor, mypy, etc).

### Return a Response Directly[¶](https://fastapi.tiangolo.com/tutorial/response-model/#return-a-response-directly "Permanent link")

The most common case would be [returning a Response directly as explained later in the advanced docs](https://fastapi.tiangolo.com/advanced/response-directly/).

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_17_1)

`from fastapi import FastAPI, Response from fastapi.responses import JSONResponse, RedirectResponse app = FastAPI() @app.get("/portal") async def get_portal(teleport: bool = False) -> Response:     if teleport:        return RedirectResponse(url="https://www.youtube.com/watch?v=dQw4w9WgXcQ")    return JSONResponse(content={"message": "Here's your interdimensional portal."})`

This simple case is handled automatically by FastAPI because the return type annotation is the class (or a subclass of) `Response`.

And tools will also be happy because both `RedirectResponse` and `JSONResponse` are subclasses of `Response`, so the type annotation is correct.

### Annotate a Response Subclass[¶](https://fastapi.tiangolo.com/tutorial/response-model/#annotate-a-response-subclass "Permanent link")

You can also use a subclass of `Response` in the type annotation:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_18_1)

`from fastapi import FastAPI from fastapi.responses import RedirectResponse app = FastAPI() @app.get("/teleport") async def get_teleport() -> RedirectResponse:     return RedirectResponse(url="https://www.youtube.com/watch?v=dQw4w9WgXcQ")`

This will also work because `RedirectResponse` is a subclass of `Response`, and FastAPI will automatically handle this simple case.

### Invalid Return Type Annotations[¶](https://fastapi.tiangolo.com/tutorial/response-model/#invalid-return-type-annotations "Permanent link")

But when you return some other arbitrary object that is not a valid Pydantic type (e.g. a database object) and you annotate it like that in the function, FastAPI will try to create a Pydantic response model from that type annotation, and will fail.

The same would happen if you had something like a union between different types where one or more of them are not valid Pydantic types, for example this would fail 💥:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_19_1)

`from fastapi import FastAPI, Response from fastapi.responses import RedirectResponse app = FastAPI() @app.get("/portal") async def get_portal(teleport: bool = False) -> Response | dict:     if teleport:        return RedirectResponse(url="https://www.youtube.com/watch?v=dQw4w9WgXcQ")    return {"message": "Here's your interdimensional portal."}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_20_1)

...this fails because the type annotation is not a Pydantic type and is not just a single `Response` class or subclass, it's a union (any of the two) between a `Response` and a `dict`.

### Disable Response Model[¶](https://fastapi.tiangolo.com/tutorial/response-model/#disable-response-model "Permanent link")

Continuing from the example above, you might not want to have the default data validation, documentation, filtering, etc. that is performed by FastAPI.

But you might want to still keep the return type annotation in the function to get the support from tools like editors and type checkers (e.g. mypy).

In this case, you can disable the response model generation by setting `response_model=None`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_21_1)

`from fastapi import FastAPI, Response from fastapi.responses import RedirectResponse app = FastAPI() @app.get("/portal", response_model=None) async def get_portal(teleport: bool = False) -> Response | dict:     if teleport:        return RedirectResponse(url="https://www.youtube.com/watch?v=dQw4w9WgXcQ")    return {"message": "Here's your interdimensional portal."}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_22_1)

This will make FastAPI skip the response model generation and that way you can have any return type annotations you need without it affecting your FastAPI application. 🤓

## Response Model encoding parameters[¶](https://fastapi.tiangolo.com/tutorial/response-model/#response-model-encoding-parameters "Permanent link")

Your response model could have default values, like:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_23_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float = 10.5    tags: list[str] = [] items = {     "foo": {"name": "Foo", "price": 50.2},    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []}, } @app.get("/items/{item_id}", response_model=Item, response_model_exclude_unset=True) async def read_item(item_id: str):     return items[item_id]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_24_1)[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_24_2)

- `description: Union[str, None] = None` (or `str | None = None` in Python 3.10) has a default of `None`.
- `tax: float = 10.5` has a default of `10.5`.
- `tags: List[str] = []` has a default of an empty list: `[]`.

but you might want to omit them from the result if they were not actually stored.

For example, if you have models with many optional attributes in a NoSQL database, but you don't want to send very long JSON responses full of default values.

### Use the `response_model_exclude_unset` parameter[¶](https://fastapi.tiangolo.com/tutorial/response-model/#use-the-response_model_exclude_unset-parameter "Permanent link")

You can set the _path operation decorator_ parameter `response_model_exclude_unset=True`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_25_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float = 10.5    tags: list[str] = [] items = {     "foo": {"name": "Foo", "price": 50.2},    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []}, } @app.get("/items/{item_id}", response_model=Item, response_model_exclude_unset=True) async def read_item(item_id: str):     return items[item_id]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_26_1)[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_26_2)

and those default values won't be included in the response, only the values actually set.

So, if you send a request to that _path operation_ for the item with ID `foo`, the response (not including default values) will be:

`{     "name": "Foo",    "price": 50.2 }`

Info

In Pydantic v1 the method was called `.dict()`, it was deprecated (but still supported) in Pydantic v2, and renamed to `.model_dump()`.

The examples here use `.dict()` for compatibility with Pydantic v1, but you should use `.model_dump()` instead if you can use Pydantic v2.

Info

FastAPI uses Pydantic model's `.dict()` with [its `exclude_unset` parameter](https://docs.pydantic.dev/1.10/usage/exporting_models/#modeldict) to achieve this.

Info

You can also use:

- `response_model_exclude_defaults=True`
- `response_model_exclude_none=True`

as described in [the Pydantic docs](https://docs.pydantic.dev/1.10/usage/exporting_models/#modeldict) for `exclude_defaults` and `exclude_none`.

#### Data with values for fields with defaults[¶](https://fastapi.tiangolo.com/tutorial/response-model/#data-with-values-for-fields-with-defaults "Permanent link")

But if your data has values for the model's fields with default values, like the item with ID `bar`:

`{     "name": "Bar",    "description": "The bartenders",    "price": 62,    "tax": 20.2 }`

they will be included in the response.

#### Data with the same values as the defaults[¶](https://fastapi.tiangolo.com/tutorial/response-model/#data-with-the-same-values-as-the-defaults "Permanent link")

If the data has the same values as the default ones, like the item with ID `baz`:

`{     "name": "Baz",    "description": None,    "price": 50.2,    "tax": 10.5,    "tags": [] }`

FastAPI is smart enough (actually, Pydantic is smart enough) to realize that, even though `description`, `tax`, and `tags` have the same values as the defaults, they were set explicitly (instead of taken from the defaults).

So, they will be included in the JSON response.

Tip

Notice that the default values can be anything, not only `None`.

They can be a list (`[]`), a `float` of `10.5`, etc.

### `response_model_include` and `response_model_exclude`[¶](https://fastapi.tiangolo.com/tutorial/response-model/#response_model_include-and-response_model_exclude "Permanent link")

You can also use the _path operation decorator_ parameters `response_model_include` and `response_model_exclude`.

They take a `set` of `str` with the name of the attributes to include (omitting the rest) or to exclude (including the rest).

This can be used as a quick shortcut if you have only one Pydantic model and want to remove some data from the output.

Tip

But it is still recommended to use the ideas above, using multiple classes, instead of these parameters.

This is because the JSON Schema generated in your app's OpenAPI (and the docs) will still be the one for the complete model, even if you use `response_model_include` or `response_model_exclude` to omit some attributes.

This also applies to `response_model_by_alias` that works similarly.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_27_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float = 10.5 items = {     "foo": {"name": "Foo", "price": 50.2},    "bar": {"name": "Bar", "description": "The Bar fighters", "price": 62, "tax": 20.2},    "baz": {        "name": "Baz",        "description": "There goes my baz",        "price": 50.2,        "tax": 10.5,    }, } @app.get(     "/items/{item_id}/name",    response_model=Item,    response_model_include={"name", "description"}, ) async def read_item_name(item_id: str):     return items[item_id] @app.get("/items/{item_id}/public", response_model=Item, response_model_exclude={"tax"}) async def read_item_public_data(item_id: str):     return items[item_id]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_28_1)

Tip

The syntax `{"name", "description"}` creates a `set` with those two values.

It is equivalent to `set(["name", "description"])`.

#### Using `list`s instead of `set`s[¶](https://fastapi.tiangolo.com/tutorial/response-model/#using-lists-instead-of-sets "Permanent link")

If you forget to use a `set` and use a `list` or `tuple` instead, FastAPI will still convert it to a `set` and it will work correctly:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/response-model/#__tabbed_29_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float = 10.5 items = {     "foo": {"name": "Foo", "price": 50.2},    "bar": {"name": "Bar", "description": "The Bar fighters", "price": 62, "tax": 20.2},    "baz": {        "name": "Baz",        "description": "There goes my baz",        "price": 50.2,        "tax": 10.5,    }, } @app.get(     "/items/{item_id}/name",    response_model=Item,    response_model_include=["name", "description"], ) async def read_item_name(item_id: str):     return items[item_id] @app.get("/items/{item_id}/public", response_model=Item, response_model_exclude=["tax"]) async def read_item_public_data(item_id: str):     return items[item_id]`

# Extra Models[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#extra-models "Permanent link")

Continuing with the previous example, it will be common to have more than one related model.

This is especially the case for user models, because:

- The **input model** needs to be able to have a password.
- The **output model** should not have a password.
- The **database model** would probably need to have a hashed password.

Danger

Never store user's plaintext passwords. Always store a "secure hash" that you can then verify.

If you don't know, you will learn what a "password hash" is in the [security chapters](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#password-hashing).

## Multiple models[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#multiple-models "Permanent link")

Here's a general idea of how the models could look like with their password fields and the places where they are used:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_1_1)

`from fastapi import FastAPI from pydantic import BaseModel, EmailStr app = FastAPI() class UserIn(BaseModel):     username: str    password: str    email: EmailStr    full_name: str | None = None class UserOut(BaseModel):     username: str    email: EmailStr    full_name: str | None = None class UserInDB(BaseModel):     username: str    hashed_password: str    email: EmailStr    full_name: str | None = None def fake_password_hasher(raw_password: str):     return "supersecret" + raw_password def fake_save_user(user_in: UserIn):     hashed_password = fake_password_hasher(user_in.password)    user_in_db = UserInDB(**user_in.dict(), hashed_password=hashed_password)    print("User saved! ..not really")    return user_in_db @app.post("/user/", response_model=UserOut) async def create_user(user_in: UserIn):     user_saved = fake_save_user(user_in)    return user_saved`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_2_1)

Info

In Pydantic v1 the method was called `.dict()`, it was deprecated (but still supported) in Pydantic v2, and renamed to `.model_dump()`.

The examples here use `.dict()` for compatibility with Pydantic v1, but you should use `.model_dump()` instead if you can use Pydantic v2.

### About `**user_in.dict()`[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#about-user_indict "Permanent link")

#### Pydantic's `.dict()`[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#pydantics-dict "Permanent link")

`user_in` is a Pydantic model of class `UserIn`.

Pydantic models have a `.dict()` method that returns a `dict` with the model's data.

So, if we create a Pydantic object `user_in` like:

`user_in = UserIn(username="john", password="secret", email="john.doe@example.com")`

and then we call:

`user_dict = user_in.dict()`

we now have a `dict` with the data in the variable `user_dict` (it's a `dict` instead of a Pydantic model object).

And if we call:

`print(user_dict)`

we would get a Python `dict` with:

`{     'username': 'john',    'password': 'secret',    'email': 'john.doe@example.com',    'full_name': None, }`

#### Unpacking a `dict`[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#unpacking-a-dict "Permanent link")

If we take a `dict` like `user_dict` and pass it to a function (or class) with `**user_dict`, Python will "unpack" it. It will pass the keys and values of the `user_dict` directly as key-value arguments.

So, continuing with the `user_dict` from above, writing:

`UserInDB(**user_dict)`

would result in something equivalent to:

`UserInDB(     username="john",    password="secret",    email="john.doe@example.com",    full_name=None, )`

Or more exactly, using `user_dict` directly, with whatever contents it might have in the future:

`UserInDB(     username = user_dict["username"],    password = user_dict["password"],    email = user_dict["email"],    full_name = user_dict["full_name"], )`

#### A Pydantic model from the contents of another[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#a-pydantic-model-from-the-contents-of-another "Permanent link")

As in the example above we got `user_dict` from `user_in.dict()`, this code:

`user_dict = user_in.dict() UserInDB(**user_dict)`

would be equivalent to:

`UserInDB(**user_in.dict())`

...because `user_in.dict()` is a `dict`, and then we make Python "unpack" it by passing it to `UserInDB` prefixed with `**`.

So, we get a Pydantic model from the data in another Pydantic model.

#### Unpacking a `dict` and extra keywords[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#unpacking-a-dict-and-extra-keywords "Permanent link")

And then adding the extra keyword argument `hashed_password=hashed_password`, like in:

`UserInDB(**user_in.dict(), hashed_password=hashed_password)`

...ends up being like:

`UserInDB(     username = user_dict["username"],    password = user_dict["password"],    email = user_dict["email"],    full_name = user_dict["full_name"],    hashed_password = hashed_password, )`

Warning

The supporting additional functions `fake_password_hasher` and `fake_save_user` are just to demo a possible flow of the data, but they of course are not providing any real security.

## Reduce duplication[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#reduce-duplication "Permanent link")

Reducing code duplication is one of the core ideas in **FastAPI**.

As code duplication increments the chances of bugs, security issues, code desynchronization issues (when you update in one place but not in the others), etc.

And these models are all sharing a lot of the data and duplicating attribute names and types.

We could do better.

We can declare a `UserBase` model that serves as a base for our other models. And then we can make subclasses of that model that inherit its attributes (type declarations, validation, etc).

All the data conversion, validation, documentation, etc. will still work as normally.

That way, we can declare just the differences between the models (with plaintext `password`, with `hashed_password` and without password):

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_3_1)

`from fastapi import FastAPI from pydantic import BaseModel, EmailStr app = FastAPI() class UserBase(BaseModel):     username: str    email: EmailStr    full_name: str | None = None class UserIn(UserBase):     password: str class UserOut(UserBase):     pass class UserInDB(UserBase):     hashed_password: str def fake_password_hasher(raw_password: str):     return "supersecret" + raw_password def fake_save_user(user_in: UserIn):     hashed_password = fake_password_hasher(user_in.password)    user_in_db = UserInDB(**user_in.dict(), hashed_password=hashed_password)    print("User saved! ..not really")    return user_in_db @app.post("/user/", response_model=UserOut) async def create_user(user_in: UserIn):     user_saved = fake_save_user(user_in)    return user_saved`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_4_1)

## `Union` or `anyOf`[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#union-or-anyof "Permanent link")

You can declare a response to be the `Union` of two or more types, that means, that the response would be any of them.

It will be defined in OpenAPI with `anyOf`.

To do that, use the standard Python type hint [`typing.Union`](https://docs.python.org/3/library/typing.html#typing.Union):

Note

When defining a [`Union`](https://docs.pydantic.dev/latest/concepts/types/#unions), include the most specific type first, followed by the less specific type. In the example below, the more specific `PlaneItem` comes before `CarItem` in `Union[PlaneItem, CarItem]`.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_5_1)

`from typing import Union from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class BaseItem(BaseModel):     description: str    type: str class CarItem(BaseItem):     type: str = "car" class PlaneItem(BaseItem):     type: str = "plane"    size: int items = {     "item1": {"description": "All my friends drive a low rider", "type": "car"},    "item2": {        "description": "Music is my aeroplane, it's my aeroplane",        "type": "plane",        "size": 5,    }, } @app.get("/items/{item_id}", response_model=Union[PlaneItem, CarItem]) async def read_item(item_id: str):     return items[item_id]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_6_1)

### `Union` in Python 3.10[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#union-in-python-310 "Permanent link")

In this example we pass `Union[PlaneItem, CarItem]` as the value of the argument `response_model`.

Because we are passing it as a **value to an argument** instead of putting it in a **type annotation**, we have to use `Union` even in Python 3.10.

If it was in a type annotation we could have used the vertical bar, as:

`some_variable: PlaneItem | CarItem`

But if we put that in the assignment `response_model=PlaneItem | CarItem` we would get an error, because Python would try to perform an **invalid operation** between `PlaneItem` and `CarItem` instead of interpreting that as a type annotation.

## List of models[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#list-of-models "Permanent link")

The same way, you can declare responses of lists of objects.

For that, use the standard Python `typing.List` (or just `list` in Python 3.9 and above):

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_7_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str items = [     {"name": "Foo", "description": "There comes my hero"},    {"name": "Red", "description": "It's my aeroplane"}, ] @app.get("/items/", response_model=list[Item]) async def read_items():     return items`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_8_1)

## Response with arbitrary `dict`[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#response-with-arbitrary-dict "Permanent link")

You can also declare a response using a plain arbitrary `dict`, declaring just the type of the keys and values, without using a Pydantic model.

This is useful if you don't know the valid field/attribute names (that would be needed for a Pydantic model) beforehand.

In this case, you can use `typing.Dict` (or just `dict` in Python 3.9 and above):

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_9_1)

`from fastapi import FastAPI app = FastAPI() @app.get("/keyword-weights/", response_model=dict[str, float]) async def read_keyword_weights():     return {"foo": 2.3, "bar": 3.4}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/extra-models/#__tabbed_10_1)

## Recap[¶](https://fastapi.tiangolo.com/tutorial/extra-models/#recap "Permanent link")

Use multiple Pydantic models and inherit freely for each case.

You don't need to have a single data model per entity if that entity must be able to have different "states". As the case with the user "entity" with a state including `password`, `password_hash` and no password.

 Back to top

[

  
](https://fastapi.tiangolo.com/tutorial/response-model/)


# Response Status Code[¶](https://fastapi.tiangolo.com/tutorial/response-status-code/#response-status-code "Permanent link")

The same way you can specify a response model, you can also declare the HTTP status code used for the response with the parameter `status_code` in any of the _path operations_:

- `@app.get()`
- `@app.post()`
- `@app.put()`
- `@app.delete()`
- etc.

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/response-status-code/#__tabbed_1_1)

`from fastapi import FastAPI app = FastAPI() @app.post("/items/", status_code=201) async def create_item(name: str):     return {"name": name}`

Note

Notice that `status_code` is a parameter of the "decorator" method (`get`, `post`, etc). Not of your _path operation function_, like all the parameters and body.

The `status_code` parameter receives a number with the HTTP status code.

Info

`status_code` can alternatively also receive an `IntEnum`, such as Python's [`http.HTTPStatus`](https://docs.python.org/3/library/http.html#http.HTTPStatus).

It will:

- Return that status code in the response.
- Document it as such in the OpenAPI schema (and so, in the user interfaces):

![](https://fastapi.tiangolo.com/img/tutorial/response-status-code/image01.png)

Note

Some response codes (see the next section) indicate that the response does not have a body.

FastAPI knows this, and will produce OpenAPI docs that state there is no response body.

## About HTTP status codes[¶](https://fastapi.tiangolo.com/tutorial/response-status-code/#about-http-status-codes "Permanent link")

Note

If you already know what HTTP status codes are, skip to the next section.

In HTTP, you send a numeric status code of 3 digits as part of the response.

These status codes have a name associated to recognize them, but the important part is the number.

In short:

- `100 - 199` are for "Information". You rarely use them directly. Responses with these status codes cannot have a body.
- **`200 - 299`** are for "Successful" responses. These are the ones you would use the most.
    - `200` is the default status code, which means everything was "OK".
    - Another example would be `201`, "Created". It is commonly used after creating a new record in the database.
    - A special case is `204`, "No Content". This response is used when there is no content to return to the client, and so the response must not have a body.
- **`300 - 399`** are for "Redirection". Responses with these status codes may or may not have a body, except for `304`, "Not Modified", which must not have one.
- **`400 - 499`** are for "Client error" responses. These are the second type you would probably use the most.
    - An example is `404`, for a "Not Found" response.
    - For generic errors from the client, you can just use `400`.
- `500 - 599` are for server errors. You almost never use them directly. When something goes wrong at some part in your application code, or server, it will automatically return one of these status codes.

Tip

To know more about each status code and which code is for what, check the [MDN documentation about HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

## Shortcut to remember the names[¶](https://fastapi.tiangolo.com/tutorial/response-status-code/#shortcut-to-remember-the-names "Permanent link")

Let's see the previous example again:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/response-status-code/#__tabbed_2_1)

`from fastapi import FastAPI app = FastAPI() @app.post("/items/", status_code=201) async def create_item(name: str):     return {"name": name}`

`201` is the status code for "Created".

But you don't have to memorize what each of these codes mean.

You can use the convenience variables from `fastapi.status`.

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/response-status-code/#__tabbed_3_1)

`from fastapi import FastAPI, status app = FastAPI() @app.post("/items/", status_code=status.HTTP_201_CREATED) async def create_item(name: str):     return {"name": name}`

They are just a convenience, they hold the same number, but that way you can use the editor's autocomplete to find them:

![](https://fastapi.tiangolo.com/img/tutorial/response-status-code/image02.png)

Technical Details

You could also use `from starlette import status`.

**FastAPI** provides the same `starlette.status` as `fastapi.status` just as a convenience for you, the developer. But it comes directly from Starlette.

# Form Data[¶](https://fastapi.tiangolo.com/tutorial/request-forms/#form-data "Permanent link")

When you need to receive form fields instead of JSON, you can use `Form`.

Info

To use forms, first install [`python-multipart`](https://github.com/Kludex/python-multipart).

Make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install it, for example:

`$ pip install python-multipart`

## Import `Form`[¶](https://fastapi.tiangolo.com/tutorial/request-forms/#import-form "Permanent link")

Import `Form` from `fastapi`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-forms/#__tabbed_1_1)

`from typing import Annotated from fastapi import FastAPI, Form app = FastAPI() @app.post("/login/") async def login(username: Annotated[str, Form()], password: Annotated[str, Form()]):     return {"username": username}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-forms/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/request-forms/#__tabbed_2_2)

## Define `Form` parameters[¶](https://fastapi.tiangolo.com/tutorial/request-forms/#define-form-parameters "Permanent link")

Create form parameters the same way you would for `Body` or `Query`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-forms/#__tabbed_3_1)

`from typing import Annotated from fastapi import FastAPI, Form app = FastAPI() @app.post("/login/") async def login(username: Annotated[str, Form()], password: Annotated[str, Form()]):     return {"username": username}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-forms/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/request-forms/#__tabbed_4_2)

For example, in one of the ways the OAuth2 specification can be used (called "password flow") it is required to send a `username` and `password` as form fields.

The spec requires the fields to be exactly named `username` and `password`, and to be sent as form fields, not JSON.

With `Form` you can declare the same configurations as with `Body` (and `Query`, `Path`, `Cookie`), including validation, examples, an alias (e.g. `user-name` instead of `username`), etc.

Info

`Form` is a class that inherits directly from `Body`.

Tip

To declare form bodies, you need to use `Form` explicitly, because without it the parameters would be interpreted as query parameters or body (JSON) parameters.

## About "Form Fields"[¶](https://fastapi.tiangolo.com/tutorial/request-forms/#about-form-fields "Permanent link")

The way HTML forms (`<form></form>`) sends the data to the server normally uses a "special" encoding for that data, it's different from JSON.

**FastAPI** will make sure to read that data from the right place instead of JSON.

Technical Details

Data from forms is normally encoded using the "media type" `application/x-www-form-urlencoded`.

But when the form includes files, it is encoded as `multipart/form-data`. You'll read about handling files in the next chapter.

If you want to read more about these encodings and form fields, head to the [MDN web docs for `POST`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST).

Warning

You can declare multiple `Form` parameters in a _path operation_, but you can't also declare `Body` fields that you expect to receive as JSON, as the request will have the body encoded using `application/x-www-form-urlencoded` instead of `application/json`.

This is not a limitation of **FastAPI**, it's part of the HTTP protocol.

# Form Models[¶](https://fastapi.tiangolo.com/tutorial/request-form-models/#form-models "Permanent link")

You can use **Pydantic models** to declare **form fields** in FastAPI.

Info

To use forms, first install [`python-multipart`](https://github.com/Kludex/python-multipart).

Make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install it, for example:

`$ pip install python-multipart`

Note

This is supported since FastAPI version `0.113.0`. 🤓

## Pydantic Models for Forms[¶](https://fastapi.tiangolo.com/tutorial/request-form-models/#pydantic-models-for-forms "Permanent link")

You just need to declare a **Pydantic model** with the fields you want to receive as **form fields**, and then declare the parameter as `Form`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-form-models/#__tabbed_1_1)

`from typing import Annotated from fastapi import FastAPI, Form from pydantic import BaseModel app = FastAPI() class FormData(BaseModel):     username: str    password: str @app.post("/login/") async def login(data: Annotated[FormData, Form()]):     return data`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-form-models/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/request-form-models/#__tabbed_2_2)

**FastAPI** will **extract** the data for **each field** from the **form data** in the request and give you the Pydantic model you defined.

## Check the Docs[¶](https://fastapi.tiangolo.com/tutorial/request-form-models/#check-the-docs "Permanent link")

You can verify it in the docs UI at `/docs`:

![](https://fastapi.tiangolo.com/img/tutorial/request-form-models/image01.png)

## Forbid Extra Form Fields[¶](https://fastapi.tiangolo.com/tutorial/request-form-models/#forbid-extra-form-fields "Permanent link")

In some special use cases (probably not very common), you might want to **restrict** the form fields to only those declared in the Pydantic model. And **forbid** any **extra** fields.

Note

This is supported since FastAPI version `0.114.0`. 🤓

You can use Pydantic's model configuration to `forbid` any `extra` fields:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-form-models/#__tabbed_3_1)

`from typing import Annotated from fastapi import FastAPI, Form from pydantic import BaseModel app = FastAPI() class FormData(BaseModel):     username: str    password: str    model_config = {"extra": "forbid"} @app.post("/login/") async def login(data: Annotated[FormData, Form()]):     return data`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-form-models/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/request-form-models/#__tabbed_4_2)

If a client tries to send some extra data, they will receive an **error** response.

For example, if the client tries to send the form fields:

- `username`: `Rick`
- `password`: `Portal Gun`
- `extra`: `Mr. Poopybutthole`

They will receive an error response telling them that the field `extra` is not allowed:

`{     "detail": [        {            "type": "extra_forbidden",            "loc": ["body", "extra"],            "msg": "Extra inputs are not permitted",            "input": "Mr. Poopybutthole"        }    ] }`

## Summary[¶](https://fastapi.tiangolo.com/tutorial/request-form-models/#summary "Permanent link")

You can use Pydantic models to declare form fields in FastAPI. 😎

# Request Files[¶](https://fastapi.tiangolo.com/tutorial/request-files/#request-files "Permanent link")

You can define files to be uploaded by the client using `File`.

Info

To receive uploaded files, first install [`python-multipart`](https://github.com/Kludex/python-multipart).

Make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install it, for example:

`$ pip install python-multipart`

This is because uploaded files are sent as "form data".

## Import `File`[¶](https://fastapi.tiangolo.com/tutorial/request-files/#import-file "Permanent link")

Import `File` and `UploadFile` from `fastapi`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_1_1)

`from typing import Annotated from fastapi import FastAPI, File, UploadFile app = FastAPI() @app.post("/files/") async def create_file(file: Annotated[bytes, File()]):     return {"file_size": len(file)} @app.post("/uploadfile/") async def create_upload_file(file: UploadFile):     return {"filename": file.filename}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_2_2)

## Define `File` Parameters[¶](https://fastapi.tiangolo.com/tutorial/request-files/#define-file-parameters "Permanent link")

Create file parameters the same way you would for `Body` or `Form`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_3_1)

`from typing import Annotated from fastapi import FastAPI, File, UploadFile app = FastAPI() @app.post("/files/") async def create_file(file: Annotated[bytes, File()]):     return {"file_size": len(file)} @app.post("/uploadfile/") async def create_upload_file(file: UploadFile):     return {"filename": file.filename}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_4_2)

Info

`File` is a class that inherits directly from `Form`.

But remember that when you import `Query`, `Path`, `File` and others from `fastapi`, those are actually functions that return special classes.

Tip

To declare File bodies, you need to use `File`, because otherwise the parameters would be interpreted as query parameters or body (JSON) parameters.

The files will be uploaded as "form data".

If you declare the type of your _path operation function_ parameter as `bytes`, **FastAPI** will read the file for you and you will receive the contents as `bytes`.

Keep in mind that this means that the whole contents will be stored in memory. This will work well for small files.

But there are several cases in which you might benefit from using `UploadFile`.

## File Parameters with `UploadFile`[¶](https://fastapi.tiangolo.com/tutorial/request-files/#file-parameters-with-uploadfile "Permanent link")

Define a file parameter with a type of `UploadFile`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_5_1)

`from typing import Annotated from fastapi import FastAPI, File, UploadFile app = FastAPI() @app.post("/files/") async def create_file(file: Annotated[bytes, File()]):     return {"file_size": len(file)} @app.post("/uploadfile/") async def create_upload_file(file: UploadFile):     return {"filename": file.filename}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_6_2)

Using `UploadFile` has several advantages over `bytes`:

- You don't have to use `File()` in the default value of the parameter.
- It uses a "spooled" file:
    - A file stored in memory up to a maximum size limit, and after passing this limit it will be stored in disk.
- This means that it will work well for large files like images, videos, large binaries, etc. without consuming all the memory.
- You can get metadata from the uploaded file.
- It has a [file-like](https://docs.python.org/3/glossary.html#term-file-like-object) `async` interface.
- It exposes an actual Python [`SpooledTemporaryFile`](https://docs.python.org/3/library/tempfile.html#tempfile.SpooledTemporaryFile) object that you can pass directly to other libraries that expect a file-like object.

### `UploadFile`[¶](https://fastapi.tiangolo.com/tutorial/request-files/#uploadfile "Permanent link")

`UploadFile` has the following attributes:

- `filename`: A `str` with the original file name that was uploaded (e.g. `myimage.jpg`).
- `content_type`: A `str` with the content type (MIME type / media type) (e.g. `image/jpeg`).
- `file`: A [`SpooledTemporaryFile`](https://docs.python.org/3/library/tempfile.html#tempfile.SpooledTemporaryFile) (a [file-like](https://docs.python.org/3/glossary.html#term-file-like-object) object). This is the actual Python file object that you can pass directly to other functions or libraries that expect a "file-like" object.

`UploadFile` has the following `async` methods. They all call the corresponding file methods underneath (using the internal `SpooledTemporaryFile`).

- `write(data)`: Writes `data` (`str` or `bytes`) to the file.
- `read(size)`: Reads `size` (`int`) bytes/characters of the file.
- `seek(offset)`: Goes to the byte position `offset` (`int`) in the file.
    - E.g., `await myfile.seek(0)` would go to the start of the file.
    - This is especially useful if you run `await myfile.read()` once and then need to read the contents again.
- `close()`: Closes the file.

As all these methods are `async` methods, you need to "await" them.

For example, inside of an `async` _path operation function_ you can get the contents with:

`contents = await myfile.read()`

If you are inside of a normal `def` _path operation function_, you can access the `UploadFile.file` directly, for example:

`contents = myfile.file.read()`

`async` Technical Details

When you use the `async` methods, **FastAPI** runs the file methods in a threadpool and awaits for them.

Starlette Technical Details

**FastAPI**'s `UploadFile` inherits directly from **Starlette**'s `UploadFile`, but adds some necessary parts to make it compatible with **Pydantic** and the other parts of FastAPI.

## What is "Form Data"[¶](https://fastapi.tiangolo.com/tutorial/request-files/#what-is-form-data "Permanent link")

The way HTML forms (`<form></form>`) sends the data to the server normally uses a "special" encoding for that data, it's different from JSON.

**FastAPI** will make sure to read that data from the right place instead of JSON.

Technical Details

Data from forms is normally encoded using the "media type" `application/x-www-form-urlencoded` when it doesn't include files.

But when the form includes files, it is encoded as `multipart/form-data`. If you use `File`, **FastAPI** will know it has to get the files from the correct part of the body.

If you want to read more about these encodings and form fields, head to the [MDN web docs for `POST`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST).

Warning

You can declare multiple `File` and `Form` parameters in a _path operation_, but you can't also declare `Body` fields that you expect to receive as JSON, as the request will have the body encoded using `multipart/form-data` instead of `application/json`.

This is not a limitation of **FastAPI**, it's part of the HTTP protocol.

## Optional File Upload[¶](https://fastapi.tiangolo.com/tutorial/request-files/#optional-file-upload "Permanent link")

You can make a file optional by using standard type annotations and setting a default value of `None`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_7_1)

`from typing import Annotated from fastapi import FastAPI, File, UploadFile app = FastAPI() @app.post("/files/") async def create_file(file: Annotated[bytes | None, File()] = None):     if not file:        return {"message": "No file sent"}    else:        return {"file_size": len(file)} @app.post("/uploadfile/") async def create_upload_file(file: UploadFile | None = None):     if not file:        return {"message": "No upload file sent"}    else:        return {"filename": file.filename}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_8_2)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_8_3)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_8_4)

## `UploadFile` with Additional Metadata[¶](https://fastapi.tiangolo.com/tutorial/request-files/#uploadfile-with-additional-metadata "Permanent link")

You can also use `File()` with `UploadFile`, for example, to set additional metadata:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_9_1)

`from typing import Annotated from fastapi import FastAPI, File, UploadFile app = FastAPI() @app.post("/files/") async def create_file(file: Annotated[bytes, File(description="A file read as bytes")]):     return {"file_size": len(file)} @app.post("/uploadfile/") async def create_upload_file(     file: Annotated[UploadFile, File(description="A file read as UploadFile")], ):     return {"filename": file.filename}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_10_1)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_10_2)

## Multiple File Uploads[¶](https://fastapi.tiangolo.com/tutorial/request-files/#multiple-file-uploads "Permanent link")

It's possible to upload several files at the same time.

They would be associated to the same "form field" sent using "form data".

To use that, declare a list of `bytes` or `UploadFile`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_11_1)

`from typing import Annotated from fastapi import FastAPI, File, UploadFile from fastapi.responses import HTMLResponse app = FastAPI() @app.post("/files/") async def create_files(files: Annotated[list[bytes], File()]):     return {"file_sizes": [len(file) for file in files]} @app.post("/uploadfiles/") async def create_upload_files(files: list[UploadFile]):     return {"filenames": [file.filename for file in files]} @app.get("/") async def main():     content = """ <body> <form action="/files/" enctype="multipart/form-data" method="post"> <input name="files" type="file" multiple> <input type="submit"> </form> <form action="/uploadfiles/" enctype="multipart/form-data" method="post"> <input name="files" type="file" multiple> <input type="submit"> </form> </body>     """    return HTMLResponse(content=content)`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_12_1)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_12_2)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_12_3)

You will receive, as declared, a `list` of `bytes` or `UploadFile`s.

Technical Details

You could also use `from starlette.responses import HTMLResponse`.

**FastAPI** provides the same `starlette.responses` as `fastapi.responses` just as a convenience for you, the developer. But most of the available responses come directly from Starlette.

### Multiple File Uploads with Additional Metadata[¶](https://fastapi.tiangolo.com/tutorial/request-files/#multiple-file-uploads-with-additional-metadata "Permanent link")

And the same way as before, you can use `File()` to set additional parameters, even for `UploadFile`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_13_1)

`from typing import Annotated from fastapi import FastAPI, File, UploadFile from fastapi.responses import HTMLResponse app = FastAPI() @app.post("/files/") async def create_files(     files: Annotated[list[bytes], File(description="Multiple files as bytes")], ):     return {"file_sizes": [len(file) for file in files]} @app.post("/uploadfiles/") async def create_upload_files(     files: Annotated[        list[UploadFile], File(description="Multiple files as UploadFile")    ], ):     return {"filenames": [file.filename for file in files]} @app.get("/") async def main():     content = """ <body> <form action="/files/" enctype="multipart/form-data" method="post"> <input name="files" type="file" multiple> <input type="submit"> </form> <form action="/uploadfiles/" enctype="multipart/form-data" method="post"> <input name="files" type="file" multiple> <input type="submit"> </form> </body>     """    return HTMLResponse(content=content)`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_14_1)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_14_2)[](https://fastapi.tiangolo.com/tutorial/request-files/#__tabbed_14_3)

## Recap[¶](https://fastapi.tiangolo.com/tutorial/request-files/#recap "Permanent link")

Use `File`, `bytes`, and `UploadFile` to declare files to be uploaded in the request, sent as form data.

# Request Forms and Files[¶](https://fastapi.tiangolo.com/tutorial/request-forms-and-files/#request-forms-and-files "Permanent link")

You can define files and form fields at the same time using `File` and `Form`.

Info

To receive uploaded files and/or form data, first install [`python-multipart`](https://github.com/Kludex/python-multipart).

Make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install it, for example:

`$ pip install python-multipart`

## Import `File` and `Form`[¶](https://fastapi.tiangolo.com/tutorial/request-forms-and-files/#import-file-and-form "Permanent link")

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-forms-and-files/#__tabbed_1_1)

`from typing import Annotated from fastapi import FastAPI, File, Form, UploadFile app = FastAPI() @app.post("/files/") async def create_file(     file: Annotated[bytes, File()],    fileb: Annotated[UploadFile, File()],    token: Annotated[str, Form()], ):     return {        "file_size": len(file),        "token": token,        "fileb_content_type": fileb.content_type,    }`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-forms-and-files/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/request-forms-and-files/#__tabbed_2_2)

## Define `File` and `Form` parameters[¶](https://fastapi.tiangolo.com/tutorial/request-forms-and-files/#define-file-and-form-parameters "Permanent link")

Create file and form parameters the same way you would for `Body` or `Query`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/request-forms-and-files/#__tabbed_3_1)

`from typing import Annotated from fastapi import FastAPI, File, Form, UploadFile app = FastAPI() @app.post("/files/") async def create_file(     file: Annotated[bytes, File()],    fileb: Annotated[UploadFile, File()],    token: Annotated[str, Form()], ):     return {        "file_size": len(file),        "token": token,        "fileb_content_type": fileb.content_type,    }`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/request-forms-and-files/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/request-forms-and-files/#__tabbed_4_2)

The files and form fields will be uploaded as form data and you will receive the files and form fields.

And you can declare some of the files as `bytes` and some as `UploadFile`.

Warning

You can declare multiple `File` and `Form` parameters in a _path operation_, but you can't also declare `Body` fields that you expect to receive as JSON, as the request will have the body encoded using `multipart/form-data` instead of `application/json`.

This is not a limitation of **FastAPI**, it's part of the HTTP protocol.

# Handling Errors[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#handling-errors "Permanent link")

There are many situations in which you need to notify an error to a client that is using your API.

This client could be a browser with a frontend, a code from someone else, an IoT device, etc.

You could need to tell the client that:

- The client doesn't have enough privileges for that operation.
- The client doesn't have access to that resource.
- The item the client was trying to access doesn't exist.
- etc.

In these cases, you would normally return an **HTTP status code** in the range of **400** (from 400 to 499).

This is similar to the 200 HTTP status codes (from 200 to 299). Those "200" status codes mean that somehow there was a "success" in the request.

The status codes in the 400 range mean that there was an error from the client.

Remember all those **"404 Not Found"** errors (and jokes)?

## Use `HTTPException`[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#use-httpexception "Permanent link")

To return HTTP responses with errors to the client you use `HTTPException`.

### Import `HTTPException`[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#import-httpexception "Permanent link")

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/handling-errors/#__tabbed_1_1)

`from fastapi import FastAPI, HTTPException app = FastAPI() items = {"foo": "The Foo Wrestlers"} @app.get("/items/{item_id}") async def read_item(item_id: str):     if item_id not in items:        raise HTTPException(status_code=404, detail="Item not found")    return {"item": items[item_id]}`

### Raise an `HTTPException` in your code[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#raise-an-httpexception-in-your-code "Permanent link")

`HTTPException` is a normal Python exception with additional data relevant for APIs.

Because it's a Python exception, you don't `return` it, you `raise` it.

This also means that if you are inside a utility function that you are calling inside of your _path operation function_, and you raise the `HTTPException` from inside of that utility function, it won't run the rest of the code in the _path operation function_, it will terminate that request right away and send the HTTP error from the `HTTPException` to the client.

The benefit of raising an exception over returning a value will be more evident in the section about Dependencies and Security.

In this example, when the client requests an item by an ID that doesn't exist, raise an exception with a status code of `404`:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/handling-errors/#__tabbed_2_1)

`from fastapi import FastAPI, HTTPException app = FastAPI() items = {"foo": "The Foo Wrestlers"} @app.get("/items/{item_id}") async def read_item(item_id: str):     if item_id not in items:        raise HTTPException(status_code=404, detail="Item not found")    return {"item": items[item_id]}`

### The resulting response[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#the-resulting-response "Permanent link")

If the client requests `http://example.com/items/foo` (an `item_id` `"foo"`), that client will receive an HTTP status code of 200, and a JSON response of:

`{   "item": "The Foo Wrestlers" }`

But if the client requests `http://example.com/items/bar` (a non-existent `item_id` `"bar"`), that client will receive an HTTP status code of 404 (the "not found" error), and a JSON response of:

`{   "detail": "Item not found" }`

Tip

When raising an `HTTPException`, you can pass any value that can be converted to JSON as the parameter `detail`, not only `str`.

You could pass a `dict`, a `list`, etc.

They are handled automatically by **FastAPI** and converted to JSON.

## Add custom headers[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#add-custom-headers "Permanent link")

There are some situations in where it's useful to be able to add custom headers to the HTTP error. For example, for some types of security.

You probably won't need to use it directly in your code.

But in case you needed it for an advanced scenario, you can add custom headers:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/handling-errors/#__tabbed_3_1)

`from fastapi import FastAPI, HTTPException app = FastAPI() items = {"foo": "The Foo Wrestlers"} @app.get("/items-header/{item_id}") async def read_item_header(item_id: str):     if item_id not in items:        raise HTTPException(            status_code=404,            detail="Item not found",            headers={"X-Error": "There goes my error"},        )    return {"item": items[item_id]}`

## Install custom exception handlers[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#install-custom-exception-handlers "Permanent link")

You can add custom exception handlers with [the same exception utilities from Starlette](https://www.starlette.io/exceptions/).

Let's say you have a custom exception `UnicornException` that you (or a library you use) might `raise`.

And you want to handle this exception globally with FastAPI.

You could add a custom exception handler with `@app.exception_handler()`:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/handling-errors/#__tabbed_4_1)

`from fastapi import FastAPI, Request from fastapi.responses import JSONResponse class UnicornException(Exception):     def __init__(self, name: str):        self.name = name app = FastAPI() @app.exception_handler(UnicornException) async def unicorn_exception_handler(request: Request, exc: UnicornException):     return JSONResponse(        status_code=418,        content={"message": f"Oops! {exc.name} did something. There goes a rainbow..."},    ) @app.get("/unicorns/{name}") async def read_unicorn(name: str):     if name == "yolo":        raise UnicornException(name=name)    return {"unicorn_name": name}`

Here, if you request `/unicorns/yolo`, the _path operation_ will `raise` a `UnicornException`.

But it will be handled by the `unicorn_exception_handler`.

So, you will receive a clean error, with an HTTP status code of `418` and a JSON content of:

`{"message": "Oops! yolo did something. There goes a rainbow..."}`

Technical Details

You could also use `from starlette.requests import Request` and `from starlette.responses import JSONResponse`.

**FastAPI** provides the same `starlette.responses` as `fastapi.responses` just as a convenience for you, the developer. But most of the available responses come directly from Starlette. The same with `Request`.

## Override the default exception handlers[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#override-the-default-exception-handlers "Permanent link")

**FastAPI** has some default exception handlers.

These handlers are in charge of returning the default JSON responses when you `raise` an `HTTPException` and when the request has invalid data.

You can override these exception handlers with your own.

### Override request validation exceptions[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#override-request-validation-exceptions "Permanent link")

When a request contains invalid data, **FastAPI** internally raises a `RequestValidationError`.

And it also includes a default exception handler for it.

To override it, import the `RequestValidationError` and use it with `@app.exception_handler(RequestValidationError)` to decorate the exception handler.

The exception handler will receive a `Request` and the exception.

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/handling-errors/#__tabbed_5_1)

`from fastapi import FastAPI, HTTPException from fastapi.exceptions import RequestValidationError from fastapi.responses import PlainTextResponse from starlette.exceptions import HTTPException as StarletteHTTPException app = FastAPI() @app.exception_handler(StarletteHTTPException) async def http_exception_handler(request, exc):     return PlainTextResponse(str(exc.detail), status_code=exc.status_code) @app.exception_handler(RequestValidationError) async def validation_exception_handler(request, exc):     return PlainTextResponse(str(exc), status_code=400) @app.get("/items/{item_id}") async def read_item(item_id: int):     if item_id == 3:        raise HTTPException(status_code=418, detail="Nope! I don't like 3.")    return {"item_id": item_id}`

Now, if you go to `/items/foo`, instead of getting the default JSON error with:

`{     "detail": [        {            "loc": [                "path",                "item_id"            ],            "msg": "value is not a valid integer",            "type": "type_error.integer"        }    ] }`

you will get a text version, with:

`1 validation error path -> item_id   value is not a valid integer (type=type_error.integer)`

#### `RequestValidationError` vs `ValidationError`[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#requestvalidationerror-vs-validationerror "Permanent link")

Warning

These are technical details that you might skip if it's not important for you now.

`RequestValidationError` is a sub-class of Pydantic's [`ValidationError`](https://docs.pydantic.dev/latest/concepts/models/#error-handling).

**FastAPI** uses it so that, if you use a Pydantic model in `response_model`, and your data has an error, you will see the error in your log.

But the client/user will not see it. Instead, the client will receive an "Internal Server Error" with an HTTP status code `500`.

It should be this way because if you have a Pydantic `ValidationError` in your _response_ or anywhere in your code (not in the client's _request_), it's actually a bug in your code.

And while you fix it, your clients/users shouldn't have access to internal information about the error, as that could expose a security vulnerability.

### Override the `HTTPException` error handler[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#override-the-httpexception-error-handler "Permanent link")

The same way, you can override the `HTTPException` handler.

For example, you could want to return a plain text response instead of JSON for these errors:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/handling-errors/#__tabbed_6_1)

`from fastapi import FastAPI, HTTPException from fastapi.exceptions import RequestValidationError from fastapi.responses import PlainTextResponse from starlette.exceptions import HTTPException as StarletteHTTPException app = FastAPI() @app.exception_handler(StarletteHTTPException) async def http_exception_handler(request, exc):     return PlainTextResponse(str(exc.detail), status_code=exc.status_code) @app.exception_handler(RequestValidationError) async def validation_exception_handler(request, exc):     return PlainTextResponse(str(exc), status_code=400) @app.get("/items/{item_id}") async def read_item(item_id: int):     if item_id == 3:        raise HTTPException(status_code=418, detail="Nope! I don't like 3.")    return {"item_id": item_id}`

Technical Details

You could also use `from starlette.responses import PlainTextResponse`.

**FastAPI** provides the same `starlette.responses` as `fastapi.responses` just as a convenience for you, the developer. But most of the available responses come directly from Starlette.

### Use the `RequestValidationError` body[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#use-the-requestvalidationerror-body "Permanent link")

The `RequestValidationError` contains the `body` it received with invalid data.

You could use it while developing your app to log the body and debug it, return it to the user, etc.

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/handling-errors/#__tabbed_7_1)

`from fastapi import FastAPI, Request, status from fastapi.encoders import jsonable_encoder from fastapi.exceptions import RequestValidationError from fastapi.responses import JSONResponse from pydantic import BaseModel app = FastAPI() @app.exception_handler(RequestValidationError) async def validation_exception_handler(request: Request, exc: RequestValidationError):     return JSONResponse(        status_code=status.HTTP_422_UNPROCESSABLE_ENTITY,        content=jsonable_encoder({"detail": exc.errors(), "body": exc.body}),    ) class Item(BaseModel):     title: str    size: int @app.post("/items/") async def create_item(item: Item):     return item`

Now try sending an invalid item like:

`{   "title": "towel",  "size": "XL" }`

You will receive a response telling you that the data is invalid containing the received body:

`{   "detail": [    {      "loc": [        "body",        "size"      ],      "msg": "value is not a valid integer",      "type": "type_error.integer"    }  ],  "body": {    "title": "towel",    "size": "XL"  } }`

#### FastAPI's `HTTPException` vs Starlette's `HTTPException`[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#fastapis-httpexception-vs-starlettes-httpexception "Permanent link")

**FastAPI** has its own `HTTPException`.

And **FastAPI**'s `HTTPException` error class inherits from Starlette's `HTTPException` error class.

The only difference is that **FastAPI**'s `HTTPException` accepts any JSON-able data for the `detail` field, while Starlette's `HTTPException` only accepts strings for it.

So, you can keep raising **FastAPI**'s `HTTPException` as normally in your code.

But when you register an exception handler, you should register it for Starlette's `HTTPException`.

This way, if any part of Starlette's internal code, or a Starlette extension or plug-in, raises a Starlette `HTTPException`, your handler will be able to catch and handle it.

In this example, to be able to have both `HTTPException`s in the same code, Starlette's exceptions is renamed to `StarletteHTTPException`:

`from starlette.exceptions import HTTPException as StarletteHTTPException`

### Reuse **FastAPI**'s exception handlers[¶](https://fastapi.tiangolo.com/tutorial/handling-errors/#reuse-fastapis-exception-handlers "Permanent link")

If you want to use the exception along with the same default exception handlers from **FastAPI**, you can import and reuse the default exception handlers from `fastapi.exception_handlers`:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/handling-errors/#__tabbed_8_1)

`from fastapi import FastAPI, HTTPException from fastapi.exception_handlers import (     http_exception_handler,    request_validation_exception_handler, ) from fastapi.exceptions import RequestValidationError from starlette.exceptions import HTTPException as StarletteHTTPException app = FastAPI() @app.exception_handler(StarletteHTTPException) async def custom_http_exception_handler(request, exc):     print(f"OMG! An HTTP error!: {repr(exc)}")    return await http_exception_handler(request, exc) @app.exception_handler(RequestValidationError) async def validation_exception_handler(request, exc):     print(f"OMG! The client sent invalid data!: {exc}")    return await request_validation_exception_handler(request, exc) @app.get("/items/{item_id}") async def read_item(item_id: int):     if item_id == 3:        raise HTTPException(status_code=418, detail="Nope! I don't like 3.")    return {"item_id": item_id}`

In this example you are just printing the error with a very expressive message, but you get the idea. You can use the exception and then just reuse the default exception handlers.

# Path Operation Configuration[¶](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#path-operation-configuration "Permanent link")

There are several parameters that you can pass to your _path operation decorator_ to configure it.

Warning

Notice that these parameters are passed directly to the _path operation decorator_, not to your _path operation function_.

## Response Status Code[¶](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#response-status-code "Permanent link")

You can define the (HTTP) `status_code` to be used in the response of your _path operation_.

You can pass directly the `int` code, like `404`.

But if you don't remember what each number code is for, you can use the shortcut constants in `status`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_1_1)

`from fastapi import FastAPI, status from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set() @app.post("/items/", response_model=Item, status_code=status.HTTP_201_CREATED) async def create_item(item: Item):     return item`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_2_2)

That status code will be used in the response and will be added to the OpenAPI schema.

Technical Details

You could also use `from starlette import status`.

**FastAPI** provides the same `starlette.status` as `fastapi.status` just as a convenience for you, the developer. But it comes directly from Starlette.

## Tags[¶](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#tags "Permanent link")

You can add tags to your _path operation_, pass the parameter `tags` with a `list` of `str` (commonly just one `str`):

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_3_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set() @app.post("/items/", response_model=Item, tags=["items"]) async def create_item(item: Item):     return item @app.get("/items/", tags=["items"]) async def read_items():     return [{"name": "Foo", "price": 42}] @app.get("/users/", tags=["users"]) async def read_users():     return [{"username": "johndoe"}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_4_2)

They will be added to the OpenAPI schema and used by the automatic documentation interfaces:

![](https://fastapi.tiangolo.com/img/tutorial/path-operation-configuration/image01.png)

### Tags with Enums[¶](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#tags-with-enums "Permanent link")

If you have a big application, you might end up accumulating **several tags**, and you would want to make sure you always use the **same tag** for related _path operations_.

In these cases, it could make sense to store the tags in an `Enum`.

**FastAPI** supports that the same way as with plain strings:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_5_1)

`from enum import Enum from fastapi import FastAPI app = FastAPI() class Tags(Enum):     items = "items"    users = "users" @app.get("/items/", tags=[Tags.items]) async def get_items():     return ["Portal gun", "Plumbus"] @app.get("/users/", tags=[Tags.users]) async def read_users():     return ["Rick", "Morty"]`

## Summary and description[¶](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#summary-and-description "Permanent link")

You can add a `summary` and `description`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_6_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set() @app.post(     "/items/",    response_model=Item,    summary="Create an item",    description="Create an item with all the information, name, description, price, tax and a set of unique tags", ) async def create_item(item: Item):     return item`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_7_1)[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_7_2)

## Description from docstring[¶](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#description-from-docstring "Permanent link")

As descriptions tend to be long and cover multiple lines, you can declare the _path operation_ description in the function docstring and **FastAPI** will read it from there.

You can write [Markdown](https://en.wikipedia.org/wiki/Markdown) in the docstring, it will be interpreted and displayed correctly (taking into account docstring indentation).

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_8_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set() @app.post("/items/", response_model=Item, summary="Create an item") async def create_item(item: Item):     """    Create an item with all the information:     - **name**: each item must have a name    - **description**: a long description    - **price**: required    - **tax**: if the item doesn't have tax, you can omit this    - **tags**: a set of unique tag strings for this item    """    return item`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_9_1)[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_9_2)

It will be used in the interactive docs:

![](https://fastapi.tiangolo.com/img/tutorial/path-operation-configuration/image02.png)

## Response description[¶](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#response-description "Permanent link")

You can specify the response description with the parameter `response_description`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_10_1)

`from fastapi import FastAPI from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str    description: str | None = None    price: float    tax: float | None = None    tags: set[str] = set() @app.post(     "/items/",    response_model=Item,    summary="Create an item",    response_description="The created item", ) async def create_item(item: Item):     """    Create an item with all the information:     - **name**: each item must have a name    - **description**: a long description    - **price**: required    - **tax**: if the item doesn't have tax, you can omit this    - **tags**: a set of unique tag strings for this item    """    return item`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_11_1)[](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_11_2)

Info

Notice that `response_description` refers specifically to the response, the `description` refers to the _path operation_ in general.

Check

OpenAPI specifies that each _path operation_ requires a response description.

So, if you don't provide one, **FastAPI** will automatically generate one of "Successful response".

![](https://fastapi.tiangolo.com/img/tutorial/path-operation-configuration/image03.png)

## Deprecate a _path operation_[¶](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#deprecate-a-path-operation "Permanent link")

If you need to mark a _path operation_ as deprecated, but without removing it, pass the parameter `deprecated`:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#__tabbed_12_1)

`from fastapi import FastAPI app = FastAPI() @app.get("/items/", tags=["items"]) async def read_items():     return [{"name": "Foo", "price": 42}] @app.get("/users/", tags=["users"]) async def read_users():     return [{"username": "johndoe"}] @app.get("/elements/", tags=["items"], deprecated=True) async def read_elements():     return [{"item_id": "Foo"}]`

It will be clearly marked as deprecated in the interactive docs:

![](https://fastapi.tiangolo.com/img/tutorial/path-operation-configuration/image04.png)

Check how deprecated and non-deprecated _path operations_ look like:

![](https://fastapi.tiangolo.com/img/tutorial/path-operation-configuration/image05.png)

## Recap[¶](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#recap "Permanent link")

You can configure and add metadata for your _path operations_ easily by passing parameters to the _path operation decorators_.

# JSON Compatible Encoder[¶](https://fastapi.tiangolo.com/tutorial/encoder/#json-compatible-encoder "Permanent link")

There are some cases where you might need to convert a data type (like a Pydantic model) to something compatible with JSON (like a `dict`, `list`, etc).

For example, if you need to store it in a database.

For that, **FastAPI** provides a `jsonable_encoder()` function.

## Using the `jsonable_encoder`[¶](https://fastapi.tiangolo.com/tutorial/encoder/#using-the-jsonable_encoder "Permanent link")

Let's imagine that you have a database `fake_db` that only receives JSON compatible data.

For example, it doesn't receive `datetime` objects, as those are not compatible with JSON.

So, a `datetime` object would have to be converted to a `str` containing the data in [ISO format](https://en.wikipedia.org/wiki/ISO_8601).

The same way, this database wouldn't receive a Pydantic model (an object with attributes), only a `dict`.

You can use `jsonable_encoder` for that.

It receives an object, like a Pydantic model, and returns a JSON compatible version:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/encoder/#__tabbed_1_1)

`from datetime import datetime from fastapi import FastAPI from fastapi.encoders import jsonable_encoder from pydantic import BaseModel fake_db = {} class Item(BaseModel):     title: str    timestamp: datetime    description: str | None = None app = FastAPI() @app.put("/items/{id}") def update_item(id: str, item: Item):     json_compatible_item_data = jsonable_encoder(item)    fake_db[id] = json_compatible_item_data`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/encoder/#__tabbed_2_1)

In this example, it would convert the Pydantic model to a `dict`, and the `datetime` to a `str`.

The result of calling it is something that can be encoded with the Python standard [`json.dumps()`](https://docs.python.org/3/library/json.html#json.dumps).

It doesn't return a large `str` containing the data in JSON format (as a string). It returns a Python standard data structure (e.g. a `dict`) with values and sub-values that are all compatible with JSON.

# Body - Updates[¶](https://fastapi.tiangolo.com/tutorial/body-updates/#body-updates "Permanent link")

## Update replacing with `PUT`[¶](https://fastapi.tiangolo.com/tutorial/body-updates/#update-replacing-with-put "Permanent link")

To update an item you can use the [HTTP `PUT`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT) operation.

You can use the `jsonable_encoder` to convert the input data to data that can be stored as JSON (e.g. with a NoSQL database). For example, converting `datetime` to `str`.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_1_1)

`from fastapi import FastAPI from fastapi.encoders import jsonable_encoder from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str | None = None    description: str | None = None    price: float | None = None    tax: float = 10.5    tags: list[str] = [] items = {     "foo": {"name": "Foo", "price": 50.2},    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []}, } @app.get("/items/{item_id}", response_model=Item) async def read_item(item_id: str):     return items[item_id] @app.put("/items/{item_id}", response_model=Item) async def update_item(item_id: str, item: Item):     update_item_encoded = jsonable_encoder(item)    items[item_id] = update_item_encoded    return update_item_encoded`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_2_2)

`PUT` is used to receive data that should replace the existing data.

### Warning about replacing[¶](https://fastapi.tiangolo.com/tutorial/body-updates/#warning-about-replacing "Permanent link")

That means that if you want to update the item `bar` using `PUT` with a body containing:

`{     "name": "Barz",    "price": 3,    "description": None, }`

because it doesn't include the already stored attribute `"tax": 20.2`, the input model would take the default value of `"tax": 10.5`.

And the data would be saved with that "new" `tax` of `10.5`.

## Partial updates with `PATCH`[¶](https://fastapi.tiangolo.com/tutorial/body-updates/#partial-updates-with-patch "Permanent link")

You can also use the [HTTP `PATCH`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) operation to _partially_ update data.

This means that you can send only the data that you want to update, leaving the rest intact.

Note

`PATCH` is less commonly used and known than `PUT`.

And many teams use only `PUT`, even for partial updates.

You are **free** to use them however you want, **FastAPI** doesn't impose any restrictions.

But this guide shows you, more or less, how they are intended to be used.

### Using Pydantic's `exclude_unset` parameter[¶](https://fastapi.tiangolo.com/tutorial/body-updates/#using-pydantics-exclude_unset-parameter "Permanent link")

If you want to receive partial updates, it's very useful to use the parameter `exclude_unset` in Pydantic's model's `.model_dump()`.

Like `item.model_dump(exclude_unset=True)`.

Info

In Pydantic v1 the method was called `.dict()`, it was deprecated (but still supported) in Pydantic v2, and renamed to `.model_dump()`.

The examples here use `.dict()` for compatibility with Pydantic v1, but you should use `.model_dump()` instead if you can use Pydantic v2.

That would generate a `dict` with only the data that was set when creating the `item` model, excluding default values.

Then you can use this to generate a `dict` with only the data that was set (sent in the request), omitting default values:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_3_1)

`from fastapi import FastAPI from fastapi.encoders import jsonable_encoder from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str | None = None    description: str | None = None    price: float | None = None    tax: float = 10.5    tags: list[str] = [] items = {     "foo": {"name": "Foo", "price": 50.2},    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []}, } @app.get("/items/{item_id}", response_model=Item) async def read_item(item_id: str):     return items[item_id] @app.patch("/items/{item_id}", response_model=Item) async def update_item(item_id: str, item: Item):     stored_item_data = items[item_id]    stored_item_model = Item(**stored_item_data)    update_data = item.dict(exclude_unset=True)    updated_item = stored_item_model.copy(update=update_data)    items[item_id] = jsonable_encoder(updated_item)    return updated_item`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_4_2)

### Using Pydantic's `update` parameter[¶](https://fastapi.tiangolo.com/tutorial/body-updates/#using-pydantics-update-parameter "Permanent link")

Now, you can create a copy of the existing model using `.model_copy()`, and pass the `update` parameter with a `dict` containing the data to update.

Info

In Pydantic v1 the method was called `.copy()`, it was deprecated (but still supported) in Pydantic v2, and renamed to `.model_copy()`.

The examples here use `.copy()` for compatibility with Pydantic v1, but you should use `.model_copy()` instead if you can use Pydantic v2.

Like `stored_item_model.model_copy(update=update_data)`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_5_1)

`from fastapi import FastAPI from fastapi.encoders import jsonable_encoder from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str | None = None    description: str | None = None    price: float | None = None    tax: float = 10.5    tags: list[str] = [] items = {     "foo": {"name": "Foo", "price": 50.2},    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []}, } @app.get("/items/{item_id}", response_model=Item) async def read_item(item_id: str):     return items[item_id] @app.patch("/items/{item_id}", response_model=Item) async def update_item(item_id: str, item: Item):     stored_item_data = items[item_id]    stored_item_model = Item(**stored_item_data)    update_data = item.dict(exclude_unset=True)    updated_item = stored_item_model.copy(update=update_data)    items[item_id] = jsonable_encoder(updated_item)    return updated_item`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_6_2)

### Partial updates recap[¶](https://fastapi.tiangolo.com/tutorial/body-updates/#partial-updates-recap "Permanent link")

In summary, to apply partial updates you would:

- (Optionally) use `PATCH` instead of `PUT`.
- Retrieve the stored data.
- Put that data in a Pydantic model.
- Generate a `dict` without default values from the input model (using `exclude_unset`).
    - This way you can update only the values actually set by the user, instead of overriding values already stored with default values in your model.
- Create a copy of the stored model, updating its attributes with the received partial updates (using the `update` parameter).
- Convert the copied model to something that can be stored in your DB (for example, using the `jsonable_encoder`).
    - This is comparable to using the model's `.model_dump()` method again, but it makes sure (and converts) the values to data types that can be converted to JSON, for example, `datetime` to `str`.
- Save the data to your DB.
- Return the updated model.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_7_1)

`from fastapi import FastAPI from fastapi.encoders import jsonable_encoder from pydantic import BaseModel app = FastAPI() class Item(BaseModel):     name: str | None = None    description: str | None = None    price: float | None = None    tax: float = 10.5    tags: list[str] = [] items = {     "foo": {"name": "Foo", "price": 50.2},    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []}, } @app.get("/items/{item_id}", response_model=Item) async def read_item(item_id: str):     return items[item_id] @app.patch("/items/{item_id}", response_model=Item) async def update_item(item_id: str, item: Item):     stored_item_data = items[item_id]    stored_item_model = Item(**stored_item_data)    update_data = item.dict(exclude_unset=True)    updated_item = stored_item_model.copy(update=update_data)    items[item_id] = jsonable_encoder(updated_item)    return updated_item`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/body-updates/#__tabbed_8_2)

Tip

You can actually use this same technique with an HTTP `PUT` operation.

But the example here uses `PATCH` because it was created for these use cases.

Note

Notice that the input model is still validated.

So, if you want to receive partial updates that can omit all the attributes, you need to have a model with all the attributes marked as optional (with default values or `None`).

To distinguish from the models with all optional values for **updates** and models with required values for **creation**, you can use the ideas described in [Extra Models](https://fastapi.tiangolo.com/tutorial/extra-models/).


# Classes as Dependencies[¶](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#classes-as-dependencies "Permanent link")

Before diving deeper into the **Dependency Injection** system, let's upgrade the previous example.

## A `dict` from the previous example[¶](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#a-dict-from-the-previous-example "Permanent link")

In the previous example, we were returning a `dict` from our dependency ("dependable"):

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_1_1)

`from typing import Annotated from fastapi import Depends, FastAPI app = FastAPI() async def common_parameters(q: str | None = None, skip: int = 0, limit: int = 100):     return {"q": q, "skip": skip, "limit": limit} @app.get("/items/") async def read_items(commons: Annotated[dict, Depends(common_parameters)]):     return commons @app.get("/users/") async def read_users(commons: Annotated[dict, Depends(common_parameters)]):     return commons`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_2_4)

But then we get a `dict` in the parameter `commons` of the _path operation function_.

And we know that editors can't provide a lot of support (like completion) for `dict`s, because they can't know their keys and value types.

We can do better...

## What makes a dependency[¶](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#what-makes-a-dependency "Permanent link")

Up to now you have seen dependencies declared as functions.

But that's not the only way to declare dependencies (although it would probably be the more common).

The key factor is that a dependency should be a "callable".

A "**callable**" in Python is anything that Python can "call" like a function.

So, if you have an object `something` (that might _not_ be a function) and you can "call" it (execute it) like:

`something()`

or

`something(some_argument, some_keyword_argument="foo")`

then it is a "callable".

## Classes as dependencies[¶](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#classes-as-dependencies_1 "Permanent link")

You might notice that to create an instance of a Python class, you use that same syntax.

For example:

`class Cat:     def __init__(self, name: str):        self.name = name fluffy = Cat(name="Mr Fluffy")`

In this case, `fluffy` is an instance of the class `Cat`.

And to create `fluffy`, you are "calling" `Cat`.

So, a Python class is also a **callable**.

Then, in **FastAPI**, you could use a Python class as a dependency.

What FastAPI actually checks is that it is a "callable" (function, class or anything else) and the parameters defined.

If you pass a "callable" as a dependency in **FastAPI**, it will analyze the parameters for that "callable", and process them in the same way as the parameters for a _path operation function_. Including sub-dependencies.

That also applies to callables with no parameters at all. The same as it would be for _path operation functions_ with no parameters.

Then, we can change the dependency "dependable" `common_parameters` from above to the class `CommonQueryParams`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_3_1)

`from typing import Annotated from fastapi import Depends, FastAPI app = FastAPI() fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}] class CommonQueryParams:     def __init__(self, q: str | None = None, skip: int = 0, limit: int = 100):        self.q = q        self.skip = skip        self.limit = limit @app.get("/items/") async def read_items(commons: Annotated[CommonQueryParams, Depends(CommonQueryParams)]):     response = {}    if commons.q:        response.update({"q": commons.q})    items = fake_items_db[commons.skip : commons.skip + commons.limit]    response.update({"items": items})    return response`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_4_4)

Pay attention to the `__init__` method used to create the instance of the class:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_5_1)

`from typing import Annotated from fastapi import Depends, FastAPI app = FastAPI() fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}] class CommonQueryParams:     def __init__(self, q: str | None = None, skip: int = 0, limit: int = 100):        self.q = q        self.skip = skip        self.limit = limit @app.get("/items/") async def read_items(commons: Annotated[CommonQueryParams, Depends(CommonQueryParams)]):     response = {}    if commons.q:        response.update({"q": commons.q})    items = fake_items_db[commons.skip : commons.skip + commons.limit]    response.update({"items": items})    return response`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_6_2)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_6_3)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_6_4)

...it has the same parameters as our previous `common_parameters`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_7_1)

`from typing import Annotated from fastapi import Depends, FastAPI app = FastAPI() async def common_parameters(q: str | None = None, skip: int = 0, limit: int = 100):     return {"q": q, "skip": skip, "limit": limit} @app.get("/items/") async def read_items(commons: Annotated[dict, Depends(common_parameters)]):     return commons @app.get("/users/") async def read_users(commons: Annotated[dict, Depends(common_parameters)]):     return commons`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_8_2)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_8_3)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_8_4)

Those parameters are what **FastAPI** will use to "solve" the dependency.

In both cases, it will have:

- An optional `q` query parameter that is a `str`.
- A `skip` query parameter that is an `int`, with a default of `0`.
- A `limit` query parameter that is an `int`, with a default of `100`.

In both cases the data will be converted, validated, documented on the OpenAPI schema, etc.

## Use it[¶](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#use-it "Permanent link")

Now you can declare your dependency using this class.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_9_1)

`from typing import Annotated from fastapi import Depends, FastAPI app = FastAPI() fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}] class CommonQueryParams:     def __init__(self, q: str | None = None, skip: int = 0, limit: int = 100):        self.q = q        self.skip = skip        self.limit = limit @app.get("/items/") async def read_items(commons: Annotated[CommonQueryParams, Depends(CommonQueryParams)]):     response = {}    if commons.q:        response.update({"q": commons.q})    items = fake_items_db[commons.skip : commons.skip + commons.limit]    response.update({"items": items})    return response`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_10_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_10_2)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_10_3)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_10_4)

**FastAPI** calls the `CommonQueryParams` class. This creates an "instance" of that class and the instance will be passed as the parameter `commons` to your function.

## Type annotation vs `Depends`[¶](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#type-annotation-vs-depends "Permanent link")

Notice how we write `CommonQueryParams` twice in the above code:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_11_1)[Python 3.8+ non-Annotated](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_11_2)

`commons: Annotated[CommonQueryParams, Depends(CommonQueryParams)]`

The last `CommonQueryParams`, in:

`... Depends(CommonQueryParams)`

...is what **FastAPI** will actually use to know what is the dependency.

It is from this one that FastAPI will extract the declared parameters and that is what FastAPI will actually call.

---

In this case, the first `CommonQueryParams`, in:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_12_1)[Python 3.8+ non-Annotated](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_12_2)

`commons: Annotated[CommonQueryParams, ...`

...doesn't have any special meaning for **FastAPI**. FastAPI won't use it for data conversion, validation, etc. (as it is using the `Depends(CommonQueryParams)` for that).

You could actually write just:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_13_1)[Python 3.8+ non-Annotated](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_13_2)

`commons: Annotated[Any, Depends(CommonQueryParams)]`

...as in:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_14_1)

`from typing import Annotated, Any from fastapi import Depends, FastAPI app = FastAPI() fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}] class CommonQueryParams:     def __init__(self, q: str | None = None, skip: int = 0, limit: int = 100):        self.q = q        self.skip = skip        self.limit = limit @app.get("/items/") async def read_items(commons: Annotated[Any, Depends(CommonQueryParams)]):     response = {}    if commons.q:        response.update({"q": commons.q})    items = fake_items_db[commons.skip : commons.skip + commons.limit]    response.update({"items": items})    return response`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_15_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_15_2)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_15_3)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_15_4)

But declaring the type is encouraged as that way your editor will know what will be passed as the parameter `commons`, and then it can help you with code completion, type checks, etc:

![](https://fastapi.tiangolo.com/img/tutorial/dependencies/image02.png)

## Shortcut[¶](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#shortcut "Permanent link")

But you see that we are having some code repetition here, writing `CommonQueryParams` twice:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_16_1)[Python 3.8+ non-Annotated](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_16_2)

`commons: Annotated[CommonQueryParams, Depends(CommonQueryParams)]`

**FastAPI** provides a shortcut for these cases, in where the dependency is _specifically_ a class that **FastAPI** will "call" to create an instance of the class itself.

For those specific cases, you can do the following:

Instead of writing:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_17_1)[Python 3.8+ non-Annotated](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_17_2)

`commons: Annotated[CommonQueryParams, Depends(CommonQueryParams)]`

...you write:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_18_1)[Python 3.8 non-Annotated](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_18_2)

`commons: Annotated[CommonQueryParams, Depends()]`

You declare the dependency as the type of the parameter, and you use `Depends()` without any parameter, instead of having to write the full class _again_ inside of `Depends(CommonQueryParams)`.

The same example would then look like:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_19_1)

`from typing import Annotated from fastapi import Depends, FastAPI app = FastAPI() fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}] class CommonQueryParams:     def __init__(self, q: str | None = None, skip: int = 0, limit: int = 100):        self.q = q        self.skip = skip        self.limit = limit @app.get("/items/") async def read_items(commons: Annotated[CommonQueryParams, Depends()]):     response = {}    if commons.q:        response.update({"q": commons.q})    items = fake_items_db[commons.skip : commons.skip + commons.limit]    response.update({"items": items})    return response`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_20_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_20_2)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_20_3)[](https://fastapi.tiangolo.com/tutorial/dependencies/classes-as-dependencies/#__tabbed_20_4)

...and **FastAPI** will know what to do.

# Dependencies in path operation decorators[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#dependencies-in-path-operation-decorators "Permanent link")

In some cases you don't really need the return value of a dependency inside your _path operation function_.

Or the dependency doesn't return a value.

But you still need it to be executed/solved.

For those cases, instead of declaring a _path operation function_ parameter with `Depends`, you can add a `list` of `dependencies` to the _path operation decorator_.

## Add `dependencies` to the _path operation decorator_[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#add-dependencies-to-the-path-operation-decorator "Permanent link")

The _path operation decorator_ receives an optional argument `dependencies`.

It should be a `list` of `Depends()`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_1_1)

`from typing import Annotated from fastapi import Depends, FastAPI, Header, HTTPException app = FastAPI() async def verify_token(x_token: Annotated[str, Header()]):     if x_token != "fake-super-secret-token":        raise HTTPException(status_code=400, detail="X-Token header invalid") async def verify_key(x_key: Annotated[str, Header()]):     if x_key != "fake-super-secret-key":        raise HTTPException(status_code=400, detail="X-Key header invalid")    return x_key @app.get("/items/", dependencies=[Depends(verify_token), Depends(verify_key)]) async def read_items():     return [{"item": "Foo"}, {"item": "Bar"}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_2_2)

These dependencies will be executed/solved the same way as normal dependencies. But their value (if they return any) won't be passed to your _path operation function_.

Tip

Some editors check for unused function parameters, and show them as errors.

Using these `dependencies` in the _path operation decorator_ you can make sure they are executed while avoiding editor/tooling errors.

It might also help avoid confusion for new developers that see an unused parameter in your code and could think it's unnecessary.

Info

In this example we use invented custom headers `X-Key` and `X-Token`.

But in real cases, when implementing security, you would get more benefits from using the integrated [Security utilities (the next chapter)](https://fastapi.tiangolo.com/tutorial/security/).

## Dependencies errors and return values[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#dependencies-errors-and-return-values "Permanent link")

You can use the same dependency _functions_ you use normally.

### Dependency requirements[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#dependency-requirements "Permanent link")

They can declare request requirements (like headers) or other sub-dependencies:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_3_1)

`from typing import Annotated from fastapi import Depends, FastAPI, Header, HTTPException app = FastAPI() async def verify_token(x_token: Annotated[str, Header()]):     if x_token != "fake-super-secret-token":        raise HTTPException(status_code=400, detail="X-Token header invalid") async def verify_key(x_key: Annotated[str, Header()]):     if x_key != "fake-super-secret-key":        raise HTTPException(status_code=400, detail="X-Key header invalid")    return x_key @app.get("/items/", dependencies=[Depends(verify_token), Depends(verify_key)]) async def read_items():     return [{"item": "Foo"}, {"item": "Bar"}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_4_2)

### Raise exceptions[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#raise-exceptions "Permanent link")

These dependencies can `raise` exceptions, the same as normal dependencies:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_5_1)

`from typing import Annotated from fastapi import Depends, FastAPI, Header, HTTPException app = FastAPI() async def verify_token(x_token: Annotated[str, Header()]):     if x_token != "fake-super-secret-token":        raise HTTPException(status_code=400, detail="X-Token header invalid") async def verify_key(x_key: Annotated[str, Header()]):     if x_key != "fake-super-secret-key":        raise HTTPException(status_code=400, detail="X-Key header invalid")    return x_key @app.get("/items/", dependencies=[Depends(verify_token), Depends(verify_key)]) async def read_items():     return [{"item": "Foo"}, {"item": "Bar"}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_6_2)

### Return values[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#return-values "Permanent link")

And they can return values or not, the values won't be used.

So, you can reuse a normal dependency (that returns a value) you already use somewhere else, and even though the value won't be used, the dependency will be executed:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_7_1)

`from typing import Annotated from fastapi import Depends, FastAPI, Header, HTTPException app = FastAPI() async def verify_token(x_token: Annotated[str, Header()]):     if x_token != "fake-super-secret-token":        raise HTTPException(status_code=400, detail="X-Token header invalid") async def verify_key(x_key: Annotated[str, Header()]):     if x_key != "fake-super-secret-key":        raise HTTPException(status_code=400, detail="X-Key header invalid")    return x_key @app.get("/items/", dependencies=[Depends(verify_token), Depends(verify_key)]) async def read_items():     return [{"item": "Foo"}, {"item": "Bar"}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#__tabbed_8_2)

## Dependencies for a group of _path operations_[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#dependencies-for-a-group-of-path-operations "Permanent link")

Later, when reading about how to structure bigger applications ([Bigger Applications - Multiple Files](https://fastapi.tiangolo.com/tutorial/bigger-applications/)), possibly with multiple files, you will learn how to declare a single `dependencies` parameter for a group of _path operations_.

## Global Dependencies[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/#global-dependencies "Permanent link")

Next we will see how to add dependencies to the whole `FastAPI` application, so that they apply to each _path operation_.


# Global Dependencies[¶](https://fastapi.tiangolo.com/tutorial/dependencies/global-dependencies/#global-dependencies "Permanent link")

For some types of applications you might want to add dependencies to the whole application.

Similar to the way you can [add `dependencies` to the _path operation decorators_](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/), you can add them to the `FastAPI` application.

In that case, they will be applied to all the _path operations_ in the application:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/global-dependencies/#__tabbed_1_1)

`from fastapi import Depends, FastAPI, Header, HTTPException from typing_extensions import Annotated async def verify_token(x_token: Annotated[str, Header()]):     if x_token != "fake-super-secret-token":        raise HTTPException(status_code=400, detail="X-Token header invalid") async def verify_key(x_key: Annotated[str, Header()]):     if x_key != "fake-super-secret-key":        raise HTTPException(status_code=400, detail="X-Key header invalid")    return x_key app = FastAPI(dependencies=[Depends(verify_token), Depends(verify_key)]) @app.get("/items/") async def read_items():     return [{"item": "Portal Gun"}, {"item": "Plumbus"}] @app.get("/users/") async def read_users():     return [{"username": "Rick"}, {"username": "Morty"}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/global-dependencies/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/global-dependencies/#__tabbed_2_2)

And all the ideas in the section about [adding `dependencies` to the _path operation decorators_](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/) still apply, but in this case, to all of the _path operations_ in the app.

## Dependencies for groups of _path operations_[¶](https://fastapi.tiangolo.com/tutorial/dependencies/global-dependencies/#dependencies-for-groups-of-path-operations "Permanent link")

Later, when reading about how to structure bigger applications ([Bigger Applications - Multiple Files](https://fastapi.tiangolo.com/tutorial/bigger-applications/)), possibly with multiple files, you will learn how to declare a single `dependencies` parameter for a group of _path operations_.

# Dependencies with yield[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#dependencies-with-yield "Permanent link")

FastAPI supports dependencies that do some extra steps after finishing.

To do this, use `yield` instead of `return`, and write the extra steps (code) after.

Tip

Make sure to use `yield` one single time per dependency.

Technical Details

Any function that is valid to use with:

- [`@contextlib.contextmanager`](https://docs.python.org/3/library/contextlib.html#contextlib.contextmanager) or
- [`@contextlib.asynccontextmanager`](https://docs.python.org/3/library/contextlib.html#contextlib.asynccontextmanager)

would be valid to use as a **FastAPI** dependency.

In fact, FastAPI uses those two decorators internally.

## A database dependency with `yield`[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#a-database-dependency-with-yield "Permanent link")

For example, you could use this to create a database session and close it after finishing.

Only the code prior to and including the `yield` statement is executed before creating a response:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_1_1)

`async def get_db():     db = DBSession()    try:        yield db    finally:        db.close()`

The yielded value is what is injected into _path operations_ and other dependencies:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_2_1)

`async def get_db():     db = DBSession()    try:        yield db    finally:        db.close()`

The code following the `yield` statement is executed after creating the response but before sending it:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_3_1)

`async def get_db():     db = DBSession()    try:        yield db    finally:        db.close()`

Tip

You can use `async` or regular functions.

**FastAPI** will do the right thing with each, the same as with normal dependencies.

## A dependency with `yield` and `try`[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#a-dependency-with-yield-and-try "Permanent link")

If you use a `try` block in a dependency with `yield`, you'll receive any exception that was thrown when using the dependency.

For example, if some code at some point in the middle, in another dependency or in a _path operation_, made a database transaction "rollback" or create any other error, you will receive the exception in your dependency.

So, you can look for that specific exception inside the dependency with `except SomeException`.

In the same way, you can use `finally` to make sure the exit steps are executed, no matter if there was an exception or not.

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_4_1)

`async def get_db():     db = DBSession()    try:        yield db    finally:        db.close()`

## Sub-dependencies with `yield`[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#sub-dependencies-with-yield "Permanent link")

You can have sub-dependencies and "trees" of sub-dependencies of any size and shape, and any or all of them can use `yield`.

**FastAPI** will make sure that the "exit code" in each dependency with `yield` is run in the correct order.

For example, `dependency_c` can have a dependency on `dependency_b`, and `dependency_b` on `dependency_a`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_5_1)

`from typing import Annotated from fastapi import Depends async def dependency_a():     dep_a = generate_dep_a()    try:        yield dep_a    finally:        dep_a.close() async def dependency_b(dep_a: Annotated[DepA, Depends(dependency_a)]):     dep_b = generate_dep_b()    try:        yield dep_b    finally:        dep_b.close(dep_a) async def dependency_c(dep_b: Annotated[DepB, Depends(dependency_b)]):     dep_c = generate_dep_c()    try:        yield dep_c    finally:        dep_c.close(dep_b)`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_6_2)

And all of them can use `yield`.

In this case `dependency_c`, to execute its exit code, needs the value from `dependency_b` (here named `dep_b`) to still be available.

And, in turn, `dependency_b` needs the value from `dependency_a` (here named `dep_a`) to be available for its exit code.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_7_1)

`from typing import Annotated from fastapi import Depends async def dependency_a():     dep_a = generate_dep_a()    try:        yield dep_a    finally:        dep_a.close() async def dependency_b(dep_a: Annotated[DepA, Depends(dependency_a)]):     dep_b = generate_dep_b()    try:        yield dep_b    finally:        dep_b.close(dep_a) async def dependency_c(dep_b: Annotated[DepB, Depends(dependency_b)]):     dep_c = generate_dep_c()    try:        yield dep_c    finally:        dep_c.close(dep_b)`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_8_2)

The same way, you could have some dependencies with `yield` and some other dependencies with `return`, and have some of those depend on some of the others.

And you could have a single dependency that requires several other dependencies with `yield`, etc.

You can have any combinations of dependencies that you want.

**FastAPI** will make sure everything is run in the correct order.

Technical Details

This works thanks to Python's [Context Managers](https://docs.python.org/3/library/contextlib.html).

**FastAPI** uses them internally to achieve this.

## Dependencies with `yield` and `HTTPException`[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#dependencies-with-yield-and-httpexception "Permanent link")

You saw that you can use dependencies with `yield` and have `try` blocks that catch exceptions.

The same way, you could raise an `HTTPException` or similar in the exit code, after the `yield`.

Tip

This is a somewhat advanced technique, and in most of the cases you won't really need it, as you can raise exceptions (including `HTTPException`) from inside of the rest of your application code, for example, in the _path operation function_.

But it's there for you if you need it. 🤓

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_9_1)

`from typing import Annotated from fastapi import Depends, FastAPI, HTTPException app = FastAPI() data = {     "plumbus": {"description": "Freshly pickled plumbus", "owner": "Morty"},    "portal-gun": {"description": "Gun to create portals", "owner": "Rick"}, } class OwnerError(Exception):     pass def get_username():     try:        yield "Rick"    except OwnerError as e:        raise HTTPException(status_code=400, detail=f"Owner error: {e}") @app.get("/items/{item_id}") def get_item(item_id: str, username: Annotated[str, Depends(get_username)]):     if item_id not in data:        raise HTTPException(status_code=404, detail="Item not found")    item = data[item_id]    if item["owner"] != username:        raise OwnerError(username)    return item`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_10_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_10_2)

An alternative you could use to catch exceptions (and possibly also raise another `HTTPException`) is to create a [Custom Exception Handler](https://fastapi.tiangolo.com/tutorial/handling-errors/#install-custom-exception-handlers).

## Dependencies with `yield` and `except`[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#dependencies-with-yield-and-except "Permanent link")

If you catch an exception using `except` in a dependency with `yield` and you don't raise it again (or raise a new exception), FastAPI won't be able to notice there was an exception, the same way that would happen with regular Python:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_11_1)

`from typing import Annotated from fastapi import Depends, FastAPI, HTTPException app = FastAPI() class InternalError(Exception):     pass def get_username():     try:        yield "Rick"    except InternalError:        print("Oops, we didn't raise again, Britney 😱") @app.get("/items/{item_id}") def get_item(item_id: str, username: Annotated[str, Depends(get_username)]):     if item_id == "portal-gun":        raise InternalError(            f"The portal gun is too dangerous to be owned by {username}"        )    if item_id != "plumbus":        raise HTTPException(            status_code=404, detail="Item not found, there's only a plumbus here"        )    return item_id`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_12_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_12_2)

In this case, the client will see an _HTTP 500 Internal Server Error_ response as it should, given that we are not raising an `HTTPException` or similar, but the server will **not have any logs** or any other indication of what was the error. 😱

### Always `raise` in Dependencies with `yield` and `except`[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#always-raise-in-dependencies-with-yield-and-except "Permanent link")

If you catch an exception in a dependency with `yield`, unless you are raising another `HTTPException` or similar, you should re-raise the original exception.

You can re-raise the same exception using `raise`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_13_1)

`from typing import Annotated from fastapi import Depends, FastAPI, HTTPException app = FastAPI() class InternalError(Exception):     pass def get_username():     try:        yield "Rick"    except InternalError:        print("We don't swallow the internal error here, we raise again 😎")        raise @app.get("/items/{item_id}") def get_item(item_id: str, username: Annotated[str, Depends(get_username)]):     if item_id == "portal-gun":        raise InternalError(            f"The portal gun is too dangerous to be owned by {username}"        )    if item_id != "plumbus":        raise HTTPException(            status_code=404, detail="Item not found, there's only a plumbus here"        )    return item_id`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_14_1)[](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_14_2)

Now the client will get the same _HTTP 500 Internal Server Error_ response, but the server will have our custom `InternalError` in the logs. 😎

## Execution of dependencies with `yield`[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#execution-of-dependencies-with-yield "Permanent link")

The sequence of execution is more or less like this diagram. Time flows from top to bottom. And each column is one of the parts interacting or executing code.

Background tasksPath OperationDep with yieldException handlerClientBackground tasksPath OperationDep with yieldException handlerClientCan raise exceptions, including HTTPExceptionRun code up to yieldopt[raise Exception]opt[handle]opt[raise]Response is already sent, can't change it anymoreopt[Tasks]opt[Raise other exception]Start requestRaise ExceptionHTTP error responseRun dependency, e.g. DB sessionRaise Exception (e.g. HTTPException)Can catch exception, raise a new HTTPException, raise other exceptionHTTP error responseReturn response to clientSend background tasksHandle exceptions in the background task code

Info

Only **one response** will be sent to the client. It might be one of the error responses or it will be the response from the _path operation_.

After one of those responses is sent, no other response can be sent.

Tip

This diagram shows `HTTPException`, but you could also raise any other exception that you catch in a dependency with `yield` or with a [Custom Exception Handler](https://fastapi.tiangolo.com/tutorial/handling-errors/#install-custom-exception-handlers).

If you raise any exception, it will be passed to the dependencies with yield, including `HTTPException`. In most cases you will want to re-raise that same exception or a new one from the dependency with `yield` to make sure it's properly handled.

## Dependencies with `yield`, `HTTPException`, `except` and Background Tasks[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#dependencies-with-yield-httpexception-except-and-background-tasks "Permanent link")

Warning

You most probably don't need these technical details, you can skip this section and continue below.

These details are useful mainly if you were using a version of FastAPI prior to 0.106.0 and used resources from dependencies with `yield` in background tasks.

### Dependencies with `yield` and `except`, Technical Details[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#dependencies-with-yield-and-except-technical-details "Permanent link")

Before FastAPI 0.110.0, if you used a dependency with `yield`, and then you captured an exception with `except` in that dependency, and you didn't raise the exception again, the exception would be automatically raised/forwarded to any exception handlers or the internal server error handler.

This was changed in version 0.110.0 to fix unhandled memory consumption from forwarded exceptions without a handler (internal server errors), and to make it consistent with the behavior of regular Python code.

### Background Tasks and Dependencies with `yield`, Technical Details[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#background-tasks-and-dependencies-with-yield-technical-details "Permanent link")

Before FastAPI 0.106.0, raising exceptions after `yield` was not possible, the exit code in dependencies with `yield` was executed _after_ the response was sent, so [Exception Handlers](https://fastapi.tiangolo.com/tutorial/handling-errors/#install-custom-exception-handlers) would have already run.

This was designed this way mainly to allow using the same objects "yielded" by dependencies inside of background tasks, because the exit code would be executed after the background tasks were finished.

Nevertheless, as this would mean waiting for the response to travel through the network while unnecessarily holding a resource in a dependency with yield (for example a database connection), this was changed in FastAPI 0.106.0.

Tip

Additionally, a background task is normally an independent set of logic that should be handled separately, with its own resources (e.g. its own database connection).

So, this way you will probably have cleaner code.

If you used to rely on this behavior, now you should create the resources for background tasks inside the background task itself, and use internally only data that doesn't depend on the resources of dependencies with `yield`.

For example, instead of using the same database session, you would create a new database session inside of the background task, and you would obtain the objects from the database using this new session. And then instead of passing the object from the database as a parameter to the background task function, you would pass the ID of that object and then obtain the object again inside the background task function.

## Context Managers[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#context-managers "Permanent link")

### What are "Context Managers"[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#what-are-context-managers "Permanent link")

"Context Managers" are any of those Python objects that you can use in a `with` statement.

For example, [you can use `with` to read a file](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files):

`with open("./somefile.txt") as f:     contents = f.read()    print(contents)`

Underneath, the `open("./somefile.txt")` creates an object that is called a "Context Manager".

When the `with` block finishes, it makes sure to close the file, even if there were exceptions.

When you create a dependency with `yield`, **FastAPI** will internally create a context manager for it, and combine it with some other related tools.

### Using context managers in dependencies with `yield`[¶](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#using-context-managers-in-dependencies-with-yield "Permanent link")

Warning

This is, more or less, an "advanced" idea.

If you are just starting with **FastAPI** you might want to skip it for now.

In Python, you can create Context Managers by [creating a class with two methods: `__enter__()` and `__exit__()`](https://docs.python.org/3/reference/datamodel.html#context-managers).

You can also use them inside of **FastAPI** dependencies with `yield` by using `with` or `async with` statements inside of the dependency function:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-with-yield/#__tabbed_15_1)

`class MySuperContextManager:     def __init__(self):        self.db = DBSession()     def __enter__(self):        return self.db     def __exit__(self, exc_type, exc_value, traceback):        self.db.close() async def get_db():     with MySuperContextManager() as db:        yield db`

Tip

Another way to create a context manager is with:

- [`@contextlib.contextmanager`](https://docs.python.org/3/library/contextlib.html#contextlib.contextmanager) or
- [`@contextlib.asynccontextmanager`](https://docs.python.org/3/library/contextlib.html#contextlib.asynccontextmanager)

using them to decorate a function with a single `yield`.

That's what **FastAPI** uses internally for dependencies with `yield`.

But you don't have to use the decorators for FastAPI dependencies (and you shouldn't).

FastAPI will do it for you internally.


# Security - First Steps[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#security-first-steps "Permanent link")

Let's imagine that you have your **backend** API in some domain.

And you have a **frontend** in another domain or in a different path of the same domain (or in a mobile application).

And you want to have a way for the frontend to authenticate with the backend, using a **username** and **password**.

We can use **OAuth2** to build that with **FastAPI**.

But let's save you the time of reading the full long specification just to find those little pieces of information you need.

Let's use the tools provided by **FastAPI** to handle security.

## How it looks[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#how-it-looks "Permanent link")

Let's first just use the code and see how it works, and then we'll come back to understand what's happening.

## Create `main.py`[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#create-mainpy "Permanent link")

Copy the example in a file `main.py`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/security/first-steps/#__tabbed_1_1)

`from typing import Annotated from fastapi import Depends, FastAPI from fastapi.security import OAuth2PasswordBearer app = FastAPI() oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") @app.get("/items/") async def read_items(token: Annotated[str, Depends(oauth2_scheme)]):     return {"token": token}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/first-steps/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/security/first-steps/#__tabbed_2_2)

## Run it[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#run-it "Permanent link")

Info

The [`python-multipart`](https://github.com/Kludex/python-multipart) package is automatically installed with **FastAPI** when you run the `pip install "fastapi[standard]"` command.

However, if you use the `pip install fastapi` command, the `python-multipart` package is not included by default.

To install it manually, make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install it with:

`$ pip install python-multipart`

This is because **OAuth2** uses "form data" for sending the `username` and `password`.

Run the example with:

[](https://fastapi.tiangolo.com/tutorial/security/first-steps/#)fastapi dev main.py  
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)  
  
[restart ↻](https://fastapi.tiangolo.com/tutorial/security/first-steps/#)

## Check it[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#check-it "Permanent link")

Go to the interactive docs at: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).

You will see something like this:

![](https://fastapi.tiangolo.com/img/tutorial/security/image01.png)

Authorize button!

You already have a shiny new "Authorize" button.

And your _path operation_ has a little lock in the top-right corner that you can click.

And if you click it, you have a little authorization form to type a `username` and `password` (and other optional fields):

![](https://fastapi.tiangolo.com/img/tutorial/security/image02.png)

Note

It doesn't matter what you type in the form, it won't work yet. But we'll get there.

This is of course not the frontend for the final users, but it's a great automatic tool to document interactively all your API.

It can be used by the frontend team (that can also be yourself).

It can be used by third party applications and systems.

And it can also be used by yourself, to debug, check and test the same application.

## The `password` flow[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#the-password-flow "Permanent link")

Now let's go back a bit and understand what is all that.

The `password` "flow" is one of the ways ("flows") defined in OAuth2, to handle security and authentication.

OAuth2 was designed so that the backend or API could be independent of the server that authenticates the user.

But in this case, the same **FastAPI** application will handle the API and the authentication.

So, let's review it from that simplified point of view:

- The user types the `username` and `password` in the frontend, and hits `Enter`.
- The frontend (running in the user's browser) sends that `username` and `password` to a specific URL in our API (declared with `tokenUrl="token"`).
- The API checks that `username` and `password`, and responds with a "token" (we haven't implemented any of this yet).
    - A "token" is just a string with some content that we can use later to verify this user.
    - Normally, a token is set to expire after some time.
        - So, the user will have to log in again at some point later.
        - And if the token is stolen, the risk is less. It is not like a permanent key that will work forever (in most of the cases).
- The frontend stores that token temporarily somewhere.
- The user clicks in the frontend to go to another section of the frontend web app.
- The frontend needs to fetch some more data from the API.
    - But it needs authentication for that specific endpoint.
    - So, to authenticate with our API, it sends a header `Authorization` with a value of `Bearer` plus the token.
    - If the token contains `foobar`, the content of the `Authorization` header would be: `Bearer foobar`.

## **FastAPI**'s `OAuth2PasswordBearer`[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#fastapis-oauth2passwordbearer "Permanent link")

**FastAPI** provides several tools, at different levels of abstraction, to implement these security features.

In this example we are going to use **OAuth2**, with the **Password** flow, using a **Bearer** token. We do that using the `OAuth2PasswordBearer` class.

Info

A "bearer" token is not the only option.

But it's the best one for our use case.

And it might be the best for most use cases, unless you are an OAuth2 expert and know exactly why there's another option that better suits your needs.

In that case, **FastAPI** also provides you with the tools to build it.

When we create an instance of the `OAuth2PasswordBearer` class we pass in the `tokenUrl` parameter. This parameter contains the URL that the client (the frontend running in the user's browser) will use to send the `username` and `password` in order to get a token.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/security/first-steps/#__tabbed_3_1)

`from typing import Annotated from fastapi import Depends, FastAPI from fastapi.security import OAuth2PasswordBearer app = FastAPI() oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") @app.get("/items/") async def read_items(token: Annotated[str, Depends(oauth2_scheme)]):     return {"token": token}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/first-steps/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/security/first-steps/#__tabbed_4_2)

Tip

Here `tokenUrl="token"` refers to a relative URL `token` that we haven't created yet. As it's a relative URL, it's equivalent to `./token`.

Because we are using a relative URL, if your API was located at `https://example.com/`, then it would refer to `https://example.com/token`. But if your API was located at `https://example.com/api/v1/`, then it would refer to `https://example.com/api/v1/token`.

Using a relative URL is important to make sure your application keeps working even in an advanced use case like [Behind a Proxy](https://fastapi.tiangolo.com/advanced/behind-a-proxy/).

This parameter doesn't create that endpoint / _path operation_, but declares that the URL `/token` will be the one that the client should use to get the token. That information is used in OpenAPI, and then in the interactive API documentation systems.

We will soon also create the actual path operation.

Info

If you are a very strict "Pythonista" you might dislike the style of the parameter name `tokenUrl` instead of `token_url`.

That's because it is using the same name as in the OpenAPI spec. So that if you need to investigate more about any of these security schemes you can just copy and paste it to find more information about it.

The `oauth2_scheme` variable is an instance of `OAuth2PasswordBearer`, but it is also a "callable".

It could be called as:

`oauth2_scheme(some, parameters)`

So, it can be used with `Depends`.

### Use it[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#use-it "Permanent link")

Now you can pass that `oauth2_scheme` in a dependency with `Depends`.

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/security/first-steps/#__tabbed_5_1)

`from typing import Annotated from fastapi import Depends, FastAPI from fastapi.security import OAuth2PasswordBearer app = FastAPI() oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") @app.get("/items/") async def read_items(token: Annotated[str, Depends(oauth2_scheme)]):     return {"token": token}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/first-steps/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/security/first-steps/#__tabbed_6_2)

This dependency will provide a `str` that is assigned to the parameter `token` of the _path operation function_.

**FastAPI** will know that it can use this dependency to define a "security scheme" in the OpenAPI schema (and the automatic API docs).

Technical Details

**FastAPI** will know that it can use the class `OAuth2PasswordBearer` (declared in a dependency) to define the security scheme in OpenAPI because it inherits from `fastapi.security.oauth2.OAuth2`, which in turn inherits from `fastapi.security.base.SecurityBase`.

All the security utilities that integrate with OpenAPI (and the automatic API docs) inherit from `SecurityBase`, that's how **FastAPI** can know how to integrate them in OpenAPI.

## What it does[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#what-it-does "Permanent link")

It will go and look in the request for that `Authorization` header, check if the value is `Bearer` plus some token, and will return the token as a `str`.

If it doesn't see an `Authorization` header, or the value doesn't have a `Bearer` token, it will respond with a 401 status code error (`UNAUTHORIZED`) directly.

You don't even have to check if the token exists to return an error. You can be sure that if your function is executed, it will have a `str` in that token.

You can try it already in the interactive docs:

![](https://fastapi.tiangolo.com/img/tutorial/security/image03.png)

We are not verifying the validity of the token yet, but that's a start already.

## Recap[¶](https://fastapi.tiangolo.com/tutorial/security/first-steps/#recap "Permanent link")

So, in just 3 or 4 extra lines, you already have some primitive form of security.

# Get Current User[¶](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#get-current-user "Permanent link")

In the previous chapter the security system (which is based on the dependency injection system) was giving the _path operation function_ a `token` as a `str`:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_1_1)

`from typing import Annotated from fastapi import Depends, FastAPI from fastapi.security import OAuth2PasswordBearer app = FastAPI() oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") @app.get("/items/") async def read_items(token: Annotated[str, Depends(oauth2_scheme)]):     return {"token": token}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_2_2)

But that is still not that useful.

Let's make it give us the current user.

## Create a user model[¶](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#create-a-user-model "Permanent link")

First, let's create a Pydantic user model.

The same way we use Pydantic to declare bodies, we can use it anywhere else:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_3_1)

`from typing import Annotated from fastapi import Depends, FastAPI from fastapi.security import OAuth2PasswordBearer from pydantic import BaseModel app = FastAPI() oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None def fake_decode_token(token):     return User(        username=token + "fakedecoded", email="john@example.com", full_name="John Doe"    ) async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    return user @app.get("/users/me") async def read_users_me(current_user: Annotated[User, Depends(get_current_user)]):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_4_4)

## Create a `get_current_user` dependency[¶](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#create-a-get_current_user-dependency "Permanent link")

Let's create a dependency `get_current_user`.

Remember that dependencies can have sub-dependencies?

`get_current_user` will have a dependency with the same `oauth2_scheme` we created before.

The same as we were doing before in the _path operation_ directly, our new dependency `get_current_user` will receive a `token` as a `str` from the sub-dependency `oauth2_scheme`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_5_1)

`from typing import Annotated from fastapi import Depends, FastAPI from fastapi.security import OAuth2PasswordBearer from pydantic import BaseModel app = FastAPI() oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None def fake_decode_token(token):     return User(        username=token + "fakedecoded", email="john@example.com", full_name="John Doe"    ) async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    return user @app.get("/users/me") async def read_users_me(current_user: Annotated[User, Depends(get_current_user)]):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_6_2)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_6_3)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_6_4)

## Get the user[¶](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#get-the-user "Permanent link")

`get_current_user` will use a (fake) utility function we created, that takes a token as a `str` and returns our Pydantic `User` model:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_7_1)

`from typing import Annotated from fastapi import Depends, FastAPI from fastapi.security import OAuth2PasswordBearer from pydantic import BaseModel app = FastAPI() oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None def fake_decode_token(token):     return User(        username=token + "fakedecoded", email="john@example.com", full_name="John Doe"    ) async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    return user @app.get("/users/me") async def read_users_me(current_user: Annotated[User, Depends(get_current_user)]):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_8_2)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_8_3)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_8_4)

## Inject the current user[¶](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#inject-the-current-user "Permanent link")

So now we can use the same `Depends` with our `get_current_user` in the _path operation_:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_9_1)

`from typing import Annotated from fastapi import Depends, FastAPI from fastapi.security import OAuth2PasswordBearer from pydantic import BaseModel app = FastAPI() oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None def fake_decode_token(token):     return User(        username=token + "fakedecoded", email="john@example.com", full_name="John Doe"    ) async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    return user @app.get("/users/me") async def read_users_me(current_user: Annotated[User, Depends(get_current_user)]):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_10_1)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_10_2)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_10_3)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_10_4)

Notice that we declare the type of `current_user` as the Pydantic model `User`.

This will help us inside of the function with all the completion and type checks.

Tip

You might remember that request bodies are also declared with Pydantic models.

Here **FastAPI** won't get confused because you are using `Depends`.

Check

The way this dependency system is designed allows us to have different dependencies (different "dependables") that all return a `User` model.

We are not restricted to having only one dependency that can return that type of data.

## Other models[¶](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#other-models "Permanent link")

You can now get the current user directly in the _path operation functions_ and deal with the security mechanisms at the **Dependency Injection** level, using `Depends`.

And you can use any model or data for the security requirements (in this case, a Pydantic model `User`).

But you are not restricted to using some specific data model, class or type.

Do you want to have an `id` and `email` and not have any `username` in your model? Sure. You can use these same tools.

Do you want to just have a `str`? Or just a `dict`? Or a database class model instance directly? It all works the same way.

You actually don't have users that log in to your application but robots, bots, or other systems, that have just an access token? Again, it all works the same.

Just use any kind of model, any kind of class, any kind of database that you need for your application. **FastAPI** has you covered with the dependency injection system.

## Code size[¶](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#code-size "Permanent link")

This example might seem verbose. Keep in mind that we are mixing security, data models, utility functions and _path operations_ in the same file.

But here's the key point.

The security and dependency injection stuff is written once.

And you can make it as complex as you want. And still, have it written only once, in a single place. With all the flexibility.

But you can have thousands of endpoints (_path operations_) using the same security system.

And all of them (or any portion of them that you want) can take advantage of re-using these dependencies or any other dependencies you create.

And all these thousands of _path operations_ can be as small as 3 lines:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_11_1)

`from typing import Annotated from fastapi import Depends, FastAPI from fastapi.security import OAuth2PasswordBearer from pydantic import BaseModel app = FastAPI() oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None def fake_decode_token(token):     return User(        username=token + "fakedecoded", email="john@example.com", full_name="John Doe"    ) async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    return user @app.get("/users/me") async def read_users_me(current_user: Annotated[User, Depends(get_current_user)]):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_12_1)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_12_2)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_12_3)[](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#__tabbed_12_4)

## Recap[¶](https://fastapi.tiangolo.com/tutorial/security/get-current-user/#recap "Permanent link")

You can now get the current user directly in your _path operation function_.

We are already halfway there.

We just need to add a _path operation_ for the user/client to actually send the `username` and `password`.

That comes next.

# Simple OAuth2 with Password and Bearer[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#simple-oauth2-with-password-and-bearer "Permanent link")

Now let's build from the previous chapter and add the missing parts to have a complete security flow.

## Get the `username` and `password`[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#get-the-username-and-password "Permanent link")

We are going to use **FastAPI** security utilities to get the `username` and `password`.

OAuth2 specifies that when using the "password flow" (that we are using) the client/user must send a `username` and `password` fields as form data.

And the spec says that the fields have to be named like that. So `user-name` or `email` wouldn't work.

But don't worry, you can show it as you wish to your final users in the frontend.

And your database models can use any other names you want.

But for the login _path operation_, we need to use these names to be compatible with the spec (and be able to, for example, use the integrated API documentation system).

The spec also states that the `username` and `password` must be sent as form data (so, no JSON here).

### `scope`[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#scope "Permanent link")

The spec also says that the client can send another form field "`scope`".

The form field name is `scope` (in singular), but it is actually a long string with "scopes" separated by spaces.

Each "scope" is just a string (without spaces).

They are normally used to declare specific security permissions, for example:

- `users:read` or `users:write` are common examples.
- `instagram_basic` is used by Facebook / Instagram.
- `https://www.googleapis.com/auth/drive` is used by Google.

Info

In OAuth2 a "scope" is just a string that declares a specific permission required.

It doesn't matter if it has other characters like `:` or if it is a URL.

Those details are implementation specific.

For OAuth2 they are just strings.

## Code to get the `username` and `password`[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#code-to-get-the-username-and-password "Permanent link")

Now let's use the utilities provided by **FastAPI** to handle this.

### `OAuth2PasswordRequestForm`[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#oauth2passwordrequestform "Permanent link")

First, import `OAuth2PasswordRequestForm`, and use it as a dependency with `Depends` in the _path operation_ for `/token`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_1_1)

`from typing import Annotated from fastapi import Depends, FastAPI, HTTPException, status from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm from pydantic import BaseModel fake_users_db = {     "johndoe": {        "username": "johndoe",        "full_name": "John Doe",        "email": "johndoe@example.com",        "hashed_password": "fakehashedsecret",        "disabled": False,    },    "alice": {        "username": "alice",        "full_name": "Alice Wonderson",        "email": "alice@example.com",        "hashed_password": "fakehashedsecret2",        "disabled": True,    }, } app = FastAPI() def fake_hash_password(password: str):     return "fakehashed" + password oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None class UserInDB(User):     hashed_password: str def get_user(db, username: str):     if username in db:        user_dict = db[username]        return UserInDB(**user_dict) def fake_decode_token(token):     # This doesn't provide any security at all    # Check the next version    user = get_user(fake_users_db, token)    return user async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    if not user:        raise HTTPException(            status_code=status.HTTP_401_UNAUTHORIZED,            detail="Invalid authentication credentials",            headers={"WWW-Authenticate": "Bearer"},        )    return user async def get_current_active_user(     current_user: Annotated[User, Depends(get_current_user)], ):     if current_user.disabled:        raise HTTPException(status_code=400, detail="Inactive user")    return current_user @app.post("/token") async def login(form_data: Annotated[OAuth2PasswordRequestForm, Depends()]):     user_dict = fake_users_db.get(form_data.username)    if not user_dict:        raise HTTPException(status_code=400, detail="Incorrect username or password")    user = UserInDB(**user_dict)    hashed_password = fake_hash_password(form_data.password)    if not hashed_password == user.hashed_password:        raise HTTPException(status_code=400, detail="Incorrect username or password")     return {"access_token": user.username, "token_type": "bearer"} @app.get("/users/me") async def read_users_me(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_2_4)

`OAuth2PasswordRequestForm` is a class dependency that declares a form body with:

- The `username`.
- The `password`.
- An optional `scope` field as a big string, composed of strings separated by spaces.
- An optional `grant_type`.

Tip

The OAuth2 spec actually _requires_ a field `grant_type` with a fixed value of `password`, but `OAuth2PasswordRequestForm` doesn't enforce it.

If you need to enforce it, use `OAuth2PasswordRequestFormStrict` instead of `OAuth2PasswordRequestForm`.

- An optional `client_id` (we don't need it for our example).
- An optional `client_secret` (we don't need it for our example).

Info

The `OAuth2PasswordRequestForm` is not a special class for **FastAPI** as is `OAuth2PasswordBearer`.

`OAuth2PasswordBearer` makes **FastAPI** know that it is a security scheme. So it is added that way to OpenAPI.

But `OAuth2PasswordRequestForm` is just a class dependency that you could have written yourself, or you could have declared `Form` parameters directly.

But as it's a common use case, it is provided by **FastAPI** directly, just to make it easier.

### Use the form data[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#use-the-form-data "Permanent link")

Tip

The instance of the dependency class `OAuth2PasswordRequestForm` won't have an attribute `scope` with the long string separated by spaces, instead, it will have a `scopes` attribute with the actual list of strings for each scope sent.

We are not using `scopes` in this example, but the functionality is there if you need it.

Now, get the user data from the (fake) database, using the `username` from the form field.

If there is no such user, we return an error saying "Incorrect username or password".

For the error, we use the exception `HTTPException`:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_3_1)

`from typing import Annotated from fastapi import Depends, FastAPI, HTTPException, status from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm from pydantic import BaseModel fake_users_db = {     "johndoe": {        "username": "johndoe",        "full_name": "John Doe",        "email": "johndoe@example.com",        "hashed_password": "fakehashedsecret",        "disabled": False,    },    "alice": {        "username": "alice",        "full_name": "Alice Wonderson",        "email": "alice@example.com",        "hashed_password": "fakehashedsecret2",        "disabled": True,    }, } app = FastAPI() def fake_hash_password(password: str):     return "fakehashed" + password oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None class UserInDB(User):     hashed_password: str def get_user(db, username: str):     if username in db:        user_dict = db[username]        return UserInDB(**user_dict) def fake_decode_token(token):     # This doesn't provide any security at all    # Check the next version    user = get_user(fake_users_db, token)    return user async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    if not user:        raise HTTPException(            status_code=status.HTTP_401_UNAUTHORIZED,            detail="Invalid authentication credentials",            headers={"WWW-Authenticate": "Bearer"},        )    return user async def get_current_active_user(     current_user: Annotated[User, Depends(get_current_user)], ):     if current_user.disabled:        raise HTTPException(status_code=400, detail="Inactive user")    return current_user @app.post("/token") async def login(form_data: Annotated[OAuth2PasswordRequestForm, Depends()]):     user_dict = fake_users_db.get(form_data.username)    if not user_dict:        raise HTTPException(status_code=400, detail="Incorrect username or password")    user = UserInDB(**user_dict)    hashed_password = fake_hash_password(form_data.password)    if not hashed_password == user.hashed_password:        raise HTTPException(status_code=400, detail="Incorrect username or password")     return {"access_token": user.username, "token_type": "bearer"} @app.get("/users/me") async def read_users_me(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_4_4)

### Check the password[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#check-the-password "Permanent link")

At this point we have the user data from our database, but we haven't checked the password.

Let's put that data in the Pydantic `UserInDB` model first.

You should never save plaintext passwords, so, we'll use the (fake) password hashing system.

If the passwords don't match, we return the same error.

#### Password hashing[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#password-hashing "Permanent link")

"Hashing" means: converting some content (a password in this case) into a sequence of bytes (just a string) that looks like gibberish.

Whenever you pass exactly the same content (exactly the same password) you get exactly the same gibberish.

But you cannot convert from the gibberish back to the password.

##### Why use password hashing[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#why-use-password-hashing "Permanent link")

If your database is stolen, the thief won't have your users' plaintext passwords, only the hashes.

So, the thief won't be able to try to use those same passwords in another system (as many users use the same password everywhere, this would be dangerous).

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_5_1)

`from typing import Annotated from fastapi import Depends, FastAPI, HTTPException, status from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm from pydantic import BaseModel fake_users_db = {     "johndoe": {        "username": "johndoe",        "full_name": "John Doe",        "email": "johndoe@example.com",        "hashed_password": "fakehashedsecret",        "disabled": False,    },    "alice": {        "username": "alice",        "full_name": "Alice Wonderson",        "email": "alice@example.com",        "hashed_password": "fakehashedsecret2",        "disabled": True,    }, } app = FastAPI() def fake_hash_password(password: str):     return "fakehashed" + password oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None class UserInDB(User):     hashed_password: str def get_user(db, username: str):     if username in db:        user_dict = db[username]        return UserInDB(**user_dict) def fake_decode_token(token):     # This doesn't provide any security at all    # Check the next version    user = get_user(fake_users_db, token)    return user async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    if not user:        raise HTTPException(            status_code=status.HTTP_401_UNAUTHORIZED,            detail="Invalid authentication credentials",            headers={"WWW-Authenticate": "Bearer"},        )    return user async def get_current_active_user(     current_user: Annotated[User, Depends(get_current_user)], ):     if current_user.disabled:        raise HTTPException(status_code=400, detail="Inactive user")    return current_user @app.post("/token") async def login(form_data: Annotated[OAuth2PasswordRequestForm, Depends()]):     user_dict = fake_users_db.get(form_data.username)    if not user_dict:        raise HTTPException(status_code=400, detail="Incorrect username or password")    user = UserInDB(**user_dict)    hashed_password = fake_hash_password(form_data.password)    if not hashed_password == user.hashed_password:        raise HTTPException(status_code=400, detail="Incorrect username or password")     return {"access_token": user.username, "token_type": "bearer"} @app.get("/users/me") async def read_users_me(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_6_2)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_6_3)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_6_4)

#### About `**user_dict`[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#about-user_dict "Permanent link")

`UserInDB(**user_dict)` means:

_Pass the keys and values of the `user_dict` directly as key-value arguments, equivalent to:_

`UserInDB(     username = user_dict["username"],    email = user_dict["email"],    full_name = user_dict["full_name"],    disabled = user_dict["disabled"],    hashed_password = user_dict["hashed_password"], )`

Info

For a more complete explanation of `**user_dict` check back in [the documentation for **Extra Models**](https://fastapi.tiangolo.com/tutorial/extra-models/#about-user_indict).

## Return the token[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#return-the-token "Permanent link")

The response of the `token` endpoint must be a JSON object.

It should have a `token_type`. In our case, as we are using "Bearer" tokens, the token type should be "`bearer`".

And it should have an `access_token`, with a string containing our access token.

For this simple example, we are going to just be completely insecure and return the same `username` as the token.

Tip

In the next chapter, you will see a real secure implementation, with password hashing and JWT tokens.

But for now, let's focus on the specific details we need.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_7_1)

`from typing import Annotated from fastapi import Depends, FastAPI, HTTPException, status from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm from pydantic import BaseModel fake_users_db = {     "johndoe": {        "username": "johndoe",        "full_name": "John Doe",        "email": "johndoe@example.com",        "hashed_password": "fakehashedsecret",        "disabled": False,    },    "alice": {        "username": "alice",        "full_name": "Alice Wonderson",        "email": "alice@example.com",        "hashed_password": "fakehashedsecret2",        "disabled": True,    }, } app = FastAPI() def fake_hash_password(password: str):     return "fakehashed" + password oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None class UserInDB(User):     hashed_password: str def get_user(db, username: str):     if username in db:        user_dict = db[username]        return UserInDB(**user_dict) def fake_decode_token(token):     # This doesn't provide any security at all    # Check the next version    user = get_user(fake_users_db, token)    return user async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    if not user:        raise HTTPException(            status_code=status.HTTP_401_UNAUTHORIZED,            detail="Invalid authentication credentials",            headers={"WWW-Authenticate": "Bearer"},        )    return user async def get_current_active_user(     current_user: Annotated[User, Depends(get_current_user)], ):     if current_user.disabled:        raise HTTPException(status_code=400, detail="Inactive user")    return current_user @app.post("/token") async def login(form_data: Annotated[OAuth2PasswordRequestForm, Depends()]):     user_dict = fake_users_db.get(form_data.username)    if not user_dict:        raise HTTPException(status_code=400, detail="Incorrect username or password")    user = UserInDB(**user_dict)    hashed_password = fake_hash_password(form_data.password)    if not hashed_password == user.hashed_password:        raise HTTPException(status_code=400, detail="Incorrect username or password")     return {"access_token": user.username, "token_type": "bearer"} @app.get("/users/me") async def read_users_me(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_8_2)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_8_3)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_8_4)

Tip

By the spec, you should return a JSON with an `access_token` and a `token_type`, the same as in this example.

This is something that you have to do yourself in your code, and make sure you use those JSON keys.

It's almost the only thing that you have to remember to do correctly yourself, to be compliant with the specifications.

For the rest, **FastAPI** handles it for you.

## Update the dependencies[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#update-the-dependencies "Permanent link")

Now we are going to update our dependencies.

We want to get the `current_user` _only_ if this user is active.

So, we create an additional dependency `get_current_active_user` that in turn uses `get_current_user` as a dependency.

Both of these dependencies will just return an HTTP error if the user doesn't exist, or if is inactive.

So, in our endpoint, we will only get a user if the user exists, was correctly authenticated, and is active:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_9_1)

`from typing import Annotated from fastapi import Depends, FastAPI, HTTPException, status from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm from pydantic import BaseModel fake_users_db = {     "johndoe": {        "username": "johndoe",        "full_name": "John Doe",        "email": "johndoe@example.com",        "hashed_password": "fakehashedsecret",        "disabled": False,    },    "alice": {        "username": "alice",        "full_name": "Alice Wonderson",        "email": "alice@example.com",        "hashed_password": "fakehashedsecret2",        "disabled": True,    }, } app = FastAPI() def fake_hash_password(password: str):     return "fakehashed" + password oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None class UserInDB(User):     hashed_password: str def get_user(db, username: str):     if username in db:        user_dict = db[username]        return UserInDB(**user_dict) def fake_decode_token(token):     # This doesn't provide any security at all    # Check the next version    user = get_user(fake_users_db, token)    return user async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     user = fake_decode_token(token)    if not user:        raise HTTPException(            status_code=status.HTTP_401_UNAUTHORIZED,            detail="Invalid authentication credentials",            headers={"WWW-Authenticate": "Bearer"},        )    return user async def get_current_active_user(     current_user: Annotated[User, Depends(get_current_user)], ):     if current_user.disabled:        raise HTTPException(status_code=400, detail="Inactive user")    return current_user @app.post("/token") async def login(form_data: Annotated[OAuth2PasswordRequestForm, Depends()]):     user_dict = fake_users_db.get(form_data.username)    if not user_dict:        raise HTTPException(status_code=400, detail="Incorrect username or password")    user = UserInDB(**user_dict)    hashed_password = fake_hash_password(form_data.password)    if not hashed_password == user.hashed_password:        raise HTTPException(status_code=400, detail="Incorrect username or password")     return {"access_token": user.username, "token_type": "bearer"} @app.get("/users/me") async def read_users_me(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return current_user`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_10_1)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_10_2)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_10_3)[](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#__tabbed_10_4)

Info

The additional header `WWW-Authenticate` with value `Bearer` we are returning here is also part of the spec.

Any HTTP (error) status code 401 "UNAUTHORIZED" is supposed to also return a `WWW-Authenticate` header.

In the case of bearer tokens (our case), the value of that header should be `Bearer`.

You can actually skip that extra header and it would still work.

But it's provided here to be compliant with the specifications.

Also, there might be tools that expect and use it (now or in the future) and that might be useful for you or your users, now or in the future.

That's the benefit of standards...

## See it in action[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#see-it-in-action "Permanent link")

Open the interactive docs: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).

### Authenticate[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#authenticate "Permanent link")

Click the "Authorize" button.

Use the credentials:

User: `johndoe`

Password: `secret`

![](https://fastapi.tiangolo.com/img/tutorial/security/image04.png)

After authenticating in the system, you will see it like:

![](https://fastapi.tiangolo.com/img/tutorial/security/image05.png)

### Get your own user data[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#get-your-own-user-data "Permanent link")

Now use the operation `GET` with the path `/users/me`.

You will get your user's data, like:

`{   "username": "johndoe",  "email": "johndoe@example.com",  "full_name": "John Doe",  "disabled": false,  "hashed_password": "fakehashedsecret" }`

![](https://fastapi.tiangolo.com/img/tutorial/security/image06.png)

If you click the lock icon and logout, and then try the same operation again, you will get an HTTP 401 error of:

`{   "detail": "Not authenticated" }`

### Inactive user[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#inactive-user "Permanent link")

Now try with an inactive user, authenticate with:

User: `alice`

Password: `secret2`

And try to use the operation `GET` with the path `/users/me`.

You will get an "Inactive user" error, like:

`{   "detail": "Inactive user" }`

## Recap[¶](https://fastapi.tiangolo.com/tutorial/security/simple-oauth2/#recap "Permanent link")

You now have the tools to implement a complete security system based on `username` and `password` for your API.

Using these tools, you can make the security system compatible with any database and with any user or data model.

The only detail missing is that it is not actually "secure" yet.

In the next chapter you'll see how to use a secure password hashing library and JWT tokens.

# OAuth2 with Password (and hashing), Bearer with JWT tokens[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#oauth2-with-password-and-hashing-bearer-with-jwt-tokens "Permanent link")

Now that we have all the security flow, let's make the application actually secure, using JWT tokens and secure password hashing.

This code is something you can actually use in your application, save the password hashes in your database, etc.

We are going to start from where we left in the previous chapter and increment it.

## About JWT[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#about-jwt "Permanent link")

JWT means "JSON Web Tokens".

It's a standard to codify a JSON object in a long dense string without spaces. It looks like this:

`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`

It is not encrypted, so, anyone could recover the information from the contents.

But it's signed. So, when you receive a token that you emitted, you can verify that you actually emitted it.

That way, you can create a token with an expiration of, let's say, 1 week. And then when the user comes back the next day with the token, you know that user is still logged in to your system.

After a week, the token will be expired and the user will not be authorized and will have to sign in again to get a new token. And if the user (or a third party) tried to modify the token to change the expiration, you would be able to discover it, because the signatures would not match.

If you want to play with JWT tokens and see how they work, check [https://jwt.io](https://jwt.io/).

## Install `PyJWT`[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#install-pyjwt "Permanent link")

We need to install `PyJWT` to generate and verify the JWT tokens in Python.

Make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install `pyjwt`:

[fast →](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#)pip install pyjwt  
████████████████████████████████ 80%

Info

If you are planning to use digital signature algorithms like RSA or ECDSA, you should install the cryptography library dependency `pyjwt[crypto]`.

You can read more about it in the [PyJWT Installation docs](https://pyjwt.readthedocs.io/en/latest/installation.html).

## Password hashing[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#password-hashing "Permanent link")

"Hashing" means converting some content (a password in this case) into a sequence of bytes (just a string) that looks like gibberish.

Whenever you pass exactly the same content (exactly the same password) you get exactly the same gibberish.

But you cannot convert from the gibberish back to the password.

### Why use password hashing[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#why-use-password-hashing "Permanent link")

If your database is stolen, the thief won't have your users' plaintext passwords, only the hashes.

So, the thief won't be able to try to use that password in another system (as many users use the same password everywhere, this would be dangerous).

## Install `passlib`[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#install-passlib "Permanent link")

PassLib is a great Python package to handle password hashes.

It supports many secure hashing algorithms and utilities to work with them.

The recommended algorithm is "Bcrypt".

Make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install PassLib with Bcrypt:

[fast →](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#)pip install "passlib[bcrypt]"  
███████████████████ 48%

Tip

With `passlib`, you could even configure it to be able to read passwords created by **Django**, a **Flask** security plug-in or many others.

So, you would be able to, for example, share the same data from a Django application in a database with a FastAPI application. Or gradually migrate a Django application using the same database.

And your users would be able to login from your Django app or from your **FastAPI** app, at the same time.

## Hash and verify the passwords[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#hash-and-verify-the-passwords "Permanent link")

Import the tools we need from `passlib`.

Create a PassLib "context". This is what will be used to hash and verify passwords.

Tip

The PassLib context also has functionality to use different hashing algorithms, including deprecated old ones only to allow verifying them, etc.

For example, you could use it to read and verify passwords generated by another system (like Django) but hash any new passwords with a different algorithm like Bcrypt.

And be compatible with all of them at the same time.

Create a utility function to hash a password coming from the user.

And another utility to verify if a received password matches the hash stored.

And another one to authenticate and return a user.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_1_1)

`from datetime import datetime, timedelta, timezone from typing import Annotated import jwt from fastapi import Depends, FastAPI, HTTPException, status from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm from jwt.exceptions import InvalidTokenError from passlib.context import CryptContext from pydantic import BaseModel # to get a string like this run: # openssl rand -hex 32 SECRET_KEY = "09d25e094faa6ca2556c818166b7a9563b93f7099f6f0f4caa6cf63b88e8d3e7" ALGORITHM = "HS256" ACCESS_TOKEN_EXPIRE_MINUTES = 30 fake_users_db = {     "johndoe": {        "username": "johndoe",        "full_name": "John Doe",        "email": "johndoe@example.com",        "hashed_password": "$2b$12$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36WQoeG6Lruj3vjPGga31lW",        "disabled": False,    } } class Token(BaseModel):     access_token: str    token_type: str class TokenData(BaseModel):     username: str | None = None class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None class UserInDB(User):     hashed_password: str pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto") oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") app = FastAPI() def verify_password(plain_password, hashed_password):     return pwd_context.verify(plain_password, hashed_password) def get_password_hash(password):     return pwd_context.hash(password) def get_user(db, username: str):     if username in db:        user_dict = db[username]        return UserInDB(**user_dict) def authenticate_user(fake_db, username: str, password: str):     user = get_user(fake_db, username)    if not user:        return False    if not verify_password(password, user.hashed_password):        return False    return user def create_access_token(data: dict, expires_delta: timedelta | None = None):     to_encode = data.copy()    if expires_delta:        expire = datetime.now(timezone.utc) + expires_delta    else:        expire = datetime.now(timezone.utc) + timedelta(minutes=15)    to_encode.update({"exp": expire})    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)    return encoded_jwt async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     credentials_exception = HTTPException(        status_code=status.HTTP_401_UNAUTHORIZED,        detail="Could not validate credentials",        headers={"WWW-Authenticate": "Bearer"},    )    try:        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])        username = payload.get("sub")        if username is None:            raise credentials_exception        token_data = TokenData(username=username)    except InvalidTokenError:        raise credentials_exception    user = get_user(fake_users_db, username=token_data.username)    if user is None:        raise credentials_exception    return user async def get_current_active_user(     current_user: Annotated[User, Depends(get_current_user)], ):     if current_user.disabled:        raise HTTPException(status_code=400, detail="Inactive user")    return current_user @app.post("/token") async def login_for_access_token(     form_data: Annotated[OAuth2PasswordRequestForm, Depends()], ) -> Token:     user = authenticate_user(fake_users_db, form_data.username, form_data.password)    if not user:        raise HTTPException(            status_code=status.HTTP_401_UNAUTHORIZED,            detail="Incorrect username or password",            headers={"WWW-Authenticate": "Bearer"},        )    access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)    access_token = create_access_token(        data={"sub": user.username}, expires_delta=access_token_expires    )    return Token(access_token=access_token, token_type="bearer") @app.get("/users/me/", response_model=User) async def read_users_me(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return current_user @app.get("/users/me/items/") async def read_own_items(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return [{"item_id": "Foo", "owner": current_user.username}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_2_1)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_2_2)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_2_3)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_2_4)

Note

If you check the new (fake) database `fake_users_db`, you will see how the hashed password looks like now: `"$2b$12$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36WQoeG6Lruj3vjPGga31lW"`.

## Handle JWT tokens[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#handle-jwt-tokens "Permanent link")

Import the modules installed.

Create a random secret key that will be used to sign the JWT tokens.

To generate a secure random secret key use the command:

[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#)openssl rand -hex 32  
09d25e094faa6ca2556c818166b7a9563b93f7099f6f0f4caa6cf63b88e8d3e7  
  
[restart ↻](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#)

And copy the output to the variable `SECRET_KEY` (don't use the one in the example).

Create a variable `ALGORITHM` with the algorithm used to sign the JWT token and set it to `"HS256"`.

Create a variable for the expiration of the token.

Define a Pydantic Model that will be used in the token endpoint for the response.

Create a utility function to generate a new access token.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_3_1)

`from datetime import datetime, timedelta, timezone from typing import Annotated import jwt from fastapi import Depends, FastAPI, HTTPException, status from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm from jwt.exceptions import InvalidTokenError from passlib.context import CryptContext from pydantic import BaseModel # to get a string like this run: # openssl rand -hex 32 SECRET_KEY = "09d25e094faa6ca2556c818166b7a9563b93f7099f6f0f4caa6cf63b88e8d3e7" ALGORITHM = "HS256" ACCESS_TOKEN_EXPIRE_MINUTES = 30 fake_users_db = {     "johndoe": {        "username": "johndoe",        "full_name": "John Doe",        "email": "johndoe@example.com",        "hashed_password": "$2b$12$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36WQoeG6Lruj3vjPGga31lW",        "disabled": False,    } } class Token(BaseModel):     access_token: str    token_type: str class TokenData(BaseModel):     username: str | None = None class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None class UserInDB(User):     hashed_password: str pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto") oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") app = FastAPI() def verify_password(plain_password, hashed_password):     return pwd_context.verify(plain_password, hashed_password) def get_password_hash(password):     return pwd_context.hash(password) def get_user(db, username: str):     if username in db:        user_dict = db[username]        return UserInDB(**user_dict) def authenticate_user(fake_db, username: str, password: str):     user = get_user(fake_db, username)    if not user:        return False    if not verify_password(password, user.hashed_password):        return False    return user def create_access_token(data: dict, expires_delta: timedelta | None = None):     to_encode = data.copy()    if expires_delta:        expire = datetime.now(timezone.utc) + expires_delta    else:        expire = datetime.now(timezone.utc) + timedelta(minutes=15)    to_encode.update({"exp": expire})    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)    return encoded_jwt async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     credentials_exception = HTTPException(        status_code=status.HTTP_401_UNAUTHORIZED,        detail="Could not validate credentials",        headers={"WWW-Authenticate": "Bearer"},    )    try:        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])        username = payload.get("sub")        if username is None:            raise credentials_exception        token_data = TokenData(username=username)    except InvalidTokenError:        raise credentials_exception    user = get_user(fake_users_db, username=token_data.username)    if user is None:        raise credentials_exception    return user async def get_current_active_user(     current_user: Annotated[User, Depends(get_current_user)], ):     if current_user.disabled:        raise HTTPException(status_code=400, detail="Inactive user")    return current_user @app.post("/token") async def login_for_access_token(     form_data: Annotated[OAuth2PasswordRequestForm, Depends()], ) -> Token:     user = authenticate_user(fake_users_db, form_data.username, form_data.password)    if not user:        raise HTTPException(            status_code=status.HTTP_401_UNAUTHORIZED,            detail="Incorrect username or password",            headers={"WWW-Authenticate": "Bearer"},        )    access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)    access_token = create_access_token(        data={"sub": user.username}, expires_delta=access_token_expires    )    return Token(access_token=access_token, token_type="bearer") @app.get("/users/me/", response_model=User) async def read_users_me(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return current_user @app.get("/users/me/items/") async def read_own_items(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return [{"item_id": "Foo", "owner": current_user.username}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_4_1)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_4_2)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_4_3)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_4_4)

## Update the dependencies[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#update-the-dependencies "Permanent link")

Update `get_current_user` to receive the same token as before, but this time, using JWT tokens.

Decode the received token, verify it, and return the current user.

If the token is invalid, return an HTTP error right away.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_5_1)

`from datetime import datetime, timedelta, timezone from typing import Annotated import jwt from fastapi import Depends, FastAPI, HTTPException, status from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm from jwt.exceptions import InvalidTokenError from passlib.context import CryptContext from pydantic import BaseModel # to get a string like this run: # openssl rand -hex 32 SECRET_KEY = "09d25e094faa6ca2556c818166b7a9563b93f7099f6f0f4caa6cf63b88e8d3e7" ALGORITHM = "HS256" ACCESS_TOKEN_EXPIRE_MINUTES = 30 fake_users_db = {     "johndoe": {        "username": "johndoe",        "full_name": "John Doe",        "email": "johndoe@example.com",        "hashed_password": "$2b$12$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36WQoeG6Lruj3vjPGga31lW",        "disabled": False,    } } class Token(BaseModel):     access_token: str    token_type: str class TokenData(BaseModel):     username: str | None = None class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None class UserInDB(User):     hashed_password: str pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto") oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") app = FastAPI() def verify_password(plain_password, hashed_password):     return pwd_context.verify(plain_password, hashed_password) def get_password_hash(password):     return pwd_context.hash(password) def get_user(db, username: str):     if username in db:        user_dict = db[username]        return UserInDB(**user_dict) def authenticate_user(fake_db, username: str, password: str):     user = get_user(fake_db, username)    if not user:        return False    if not verify_password(password, user.hashed_password):        return False    return user def create_access_token(data: dict, expires_delta: timedelta | None = None):     to_encode = data.copy()    if expires_delta:        expire = datetime.now(timezone.utc) + expires_delta    else:        expire = datetime.now(timezone.utc) + timedelta(minutes=15)    to_encode.update({"exp": expire})    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)    return encoded_jwt async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     credentials_exception = HTTPException(        status_code=status.HTTP_401_UNAUTHORIZED,        detail="Could not validate credentials",        headers={"WWW-Authenticate": "Bearer"},    )    try:        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])        username = payload.get("sub")        if username is None:            raise credentials_exception        token_data = TokenData(username=username)    except InvalidTokenError:        raise credentials_exception    user = get_user(fake_users_db, username=token_data.username)    if user is None:        raise credentials_exception    return user async def get_current_active_user(     current_user: Annotated[User, Depends(get_current_user)], ):     if current_user.disabled:        raise HTTPException(status_code=400, detail="Inactive user")    return current_user @app.post("/token") async def login_for_access_token(     form_data: Annotated[OAuth2PasswordRequestForm, Depends()], ) -> Token:     user = authenticate_user(fake_users_db, form_data.username, form_data.password)    if not user:        raise HTTPException(            status_code=status.HTTP_401_UNAUTHORIZED,            detail="Incorrect username or password",            headers={"WWW-Authenticate": "Bearer"},        )    access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)    access_token = create_access_token(        data={"sub": user.username}, expires_delta=access_token_expires    )    return Token(access_token=access_token, token_type="bearer") @app.get("/users/me/", response_model=User) async def read_users_me(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return current_user @app.get("/users/me/items/") async def read_own_items(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return [{"item_id": "Foo", "owner": current_user.username}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_6_2)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_6_3)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_6_4)

## Update the `/token` _path operation_[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#update-the-token-path-operation "Permanent link")

Create a `timedelta` with the expiration time of the token.

Create a real JWT access token and return it.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_7_1)

`from datetime import datetime, timedelta, timezone from typing import Annotated import jwt from fastapi import Depends, FastAPI, HTTPException, status from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm from jwt.exceptions import InvalidTokenError from passlib.context import CryptContext from pydantic import BaseModel # to get a string like this run: # openssl rand -hex 32 SECRET_KEY = "09d25e094faa6ca2556c818166b7a9563b93f7099f6f0f4caa6cf63b88e8d3e7" ALGORITHM = "HS256" ACCESS_TOKEN_EXPIRE_MINUTES = 30 fake_users_db = {     "johndoe": {        "username": "johndoe",        "full_name": "John Doe",        "email": "johndoe@example.com",        "hashed_password": "$2b$12$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36WQoeG6Lruj3vjPGga31lW",        "disabled": False,    } } class Token(BaseModel):     access_token: str    token_type: str class TokenData(BaseModel):     username: str | None = None class User(BaseModel):     username: str    email: str | None = None    full_name: str | None = None    disabled: bool | None = None class UserInDB(User):     hashed_password: str pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto") oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token") app = FastAPI() def verify_password(plain_password, hashed_password):     return pwd_context.verify(plain_password, hashed_password) def get_password_hash(password):     return pwd_context.hash(password) def get_user(db, username: str):     if username in db:        user_dict = db[username]        return UserInDB(**user_dict) def authenticate_user(fake_db, username: str, password: str):     user = get_user(fake_db, username)    if not user:        return False    if not verify_password(password, user.hashed_password):        return False    return user def create_access_token(data: dict, expires_delta: timedelta | None = None):     to_encode = data.copy()    if expires_delta:        expire = datetime.now(timezone.utc) + expires_delta    else:        expire = datetime.now(timezone.utc) + timedelta(minutes=15)    to_encode.update({"exp": expire})    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)    return encoded_jwt async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):     credentials_exception = HTTPException(        status_code=status.HTTP_401_UNAUTHORIZED,        detail="Could not validate credentials",        headers={"WWW-Authenticate": "Bearer"},    )    try:        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])        username = payload.get("sub")        if username is None:            raise credentials_exception        token_data = TokenData(username=username)    except InvalidTokenError:        raise credentials_exception    user = get_user(fake_users_db, username=token_data.username)    if user is None:        raise credentials_exception    return user async def get_current_active_user(     current_user: Annotated[User, Depends(get_current_user)], ):     if current_user.disabled:        raise HTTPException(status_code=400, detail="Inactive user")    return current_user @app.post("/token") async def login_for_access_token(     form_data: Annotated[OAuth2PasswordRequestForm, Depends()], ) -> Token:     user = authenticate_user(fake_users_db, form_data.username, form_data.password)    if not user:        raise HTTPException(            status_code=status.HTTP_401_UNAUTHORIZED,            detail="Incorrect username or password",            headers={"WWW-Authenticate": "Bearer"},        )    access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)    access_token = create_access_token(        data={"sub": user.username}, expires_delta=access_token_expires    )    return Token(access_token=access_token, token_type="bearer") @app.get("/users/me/", response_model=User) async def read_users_me(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return current_user @app.get("/users/me/items/") async def read_own_items(     current_user: Annotated[User, Depends(get_current_active_user)], ):     return [{"item_id": "Foo", "owner": current_user.username}]`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_8_1)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_8_2)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_8_3)[](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#__tabbed_8_4)

### Technical details about the JWT "subject" `sub`[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#technical-details-about-the-jwt-subject-sub "Permanent link")

The JWT specification says that there's a key `sub`, with the subject of the token.

It's optional to use it, but that's where you would put the user's identification, so we are using it here.

JWT might be used for other things apart from identifying a user and allowing them to perform operations directly on your API.

For example, you could identify a "car" or a "blog post".

Then you could add permissions about that entity, like "drive" (for the car) or "edit" (for the blog).

And then, you could give that JWT token to a user (or bot), and they could use it to perform those actions (drive the car, or edit the blog post) without even needing to have an account, just with the JWT token your API generated for that.

Using these ideas, JWT can be used for way more sophisticated scenarios.

In those cases, several of those entities could have the same ID, let's say `foo` (a user `foo`, a car `foo`, and a blog post `foo`).

So, to avoid ID collisions, when creating the JWT token for the user, you could prefix the value of the `sub` key, e.g. with `username:`. So, in this example, the value of `sub` could have been: `username:johndoe`.

The important thing to keep in mind is that the `sub` key should have a unique identifier across the entire application, and it should be a string.

## Check it[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#check-it "Permanent link")

Run the server and go to the docs: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).

You'll see the user interface like:

![](https://fastapi.tiangolo.com/img/tutorial/security/image07.png)

Authorize the application the same way as before.

Using the credentials:

Username: `johndoe` Password: `secret`

Check

Notice that nowhere in the code is the plaintext password "`secret`", we only have the hashed version.

![](https://fastapi.tiangolo.com/img/tutorial/security/image08.png)

Call the endpoint `/users/me/`, you will get the response as:

`{   "username": "johndoe",  "email": "johndoe@example.com",  "full_name": "John Doe",  "disabled": false }`

![](https://fastapi.tiangolo.com/img/tutorial/security/image09.png)

If you open the developer tools, you could see how the data sent only includes the token, the password is only sent in the first request to authenticate the user and get that access token, but not afterwards:

![](https://fastapi.tiangolo.com/img/tutorial/security/image10.png)

Note

Notice the header `Authorization`, with a value that starts with `Bearer`.

## Advanced usage with `scopes`[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#advanced-usage-with-scopes "Permanent link")

OAuth2 has the notion of "scopes".

You can use them to add a specific set of permissions to a JWT token.

Then you can give this token to a user directly or a third party, to interact with your API with a set of restrictions.

You can learn how to use them and how they are integrated into **FastAPI** later in the **Advanced User Guide**.

## Recap[¶](https://fastapi.tiangolo.com/tutorial/security/oauth2-jwt/#recap "Permanent link")

With what you have seen up to now, you can set up a secure **FastAPI** application using standards like OAuth2 and JWT.

In almost any framework handling the security becomes a rather complex subject quite quickly.

Many packages that simplify it a lot have to make many compromises with the data model, database, and available features. And some of these packages that simplify things too much actually have security flaws underneath.

---

**FastAPI** doesn't make any compromise with any database, data model or tool.

It gives you all the flexibility to choose the ones that fit your project the best.

And you can use directly many well maintained and widely used packages like `passlib` and `PyJWT`, because **FastAPI** doesn't require any complex mechanisms to integrate external packages.

But it provides you the tools to simplify the process as much as possible without compromising flexibility, robustness, or security.

And you can use and implement secure, standard protocols, like OAuth2 in a relatively simple way.

You can learn more in the **Advanced User Guide** about how to use OAuth2 "scopes", for a more fine-grained permission system, following these same standards. OAuth2 with scopes is the mechanism used by many big authentication providers, like Facebook, Google, GitHub, Microsoft, Twitter, etc. to authorize third party applications to interact with their APIs on behalf of their users.


# Middleware[¶](https://fastapi.tiangolo.com/tutorial/middleware/#middleware "Permanent link")

You can add middleware to **FastAPI** applications.

A "middleware" is a function that works with every **request** before it is processed by any specific _path operation_. And also with every **response** before returning it.

- It takes each **request** that comes to your application.
- It can then do something to that **request** or run any needed code.
- Then it passes the **request** to be processed by the rest of the application (by some _path operation_).
- It then takes the **response** generated by the application (by some _path operation_).
- It can do something to that **response** or run any needed code.
- Then it returns the **response**.

Technical Details

If you have dependencies with `yield`, the exit code will run _after_ the middleware.

If there were any background tasks (covered in the [Background Tasks](https://fastapi.tiangolo.com/tutorial/background-tasks/) section, you will see it later), they will run _after_ all the middleware.

## Create a middleware[¶](https://fastapi.tiangolo.com/tutorial/middleware/#create-a-middleware "Permanent link")

To create a middleware you use the decorator `@app.middleware("http")` on top of a function.

The middleware function receives:

- The `request`.
- A function `call_next` that will receive the `request` as a parameter.
    - This function will pass the `request` to the corresponding _path operation_.
    - Then it returns the `response` generated by the corresponding _path operation_.
- You can then further modify the `response` before returning it.

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/middleware/#__tabbed_1_1)

`import time from fastapi import FastAPI, Request app = FastAPI() @app.middleware("http") async def add_process_time_header(request: Request, call_next):     start_time = time.perf_counter()    response = await call_next(request)    process_time = time.perf_counter() - start_time    response.headers["X-Process-Time"] = str(process_time)    return response`

Tip

Keep in mind that custom proprietary headers can be added [using the 'X-' prefix](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers).

But if you have custom headers that you want a client in a browser to be able to see, you need to add them to your CORS configurations ([CORS (Cross-Origin Resource Sharing)](https://fastapi.tiangolo.com/tutorial/cors/)) using the parameter `expose_headers` documented in [Starlette's CORS docs](https://www.starlette.io/middleware/#corsmiddleware).

Technical Details

You could also use `from starlette.requests import Request`.

**FastAPI** provides it as a convenience for you, the developer. But it comes directly from Starlette.

### Before and after the `response`[¶](https://fastapi.tiangolo.com/tutorial/middleware/#before-and-after-the-response "Permanent link")

You can add code to be run with the `request`, before any _path operation_ receives it.

And also after the `response` is generated, before returning it.

For example, you could add a custom header `X-Process-Time` containing the time in seconds that it took to process the request and generate a response:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/middleware/#__tabbed_2_1)

`import time from fastapi import FastAPI, Request app = FastAPI() @app.middleware("http") async def add_process_time_header(request: Request, call_next):     start_time = time.perf_counter()    response = await call_next(request)    process_time = time.perf_counter() - start_time    response.headers["X-Process-Time"] = str(process_time)    return response`

Tip

Here we use [`time.perf_counter()`](https://docs.python.org/3/library/time.html#time.perf_counter) instead of `time.time()` because it can be more precise for these use cases. 🤓

## Multiple middleware execution order[¶](https://fastapi.tiangolo.com/tutorial/middleware/#multiple-middleware-execution-order "Permanent link")

When you add multiple middlewares using either `@app.middleware()` decorator or `app.add_middleware()` method, each new middleware wraps the application, forming a stack. The last middleware added is the _outermost_, and the first is the _innermost_.

On the request path, the _outermost_ middleware runs first.

On the response path, it runs last.

For example:

`app.add_middleware(MiddlewareA) app.add_middleware(MiddlewareB)`

This results in the following execution order:

- **Request**: MiddlewareB → MiddlewareA → route
    
- **Response**: route → MiddlewareA → MiddlewareB
    

This stacking behavior ensures that middlewares are executed in a predictable and controllable order.

## Other middlewares[¶](https://fastapi.tiangolo.com/tutorial/middleware/#other-middlewares "Permanent link")

You can later read more about other middlewares in the [Advanced User Guide: Advanced Middleware](https://fastapi.tiangolo.com/advanced/middleware/).

You will read about how to handle CORS with a middleware in the next section.

# CORS (Cross-Origin Resource Sharing)[¶](https://fastapi.tiangolo.com/tutorial/cors/#cors-cross-origin-resource-sharing "Permanent link")

[CORS or "Cross-Origin Resource Sharing"](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) refers to the situations when a frontend running in a browser has JavaScript code that communicates with a backend, and the backend is in a different "origin" than the frontend.

## Origin[¶](https://fastapi.tiangolo.com/tutorial/cors/#origin "Permanent link")

An origin is the combination of protocol (`http`, `https`), domain (`myapp.com`, `localhost`, `localhost.tiangolo.com`), and port (`80`, `443`, `8080`).

So, all these are different origins:

- `http://localhost`
- `https://localhost`
- `http://localhost:8080`

Even if they are all in `localhost`, they use different protocols or ports, so, they are different "origins".

## Steps[¶](https://fastapi.tiangolo.com/tutorial/cors/#steps "Permanent link")

So, let's say you have a frontend running in your browser at `http://localhost:8080`, and its JavaScript is trying to communicate with a backend running at `http://localhost` (because we don't specify a port, the browser will assume the default port `80`).

Then, the browser will send an HTTP `OPTIONS` request to the `:80`-backend, and if the backend sends the appropriate headers authorizing the communication from this different origin (`http://localhost:8080`) then the `:8080`-browser will let the JavaScript in the frontend send its request to the `:80`-backend.

To achieve this, the `:80`-backend must have a list of "allowed origins".

In this case, the list would have to include `http://localhost:8080` for the `:8080`-frontend to work correctly.

## Wildcards[¶](https://fastapi.tiangolo.com/tutorial/cors/#wildcards "Permanent link")

It's also possible to declare the list as `"*"` (a "wildcard") to say that all are allowed.

But that will only allow certain types of communication, excluding everything that involves credentials: Cookies, Authorization headers like those used with Bearer Tokens, etc.

So, for everything to work correctly, it's better to specify explicitly the allowed origins.

## Use `CORSMiddleware`[¶](https://fastapi.tiangolo.com/tutorial/cors/#use-corsmiddleware "Permanent link")

You can configure it in your **FastAPI** application using the `CORSMiddleware`.

- Import `CORSMiddleware`.
- Create a list of allowed origins (as strings).
- Add it as a "middleware" to your **FastAPI** application.

You can also specify whether your backend allows:

- Credentials (Authorization headers, Cookies, etc).
- Specific HTTP methods (`POST`, `PUT`) or all of them with the wildcard `"*"`.
- Specific HTTP headers or all of them with the wildcard `"*"`.

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/cors/#__tabbed_1_1)

`from fastapi import FastAPI from fastapi.middleware.cors import CORSMiddleware app = FastAPI() origins = [     "http://localhost.tiangolo.com",    "https://localhost.tiangolo.com",    "http://localhost",    "http://localhost:8080", ] app.add_middleware(     CORSMiddleware,    allow_origins=origins,    allow_credentials=True,    allow_methods=["*"],    allow_headers=["*"], ) @app.get("/") async def main():     return {"message": "Hello World"}`

The default parameters used by the `CORSMiddleware` implementation are restrictive by default, so you'll need to explicitly enable particular origins, methods, or headers, in order for browsers to be permitted to use them in a Cross-Domain context.

The following arguments are supported:

- `allow_origins` - A list of origins that should be permitted to make cross-origin requests. E.g. `['https://example.org', 'https://www.example.org']`. You can use `['*']` to allow any origin.
- `allow_origin_regex` - A regex string to match against origins that should be permitted to make cross-origin requests. e.g. `'https://.*\.example\.org'`.
- `allow_methods` - A list of HTTP methods that should be allowed for cross-origin requests. Defaults to `['GET']`. You can use `['*']` to allow all standard methods.
- `allow_headers` - A list of HTTP request headers that should be supported for cross-origin requests. Defaults to `[]`. You can use `['*']` to allow all headers. The `Accept`, `Accept-Language`, `Content-Language` and `Content-Type` headers are always allowed for [simple CORS requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#simple_requests).
- `allow_credentials` - Indicate that cookies should be supported for cross-origin requests. Defaults to `False`.
    
    None of `allow_origins`, `allow_methods` and `allow_headers` can be set to `['*']` if `allow_credentials` is set to `True`. All of them must be [explicitly specified](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#credentialed_requests_and_wildcards).
    
- `expose_headers` - Indicate any response headers that should be made accessible to the browser. Defaults to `[]`.
    
- `max_age` - Sets a maximum time in seconds for browsers to cache CORS responses. Defaults to `600`.

The middleware responds to two particular types of HTTP request...

### CORS preflight requests[¶](https://fastapi.tiangolo.com/tutorial/cors/#cors-preflight-requests "Permanent link")

These are any `OPTIONS` request with `Origin` and `Access-Control-Request-Method` headers.

In this case the middleware will intercept the incoming request and respond with appropriate CORS headers, and either a `200` or `400` response for informational purposes.

### Simple requests[¶](https://fastapi.tiangolo.com/tutorial/cors/#simple-requests "Permanent link")

Any request with an `Origin` header. In this case the middleware will pass the request through as normal, but will include appropriate CORS headers on the response.

## More info[¶](https://fastapi.tiangolo.com/tutorial/cors/#more-info "Permanent link")

For more info about CORS, check the [Mozilla CORS documentation](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).

Technical Details

You could also use `from starlette.middleware.cors import CORSMiddleware`.

**FastAPI** provides several middlewares in `fastapi.middleware` just as a convenience for you, the developer. But most of the available middlewares come directly from Starlette.


# SQL (Relational) Databases[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#sql-relational-databases "Permanent link")

**FastAPI** doesn't require you to use a SQL (relational) database. But you can use **any database** that you want.

Here we'll see an example using [SQLModel](https://sqlmodel.tiangolo.com/).

**SQLModel** is built on top of [SQLAlchemy](https://www.sqlalchemy.org/) and Pydantic. It was made by the same author of **FastAPI** to be the perfect match for FastAPI applications that need to use **SQL databases**.

Tip

You could use any other SQL or NoSQL database library you want (in some cases called "ORMs"), FastAPI doesn't force you to use anything. 😎

As SQLModel is based on SQLAlchemy, you can easily use **any database supported** by SQLAlchemy (which makes them also supported by SQLModel), like:

- PostgreSQL
- MySQL
- SQLite
- Oracle
- Microsoft SQL Server, etc.

In this example, we'll use **SQLite**, because it uses a single file and Python has integrated support. So, you can copy this example and run it as is.

Later, for your production application, you might want to use a database server like **PostgreSQL**.

Tip

There is an official project generator with **FastAPI** and **PostgreSQL** including a frontend and more tools: [https://github.com/fastapi/full-stack-fastapi-template](https://github.com/fastapi/full-stack-fastapi-template)

This is a very simple and short tutorial, if you want to learn about databases in general, about SQL, or more advanced features, go to the [SQLModel docs](https://sqlmodel.tiangolo.com/).

## Install `SQLModel`[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#install-sqlmodel "Permanent link")

First, make sure you create your [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install `sqlmodel`:

[fast →](https://fastapi.tiangolo.com/tutorial/sql-databases/#)pip install sqlmodel

## Create the App with a Single Model[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#create-the-app-with-a-single-model "Permanent link")

We'll create the simplest first version of the app with a single **SQLModel** model first.

Later we'll improve it increasing security and versatility with **multiple models** below. 🤓

### Create Models[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#create-models "Permanent link")

Import `SQLModel` and create a database model:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_1_1)

`from typing import Annotated from fastapi import Depends, FastAPI, HTTPException, Query from sqlmodel import Field, Session, SQLModel, create_engine, select class Hero(SQLModel, table=True):     id: int | None = Field(default=None, primary_key=True)    name: str = Field(index=True)    age: int | None = Field(default=None, index=True)    secret_name: str # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_2_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_3_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_3_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_3_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_3_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_3_5)

The `Hero` class is very similar to a Pydantic model (in fact, underneath, it actually _is a Pydantic model_).

There are a few differences:

- `table=True` tells SQLModel that this is a _table model_, it should represent a **table** in the SQL database, it's not just a _data model_ (as would be any other regular Pydantic class).
    
- `Field(primary_key=True)` tells SQLModel that the `id` is the **primary key** in the SQL database (you can learn more about SQL primary keys in the SQLModel docs).
    
    By having the type as `int | None`, SQLModel will know that this column should be an `INTEGER` in the SQL database and that it should be `NULLABLE`.
    
- `Field(index=True)` tells SQLModel that it should create a **SQL index** for this column, that would allow faster lookups in the database when reading data filtered by this column.
    
    SQLModel will know that something declared as `str` will be a SQL column of type `TEXT` (or `VARCHAR`, depending on the database).
    

### Create an Engine[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#create-an-engine "Permanent link")

A SQLModel `engine` (underneath it's actually a SQLAlchemy `engine`) is what **holds the connections** to the database.

You would have **one single `engine` object** for all your code to connect to the same database.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_4_1)

`# Code above omitted 👆 sqlite_file_name = "database.db" sqlite_url = f"sqlite:///{sqlite_file_name}" connect_args = {"check_same_thread": False} engine = create_engine(sqlite_url, connect_args=connect_args) # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_5_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_6_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_6_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_6_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_6_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_6_5)

Using `check_same_thread=False` allows FastAPI to use the same SQLite database in different threads. This is necessary as **one single request** could use **more than one thread** (for example in dependencies).

Don't worry, with the way the code is structured, we'll make sure we use **a single SQLModel _session_ per request** later, this is actually what the `check_same_thread` is trying to achieve.

### Create the Tables[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#create-the-tables "Permanent link")

We then add a function that uses `SQLModel.metadata.create_all(engine)` to **create the tables** for all the _table models_.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_7_1)

`# Code above omitted 👆 def create_db_and_tables():     SQLModel.metadata.create_all(engine) # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_8_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_9_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_9_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_9_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_9_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_9_5)

### Create a Session Dependency[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#create-a-session-dependency "Permanent link")

A **`Session`** is what stores the **objects in memory** and keeps track of any changes needed in the data, then it **uses the `engine`** to communicate with the database.

We will create a FastAPI **dependency** with `yield` that will provide a new `Session` for each request. This is what ensures that we use a single session per request. 🤓

Then we create an `Annotated` dependency `SessionDep` to simplify the rest of the code that will use this dependency.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_10_1)

`# Code above omitted 👆 def get_session():     with Session(engine) as session:        yield session SessionDep = Annotated[Session, Depends(get_session)] # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_11_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_12_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_12_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_12_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_12_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_12_5)

### Create Database Tables on Startup[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#create-database-tables-on-startup "Permanent link")

We will create the database tables when the application starts.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_13_1)

`# Code above omitted 👆 app = FastAPI() @app.on_event("startup") def on_startup():     create_db_and_tables() # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_14_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_15_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_15_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_15_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_15_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_15_5)

Here we create the tables on an application startup event.

For production you would probably use a migration script that runs before you start your app. 🤓

Tip

SQLModel will have migration utilities wrapping Alembic, but for now, you can use [Alembic](https://alembic.sqlalchemy.org/en/latest/) directly.

### Create a Hero[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#create-a-hero "Permanent link")

Because each SQLModel model is also a Pydantic model, you can use it in the same **type annotations** that you could use Pydantic models.

For example, if you declare a parameter of type `Hero`, it will be read from the **JSON body**.

The same way, you can declare it as the function's **return type**, and then the shape of the data will show up in the automatic API docs UI.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_16_1)

`# Code above omitted 👆 @app.post("/heroes/") def create_hero(hero: Hero, session: SessionDep) -> Hero:     session.add(hero)    session.commit()    session.refresh(hero)    return hero # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_17_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_18_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_18_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_18_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_18_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_18_5)

Here we use the `SessionDep` dependency (a `Session`) to add the new `Hero` to the `Session` instance, commit the changes to the database, refresh the data in the `hero`, and then return it.

### Read Heroes[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#read-heroes "Permanent link")

We can **read** `Hero`s from the database using a `select()`. We can include a `limit` and `offset` to paginate the results.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_19_1)

`# Code above omitted 👆 @app.get("/heroes/") def read_heroes(     session: SessionDep,    offset: int = 0,    limit: Annotated[int, Query(le=100)] = 100, ) -> list[Hero]:     heroes = session.exec(select(Hero).offset(offset).limit(limit)).all()    return heroes # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_20_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_21_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_21_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_21_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_21_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_21_5)

### Read One Hero[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#read-one-hero "Permanent link")

We can **read** a single `Hero`.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_22_1)

`# Code above omitted 👆 @app.get("/heroes/{hero_id}") def read_hero(hero_id: int, session: SessionDep) -> Hero:     hero = session.get(Hero, hero_id)    if not hero:        raise HTTPException(status_code=404, detail="Hero not found")    return hero # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_23_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_24_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_24_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_24_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_24_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_24_5)

### Delete a Hero[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#delete-a-hero "Permanent link")

We can also **delete** a `Hero`.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_25_1)

`# Code above omitted 👆 @app.delete("/heroes/{hero_id}") def delete_hero(hero_id: int, session: SessionDep):     hero = session.get(Hero, hero_id)    if not hero:        raise HTTPException(status_code=404, detail="Hero not found")    session.delete(hero)    session.commit()    return {"ok": True}`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_26_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_27_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_27_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_27_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_27_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_27_5)

### Run the App[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#run-the-app "Permanent link")

You can run the app:

[fast →](https://fastapi.tiangolo.com/tutorial/sql-databases/#)fastapi dev m

Then go to the `/docs` UI, you will see that **FastAPI** is using these **models** to **document** the API, and it will use them to **serialize** and **validate** the data too.

![](https://fastapi.tiangolo.com/img/tutorial/sql-databases/image01.png)

## Update the App with Multiple Models[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#update-the-app-with-multiple-models "Permanent link")

Now let's **refactor** this app a bit to increase **security** and **versatility**.

If you check the previous app, in the UI you can see that, up to now, it lets the client decide the `id` of the `Hero` to create. 😱

We shouldn't let that happen, they could overwrite an `id` we already have assigned in the DB. Deciding the `id` should be done by the **backend** or the **database**, **not by the client**.

Additionally, we create a `secret_name` for the hero, but so far, we are returning it everywhere, that's not very **secret**... 😅

We'll fix these things by adding a few **extra models**. Here's where SQLModel will shine. ✨

### Create Multiple Models[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#create-multiple-models "Permanent link")

In **SQLModel**, any model class that has `table=True` is a **table model**.

And any model class that doesn't have `table=True` is a **data model**, these ones are actually just Pydantic models (with a couple of small extra features). 🤓

With SQLModel, we can use **inheritance** to **avoid duplicating** all the fields in all the cases.

#### `HeroBase` - the base class[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#herobase-the-base-class "Permanent link")

Let's start with a `HeroBase` model that has all the **fields that are shared** by all the models:

- `name`
- `age`

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_28_1)

`# Code above omitted 👆 class HeroBase(SQLModel):     name: str = Field(index=True)    age: int | None = Field(default=None, index=True) # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_29_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_30_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_30_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_30_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_30_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_30_5)

#### `Hero` - the _table model_[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#hero-the-table-model "Permanent link")

Then let's create `Hero`, the actual _table model_, with the **extra fields** that are not always in the other models:

- `id`
- `secret_name`

Because `Hero` inherits form `HeroBase`, it **also** has the **fields** declared in `HeroBase`, so all the fields for `Hero` are:

- `id`
- `name`
- `age`
- `secret_name`

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_31_1)

`# Code above omitted 👆 class HeroBase(SQLModel):     name: str = Field(index=True)    age: int | None = Field(default=None, index=True) class Hero(HeroBase, table=True):     id: int | None = Field(default=None, primary_key=True)    secret_name: str # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_32_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_33_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_33_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_33_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_33_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_33_5)

#### `HeroPublic` - the public _data model_[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#heropublic-the-public-data-model "Permanent link")

Next, we create a `HeroPublic` model, this is the one that will be **returned** to the clients of the API.

It has the same fields as `HeroBase`, so it won't include `secret_name`.

Finally, the identity of our heroes is protected! 🥷

It also re-declares `id: int`. By doing this, we are making a **contract** with the API clients, so that they can always expect the `id` to be there and to be an `int` (it will never be `None`).

Tip

Having the return model ensure that a value is always available and always `int` (not `None`) is very useful for the API clients, they can write much simpler code having this certainty.

Also, **automatically generated clients** will have simpler interfaces, so that the developers communicating with your API can have a much better time working with your API. 😎

All the fields in `HeroPublic` are the same as in `HeroBase`, with `id` declared as `int` (not `None`):

- `id`
- `name`
- `age`

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_34_1)

`# Code above omitted 👆 class HeroBase(SQLModel):     name: str = Field(index=True)    age: int | None = Field(default=None, index=True) class Hero(HeroBase, table=True):     id: int | None = Field(default=None, primary_key=True)    secret_name: str class HeroPublic(HeroBase):     id: int # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_35_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_36_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_36_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_36_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_36_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_36_5)

#### `HeroCreate` - the _data model_ to create a hero[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#herocreate-the-data-model-to-create-a-hero "Permanent link")

Now we create a `HeroCreate` model, this is the one that will **validate** the data from the clients.

It has the same fields as `HeroBase`, and it also has `secret_name`.

Now, when the clients **create a new hero**, they will send the `secret_name`, it will be stored in the database, but those secret names won't be returned in the API to the clients.

Tip

This is how you would handle **passwords**. Receive them, but don't return them in the API.

You would also **hash** the values of the passwords before storing them, **never store them in plain text**.

The fields of `HeroCreate` are:

- `name`
- `age`
- `secret_name`

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_37_1)

`# Code above omitted 👆 class HeroBase(SQLModel):     name: str = Field(index=True)    age: int | None = Field(default=None, index=True) class Hero(HeroBase, table=True):     id: int | None = Field(default=None, primary_key=True)    secret_name: str class HeroPublic(HeroBase):     id: int class HeroCreate(HeroBase):     secret_name: str # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_38_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_39_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_39_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_39_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_39_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_39_5)

#### `HeroUpdate` - the _data model_ to update a hero[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#heroupdate-the-data-model-to-update-a-hero "Permanent link")

We didn't have a way to **update a hero** in the previous version of the app, but now with **multiple models**, we can do it. 🎉

The `HeroUpdate` _data model_ is somewhat special, it has **all the same fields** that would be needed to create a new hero, but all the fields are **optional** (they all have a default value). This way, when you update a hero, you can send just the fields that you want to update.

Because all the **fields actually change** (the type now includes `None` and they now have a default value of `None`), we need to **re-declare** them.

We don't really need to inherit from `HeroBase` because we are re-declaring all the fields. I'll leave it inheriting just for consistency, but this is not necessary. It's more a matter of personal taste. 🤷

The fields of `HeroUpdate` are:

- `name`
- `age`
- `secret_name`

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_40_1)

`# Code above omitted 👆 class HeroBase(SQLModel):     name: str = Field(index=True)    age: int | None = Field(default=None, index=True) class Hero(HeroBase, table=True):     id: int | None = Field(default=None, primary_key=True)    secret_name: str class HeroPublic(HeroBase):     id: int class HeroCreate(HeroBase):     secret_name: str class HeroUpdate(HeroBase):     name: str | None = None    age: int | None = None    secret_name: str | None = None # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_41_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_42_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_42_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_42_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_42_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_42_5)

### Create with `HeroCreate` and return a `HeroPublic`[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#create-with-herocreate-and-return-a-heropublic "Permanent link")

Now that we have **multiple models**, we can update the parts of the app that use them.

We receive in the request a `HeroCreate` _data model_, and from it, we create a `Hero` _table model_.

This new _table model_ `Hero` will have the fields sent by the client, and will also have an `id` generated by the database.

Then we return the same _table model_ `Hero` as is from the function. But as we declare the `response_model` with the `HeroPublic` _data model_, **FastAPI** will use `HeroPublic` to validate and serialize the data.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_43_1)

`# Code above omitted 👆 @app.post("/heroes/", response_model=HeroPublic) def create_hero(hero: HeroCreate, session: SessionDep):     db_hero = Hero.model_validate(hero)    session.add(db_hero)    session.commit()    session.refresh(db_hero)    return db_hero # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_44_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_45_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_45_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_45_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_45_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_45_5)

Tip

Now we use `response_model=HeroPublic` instead of the **return type annotation** `-> HeroPublic` because the value that we are returning is actually _not_ a `HeroPublic`.

If we had declared `-> HeroPublic`, your editor and linter would complain (rightfully so) that you are returning a `Hero` instead of a `HeroPublic`.

By declaring it in `response_model` we are telling **FastAPI** to do its thing, without interfering with the type annotations and the help from your editor and other tools.

### Read Heroes with `HeroPublic`[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#read-heroes-with-heropublic "Permanent link")

We can do the same as before to **read** `Hero`s, again, we use `response_model=list[HeroPublic]` to ensure that the data is validated and serialized correctly.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_46_1)

`# Code above omitted 👆 @app.get("/heroes/", response_model=list[HeroPublic]) def read_heroes(     session: SessionDep,    offset: int = 0,    limit: Annotated[int, Query(le=100)] = 100, ):     heroes = session.exec(select(Hero).offset(offset).limit(limit)).all()    return heroes # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_47_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_48_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_48_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_48_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_48_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_48_5)

### Read One Hero with `HeroPublic`[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#read-one-hero-with-heropublic "Permanent link")

We can **read** a single hero:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_49_1)

`# Code above omitted 👆 @app.get("/heroes/{hero_id}", response_model=HeroPublic) def read_hero(hero_id: int, session: SessionDep):     hero = session.get(Hero, hero_id)    if not hero:        raise HTTPException(status_code=404, detail="Hero not found")    return hero # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_50_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_51_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_51_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_51_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_51_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_51_5)

### Update a Hero with `HeroUpdate`[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#update-a-hero-with-heroupdate "Permanent link")

We can **update a hero**. For this we use an HTTP `PATCH` operation.

And in the code, we get a `dict` with all the data sent by the client, **only the data sent by the client**, excluding any values that would be there just for being the default values. To do it we use `exclude_unset=True`. This is the main trick. 🪄

Then we use `hero_db.sqlmodel_update(hero_data)` to update the `hero_db` with the data from `hero_data`.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_52_1)

`# Code above omitted 👆 @app.patch("/heroes/{hero_id}", response_model=HeroPublic) def update_hero(hero_id: int, hero: HeroUpdate, session: SessionDep):     hero_db = session.get(Hero, hero_id)    if not hero_db:        raise HTTPException(status_code=404, detail="Hero not found")    hero_data = hero.model_dump(exclude_unset=True)    hero_db.sqlmodel_update(hero_data)    session.add(hero_db)    session.commit()    session.refresh(hero_db)    return hero_db # Code below omitted 👇`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_53_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_54_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_54_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_54_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_54_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_54_5)

### Delete a Hero Again[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#delete-a-hero-again "Permanent link")

**Deleting** a hero stays pretty much the same.

We won't satisfy the desire to refactor everything in this one. 😅

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_55_1)

`# Code above omitted 👆 @app.delete("/heroes/{hero_id}") def delete_hero(hero_id: int, session: SessionDep):     hero = session.get(Hero, hero_id)    if not hero:        raise HTTPException(status_code=404, detail="Hero not found")    session.delete(hero)    session.commit()    return {"ok": True}`

👀 Full file preview

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_56_1)

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_57_1)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_57_2)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_57_3)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_57_4)[](https://fastapi.tiangolo.com/tutorial/sql-databases/#__tabbed_57_5)

### Run the App Again[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#run-the-app-again "Permanent link")

You can run the app again:

[fast →](https://fastapi.tiangolo.com/tutorial/sql-databases/#)fasta

If you go to the `/docs` API UI, you will see that it is now updated, and it won't expect to receive the `id` from the client when creating a hero, etc.

![](https://fastapi.tiangolo.com/img/tutorial/sql-databases/image02.png)

## Recap[¶](https://fastapi.tiangolo.com/tutorial/sql-databases/#recap "Permanent link")

You can use [**SQLModel**](https://sqlmodel.tiangolo.com/) to interact with a SQL database and simplify the code with _data models_ and _table models_.

You can learn a lot more at the **SQLModel** docs, there's a longer mini [tutorial on using SQLModel with **FastAPI**](https://sqlmodel.tiangolo.com/tutorial/fastapi/). 🚀

# Bigger Applications - Multiple Files[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#bigger-applications-multiple-files "Permanent link")

If you are building an application or a web API, it's rarely the case that you can put everything in a single file.

**FastAPI** provides a convenience tool to structure your application while keeping all the flexibility.

Info

If you come from Flask, this would be the equivalent of Flask's Blueprints.

## An example file structure[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#an-example-file-structure "Permanent link")

Let's say you have a file structure like this:

`. ├── app │   ├── __init__.py │   ├── main.py │   ├── dependencies.py │   └── routers │   │   ├── __init__.py │   │   ├── items.py │   │   └── users.py │   └── internal │       ├── __init__.py │       └── admin.py`

Tip

There are several `__init__.py` files: one in each directory or subdirectory.

This is what allows importing code from one file into another.

For example, in `app/main.py` you could have a line like:

`from app.routers import items`

- The `app` directory contains everything. And it has an empty file `app/__init__.py`, so it is a "Python package" (a collection of "Python modules"): `app`.
- It contains an `app/main.py` file. As it is inside a Python package (a directory with a file `__init__.py`), it is a "module" of that package: `app.main`.
- There's also an `app/dependencies.py` file, just like `app/main.py`, it is a "module": `app.dependencies`.
- There's a subdirectory `app/routers/` with another file `__init__.py`, so it's a "Python subpackage": `app.routers`.
- The file `app/routers/items.py` is inside a package, `app/routers/`, so, it's a submodule: `app.routers.items`.
- The same with `app/routers/users.py`, it's another submodule: `app.routers.users`.
- There's also a subdirectory `app/internal/` with another file `__init__.py`, so it's another "Python subpackage": `app.internal`.
- And the file `app/internal/admin.py` is another submodule: `app.internal.admin`.

![](https://fastapi.tiangolo.com/img/tutorial/bigger-applications/package.drawio.svg)

The same file structure with comments:

`. ├── app                  # "app" is a Python package │   ├── __init__.py      # this file makes "app" a "Python package" │   ├── main.py          # "main" module, e.g. import app.main │   ├── dependencies.py  # "dependencies" module, e.g. import app.dependencies │   └── routers          # "routers" is a "Python subpackage" │   │   ├── __init__.py  # makes "routers" a "Python subpackage" │   │   ├── items.py     # "items" submodule, e.g. import app.routers.items │   │   └── users.py     # "users" submodule, e.g. import app.routers.users │   └── internal         # "internal" is a "Python subpackage" │       ├── __init__.py  # makes "internal" a "Python subpackage" │       └── admin.py     # "admin" submodule, e.g. import app.internal.admin`

## `APIRouter`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#apirouter "Permanent link")

Let's say the file dedicated to handling just users is the submodule at `/app/routers/users.py`.

You want to have the _path operations_ related to your users separated from the rest of the code, to keep it organized.

But it's still part of the same **FastAPI** application/web API (it's part of the same "Python Package").

You can create the _path operations_ for that module using `APIRouter`.

### Import `APIRouter`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#import-apirouter "Permanent link")

You import it and create an "instance" the same way you would with the class `FastAPI`:

app/routers/users.py

`from fastapi import APIRouter router = APIRouter() @router.get("/users/", tags=["users"]) async def read_users():     return [{"username": "Rick"}, {"username": "Morty"}] @router.get("/users/me", tags=["users"]) async def read_user_me():     return {"username": "fakecurrentuser"} @router.get("/users/{username}", tags=["users"]) async def read_user(username: str):     return {"username": username}`

### _Path operations_ with `APIRouter`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#path-operations-with-apirouter "Permanent link")

And then you use it to declare your _path operations_.

Use it the same way you would use the `FastAPI` class:

app/routers/users.py

`from fastapi import APIRouter router = APIRouter() @router.get("/users/", tags=["users"]) async def read_users():     return [{"username": "Rick"}, {"username": "Morty"}] @router.get("/users/me", tags=["users"]) async def read_user_me():     return {"username": "fakecurrentuser"} @router.get("/users/{username}", tags=["users"]) async def read_user(username: str):     return {"username": username}`

You can think of `APIRouter` as a "mini `FastAPI`" class.

All the same options are supported.

All the same `parameters`, `responses`, `dependencies`, `tags`, etc.

Tip

In this example, the variable is called `router`, but you can name it however you want.

We are going to include this `APIRouter` in the main `FastAPI` app, but first, let's check the dependencies and another `APIRouter`.

## Dependencies[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#dependencies "Permanent link")

We see that we are going to need some dependencies used in several places of the application.

So we put them in their own `dependencies` module (`app/dependencies.py`).

We will now use a simple dependency to read a custom `X-Token` header:

[Python 3.9+](https://fastapi.tiangolo.com/tutorial/bigger-applications/#__tabbed_1_1)[Python 3.8+](https://fastapi.tiangolo.com/tutorial/bigger-applications/#__tabbed_1_2)[Python 3.8+ non-Annotated](https://fastapi.tiangolo.com/tutorial/bigger-applications/#__tabbed_1_3)

app/dependencies.py

`from typing import Annotated from fastapi import Header, HTTPException async def get_token_header(x_token: Annotated[str, Header()]):     if x_token != "fake-super-secret-token":        raise HTTPException(status_code=400, detail="X-Token header invalid") async def get_query_token(token: str):     if token != "jessica":        raise HTTPException(status_code=400, detail="No Jessica token provided")`

Tip

We are using an invented header to simplify this example.

But in real cases you will get better results using the integrated [Security utilities](https://fastapi.tiangolo.com/tutorial/security/).

## Another module with `APIRouter`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#another-module-with-apirouter "Permanent link")

Let's say you also have the endpoints dedicated to handling "items" from your application in the module at `app/routers/items.py`.

You have _path operations_ for:

- `/items/`
- `/items/{item_id}`

It's all the same structure as with `app/routers/users.py`.

But we want to be smarter and simplify the code a bit.

We know all the _path operations_ in this module have the same:

- Path `prefix`: `/items`.
- `tags`: (just one tag: `items`).
- Extra `responses`.
- `dependencies`: they all need that `X-Token` dependency we created.

So, instead of adding all that to each _path operation_, we can add it to the `APIRouter`.

app/routers/items.py

`from fastapi import APIRouter, Depends, HTTPException from ..dependencies import get_token_header router = APIRouter(     prefix="/items",    tags=["items"],    dependencies=[Depends(get_token_header)],    responses={404: {"description": "Not found"}}, ) fake_items_db = {"plumbus": {"name": "Plumbus"}, "gun": {"name": "Portal Gun"}} @router.get("/") async def read_items():     return fake_items_db @router.get("/{item_id}") async def read_item(item_id: str):     if item_id not in fake_items_db:        raise HTTPException(status_code=404, detail="Item not found")    return {"name": fake_items_db[item_id]["name"], "item_id": item_id} @router.put(     "/{item_id}",    tags=["custom"],    responses={403: {"description": "Operation forbidden"}}, ) async def update_item(item_id: str):     if item_id != "plumbus":        raise HTTPException(            status_code=403, detail="You can only update the item: plumbus"        )    return {"item_id": item_id, "name": "The great Plumbus"}`

As the path of each _path operation_ has to start with `/`, like in:

`@router.get("/{item_id}") async def read_item(item_id: str):     ...`

...the prefix must not include a final `/`.

So, the prefix in this case is `/items`.

We can also add a list of `tags` and extra `responses` that will be applied to all the _path operations_ included in this router.

And we can add a list of `dependencies` that will be added to all the _path operations_ in the router and will be executed/solved for each request made to them.

Tip

Note that, much like [dependencies in _path operation decorators_](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/), no value will be passed to your _path operation function_.

The end result is that the item paths are now:

- `/items/`
- `/items/{item_id}`

...as we intended.

- They will be marked with a list of tags that contain a single string `"items"`.
    - These "tags" are especially useful for the automatic interactive documentation systems (using OpenAPI).
- All of them will include the predefined `responses`.
- All these _path operations_ will have the list of `dependencies` evaluated/executed before them.
    - If you also declare dependencies in a specific _path operation_, **they will be executed too**.
    - The router dependencies are executed first, then the [`dependencies` in the decorator](https://fastapi.tiangolo.com/tutorial/dependencies/dependencies-in-path-operation-decorators/), and then the normal parameter dependencies.
    - You can also add [`Security` dependencies with `scopes`](https://fastapi.tiangolo.com/advanced/security/oauth2-scopes/).

Tip

Having `dependencies` in the `APIRouter` can be used, for example, to require authentication for a whole group of _path operations_. Even if the dependencies are not added individually to each one of them.

Check

The `prefix`, `tags`, `responses`, and `dependencies` parameters are (as in many other cases) just a feature from **FastAPI** to help you avoid code duplication.

### Import the dependencies[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#import-the-dependencies "Permanent link")

This code lives in the module `app.routers.items`, the file `app/routers/items.py`.

And we need to get the dependency function from the module `app.dependencies`, the file `app/dependencies.py`.

So we use a relative import with `..` for the dependencies:

app/routers/items.py

`from fastapi import APIRouter, Depends, HTTPException from ..dependencies import get_token_header router = APIRouter(     prefix="/items",    tags=["items"],    dependencies=[Depends(get_token_header)],    responses={404: {"description": "Not found"}}, ) fake_items_db = {"plumbus": {"name": "Plumbus"}, "gun": {"name": "Portal Gun"}} @router.get("/") async def read_items():     return fake_items_db @router.get("/{item_id}") async def read_item(item_id: str):     if item_id not in fake_items_db:        raise HTTPException(status_code=404, detail="Item not found")    return {"name": fake_items_db[item_id]["name"], "item_id": item_id} @router.put(     "/{item_id}",    tags=["custom"],    responses={403: {"description": "Operation forbidden"}}, ) async def update_item(item_id: str):     if item_id != "plumbus":        raise HTTPException(            status_code=403, detail="You can only update the item: plumbus"        )    return {"item_id": item_id, "name": "The great Plumbus"}`

#### How relative imports work[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#how-relative-imports-work "Permanent link")

Tip

If you know perfectly how imports work, continue to the next section below.

A single dot `.`, like in:

`from .dependencies import get_token_header`

would mean:

- Starting in the same package that this module (the file `app/routers/items.py`) lives in (the directory `app/routers/`)...
- find the module `dependencies` (an imaginary file at `app/routers/dependencies.py`)...
- and from it, import the function `get_token_header`.

But that file doesn't exist, our dependencies are in a file at `app/dependencies.py`.

Remember how our app/file structure looks like:

![](https://fastapi.tiangolo.com/img/tutorial/bigger-applications/package.drawio.svg)

---

The two dots `..`, like in:

`from ..dependencies import get_token_header`

mean:

- Starting in the same package that this module (the file `app/routers/items.py`) lives in (the directory `app/routers/`)...
- go to the parent package (the directory `app/`)...
- and in there, find the module `dependencies` (the file at `app/dependencies.py`)...
- and from it, import the function `get_token_header`.

That works correctly! 🎉

---

The same way, if we had used three dots `...`, like in:

`from ...dependencies import get_token_header`

that would mean:

- Starting in the same package that this module (the file `app/routers/items.py`) lives in (the directory `app/routers/`)...
- go to the parent package (the directory `app/`)...
- then go to the parent of that package (there's no parent package, `app` is the top level 😱)...
- and in there, find the module `dependencies` (the file at `app/dependencies.py`)...
- and from it, import the function `get_token_header`.

That would refer to some package above `app/`, with its own file `__init__.py`, etc. But we don't have that. So, that would throw an error in our example. 🚨

But now you know how it works, so you can use relative imports in your own apps no matter how complex they are. 🤓

### Add some custom `tags`, `responses`, and `dependencies`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#add-some-custom-tags-responses-and-dependencies "Permanent link")

We are not adding the prefix `/items` nor the `tags=["items"]` to each _path operation_ because we added them to the `APIRouter`.

But we can still add _more_ `tags` that will be applied to a specific _path operation_, and also some extra `responses` specific to that _path operation_:

app/routers/items.py

`from fastapi import APIRouter, Depends, HTTPException from ..dependencies import get_token_header router = APIRouter(     prefix="/items",    tags=["items"],    dependencies=[Depends(get_token_header)],    responses={404: {"description": "Not found"}}, ) fake_items_db = {"plumbus": {"name": "Plumbus"}, "gun": {"name": "Portal Gun"}} @router.get("/") async def read_items():     return fake_items_db @router.get("/{item_id}") async def read_item(item_id: str):     if item_id not in fake_items_db:        raise HTTPException(status_code=404, detail="Item not found")    return {"name": fake_items_db[item_id]["name"], "item_id": item_id} @router.put(     "/{item_id}",    tags=["custom"],    responses={403: {"description": "Operation forbidden"}}, ) async def update_item(item_id: str):     if item_id != "plumbus":        raise HTTPException(            status_code=403, detail="You can only update the item: plumbus"        )    return {"item_id": item_id, "name": "The great Plumbus"}`

Tip

This last path operation will have the combination of tags: `["items", "custom"]`.

And it will also have both responses in the documentation, one for `404` and one for `403`.

## The main `FastAPI`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#the-main-fastapi "Permanent link")

Now, let's see the module at `app/main.py`.

Here's where you import and use the class `FastAPI`.

This will be the main file in your application that ties everything together.

And as most of your logic will now live in its own specific module, the main file will be quite simple.

### Import `FastAPI`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#import-fastapi "Permanent link")

You import and create a `FastAPI` class as normally.

And we can even declare [global dependencies](https://fastapi.tiangolo.com/tutorial/dependencies/global-dependencies/) that will be combined with the dependencies for each `APIRouter`:

app/main.py

`from fastapi import Depends, FastAPI from .dependencies import get_query_token, get_token_header from .internal import admin from .routers import items, users app = FastAPI(dependencies=[Depends(get_query_token)]) app.include_router(users.router) app.include_router(items.router) app.include_router(     admin.router,    prefix="/admin",    tags=["admin"],    dependencies=[Depends(get_token_header)],    responses={418: {"description": "I'm a teapot"}}, ) @app.get("/") async def root():     return {"message": "Hello Bigger Applications!"}`

### Import the `APIRouter`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#import-the-apirouter "Permanent link")

Now we import the other submodules that have `APIRouter`s:

app/main.py

`from fastapi import Depends, FastAPI from .dependencies import get_query_token, get_token_header from .internal import admin from .routers import items, users app = FastAPI(dependencies=[Depends(get_query_token)]) app.include_router(users.router) app.include_router(items.router) app.include_router(     admin.router,    prefix="/admin",    tags=["admin"],    dependencies=[Depends(get_token_header)],    responses={418: {"description": "I'm a teapot"}}, ) @app.get("/") async def root():     return {"message": "Hello Bigger Applications!"}`

As the files `app/routers/users.py` and `app/routers/items.py` are submodules that are part of the same Python package `app`, we can use a single dot `.` to import them using "relative imports".

### How the importing works[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#how-the-importing-works "Permanent link")

The section:

`from .routers import items, users`

means:

- Starting in the same package that this module (the file `app/main.py`) lives in (the directory `app/`)...
- look for the subpackage `routers` (the directory at `app/routers/`)...
- and from it, import the submodule `items` (the file at `app/routers/items.py`) and `users` (the file at `app/routers/users.py`)...

The module `items` will have a variable `router` (`items.router`). This is the same one we created in the file `app/routers/items.py`, it's an `APIRouter` object.

And then we do the same for the module `users`.

We could also import them like:

`from app.routers import items, users`

Info

The first version is a "relative import":

`from .routers import items, users`

The second version is an "absolute import":

`from app.routers import items, users`

To learn more about Python Packages and Modules, read [the official Python documentation about Modules](https://docs.python.org/3/tutorial/modules.html).

### Avoid name collisions[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#avoid-name-collisions "Permanent link")

We are importing the submodule `items` directly, instead of importing just its variable `router`.

This is because we also have another variable named `router` in the submodule `users`.

If we had imported one after the other, like:

`from .routers.items import router from .routers.users import router`

the `router` from `users` would overwrite the one from `items` and we wouldn't be able to use them at the same time.

So, to be able to use both of them in the same file, we import the submodules directly:

app/main.py

`from fastapi import Depends, FastAPI from .dependencies import get_query_token, get_token_header from .internal import admin from .routers import items, users app = FastAPI(dependencies=[Depends(get_query_token)]) app.include_router(users.router) app.include_router(items.router) app.include_router(     admin.router,    prefix="/admin",    tags=["admin"],    dependencies=[Depends(get_token_header)],    responses={418: {"description": "I'm a teapot"}}, ) @app.get("/") async def root():     return {"message": "Hello Bigger Applications!"}`

### Include the `APIRouter`s for `users` and `items`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#include-the-apirouters-for-users-and-items "Permanent link")

Now, let's include the `router`s from the submodules `users` and `items`:

app/main.py

`from fastapi import Depends, FastAPI from .dependencies import get_query_token, get_token_header from .internal import admin from .routers import items, users app = FastAPI(dependencies=[Depends(get_query_token)]) app.include_router(users.router) app.include_router(items.router) app.include_router(     admin.router,    prefix="/admin",    tags=["admin"],    dependencies=[Depends(get_token_header)],    responses={418: {"description": "I'm a teapot"}}, ) @app.get("/") async def root():     return {"message": "Hello Bigger Applications!"}`

Info

`users.router` contains the `APIRouter` inside of the file `app/routers/users.py`.

And `items.router` contains the `APIRouter` inside of the file `app/routers/items.py`.

With `app.include_router()` we can add each `APIRouter` to the main `FastAPI` application.

It will include all the routes from that router as part of it.

Technical Details

It will actually internally create a _path operation_ for each _path operation_ that was declared in the `APIRouter`.

So, behind the scenes, it will actually work as if everything was the same single app.

Check

You don't have to worry about performance when including routers.

This will take microseconds and will only happen at startup.

So it won't affect performance. ⚡

### Include an `APIRouter` with a custom `prefix`, `tags`, `responses`, and `dependencies`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#include-an-apirouter-with-a-custom-prefix-tags-responses-and-dependencies "Permanent link")

Now, let's imagine your organization gave you the `app/internal/admin.py` file.

It contains an `APIRouter` with some admin _path operations_ that your organization shares between several projects.

For this example it will be super simple. But let's say that because it is shared with other projects in the organization, we cannot modify it and add a `prefix`, `dependencies`, `tags`, etc. directly to the `APIRouter`:

app/internal/admin.py

`from fastapi import APIRouter router = APIRouter() @router.post("/") async def update_admin():     return {"message": "Admin getting schwifty"}`

But we still want to set a custom `prefix` when including the `APIRouter` so that all its _path operations_ start with `/admin`, we want to secure it with the `dependencies` we already have for this project, and we want to include `tags` and `responses`.

We can declare all that without having to modify the original `APIRouter` by passing those parameters to `app.include_router()`:

app/main.py

`from fastapi import Depends, FastAPI from .dependencies import get_query_token, get_token_header from .internal import admin from .routers import items, users app = FastAPI(dependencies=[Depends(get_query_token)]) app.include_router(users.router) app.include_router(items.router) app.include_router(     admin.router,    prefix="/admin",    tags=["admin"],    dependencies=[Depends(get_token_header)],    responses={418: {"description": "I'm a teapot"}}, ) @app.get("/") async def root():     return {"message": "Hello Bigger Applications!"}`

That way, the original `APIRouter` will stay unmodified, so we can still share that same `app/internal/admin.py` file with other projects in the organization.

The result is that in our app, each of the _path operations_ from the `admin` module will have:

- The prefix `/admin`.
- The tag `admin`.
- The dependency `get_token_header`.
- The response `418`. 🍵

But that will only affect that `APIRouter` in our app, not in any other code that uses it.

So, for example, other projects could use the same `APIRouter` with a different authentication method.

### Include a _path operation_[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#include-a-path-operation "Permanent link")

We can also add _path operations_ directly to the `FastAPI` app.

Here we do it... just to show that we can 🤷:

app/main.py

`from fastapi import Depends, FastAPI from .dependencies import get_query_token, get_token_header from .internal import admin from .routers import items, users app = FastAPI(dependencies=[Depends(get_query_token)]) app.include_router(users.router) app.include_router(items.router) app.include_router(     admin.router,    prefix="/admin",    tags=["admin"],    dependencies=[Depends(get_token_header)],    responses={418: {"description": "I'm a teapot"}}, ) @app.get("/") async def root():     return {"message": "Hello Bigger Applications!"}`

and it will work correctly, together with all the other _path operations_ added with `app.include_router()`.

Very Technical Details

**Note**: this is a very technical detail that you probably can **just skip**.

---

The `APIRouter`s are not "mounted", they are not isolated from the rest of the application.

This is because we want to include their _path operations_ in the OpenAPI schema and the user interfaces.

As we cannot just isolate them and "mount" them independently of the rest, the _path operations_ are "cloned" (re-created), not included directly.

## Check the automatic API docs[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#check-the-automatic-api-docs "Permanent link")

Now, run your app:

[fast →](https://fastapi.tiangolo.com/tutorial/bigger-applications/#)fastapi dev app/main

And open the docs at [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).

You will see the automatic API docs, including the paths from all the submodules, using the correct paths (and prefixes) and the correct tags:

![](https://fastapi.tiangolo.com/img/tutorial/bigger-applications/image01.png)

## Include the same router multiple times with different `prefix`[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#include-the-same-router-multiple-times-with-different-prefix "Permanent link")

You can also use `.include_router()` multiple times with the _same_ router using different prefixes.

This could be useful, for example, to expose the same API under different prefixes, e.g. `/api/v1` and `/api/latest`.

This is an advanced usage that you might not really need, but it's there in case you do.

## Include an `APIRouter` in another[¶](https://fastapi.tiangolo.com/tutorial/bigger-applications/#include-an-apirouter-in-another "Permanent link")

The same way you can include an `APIRouter` in a `FastAPI` application, you can include an `APIRouter` in another `APIRouter` using:

`router.include_router(other_router)`

Make sure you do it before including `router` in the `FastAPI` app, so that the _path operations_ from `other_router` are also included.


# Background Tasks[¶](https://fastapi.tiangolo.com/tutorial/background-tasks/#background-tasks "Permanent link")

You can define background tasks to be run _after_ returning a response.

This is useful for operations that need to happen after a request, but that the client doesn't really have to be waiting for the operation to complete before receiving the response.

This includes, for example:

- Email notifications sent after performing an action:
    - As connecting to an email server and sending an email tends to be "slow" (several seconds), you can return the response right away and send the email notification in the background.
- Processing data:
    - For example, let's say you receive a file that must go through a slow process, you can return a response of "Accepted" (HTTP 202) and process the file in the background.

## Using `BackgroundTasks`[¶](https://fastapi.tiangolo.com/tutorial/background-tasks/#using-backgroundtasks "Permanent link")

First, import `BackgroundTasks` and define a parameter in your _path operation function_ with a type declaration of `BackgroundTasks`:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/background-tasks/#__tabbed_1_1)

`from fastapi import BackgroundTasks, FastAPI app = FastAPI() def write_notification(email: str, message=""):     with open("log.txt", mode="w") as email_file:        content = f"notification for {email}: {message}"        email_file.write(content) @app.post("/send-notification/{email}") async def send_notification(email: str, background_tasks: BackgroundTasks):     background_tasks.add_task(write_notification, email, message="some notification")    return {"message": "Notification sent in the background"}`

**FastAPI** will create the object of type `BackgroundTasks` for you and pass it as that parameter.

## Create a task function[¶](https://fastapi.tiangolo.com/tutorial/background-tasks/#create-a-task-function "Permanent link")

Create a function to be run as the background task.

It is just a standard function that can receive parameters.

It can be an `async def` or normal `def` function, **FastAPI** will know how to handle it correctly.

In this case, the task function will write to a file (simulating sending an email).

And as the write operation doesn't use `async` and `await`, we define the function with normal `def`:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/background-tasks/#__tabbed_2_1)

`from fastapi import BackgroundTasks, FastAPI app = FastAPI() def write_notification(email: str, message=""):     with open("log.txt", mode="w") as email_file:        content = f"notification for {email}: {message}"        email_file.write(content) @app.post("/send-notification/{email}") async def send_notification(email: str, background_tasks: BackgroundTasks):     background_tasks.add_task(write_notification, email, message="some notification")    return {"message": "Notification sent in the background"}`

## Add the background task[¶](https://fastapi.tiangolo.com/tutorial/background-tasks/#add-the-background-task "Permanent link")

Inside of your _path operation function_, pass your task function to the _background tasks_ object with the method `.add_task()`:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/background-tasks/#__tabbed_3_1)

`from fastapi import BackgroundTasks, FastAPI app = FastAPI() def write_notification(email: str, message=""):     with open("log.txt", mode="w") as email_file:        content = f"notification for {email}: {message}"        email_file.write(content) @app.post("/send-notification/{email}") async def send_notification(email: str, background_tasks: BackgroundTasks):     background_tasks.add_task(write_notification, email, message="some notification")    return {"message": "Notification sent in the background"}`

`.add_task()` receives as arguments:

- A task function to be run in the background (`write_notification`).
- Any sequence of arguments that should be passed to the task function in order (`email`).
- Any keyword arguments that should be passed to the task function (`message="some notification"`).

## Dependency Injection[¶](https://fastapi.tiangolo.com/tutorial/background-tasks/#dependency-injection "Permanent link")

Using `BackgroundTasks` also works with the dependency injection system, you can declare a parameter of type `BackgroundTasks` at multiple levels: in a _path operation function_, in a dependency (dependable), in a sub-dependency, etc.

**FastAPI** knows what to do in each case and how to reuse the same object, so that all the background tasks are merged together and are run in the background afterwards:

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/background-tasks/#__tabbed_4_1)

`from typing import Annotated from fastapi import BackgroundTasks, Depends, FastAPI app = FastAPI() def write_log(message: str):     with open("log.txt", mode="a") as log:        log.write(message) def get_query(background_tasks: BackgroundTasks, q: str | None = None):     if q:        message = f"found query: {q}\n"        background_tasks.add_task(write_log, message)    return q @app.post("/send-notification/{email}") async def send_notification(     email: str, background_tasks: BackgroundTasks, q: Annotated[str, Depends(get_query)] ):     message = f"message to {email}\n"    background_tasks.add_task(write_log, message)    return {"message": "Message sent"}`

🤓 Other versions and variants

[](https://fastapi.tiangolo.com/tutorial/background-tasks/#__tabbed_5_1)[](https://fastapi.tiangolo.com/tutorial/background-tasks/#__tabbed_5_2)[](https://fastapi.tiangolo.com/tutorial/background-tasks/#__tabbed_5_3)[](https://fastapi.tiangolo.com/tutorial/background-tasks/#__tabbed_5_4)

In this example, the messages will be written to the `log.txt` file _after_ the response is sent.

If there was a query in the request, it will be written to the log in a background task.

And then another background task generated at the _path operation function_ will write a message using the `email` path parameter.

## Technical Details[¶](https://fastapi.tiangolo.com/tutorial/background-tasks/#technical-details "Permanent link")

The class `BackgroundTasks` comes directly from [`starlette.background`](https://www.starlette.io/background/).

It is imported/included directly into FastAPI so that you can import it from `fastapi` and avoid accidentally importing the alternative `BackgroundTask` (without the `s` at the end) from `starlette.background`.

By only using `BackgroundTasks` (and not `BackgroundTask`), it's then possible to use it as a _path operation function_ parameter and have **FastAPI** handle the rest for you, just like when using the `Request` object directly.

It's still possible to use `BackgroundTask` alone in FastAPI, but you have to create the object in your code and return a Starlette `Response` including it.

You can see more details in [Starlette's official docs for Background Tasks](https://www.starlette.io/background/).

## Caveat[¶](https://fastapi.tiangolo.com/tutorial/background-tasks/#caveat "Permanent link")

If you need to perform heavy background computation and you don't necessarily need it to be run by the same process (for example, you don't need to share memory, variables, etc), you might benefit from using other bigger tools like [Celery](https://docs.celeryq.dev/).

They tend to require more complex configurations, a message/job queue manager, like RabbitMQ or Redis, but they allow you to run background tasks in multiple processes, and especially, in multiple servers.

But if you need to access variables and objects from the same **FastAPI** app, or you need to perform small background tasks (like sending an email notification), you can simply just use `BackgroundTasks`.

## Recap[¶](https://fastapi.tiangolo.com/tutorial/background-tasks/#recap "Permanent link")

Import and use `BackgroundTasks` with parameters in _path operation functions_ and dependencies to add background tasks.

# Metadata and Docs URLs[¶](https://fastapi.tiangolo.com/tutorial/metadata/#metadata-and-docs-urls "Permanent link")

You can customize several metadata configurations in your **FastAPI** application.

## Metadata for API[¶](https://fastapi.tiangolo.com/tutorial/metadata/#metadata-for-api "Permanent link")

You can set the following fields that are used in the OpenAPI specification and the automatic API docs UIs:

|Parameter|Type|Description|
|---|---|---|
|`title`|`str`|The title of the API.|
|`summary`|`str`|A short summary of the API. Available since OpenAPI 3.1.0, FastAPI 0.99.0.|
|`description`|`str`|A short description of the API. It can use Markdown.|
|`version`|`string`|The version of the API. This is the version of your own application, not of OpenAPI. For example `2.5.0`.|
|`terms_of_service`|`str`|A URL to the Terms of Service for the API. If provided, this has to be a URL.|
|`contact`|`dict`|The contact information for the exposed API. It can contain several fields.`contact` fields<br><br>\|<br>\|---\|---\|---\|<br>\|<br>\|<br>\||
|`license_info`|`dict`|The license information for the exposed API. It can contain several fields.`license_info` fields<br><br>\|<br>\|---\|---\|---\|<br>\|<br>\|[](https://spdx.org/licenses/)\|<br>\||

You can set them as follows:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/metadata/#__tabbed_1_1)

`from fastapi import FastAPI description = """ ChimichangApp API helps you do awesome stuff. 🚀 ## Items You can **read items**. ## Users You will be able to: * **Create users** (_not implemented_). * **Read users** (_not implemented_). """ app = FastAPI(     title="ChimichangApp",    description=description,    summary="Deadpool's favorite app. Nuff said.",    version="0.0.1",    terms_of_service="http://example.com/terms/",    contact={        "name": "Deadpoolio the Amazing",        "url": "http://x-force.example.com/contact/",        "email": "dp@x-force.example.com",    },    license_info={        "name": "Apache 2.0",        "url": "https://www.apache.org/licenses/LICENSE-2.0.html",    }, ) @app.get("/items/") async def read_items():     return [{"name": "Katana"}]`

Tip

You can write Markdown in the `description` field and it will be rendered in the output.

With this configuration, the automatic API docs would look like:

![](https://fastapi.tiangolo.com/img/tutorial/metadata/image01.png)

## License identifier[¶](https://fastapi.tiangolo.com/tutorial/metadata/#license-identifier "Permanent link")

Since OpenAPI 3.1.0 and FastAPI 0.99.0, you can also set the `license_info` with an `identifier` instead of a `url`.

For example:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/metadata/#__tabbed_2_1)

`from fastapi import FastAPI description = """ ChimichangApp API helps you do awesome stuff. 🚀 ## Items You can **read items**. ## Users You will be able to: * **Create users** (_not implemented_). * **Read users** (_not implemented_). """ app = FastAPI(     title="ChimichangApp",    description=description,    summary="Deadpool's favorite app. Nuff said.",    version="0.0.1",    terms_of_service="http://example.com/terms/",    contact={        "name": "Deadpoolio the Amazing",        "url": "http://x-force.example.com/contact/",        "email": "dp@x-force.example.com",    },    license_info={        "name": "Apache 2.0",        "identifier": "MIT",    }, ) @app.get("/items/") async def read_items():     return [{"name": "Katana"}]`

## Metadata for tags[¶](https://fastapi.tiangolo.com/tutorial/metadata/#metadata-for-tags "Permanent link")

You can also add additional metadata for the different tags used to group your path operations with the parameter `openapi_tags`.

It takes a list containing one dictionary for each tag.

Each dictionary can contain:

- `name` (**required**): a `str` with the same tag name you use in the `tags` parameter in your _path operations_ and `APIRouter`s.
- `description`: a `str` with a short description for the tag. It can have Markdown and will be shown in the docs UI.
- `externalDocs`: a `dict` describing external documentation with:
    - `description`: a `str` with a short description for the external docs.
    - `url` (**required**): a `str` with the URL for the external documentation.

### Create metadata for tags[¶](https://fastapi.tiangolo.com/tutorial/metadata/#create-metadata-for-tags "Permanent link")

Let's try that in an example with tags for `users` and `items`.

Create metadata for your tags and pass it to the `openapi_tags` parameter:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/metadata/#__tabbed_3_1)

`from fastapi import FastAPI tags_metadata = [     {        "name": "users",        "description": "Operations with users. The **login** logic is also here.",    },    {        "name": "items",        "description": "Manage items. So _fancy_ they have their own docs.",        "externalDocs": {            "description": "Items external docs",            "url": "https://fastapi.tiangolo.com/",        },    }, ] app = FastAPI(openapi_tags=tags_metadata) @app.get("/users/", tags=["users"]) async def get_users():     return [{"name": "Harry"}, {"name": "Ron"}] @app.get("/items/", tags=["items"]) async def get_items():     return [{"name": "wand"}, {"name": "flying broom"}]`

Notice that you can use Markdown inside of the descriptions, for example "login" will be shown in bold (**login**) and "fancy" will be shown in italics (_fancy_).

Tip

You don't have to add metadata for all the tags that you use.

### Use your tags[¶](https://fastapi.tiangolo.com/tutorial/metadata/#use-your-tags "Permanent link")

Use the `tags` parameter with your _path operations_ (and `APIRouter`s) to assign them to different tags:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/metadata/#__tabbed_4_1)

`from fastapi import FastAPI tags_metadata = [     {        "name": "users",        "description": "Operations with users. The **login** logic is also here.",    },    {        "name": "items",        "description": "Manage items. So _fancy_ they have their own docs.",        "externalDocs": {            "description": "Items external docs",            "url": "https://fastapi.tiangolo.com/",        },    }, ] app = FastAPI(openapi_tags=tags_metadata) @app.get("/users/", tags=["users"]) async def get_users():     return [{"name": "Harry"}, {"name": "Ron"}] @app.get("/items/", tags=["items"]) async def get_items():     return [{"name": "wand"}, {"name": "flying broom"}]`

Info

Read more about tags in [Path Operation Configuration](https://fastapi.tiangolo.com/tutorial/path-operation-configuration/#tags).

### Check the docs[¶](https://fastapi.tiangolo.com/tutorial/metadata/#check-the-docs "Permanent link")

Now, if you check the docs, they will show all the additional metadata:

![](https://fastapi.tiangolo.com/img/tutorial/metadata/image02.png)

### Order of tags[¶](https://fastapi.tiangolo.com/tutorial/metadata/#order-of-tags "Permanent link")

The order of each tag metadata dictionary also defines the order shown in the docs UI.

For example, even though `users` would go after `items` in alphabetical order, it is shown before them, because we added their metadata as the first dictionary in the list.

## OpenAPI URL[¶](https://fastapi.tiangolo.com/tutorial/metadata/#openapi-url "Permanent link")

By default, the OpenAPI schema is served at `/openapi.json`.

But you can configure it with the parameter `openapi_url`.

For example, to set it to be served at `/api/v1/openapi.json`:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/metadata/#__tabbed_5_1)

`from fastapi import FastAPI app = FastAPI(openapi_url="/api/v1/openapi.json") @app.get("/items/") async def read_items():     return [{"name": "Foo"}]`

If you want to disable the OpenAPI schema completely you can set `openapi_url=None`, that will also disable the documentation user interfaces that use it.

## Docs URLs[¶](https://fastapi.tiangolo.com/tutorial/metadata/#docs-urls "Permanent link")

You can configure the two documentation user interfaces included:

- **Swagger UI**: served at `/docs`.
    - You can set its URL with the parameter `docs_url`.
    - You can disable it by setting `docs_url=None`.
- **ReDoc**: served at `/redoc`.
    - You can set its URL with the parameter `redoc_url`.
    - You can disable it by setting `redoc_url=None`.

For example, to set Swagger UI to be served at `/documentation` and disable ReDoc:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/metadata/#__tabbed_6_1)

`from fastapi import FastAPI app = FastAPI(docs_url="/documentation", redoc_url=None) @app.get("/items/") async def read_items():     return [{"name": "Foo"}]`

# Static Files[¶](https://fastapi.tiangolo.com/tutorial/static-files/#static-files "Permanent link")

You can serve static files automatically from a directory using `StaticFiles`.

## Use `StaticFiles`[¶](https://fastapi.tiangolo.com/tutorial/static-files/#use-staticfiles "Permanent link")

- Import `StaticFiles`.
- "Mount" a `StaticFiles()` instance in a specific path.

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/static-files/#__tabbed_1_1)

`from fastapi import FastAPI from fastapi.staticfiles import StaticFiles app = FastAPI() app.mount("/static", StaticFiles(directory="static"), name="static")`

Technical Details

You could also use `from starlette.staticfiles import StaticFiles`.

**FastAPI** provides the same `starlette.staticfiles` as `fastapi.staticfiles` just as a convenience for you, the developer. But it actually comes directly from Starlette.

### What is "Mounting"[¶](https://fastapi.tiangolo.com/tutorial/static-files/#what-is-mounting "Permanent link")

"Mounting" means adding a complete "independent" application in a specific path, that then takes care of handling all the sub-paths.

This is different from using an `APIRouter` as a mounted application is completely independent. The OpenAPI and docs from your main application won't include anything from the mounted application, etc.

You can read more about this in the [Advanced User Guide](https://fastapi.tiangolo.com/advanced/).

## Details[¶](https://fastapi.tiangolo.com/tutorial/static-files/#details "Permanent link")

The first `"/static"` refers to the sub-path this "sub-application" will be "mounted" on. So, any path that starts with `"/static"` will be handled by it.

The `directory="static"` refers to the name of the directory that contains your static files.

The `name="static"` gives it a name that can be used internally by **FastAPI**.

All these parameters can be different than "`static`", adjust them with the needs and specific details of your own application.

## More info[¶](https://fastapi.tiangolo.com/tutorial/static-files/#more-info "Permanent link")

For more details and options check [Starlette's docs about Static Files](https://www.starlette.io/staticfiles/).

# Testing[¶](https://fastapi.tiangolo.com/tutorial/testing/#testing "Permanent link")

Thanks to [Starlette](https://www.starlette.io/testclient/), testing **FastAPI** applications is easy and enjoyable.

It is based on [HTTPX](https://www.python-httpx.org/), which in turn is designed based on Requests, so it's very familiar and intuitive.

With it, you can use [pytest](https://docs.pytest.org/) directly with **FastAPI**.

## Using `TestClient`[¶](https://fastapi.tiangolo.com/tutorial/testing/#using-testclient "Permanent link")

Info

To use `TestClient`, first install [`httpx`](https://www.python-httpx.org/).

Make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install it, for example:

`$ pip install httpx`

Import `TestClient`.

Create a `TestClient` by passing your **FastAPI** application to it.

Create functions with a name that starts with `test_` (this is standard `pytest` conventions).

Use the `TestClient` object the same way as you do with `httpx`.

Write simple `assert` statements with the standard Python expressions that you need to check (again, standard `pytest`).

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/testing/#__tabbed_1_1)

`from fastapi import FastAPI from fastapi.testclient import TestClient app = FastAPI() @app.get("/") async def read_main():     return {"msg": "Hello World"} client = TestClient(app) def test_read_main():     response = client.get("/")    assert response.status_code == 200    assert response.json() == {"msg": "Hello World"}`

Tip

Notice that the testing functions are normal `def`, not `async def`.

And the calls to the client are also normal calls, not using `await`.

This allows you to use `pytest` directly without complications.

Technical Details

You could also use `from starlette.testclient import TestClient`.

**FastAPI** provides the same `starlette.testclient` as `fastapi.testclient` just as a convenience for you, the developer. But it comes directly from Starlette.

Tip

If you want to call `async` functions in your tests apart from sending requests to your FastAPI application (e.g. asynchronous database functions), have a look at the [Async Tests](https://fastapi.tiangolo.com/advanced/async-tests/) in the advanced tutorial.

## Separating tests[¶](https://fastapi.tiangolo.com/tutorial/testing/#separating-tests "Permanent link")

In a real application, you probably would have your tests in a different file.

And your **FastAPI** application might also be composed of several files/modules, etc.

### **FastAPI** app file[¶](https://fastapi.tiangolo.com/tutorial/testing/#fastapi-app-file "Permanent link")

Let's say you have a file structure as described in [Bigger Applications](https://fastapi.tiangolo.com/tutorial/bigger-applications/):

`. ├── app │   ├── __init__.py │   └── main.py`

In the file `main.py` you have your **FastAPI** app:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/testing/#__tabbed_2_1)

`from fastapi import FastAPI app = FastAPI() @app.get("/") async def read_main():     return {"msg": "Hello World"}`

### Testing file[¶](https://fastapi.tiangolo.com/tutorial/testing/#testing-file "Permanent link")

Then you could have a file `test_main.py` with your tests. It could live on the same Python package (the same directory with a `__init__.py` file):

`. ├── app │   ├── __init__.py │   ├── main.py │   └── test_main.py`

Because this file is in the same package, you can use relative imports to import the object `app` from the `main` module (`main.py`):

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/testing/#__tabbed_3_1)

`from fastapi.testclient import TestClient from .main import app client = TestClient(app) def test_read_main():     response = client.get("/")    assert response.status_code == 200    assert response.json() == {"msg": "Hello World"}`

...and have the code for the tests just like before.

## Testing: extended example[¶](https://fastapi.tiangolo.com/tutorial/testing/#testing-extended-example "Permanent link")

Now let's extend this example and add more details to see how to test different parts.

### Extended **FastAPI** app file[¶](https://fastapi.tiangolo.com/tutorial/testing/#extended-fastapi-app-file "Permanent link")

Let's continue with the same file structure as before:

`. ├── app │   ├── __init__.py │   ├── main.py │   └── test_main.py`

Let's say that now the file `main.py` with your **FastAPI** app has some other **path operations**.

It has a `GET` operation that could return an error.

It has a `POST` operation that could return several errors.

Both _path operations_ require an `X-Token` header.

[Python 3.10+](https://fastapi.tiangolo.com/tutorial/testing/#__tabbed_4_1)[Python 3.9+](https://fastapi.tiangolo.com/tutorial/testing/#__tabbed_4_2)[Python 3.8+](https://fastapi.tiangolo.com/tutorial/testing/#__tabbed_4_3)[Python 3.10+ non-Annotated](https://fastapi.tiangolo.com/tutorial/testing/#__tabbed_4_4)[Python 3.8+ non-Annotated](https://fastapi.tiangolo.com/tutorial/testing/#__tabbed_4_5)

`from typing import Annotated from fastapi import FastAPI, Header, HTTPException from pydantic import BaseModel fake_secret_token = "coneofsilence" fake_db = {     "foo": {"id": "foo", "title": "Foo", "description": "There goes my hero"},    "bar": {"id": "bar", "title": "Bar", "description": "The bartenders"}, } app = FastAPI() class Item(BaseModel):     id: str    title: str    description: str | None = None @app.get("/items/{item_id}", response_model=Item) async def read_main(item_id: str, x_token: Annotated[str, Header()]):     if x_token != fake_secret_token:        raise HTTPException(status_code=400, detail="Invalid X-Token header")    if item_id not in fake_db:        raise HTTPException(status_code=404, detail="Item not found")    return fake_db[item_id] @app.post("/items/", response_model=Item) async def create_item(item: Item, x_token: Annotated[str, Header()]):     if x_token != fake_secret_token:        raise HTTPException(status_code=400, detail="Invalid X-Token header")    if item.id in fake_db:        raise HTTPException(status_code=409, detail="Item already exists")    fake_db[item.id] = item    return item`

### Extended testing file[¶](https://fastapi.tiangolo.com/tutorial/testing/#extended-testing-file "Permanent link")

You could then update `test_main.py` with the extended tests:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/testing/#__tabbed_5_1)

`from fastapi.testclient import TestClient from .main import app client = TestClient(app) def test_read_item():     response = client.get("/items/foo", headers={"X-Token": "coneofsilence"})    assert response.status_code == 200    assert response.json() == {        "id": "foo",        "title": "Foo",        "description": "There goes my hero",    } def test_read_item_bad_token():     response = client.get("/items/foo", headers={"X-Token": "hailhydra"})    assert response.status_code == 400    assert response.json() == {"detail": "Invalid X-Token header"} def test_read_nonexistent_item():     response = client.get("/items/baz", headers={"X-Token": "coneofsilence"})    assert response.status_code == 404    assert response.json() == {"detail": "Item not found"} def test_create_item():     response = client.post(        "/items/",        headers={"X-Token": "coneofsilence"},        json={"id": "foobar", "title": "Foo Bar", "description": "The Foo Barters"},    )    assert response.status_code == 200    assert response.json() == {        "id": "foobar",        "title": "Foo Bar",        "description": "The Foo Barters",    } def test_create_item_bad_token():     response = client.post(        "/items/",        headers={"X-Token": "hailhydra"},        json={"id": "bazz", "title": "Bazz", "description": "Drop the bazz"},    )    assert response.status_code == 400    assert response.json() == {"detail": "Invalid X-Token header"} def test_create_existing_item():     response = client.post(        "/items/",        headers={"X-Token": "coneofsilence"},        json={            "id": "foo",            "title": "The Foo ID Stealers",            "description": "There goes my stealer",        },    )    assert response.status_code == 409    assert response.json() == {"detail": "Item already exists"}`

Whenever you need the client to pass information in the request and you don't know how to, you can search (Google) how to do it in `httpx`, or even how to do it with `requests`, as HTTPX's design is based on Requests' design.

Then you just do the same in your tests.

E.g.:

- To pass a _path_ or _query_ parameter, add it to the URL itself.
- To pass a JSON body, pass a Python object (e.g. a `dict`) to the parameter `json`.
- If you need to send _Form Data_ instead of JSON, use the `data` parameter instead.
- To pass _headers_, use a `dict` in the `headers` parameter.
- For _cookies_, a `dict` in the `cookies` parameter.

For more information about how to pass data to the backend (using `httpx` or the `TestClient`) check the [HTTPX documentation](https://www.python-httpx.org/).

Info

Note that the `TestClient` receives data that can be converted to JSON, not Pydantic models.

If you have a Pydantic model in your test and you want to send its data to the application during testing, you can use the `jsonable_encoder` described in [JSON Compatible Encoder](https://fastapi.tiangolo.com/tutorial/encoder/).

## Run it[¶](https://fastapi.tiangolo.com/tutorial/testing/#run-it "Permanent link")

After that, you just need to install `pytest`.

Make sure you create a [virtual environment](https://fastapi.tiangolo.com/virtual-environments/), activate it, and then install it, for example:

[fast →](https://fastapi.tiangolo.com/tutorial/testing/#)pip install p

It will detect the files and tests automatically, execute them, and report the results back to you.

Run the tests with:


# Debugging[¶](https://fastapi.tiangolo.com/tutorial/debugging/#debugging "Permanent link")

You can connect the debugger in your editor, for example with Visual Studio Code or PyCharm.

## Call `uvicorn`[¶](https://fastapi.tiangolo.com/tutorial/debugging/#call-uvicorn "Permanent link")

In your FastAPI application, import and run `uvicorn` directly:

[Python 3.8+](https://fastapi.tiangolo.com/tutorial/debugging/#__tabbed_1_1)

`import uvicorn from fastapi import FastAPI app = FastAPI() @app.get("/") def root():     a = "a"    b = "b" + a    return {"hello world": b} if __name__ == "__main__":     uvicorn.run(app, host="0.0.0.0", port=8000)`

### About `__name__ == "__main__"`[¶](https://fastapi.tiangolo.com/tutorial/debugging/#about-__name__-__main__ "Permanent link")

The main purpose of the `__name__ == "__main__"` is to have some code that is executed when your file is called with:

[fast →](https://fastapi.tiangolo.com/tutorial/debugging/#)python myapp.py

but is not called when another file imports it, like in:

`from myapp import app`

#### More details[¶](https://fastapi.tiangolo.com/tutorial/debugging/#more-details "Permanent link")

Let's say your file is named `myapp.py`.

If you run it with:

[fast →](https://fastapi.tiangolo.com/tutorial/debugging/#)python myapp.py

then the internal variable `__name__` in your file, created automatically by Python, will have as value the string `"__main__"`.

So, the section:

    `uvicorn.run(app, host="0.0.0.0", port=8000)`

will run.

---

This won't happen if you import that module (file).

So, if you have another file `importer.py` with:

`from myapp import app # Some more code`

in that case, the automatically created variable inside of `myapp.py` will not have the variable `__name__` with a value of `"__main__"`.

So, the line:

    `uvicorn.run(app, host="0.0.0.0", port=8000)`

will not be executed.

Info

For more information, check [the official Python docs](https://docs.python.org/3/library/__main__.html).

## Run your code with your debugger[¶](https://fastapi.tiangolo.com/tutorial/debugging/#run-your-code-with-your-debugger "Permanent link")

Because you are running the Uvicorn server directly from your code, you can call your Python program (your FastAPI application) directly from the debugger.

---

For example, in Visual Studio Code, you can:

- Go to the "Debug" panel.
- "Add configuration...".
- Select "Python"
- Run the debugger with the option "`Python: Current File (Integrated Terminal)`".

It will then start the server with your **FastAPI** code, stop at your breakpoints, etc.

Here's how it might look:

![](https://fastapi.tiangolo.com/img/tutorial/debugging/image01.png)

---

If you use Pycharm, you can:

- Open the "Run" menu.
- Select the option "Debug...".
- Then a context menu shows up.
- Select the file to debug (in this case, `main.py`).

It will then start the server with your **FastAPI** code, stop at your breakpoints, etc.

Here's how it might look:

![](https://fastapi.tiangolo.com/img/tutorial/debugging/image02.png)