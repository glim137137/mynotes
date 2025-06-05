# FastAPI

**文章参考**：[FastAPI官方文档](https://fastapi.tiangolo.com/)

[TOC]

# 介绍

FastAPI 是一个现代、快速（高性能）的 Web 框架，用于基于 Python 构建 API。它基于标准 Python 类型提示，使用 **Starlette** 和 **Pydantic** 构建。FastAPI 的主要特点包括：

- **快速**：与 NodeJS 和 Go 相当的高性能，是最快的 Python Web 框架之一。
- **易用**：直观的 API 设计，开发者友好。
- **自动文档**：自动生成交互式 API 文档（Swagger UI 和 ReDoc）。
- **类型安全**：基于 Python 类型提示，减少错误并提高代码可维护性。
- **异步支持**：原生支持异步请求处理。

## FastAPI 的优势

1. **高性能**：FastAPI 基于 Starlette（异步框架）和 Pydantic（数据验证库），性能接近 NodeJS 和 Go。
2. **自动文档生成**：自动生成 Swagger UI 和 ReDoc 文档，方便开发者测试和调试 API。
3. **类型安全**：利用 Python 的类型提示系统，提供更好的代码提示和错误检查。
4. **异步支持**：支持 `async` 和 `await`，适合高并发场景。
5. **标准化**：基于 OpenAPI 和 JSON Schema，兼容性强。

## 安装 FastAPI

在开始使用 FastAPI 之前，需要安装 FastAPI 和 ASGI 服务器（如 Uvicorn 或 Hypercorn）。可以通过以下命令安装：

```bash
pip install fastapi uvicorn
```

## 创建第一个 FastAPI 应用

以下是一个简单的 FastAPI 应用示例：

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello, FastAPI!"}

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

### 运行应用

使用 Uvicorn 运行 FastAPI 应用：

```bash
uvicorn main:app --reload
```

- `main`：Python 文件名（不含 `.py`）。
- `app`：FastAPI 实例的名称。
- `--reload`：启用热重载，适合开发环境。

访问 `http://127.0.0.1:8000` 查看 API 文档。

# FastAPI 基础

## 路径

FastAPI 支持常见的 HTTP 方法（GET、POST、PUT、DELETE 等），通过装饰器定义路径操作：

```python
from fastapi import FastAPI

app = FastAPI()

# GET 请求
@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}

# POST 请求
@app.post("/items/")
def create_item(item: dict):
    return {"item": item}

# PUT 请求
@app.put("/items/{item_id}")
def update_item(item_id: int, item: dict):
    return {"item_id": item_id, "item": item}

# DELETE 请求
@app.delete("/items/{item_id}")
def delete_item(item_id: int):
    return {"message": "Item deleted"}
```

### 路径参数

路径参数是 URL 的一部分，通过 `{}` 定义：

```python
@app.get("/items/{item_id}")
def read_item(item_id):
    return {"item_id": item_id}
```

这段代码把路径参数 `item_id` 的值传递给路径函数的参数 `item_id`。

运行示例并访问 http://127.0.0.1:8000/items/foo，可获得如下响应：

```json
{"item_id":"foo"}
```

#### 声明路径参数的类型

使用 Python 标准类型注解，声明路径操作函数中路径参数的类型。

```python
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```

##### 数据校验

参数会进行校验，如果参数类型不合法，则会获得如下响应：

```json
{
    "detail": [
        {
            "loc": [
                "path",
                "item_id"
            ],
            "msg": "value is not a valid integer",
            "type": "type_error.integer"
        }
    ]
}
```

##### 数据解析

运行示例并访问 http://127.0.0.1:8000/items/3，返回的响应如下：

```json
{"item_id":3}
```

> 注意，函数接收并返回的值是 `3`（ `int`），不是 `"3"`（`str`）。
>
> **FastAPI** 通过类型声明自动**解析**请求中的数据（将来自HTTP请求的字符串转换为Python数据类型）。

#### 顺序很重要

有时，*路径操作*中的路径是写死的。

比如要使用 `/users/me` 获取当前用户的数据。

然后还要使用 `/users/{user_id}`，通过用户 ID 获取指定用户的数据。

由于*路径操作*是按顺序依次运行的，因此，一定要在 `/users/{user_id}` 之前声明 `/users/me` ：

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/users/me")
async def read_user_me():
    return {"user_id": "the current user"}


@app.get("/users/{user_id}")
async def read_user(user_id: str):
    return {"user_id": user_id}
```

否则，`/users/{user_id}` 将匹配 `/users/me`，FastAPI 会**认为**正在接收值为 `"me"` 的 `user_id` 参数。

#### 预设值

路径操作使用 Python 的 `Enum` 类型接收预设的*路径参数*。

##### 创建 `Enum` 类

导入 `Enum` 并创建继承自 `str` 和 `Enum` 的子类。

通过从 `str` 继承，API 文档就能把值的类型定义为**字符串**，并且能正确渲染。

然后，创建包含固定值的类属性，这些固定值是可用的有效值：

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
    if model_name is ModelName.alexnet:
        return {"model_name": model_name, "message": "Deep Learning FTW!"}

    if model_name.value == "lenet":
        return {"model_name": model_name, "message": "LeCNN all the images"}

    return {"model_name": model_name, "message": "Have some residuals"}
```

#### 包含路径的路径参数

假设*路径操作*的路径为 `/files/{file_path}`。

但需要 `file_path` 中也包含*路径*，比如，`home/johndoe/myfile.txt`。

此时，该文件的 URL 是这样的：`/files/home/johndoe/myfile.txt`。

##### OpenAPI 支持

OpenAPI 不支持声明包含路径的*路径参数*，因为这会导致测试和定义更加困难。

不过，仍可使用 Starlette 内置工具在 **FastAPI** 中实现这一功能。

而且不影响文档正常运行，但是不会添加该参数包含路径的说明。

##### 路径转换器

直接使用 Starlette 的选项声明包含*路径*的*路径参数*：

```
/files/{file_path:path}
```

本例中，参数名为 `file_path`，结尾部分的 `:path` 说明该参数应匹配*路径*。

用法如下：

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/files/{file_path:path}")
async def read_file(file_path: str):
    return {"file_path": file_path}
```

> 注意，包含 `/home/johndoe/myfile.txt` 的路径参数要以斜杠（`/`）开头。
>
> 本例中的 URL 是 `/files//home/johndoe/myfile.txt`。注意，`files` 和 `home` 之间要使用**双斜杠**（`//`）。

### 查询参数

声明的参数不是路径参数时，**路径操作函数**会把该参数自动解释为**查询参数**。

```python
from fastapi import FastAPI

app = FastAPI()

fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}]


@app.get("/items/")
async def read_item(skip: int = 0, limit: int = 10):
    return fake_items_db[skip : skip + limit]
```

查询字符串是键值对的集合，这些键值对位于 URL 的 `?` 之后，以 `&` 分隔。

例如，以下 URL 中：

```
http://127.0.0.1:8000/items/?skip=0&limit=10
```

查询参数为：

- `skip`：值为 `0`
- `limit`：值为 `10`

这些值都是 URL 的组成部分，因此，它们的类型**本应**是字符串。但声明 Python 类型（上例中为 `int`）之后，这些值就会转换为声明的类型，并进行类型校验。

#### 默认值

查询参数不是路径的固定内容，它是可选的，还支持默认值。

上例用 `skip=0` 和 `limit=10` 设定默认值。

访问 URL：

```
http://127.0.0.1:8000/items/
```

与访问以下地址相同：

```
http://127.0.0.1:8000/items/?skip=0&limit=10
```

但如果访问：

```
http://127.0.0.1:8000/items/?skip=20
```

查询参数的值就是：

- `skip=20`：在 URL 中设定的值
- `limit=10`：使用默认值

#### 可选参数 & 必选参数

同理，把默认值设为 `None` 即可声明**可选的**查询参数：

```python
@app.get("/items/{item_id}")
async def read_item(item_id: str, q: str | None = None):
    if q:
        return {"item_id": item_id, "q": q}
    return {"item_id": item_id}
```

本例中，查询参数 `q` 是可选的，默认值为 `None`。

> 注意，**FastAPI** 可以识别出 `item_id` 是路径参数，`q` 不是路径参数，而是查询参数。

如果要把查询参数设置为**必选**，就不要声明默认值：

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/items/{item_id}")
async def read_user_item(item_id: str, needy: str):
    item = {"item_id": item_id, "needy": needy}
    return item
```

这里的查询参数 `needy` 是类型为 `str` 的必选查询参数。

在浏览器中打开如下 URL：

```
http://127.0.0.1:8000/items/foo-item
```

……因为路径中没有必选参数 `needy`，返回的响应中会显示如下错误信息：

```json
{
    "detail": [
        {
            "loc": [
                "query",
                "needy"
            ],
            "msg": "field required",
            "type": "value_error.missing"
        }
    ]
}
```

#### 参数类型转换

参数还可以声明为 `bool` 类型，FastAPI 会自动转换参数类型：

```python
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
```

本例中，访问：

```
http://127.0.0.1:8000/items/foo?short=1
http://127.0.0.1:8000/items/foo?short=True
http://127.0.0.1:8000/items/foo?short=true
http://127.0.0.1:8000/items/foo?short=on
http://127.0.0.1:8000/items/foo?short=yes
```

或其它任意大小写形式（大写、首字母大写等），函数接收的 `short` 参数都是布尔值 `True`。值为 `False` 时也一样。

#### 多个路径

**FastAPI** 可以识别同时声明的多个路径参数和查询参数。

而且声明查询参数的顺序并不重要。

FastAPI 通过参数名进行检测：

```python
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
```

#### 查询参数模型

如果你有**一组具有相关性的查询参数**，你可以创建一个 **Pydantic 模型**来声明它们。

这将允许你在**多个地方**去**复用模型**，并且一次性为所有参数声明验证和元数据。😎

##### 使用 Pydantic 模型构建

在一个 **Pydantic 模型**中声明你需要的**查询参数**，然后将参数声明为 `Query`：

```python
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
```

可能的url，

```
GET /items/?limit=20&offset=5&order_by=updated_at&tags=tag1&tags=tag2
```

### 请求体

FastAPI 使用**请求体**从客户端（例如浏览器）向 API 发送数据。

**请求体**是客户端发送给 API 的数据。**响应体**是 API 发送给客户端的数据。

API 基本上肯定要发送**响应体**，但是客户端不一定发送**请求体**。

使用 [Pydantic](https://docs.pydantic.dev/) 模型声明**请求体**，能充分利用它的功能和优点。

#### 创建数据模型

导入 Pydantic 的 `BaseModel`，把数据模型声明为继承 `BaseModel` 的类。

使用 Python 标准类型声明所有属性：

```python
from fastapi import FastAPI
from pydantic import BaseModel


class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None


app = FastAPI()


@app.post("/items/")
async def create_item(item: Item): # 声明请求体参数
    item_dict = item.dict()
    if item.tax is not None: # 使用模型: 在路径操作函数内部直接访问模型对象的属性
        price_with_tax = item.price + item.tax
        item_dict.update({"price_with_tax": price_with_tax})
    return item_dict
```

与声明查询参数一样，包含默认值的模型属性是可选的，否则就是必选的。默认值为 `None` 的模型属性也是可选的。

例如，上述模型声明如下 JSON **对象**（即 Python **字典**）：

```json
{
    "name": "Foo",
    "description": "An optional description",
    "price": 45.2,
    "tax": 3.5
}
```

……由于 `description` 和 `tax` 是可选的（默认值为 `None`），下面的 JSON **对象**也有效：

```json
{
    "name": "Foo",
    "price": 45.2
}
```

#### 发送请求体

**FastAPI** 支持同时声明**请求体**、**路径参数**和**查询参数**。

**FastAPI** 能够正确识别这三种参数，并从正确的位置获取数据。

```python
@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Item, q: str | None = None):
    result = {"item_id": item_id, **item.dict()}
    if q:
        result.update({"q": q})
    return result
```

函数参数按如下规则进行识别：

- **路径**中声明了相同参数的参数，是路径参数
- 类型是（`int`、`float`、`str`、`bool` 等）**单类型**的参数，是**查询**参数
- 类型是 **Pydantic 模型**的参数，是**请求体**

我们这里使用 curl，

```bash
curl -X PUT "http://localhost:8000/items/1?q=test" \
     -H "Content-Type: application/json" \
     -d '{"name":"Laptop","description":"A high-performance laptop","price":999.99,"tax":99.99}'
```

#### 请求体中的单一值

与使用 `Query` 和 `Path` 为查询参数和路径参数定义额外数据的方式相同，**FastAPI** 提供了一个同等的 `Body`。

例如，为了扩展先前的模型，你可能决定除了 `item` 和 `user` 之外，还想在同一请求体中具有另一个键 `importance`。

如果你就按原样声明它，因为它是一个单一值，**FastAPI** 将假定它是一个查询参数。

但是你可以使用 `Body` 指示 **FastAPI** 将其作为请求体的另一个键进行处理。

```python
from typing import Annotated

from fastapi import Body, FastAPI
from pydantic import BaseModel

app = FastAPI()


class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None


class User(BaseModel):
    username: str
    full_name: str | None = None


@app.put("/items/{item_id}")
async def update_item(
    item_id: int, item: Item, user: User, importance: Annotated[int, Body()]
):
    results = {"item_id": item_id, "item": item, "user": user, "importance": importance}
    return results
```

在这种情况下，**FastAPI** 将期望像这样的请求体：

```
{
    "item": {
        "name": "Foo",
        "description": "The pretender",
        "price": 42.0,
        "tax": 3.2
    },
    "user": {
        "username": "dave",
        "full_name": "Dave Grohl"
    },
    "importance": 5
}
```

同样的，它将转换数据类型，校验，生成文档等。

#### 嵌入单个请求体参数

假设你只有一个来自 Pydantic 模型 `Item` 的请求体参数 `item`。

默认情况下，**FastAPI** 将直接期望这样的请求体。

但是，如果你希望它期望一个拥有 `item` 键并在值中包含模型内容的 JSON，就像在声明额外的请求体参数时所做的那样，则可以使用一个特殊的 `Body` 参数 `embed`：

```
item: Item = Body(embed=True)
```

比如：

```python
from typing import Annotated

from fastapi import Body, FastAPI
from pydantic import BaseModel

app = FastAPI()


class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None


@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Annotated[Item, Body(embed=True)]):
    results = {"item_id": item_id, "item": item}
    return results
```

在这种情况下，**FastAPI** 将期望像这样的请求体：

```
{
    "item": {
        "name": "Foo",
        "description": "The pretender",
        "price": 42.0,
        "tax": 3.2
    }
}
```

而不是：

```
{
    "name": "Foo",
    "description": "The pretender",
    "price": 42.0,
    "tax": 3.2
}
```

#### 字段

与在*路径操作函数*中使用 `Query`、`Path` 、`Body` 声明校验与元数据的方式一样，可以使用 Pydantic 的 `Field` 在 Pydantic 模型内部声明校验和元数据。

##### 导入 `Field`

```python
from typing import Annotated

from fastapi import Body, FastAPI
from pydantic import BaseModel, Field # 从 Pydantic 中导入 Field

app = FastAPI()


class Item(BaseModel):
    name: str
    # 使用 Field 定义模型的属性
    description: str | None = Field(
        default=None, title="The description of the item", max_length=300
    ) 
    price: float = Field(gt=0, description="The price must be greater than zero")
    tax: float | None = None


@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Annotated[Item, Body(embed=True)]):
    results = {"item_id": item_id, "item": item}
    return results
```

> 实际上，`Query`、`Path` 都是 `Params` 的子类，而 `Params` 类又是 Pydantic 中 `FieldInfo` 的子类。
>
> Pydantic 的 `Field` 返回也是 `FieldInfo` 的类实例。
>
> `Body` 直接返回的也是 `FieldInfo` 的子类的对象。后文还会介绍一些 `Body` 的子类。
>
> 注意，从 `fastapi` 导入的 `Query`、`Path` 等对象实际上都是返回特殊类的函数。

#### 嵌套模型

使用 **FastAPI**，你可以定义、校验、记录文档并使用任意深度嵌套的模型（归功于Pydantic）。

##### list 类型 & set 类型嵌套

```python
class Tag(BaseModel):
    name: str
    definition: str

class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None
    # tags: list[Tag] = []
    # 但是随后我们考虑了一下，意识到标签不应该重复，它们很大可能会是唯一的字符串。
    tags: set[Tag] = set()
```

这将期望（转换，校验，记录文档等）下面这样的 JSON 请求体：

```
{
    "name": "Foo",
    "description": "The pretender",
    "price": 42.0,
    "tax": 3.2,
    "tags": [
        {
            "name": "hate",
            "definition": "The Foo live"
        },
        {
            "name": "love",
            "definition": "The Baz"
        }
    ]
}
```

##### 请求体嵌套

Pydantic 模型的每个属性都具有类型。

但是这个类型本身可以是另一个 Pydantic 模型。

因此，你可以声明拥有特定属性名称、类型和校验的深度嵌套的 JSON 对象。

上述这些都可以任意的嵌套。

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()


class Image(BaseModel):
    url: str
    name: str


class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None
    tags: set[str] = set()
    image: Image | None = None


@app.put("/items/{item_id}")
async def update_item(item_id: int, item: Item):
    results = {"item_id": item_id, "item": item}
    return results
```

这意味着 **FastAPI** 将期望类似于以下内容的请求体：

```
{
    "name": "Foo",
    "description": "The pretender",
    "price": 42.0,
    "tax": 3.2,
    "tags": ["rock", "metal", "bar"],
    "image": {
        "url": "http://example.com/baz.jpg",
        "name": "The Foo live"
    }
}
```

#### 任意 `dict` 构成的请求体

你也可以将请求体声明为使用某类型的键和其他类型值的 `dict`。

无需事先知道有效的字段/属性（在使用 Pydantic 模型的场景）名称是什么。

如果你想接收一些尚且未知的键，这将很有用。

------

其他有用的场景是当你想要接收其他类型的键时，例如 `int`。

这也是我们在接下来将看到的。

在下面的例子中，你将接受任意键为 `int` 类型并且值为 `float` 类型的 `dict`：

```python
from fastapi import FastAPI

app = FastAPI()


@app.post("/index-weights/")
async def create_index_weights(weights: dict[int, float]):
    return weights
```

> 请记住 JSON 仅支持将 `str` 作为键。
>
> 但是 Pydantic 具有自动转换数据的功能。
>
> 这意味着，即使你的 API 客户端只能将字符串作为键发送，只要这些字符串内容仅包含整数，Pydantic 就会对其进行转换并校验。
>
> 然后你接收的名为 `weights` 的 `dict` 实际上将具有 `int` 类型的键和 `float` 类型的值。

## 校验

### 查询参数校验

**FastAPI** 允许为**查询参数**声明额外的信息和校验。

让我们以下面的应用程序为例：

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/items/")
async def read_items(q: str | None = None):
    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}
    if q:
        results.update({"q": q})
    return results
```

我们打算添加约束条件：即使 `q` 是可选的，但只要提供了该参数，则该参数值**不能超过50个字符的长度**。

#### 导入 `Query`

为此，首先从 `fastapi` 导入 `Query`：

```python
from typing import Union

from fastapi import FastAPI, Query

app = FastAPI()


@app.get("/items/")
async def read_items(q: Union[str, None] = Query(default=None, max_length=50)): # 使用 Query 作为默认值
    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}
    if q:
        results.update({"q": q})
    return results
```

由于我们必须用 `Query(default=None)` 替换默认值 `None`，`Query` 的第一个参数同样也是用于定义默认值。

所以：

```
q: Union[str, None] = Query(default=None)
```

...使得参数可选，等同于：

```
q: str = None
q: str | None = None
```

#### 添加更多校验

你还可以添加 `min_length` 参数

```python
async def read_items(
    q: Union[str, None] = Query(default=None, min_length=3, max_length=50),
):
```

你可以定义一个参数值必须匹配的正则表达式，

```python
async def read_items(
    q: Union[str, None] = Query(
        default=None, min_length=3, max_length=50, pattern="^fixedquery$"
    ),
):
```

你可以向 `Query` 的第一个参数传入 `None` 用作查询参数的默认值，以同样的方式你也可以传递其他默认值。

同样，当你在使用 `Query` 且需要声明一个值是必需的时，只需不声明默认参数。

```python
async def read_items(q: str = Query(min_length=3)):
```

#### 查询参数列表 / 多个值

当你使用 `Query` 显式地定义查询参数时，你还可以声明它去接收一组值，或换句话来说，接收多个值。

例如，要声明一个可在 URL 中出现多次的查询参数 `q`，你可以这样写：

```python
@app.get("/items/")
async def read_items(q: Union[List[str], None] = Query(default=None)):
    query_items = {"q": q}
    return query_items
```

然后，输入如下网址：

```
http://localhost:8000/items/?q=foo&q=bar
```

你会在*路径操作函数*的*函数参数* `q` 中以一个 Python `list` 的形式接收到*查询参数* `q` 的多个值（`foo` 和 `bar`）。

因此，该 URL 的响应将会是：

```
{
  "q": [
    "foo",
    "bar"
  ]
}
```

#### 声明更多元数据

你可以添加更多有关该参数的信息。

这些信息将包含在生成的 OpenAPI 模式中，并由文档用户界面和外部工具所使用。

你可以添加 `title` 以及 `description`，

```python
@app.get("/items/")
async def read_items(
    q: Union[str, None] = Query(
        default=None,
        title="Query string",
        description="Query string for the items to search in the database that have a good match",
        min_length=3,
    ),
):
```

#### 别名参数

假设你想要查询参数为 `item-query`。

像下面这样：

```
http://127.0.0.1:8000/items/?item-query=foobaritems
```

但是 `item-query` 不是一个有效的 Python 变量名称。

最接近的有效名称是 `item_query`。

但是你仍然要求它在 URL 中必须是 `item-query`...

这时你可以用 `alias` 参数声明一个别名，该别名将用于在 URL 中查找查询参数值：

```python
async def read_items(q: Union[str, None] = Query(default=None, alias="item-query")):
```

与使用 `Query` 为查询参数声明更多的校验和元数据的方式相同，你也可以使用 `Path` 为路径参数声明相同类型的校验和元数据。

### 路径参数校验

与使用 `Query` 为查询参数声明更多的校验和元数据的方式相同，你也可以使用 `Path` 为路径参数声明相同类型的校验和元数据。

#### 导入 Path

首先，从 `fastapi` 导入 `Path`：

```python
from typing import Annotated # 用于为类型注解附加元数据。Annotated[Type, metadata]

from fastapi import FastAPI, Path, Query

app = FastAPI()
```

#### 声明元数据

你可以声明与 `Query` 相同的所有参数。

例如，要声明路径参数 `item_id`的 `title` 元数据值，你可以输入：

```python
@app.get("/items/{item_id}")
async def read_items(
    item_id: Annotated[int, Path(title="The ID of the item to get")],
    q: Annotated[str | None, Query(alias="item-query")] = None,
):
    results = {"item_id": item_id}
    if q:
        results.update({"q": q})
    return results
```

#### 按需对参数排序

假设你想要声明一个必需的 `str` 类型查询参数 `q`。

而且你不需要为该参数声明任何其他内容，所以实际上你并不需要使用 `Query`。

但是你仍然需要使用 `Path` 来声明路径参数 `item_id`。

如果你将带有「默认值」的参数放在没有「默认值」的参数之前，Python 将会报错。

但是你可以对其重新排序，并将不带默认值的值（查询参数 `q`）放到最前面。

对 **FastAPI** 来说这无关紧要。它将通过参数的名称、类型和默认值声明（`Query`、`Path` 等）来检测参数，而不在乎参数的顺序。

因此，你可以将函数声明为：

```python
@app.get("/items/{item_id}")
async def read_items(q: str, item_id: int = Path(title="The ID of the item to get")):
```

如果你想不使用 `Query` 声明没有默认值的查询参数 `q`，同时使用 `Path` 声明路径参数 `item_id`，并使它们的顺序与上面不同，Python 对此有一些特殊的语法。

传递 `*` 作为函数的第一个参数。

Python 不会对该 `*` 做任何事情，但是它将知道之后的所有参数都应作为关键字参数（键值对），也被称为 `kwargs`，来调用。即使它们没有默认值。

```python
@app.get("/items/{item_id}")
async def read_items(*, item_id: int = Path(title="The ID of the item to get"), q: str):
```

### 数值校验

使用 `Query` 和 `Path`（以及你将在后面看到的其他类）可以声明字符串约束，但也可以声明数值约束。

像下面这样，添加 `ge=1` 后，`item_id` 将必须是一个大于（`g`reater than）或等于（`e`qual）`1` 的整数。

```python
@app.get("/items/{item_id}")
async def read_items(
    *, item_id: int = Path(title="The ID of the item to get", ge=1), q: str
):
```

同样的规则适用于：

- `gt`：大于（`g`reater `t`han）
- `ge`：大于等于（`g`reater than or `e`qual）
- `lt`：小于（`l`ess `t`han）
- `le`：小于等于（`l`ess than or `e`qual）

## 数据类型

到目前为止，您一直在使用常见的数据类型，如:

- `int`
- `float`
- `str`
- `bool`

但是您也可以使用更复杂的数据类型。

### 其他数据类型

下面是一些你可以使用的其他数据类型:

- ```
    UUID
    ```

    - 一种标准的 "通用唯一标识符" ，在许多数据库和系统中用作ID。
    - 在请求和响应中将以 `str` 表示。

- ```
    datetime.datetime
    ```

    - 一个 Python `datetime.datetime`.
    - 在请求和响应中将表示为 ISO 8601 格式的 `str` ，比如: `2008-09-15T15:53:00+05:00`.

- ```
    datetime.date
    ```

    - Python `datetime.date`.
    - 在请求和响应中将表示为 ISO 8601 格式的 `str` ，比如: `2008-09-15`.

- ```
    datetime.time
    ```

    - 一个 Python `datetime.time`.
    - 在请求和响应中将表示为 ISO 8601 格式的 `str` ，比如: `14:23:55.003`.

- ```
    datetime.timedelta
    ```

    - 一个 Python `datetime.timedelta`.
    - 在请求和响应中将表示为 `float` 代表总秒数。
    - Pydantic 也允许将其表示为 "ISO 8601 时间差异编码", [查看文档了解更多信息](https://docs.pydantic.dev/latest/concepts/serialization/#json_encoders)。

- ```
    frozenset
    ```

    - 在请求和响应中，作为 `set` 对待：
        - 在请求中，列表将被读取，消除重复，并将其转换为一个 `set`。
        - 在响应中 `set` 将被转换为 `list` 。
        - 产生的模式将指定那些 `set` 的值是唯一的 (使用 JSON 模式的 `uniqueItems`)。

- ```
    bytes
    ```

    - 标准的 Python `bytes`。
    - 在请求和响应中被当作 `str` 处理。
    - 生成的模式将指定这个 `str` 是 `binary` "格式"。

- ```
    Decimal
    ```

    - 标准的 Python `Decimal`。
    - 在请求和响应中被当做 `float` 一样处理。

### 示例

下面是一个*路径操作*的示例，其中的参数使用了上面的一些类型。

```python
from datetime import datetime, time, timedelta
from typing import Annotated
from uuid import UUID

from fastapi import Body, FastAPI

app = FastAPI()


@app.put("/items/{item_id}")
async def read_items(
    item_id: UUID,
    start_datetime: Annotated[datetime, Body()],
    end_datetime: Annotated[datetime, Body()],
    process_after: Annotated[timedelta, Body()],
    repeat_at: Annotated[time | None, Body()] = None,
):
    start_process = start_datetime + process_after
    duration = end_datetime - start_process
    return {
        "item_id": item_id,
        "start_datetime": start_datetime,
        "end_datetime": end_datetime,
        "process_after": process_after,
        "repeat_at": repeat_at,
        "start_process": start_process,
        "duration": duration,
    }
```

### HttpUrl 类型

```python
from pydantic import BaseModel, HttpUrl

class Image(BaseModel):
    url: HttpUrl
    name: str
```

该字符串将被检查是否为有效的 URL，并在 JSON Schema / OpenAPI 文档中进行记录。

### EmailStr 类型

### Cookie 参数

定义 `Cookie` 参数与定义 `Query` 和 `Path` 参数一样。

```python
from typing import Annotated

from fastapi import Cookie, FastAPI

app = FastAPI()


@app.get("/items/")
async def read_items(ads_id: Annotated[str | None, Cookie()] = None):
    return {"ads_id": ads_id}
```

> `Cookie` 、`Path` 、`Query` 是**兄弟类**，都继承自共用的 `Param` 类。
>
> 注意，从 `fastapi` 导入的 `Query`、`Path`、`Cookie` 等对象，实际上是返回**特殊类的函数**。

#### Cookie 参数模型

如果您有一组相关的 **cookie**，您可以创建一个 **Pydantic 模型**来声明它们。🍪

这将允许您在**多个地方**能够**重用模型**，并且可以一次性声明所有参数的验证方式和元数据。😎

```python
from typing import Annotated

from fastapi import Cookie, FastAPI
from pydantic import BaseModel

app = FastAPI()


class Cookies(BaseModel):
    session_id: str
    fatebook_tracker: str | None = None
    googall_tracker: str | None = None


@app.get("/items/")
async def read_items(cookies: Annotated[Cookies, Cookie()]):
    return cookies
```

**FastAPI** 将从请求中接收到的 **cookie** 中**提取**出**每个字段**的数据，并提供您定义的 Pydantic 模型。

#### 禁止额外的 Cookie

在某些特殊使用情况下（可能并不常见），您可能希望**限制**您想要接收的 cookie。

您的 API 现在可以控制自己的 cookie 同意。🤪🍪

您可以使用 Pydantic 的模型配置来禁止（ `forbid` ）任何额外（ `extra` ）字段：

```python
from typing import Annotated, Union

from fastapi import Cookie, FastAPI
from pydantic import BaseModel

app = FastAPI()


class Cookies(BaseModel):
    model_config = {"extra": "forbid"}

    session_id: str
    fatebook_tracker: Union[str, None] = None
    googall_tracker: Union[str, None] = None


@app.get("/items/")
async def read_items(cookies: Annotated[Cookies, Cookie()]):
    return cookies
```

如果客户尝试发送一些**额外的 cookie**，他们将收到**错误**响应。

可怜的 cookie 通知条，费尽心思为了获得您的同意，却被API 拒绝了。🍪

例如，如果客户端尝试发送一个值为 `good-list-please` 的 `santa_tracker` cookie，客户端将收到一个**错误**响应，告知他们 `santa_tracker` cookie 是不允许的：

```
{
    "detail": [
        {
            "type": "extra_forbidden",
            "loc": ["cookie", "santa_tracker"],
            "msg": "Extra inputs are not permitted",
            "input": "good-list-please",
        }
    ]
}
```

### Header 参数

```python
from typing import Annotated

from fastapi import FastAPI, Header

app = FastAPI()


@app.get("/items/")
async def read_items(user_agent: Annotated[str | None, Header()] = None):
    return {"User-Agent": user_agent}
```

#### 自动转换

`Header` 比 `Path`、`Query` 和 `Cookie` 提供了更多功能。

大部分标准请求头用**连字符**分隔，即**减号**（`-`）。

但是 `user-agent` 这样的变量在 Python 中是无效的，并且`fastapi` 要求**变量名（函数参数名）**必须和**返回的键名**一致。

因此，默认情况下，`Header` 把参数名中的字符由下划线（`_`）改为连字符（`-`）来提取并存档请求头 。

同时，HTTP 的请求头不区分大小写，可以使用 Python 标准样式（即 **snake_case**）进行声明。

因此，可以像在 Python 代码中一样使用 `user_agent` ，无需把首字母大写为 `User_Agent` 等形式。

如需禁用下划线自动转换为连字符，可以把 `Header` 的 `convert_underscores` 参数设置为 `False`：

```python
@app.get("/items/")
async def read_items(
    strange_header: Annotated[str | None, Header(convert_underscores=False)] = None,
):
    return {"strange_header": strange_header}
```

#### 重复的请求头

有时，可能需要接收重复的请求头。即同一个请求头有多个值。

类型声明中可以使用 `list` 定义多个请求头。

使用 Python `list` 可以接收重复请求头所有的值。

例如，声明 `X-Token` 多次出现的请求头，可以写成这样：

```python
from typing import Annotated

from fastapi import FastAPI, Header

app = FastAPI()


@app.get("/items/")
async def read_items(x_token: Annotated[list[str] | None, Header()] = None):
    return {"X-Token values": x_token}
```

与*路径操作*通信时，以下面的方式发送两个 HTTP 请求头：

```
X-Token: foo
X-Token: bar
```

响应结果是：

```
{
    "X-Token values": [
        "bar",
        "foo"
    ]
}
```

#### Header 参数模型

这与Cookie 参数模型几乎一样，你也可以禁止额外的 `Headers`。

```python
from typing import Annotated

from fastapi import FastAPI, Header
from pydantic import BaseModel

app = FastAPI()


class CommonHeaders(BaseModel):
    model_config = {"extra": "forbid"}

    host: str
    save_data: bool
    if_modified_since: str | None = None
    traceparent: str | None = None
    x_tag: list[str] = []


@app.get("/items/")
async def read_items(headers: Annotated[CommonHeaders, Header()]):
    return headers
```

### 表单数据

接收的不是 JSON，而是表单字段时，要使用 `Form`。

> 要使用表单，需预先安装 [`python-multipart`](https://github.com/Kludex/python-multipart)。
>
> 例如，`pip install python-multipart`。

#### 导入 `Form`

```python
from fastapi import FastAPI, Form

app = FastAPI()


@app.post("/login/")
async def login(username: str = Form(), password: str = Form()):
    return {"username": username}
```

例如，OAuth2 规范的 "密码流" 模式规定要通过表单字段发送 `username` 和 `password`。

该规范要求字段必须命名为 `username` 和 `password`，并通过表单字段发送，不能用 JSON。

使用 `Form` 可以声明与 `Body` （及 `Query`、`Path`、`Cookie`）相同的元数据和验证。

> `Form` 是直接继承自 `Body` 的类。
>
> 声明表单体要显式使用 `Form` ，否则，FastAPI 会把该参数当作查询参数或请求体（JSON）参数。

#### 关于 "表单字段"

与 JSON 不同，HTML 表单（`<form></form>`）向服务器发送数据通常使用「特殊」的编码。

**FastAPI** 要确保从正确的位置读取数据，而不是读取 JSON。

**技术细节**

表单数据的「媒体类型」编码一般为 `application/x-www-form-urlencoded`。

但包含文件的表单编码为 `multipart/form-data`。

> 可在一个*路径操作*中声明多个 `Form` 参数，但不能同时声明要接收 JSON 的 `Body` 字段。因为此时请求体的编码是 `application/x-www-form-urlencoded`，不是 `application/json`。
>
> 这不是 **FastAPI** 的问题，而是 HTTP 协议的规定。

#### 表单模型

同样你可以禁止（ `forbid` ）任何额外（ `extra` ）字段。

```python
from typing import Annotated

from fastapi import FastAPI, Form
from pydantic import BaseModel

app = FastAPI()


class FormData(BaseModel):
    username: str
    password: str
    model_config = {"extra": "forbid"}


@app.post("/login/")
async def login(data: Annotated[FormData, Form()]):
    return data
```

## 文件

`File` 用于定义客户端的上传文件。

### 导入 `File`

```python
from fastapi import FastAPI, File, UploadFile

app = FastAPI()


@app.post("/files/")
async def create_file(file: bytes = File()):
    return {"file_size": len(file)}
```

> `File` 是直接继承自 `Form` 的类。

文件作为「表单数据」上传。

如果把*路径操作函数*参数的类型声明为 `bytes`，**FastAPI** 将以 `bytes` 形式读取和接收文件内容。

这种方式把文件的所有内容都存储在内存里，适用于小型文件。

不过，很多情况下，`UploadFile` 更好用。

### 含 `UploadFile` 的文件参数

```python
@app.post("/uploadfile/")
async def create_upload_file(file: UploadFile):
    return {"filename": file.filename}
```

`UploadFile` 与 `bytes` 相比有更多优势：

- 使用`spooled`文件：
    - 存储在内存的文件超出最大上限时，FastAPI 会把文件存入磁盘；
- 这种方式更适于处理图像、视频、二进制文件等大型文件，好处是不会占用所有内存；
- 可获取上传文件的元数据；
- 自带 [file-like](https://docs.python.org/zh-cn/3/glossary.html#term-file-like-object) `async` 接口；
- 暴露的 Python [`SpooledTemporaryFile`](https://docs.python.org/zh-cn/3/library/tempfile.html#tempfile.SpooledTemporaryFile) 对象，可直接传递给其他预期「file-like」对象的库。

#### `UploadFile`

`UploadFile` 的属性如下：

- `filename`：上传文件名字符串（`str`），例如， `myimage.jpg`；
- `content_type`：内容类型（MIME 类型 / 媒体类型）字符串（`str`），例如，`image/jpeg`；
- `file`： [`SpooledTemporaryFile`](https://docs.python.org/zh-cn/3/library/tempfile.html#tempfile.SpooledTemporaryFile)（ [file-like](https://docs.python.org/zh-cn/3/glossary.html#term-file-like-object) 对象）。其实就是 Python文件，可直接传递给其他预期 `file-like` 对象的函数或支持库。

`UploadFile` 支持以下 `async` 方法，（使用内部 `SpooledTemporaryFile`）可调用相应的文件方法。

- `write(data)`：把 `data` （`str` 或 `bytes`）写入文件；
- `read(size)`：按指定数量的字节或字符（`size` (`int`)）读取文件内容；
- `seek(offset)`：移动至文件`offset`（`int`）字节处的位置；
    - 例如，`await myfile.seek(0)` 移动到文件开头；
    - 执行 `await myfile.read()` 后，需再次读取已读取内容时，这种方法特别好用；
- `close()`：关闭文件。

因为上述方法都是 `async` 方法，要搭配「await」使用。

例如，在 `async` *路径操作函数* 内，要用以下方式读取文件内容：

```python
contents = await myfile.read()
```

在普通 `def` *路径操作函数* 内，则可以直接访问 `UploadFile.file`，例如：

```python
contents = myfile.file.read()
```

### 多文件上传

FastAPI 支持同时上传多个文件。

可用同一个「表单字段」发送含多个文件的「表单数据」。

上传多个文件时，要声明含 `bytes` 或 `UploadFile` 的列表（`List`）：

```python
from fastapi import FastAPI, File, UploadFile
from fastapi.responses import HTMLResponse

app = FastAPI()


@app.post("/files/")
async def create_files(
    files: list[bytes] = File(description="Multiple files as bytes"),
):
    return {"file_sizes": [len(file) for file in files]}


@app.post("/uploadfiles/")
async def create_upload_files(
    files: list[UploadFile] = File(description="Multiple files as UploadFile"),
):
    return {"filenames": [file.filename for file in files]}


@app.get("/")
async def main():
    content = """
<body>
<form action="/files/" enctype="multipart/form-data" method="post">
<input name="files" type="file" multiple>
<input type="submit">
</form>
<form action="/uploadfiles/" enctype="multipart/form-data" method="post">
<input name="files" type="file" multiple>
<input type="submit">
</form>
</body>
    """
    return HTMLResponse(content=content)
```

### 请求 表单+文件

FastAPI 支持同时使用 `File` 和 `Form` 定义文件和表单字段。

```python
from fastapi import FastAPI, File, Form, UploadFile

app = FastAPI()


@app.post("/files/")
async def create_file(
    file: bytes = File(), fileb: UploadFile = File(), token: str = Form()
):
    return {
        "file_size": len(file),
        "token": token,
        "fileb_content_type": fileb.content_type,
    }
```





## 响应模型

可以定义返回数据的模型，确保响应数据符合预期：

```python
@app.post("/items/", response_model=Item)
def create_item(item: Item):
    return item
```

FastAPI 将使用此 `response_model` 来：

- 将输出数据转换为其声明的类型。
- 校验数据。
- 在 OpenAPI 的*路径操作*中为响应添加一个 JSON Schema。
- 并在自动生成文档系统中使用。

但最重要的是：

- 会将输出数据限制在该模型定义内。下面我们会看到这一点有多重要。

我们创建一个有明文密码的输入模型和一个没有明文密码的输出模型：

```python
from typing import Any

from fastapi import FastAPI
from pydantic import BaseModel, EmailStr

app = FastAPI()


class UserIn(BaseModel):
    username: str
    password: str
    email: EmailStr
    full_name: str | None = None

# 不包含密码的 UserOut 模型
class UserOut(BaseModel):
    username: str
    email: EmailStr
    full_name: str | None = None


@app.post("/user/", response_model=UserOut)
async def create_user(user: UserIn) -> Any:
    return user
```

因此，**FastAPI** 将会负责过滤掉未在输出模型中声明的所有数据（使用 Pydantic）。

### 响应模型编码参数

你的响应模型可以具有默认值，例如：

```python
from typing import List, Union

from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()


class Item(BaseModel):
    name: str
    description: Union[str, None] = None
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

- `description: Union[str, None] = None` 具有默认值 `None`。
- `tax: float = 10.5` 具有默认值 `10.5`.
- `tags: List[str] = []` 具有一个空列表作为默认值： `[]`.

但如果它们并**没有存储实际的值**，你可能想从结果中忽略它们的默认值。

举个例子，当你在 NoSQL 数据库中保存了具有许多可选属性的模型，但你又不想发送充满默认值的很长的 JSON 响应。

#### 使用 `response_model_exclude_unset` 参数

```python
@app.get("/items/{item_id}", response_model=Item, response_model_exclude_unset=True)
async def read_item(item_id: str):
    return items[item_id]
```

然后响应中将不会包含那些默认值，而是仅有实际设置的值。

##### 缺失默认值字段的数据

因此，如果你向*路径操作*发送 ID 为 `foo` 的商品的请求，则响应（不包括默认值）将为：

```
{
    "name": "Foo",
    "price": 50.2
}
```

##### 默认值字段有实际值的数据

但是，如果你的数据在具有默认值的模型字段中有实际的值，例如 ID 为 `bar` 的项：

```
{
    "name": "Bar",
    "description": "The bartenders",
    "price": 62,
    "tax": 20.2
}
```

这些值将包含在响应中。

##### 具有与默认值相同值的数据

如果数据具有与默认值相同的值，例如 ID 为 `baz` 的项：

```
{
    "name": "Baz",
    "description": None,
    "price": 50.2,
    "tax": 10.5,
    "tags": []
}
```

即使 `description`、`tax` 和 `tags` 具有与默认值相同的值，FastAPI 足够聪明 (实际上是 Pydantic 足够聪明) 去认识到这一点，它们的值被显式地所设定（而不是取自默认值）。

因此，它们将包含在 JSON 响应中。

#### `response_model_include` 和 `response_model_exclude`

你还可以使用*路径操作装饰器*的 `response_model_include` 和 `response_model_exclude` 参数。

它们接收一个由属性名称 `str` 组成的 `set` 来包含（忽略其他的）或者排除（包含其他的）这些属性。

如果你只有一个 Pydantic 模型，并且想要从输出中移除一些数据，则可以使用这种快捷方法。

> **但是依然建议你使用上面提到的主意，使用多个类而不是这些参数。**
>
> 这是因为即使使用 `response_model_include` 或 `response_model_exclude` 来省略某些属性，在应用程序的 OpenAPI 定义（和文档）中生成的 JSON Schema 仍将是完整的模型。
>
> 这也适用于作用类似的 `response_model_by_alias`。

```python
@app.get(
    "/items/{item_id}/name",
    response_model=Item,
    response_model_include={"name", "description"},
)
async def read_item_name(item_id: str):
    return items[item_id]
```

### 多个模型

多个关联模型这种情况很常见。

特别是用户模型，因为：

- **输入模型**应该含密码
- **输出模型**不应含密码
- **数据库模型**需要加密的密码

下面的代码展示了不同模型处理密码字段的方式，及使用位置的大致思路：

```python
from fastapi import FastAPI
from pydantic import BaseModel, EmailStr

app = FastAPI()


class UserIn(BaseModel):
    username: str
    password: str
    email: EmailStr
    full_name: str | None = None


class UserOut(BaseModel):
    username: str
    email: EmailStr
    full_name: str | None = None


class UserInDB(BaseModel):
    username: str
    hashed_password: str
    email: EmailStr
    full_name: str | None = None


def fake_password_hasher(raw_password: str):
    return "supersecret" + raw_password


def fake_save_user(user_in: UserIn):
    hashed_password = fake_password_hasher(user_in.password)
    user_in_db = UserInDB(**user_in.dict(), hashed_password=hashed_password)
    print("User saved! ..not really")
    return user_in_db


@app.post("/user/", response_model=UserOut)
async def create_user(user_in: UserIn):
    user_saved = fake_save_user(user_in)
    return user_saved
```

#### `**user_in.dict()` 简介

##### Pydantic 的 `.dict()`

`user_in` 是类 `UserIn` 的 Pydantic 模型。

Pydantic 模型支持 `.dict()` 方法，能返回包含模型数据的**字典**。

因此，如果使用如下方式创建 Pydantic 对象 `user_in`：

```python
user_in = UserIn(username="john", password="secret", email="john.doe@example.com")
```

就能以如下方式调用：

```python
user_dict = user_in.dict()
```

现在，变量 `user_dict`中的就是包含数据的**字典**（变量 `user_dict` 是字典，不是 Pydantic 模型对象）。

以如下方式调用：

```python
print(user_dict)
```

输出的就是 Python **字典**：

```
{
    'username': 'john',
    'password': 'secret',
    'email': 'john.doe@example.com',
    'full_name': None,
}
```

##### 解包 `dict`

把**字典** `user_dict` 以 `**user_dict` 形式传递给函数（或类），Python 会执行**解包**操作。它会把 `user_dict` 的键和值作为关键字参数直接传递。

因此，接着上面的 `user_dict` 继续编写如下代码：

```python
user_dict = user_in.dict()
UserInDB(**user_dict)

# 等效于
UserInDB(**user_in.dict())
```

就会生成如下结果：

```
UserInDB(
    username="john",
    password="secret",
    email="john.doe@example.com",
    full_name=None,
)
```

或更精准，直接把可能会用到的内容与 `user_dict` 一起使用：

```
UserInDB(
    username = user_dict["username"],
    password = user_dict["password"],
    email = user_dict["email"],
    full_name = user_dict["full_name"],
)
```

##### 更多关键字

接下来，继续添加关键字参数 `hashed_password=hashed_password`，例如：

```
UserInDB(**user_in.dict(), hashed_password=hashed_password)
```

……输出结果如下：

```
UserInDB(
    username = user_dict["username"],
    password = user_dict["password"],
    email = user_dict["email"],
    full_name = user_dict["full_name"],
    hashed_password = hashed_password,
)
```

### 减少重复

**FastAPI** 的核心思想就是减少代码重复。

代码重复会导致 bug、安全问题、代码失步等问题（更新了某个位置的代码，但没有同步更新其它位置的代码）。

上面的这些模型共享了大量数据，拥有重复的属性名和类型。

FastAPI 可以做得更好。

声明 `UserBase` 模型作为其它模型的**基类**。然后，用该类衍生出继承其属性（类型声明、验证等）的子类。

所有数据转换、校验、文档等功能仍将正常运行。

这样，就可以仅声明模型之间的差异部分（具有明文的 `password`、具有 `hashed_password` 以及不包括密码）。

通过这种方式，可以**只声明模型之间的区别**（分别包含明文密码、哈希密码，以及无密码的模型）。

```python
from fastapi import FastAPI
from pydantic import BaseModel, EmailStr

app = FastAPI()


class UserBase(BaseModel):
    username: str
    email: EmailStr
    full_name: str | None = None


class UserIn(UserBase):
    password: str


class UserOut(UserBase):
    pass


class UserInDB(UserBase):
    hashed_password: str


def fake_password_hasher(raw_password: str):
    return "supersecret" + raw_password


def fake_save_user(user_in: UserIn):
    hashed_password = fake_password_hasher(user_in.password)
    user_in_db = UserInDB(**user_in.dict(), hashed_password=hashed_password)
    print("User saved! ..not really")
    return user_in_db


@app.post("/user/", response_model=UserOut)
async def create_user(user_in: UserIn):
    user_saved = fake_save_user(user_in)
    return user_saved
```

### `Union` 或者 `anyOf`

响应可以声明为两种类型的 `Union` 类型，即该响应可以是两种类型中的任意类型。

在 OpenAPI 中可以使用 `anyOf` 定义。

```python
@app.get("/items/{item_id}", response_model=Union[PlaneItem, CarItem])
async def read_item(item_id: str):
    return items[item_id]
```

### 模型列表

```python
items = [
    {"name": "Foo", "description": "There comes my hero"},
    {"name": "Red", "description": "It's my aeroplane"},
]

@app.get("/items/", response_model=list[Item])
async def read_items():
    return items
```

### 任意 `dict` 构成的响应

任意的 `dict` 都能用于声明响应，只要声明键和值的类型，无需使用 Pydantic 模型。

事先不知道可用的字段 / 属性名时（Pydantic 模型必须知道字段是什么），这种方式特别有用。

此时，可以使用 `typing.Dict`：

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/keyword-weights/", response_model=dict[str, float])
async def read_keyword_weights():
    return {"foo": 2.3, "bar": 3.4}
```

### 状态码

在 HTTP 协议中，发送 3 位数的数字状态码是响应的一部分。

这些状态码都具有便于识别的关联名称，但是重要的还是数字。

简言之：

- `100` 及以上的状态码用于返回**信息**。这类状态码很少直接使用。具有这些状态码的响应不能包含响应体
- `200`及以上的状态码用于表示成功。这些状态码是最常用的
    - `200` 是默认状态代码，表示一切**正常**
    - `201` 表示**已创建**，通常在数据库中创建新记录后使用
    - `204` 是一种特殊的例子，表示**无内容**。该响应在没有为客户端返回内容时使用，因此，该响应不能包含响应体
- `300` 及以上的状态码用于**重定向**。具有这些状态码的响应不一定包含响应体，但 `304`**未修改**是个例外，该响应不得包含响应体
- `400`及以上的状态码用于表示客户端错误。这些可能是第二常用的类型
    - `404`，用于**未找到**响应
    - 对于来自客户端的一般错误，可以只使用 `400`
- `500` 及以上的状态码用于表示服务器端错误。几乎永远不会直接使用这些状态码。应用代码或服务器出现问题时，会自动返回这些状态代码

#### 状态码名称快捷方式

再看下之前的例子：

```python
from fastapi import FastAPI

app = FastAPI()


@app.post("/items/", status_code=201)
async def create_item(name: str):
    return {"name": name}
```

`201` 表示**已创建**的状态码。

但我们没有必要记住所有代码的含义。

可以使用 `fastapi.status` 中的快捷变量。

```python
from fastapi import FastAPI, status

app = FastAPI()


@app.post("/items/", status_code=status.HTTP_201_CREATED)
async def create_item(name: str):
    return {"name": name}
```

这只是一种快捷方式，具有相同的数字代码，但它可以使用编辑器的自动补全功能

## 处理错误

某些情况下，需要向客户端返回错误提示。

这里所谓的客户端包括前端浏览器、其他应用程序、物联网设备等。

需要向客户端返回错误提示的场景主要如下：

- 客户端没有执行操作的权限
- 客户端没有访问资源的权限
- 客户端要访问的项目不存在
- 等等 ...

遇到这些情况时，通常要返回 **4XX**（400 至 499）**HTTP 状态码**。

**4XX** 状态码与表示请求成功的 **2XX**（200 至 299） HTTP 状态码类似。

只不过，**4XX** 状态码表示客户端发生的错误。

大家都知道**「404 Not Found」**错误，还有调侃这个错误的笑话吧？

### 使用 `HTTPException`

向客户端返回 HTTP 错误响应，可以使用 `HTTPException`。

本例中，客户端用 `ID` 请求的 `item` 不存在时，触发状态码为 `404` 的异常：

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

items = {"foo": "The Foo Wrestlers"}


@app.get("/items/{item_id}")
async def read_item(item_id: str):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"item": items[item_id]}
```

#### 响应结果

请求为 `http://example.com/items/foo`（`item_id` 为 `「foo」`）时，客户端会接收到 HTTP 状态码 - 200 及如下 JSON 响应结果：

```
{
  "item": "The Foo Wrestlers"
}
```

但如果客户端请求 `http://example.com/items/bar`（`item_id` `「bar」` 不存在时），则会接收到 HTTP 状态码 - 404（「未找到」错误）及如下 JSON 响应结果：

```
{
  "detail": "Item not found"
}
```

> 触发 `HTTPException` 时，可以用参数 `detail` 传递任何能转换为 JSON 的值，不仅限于 `str`。
>
> 还支持传递 `dict`、`list` 等数据结构。
>
> **FastAPI** 能自动处理这些数据，并将之转换为 JSON。

#### 添加自定义响应头

有些场景下要为 HTTP 错误添加自定义响应头。例如，出于某些方面的安全需要。

一般情况下可能不会需要在代码中直接使用响应头。

但对于某些高级应用场景，还是需要添加自定义响应头：

```python
raise HTTPException(
            status_code=404,
            detail="Item not found",
            headers={"X-Error": "There goes my error"},
        )
```

### 自定义异常处理器

假设要触发的自定义异常叫作 `UnicornException`。

且需要 FastAPI 实现全局处理该异常。

此时，可以用 `@app.exception_handler()` 添加自定义异常控制器：

```python
from fastapi import FastAPI, Request
from fastapi.responses import JSONResponse


class UnicornException(Exception):
    def __init__(self, name: str):
        self.name = name


app = FastAPI()


@app.exception_handler(UnicornException)
async def unicorn_exception_handler(request: Request, exc: UnicornException):
    return JSONResponse(
        status_code=418,
        content={"message": f"Oops! {exc.name} did something. There goes a rainbow..."},
    )


@app.get("/unicorns/{name}")
async def read_unicorn(name: str):
    if name == "yolo":
        raise UnicornException(name=name)
    return {"unicorn_name": name}
```

请求 `/unicorns/yolo` 时，路径操作会触发 `UnicornException`。

但该异常将会被 `unicorn_exception_handler` 处理。

接收到的错误信息清晰明了，HTTP 状态码为 `418`，JSON 内容如下：

```
{"message": "Oops! yolo did something. There goes a rainbow..."}
```

### 覆盖默认异常处理器

**FastAPI** 自带了一些默认异常处理器。

触发 **`HTTPException`** 或**请求无效数据**时，这些处理器返回默认的 JSON 响应结果。

不过，也可以使用自定义处理器覆盖默认异常处理器。

```python
from fastapi import FastAPI, HTTPException
from fastapi.exceptions import RequestValidationError
from fastapi.responses import PlainTextResponse
from starlette.exceptions import HTTPException as StarletteHTTPException

app = FastAPI()

# 覆盖 HTTPException 错误处理器 StarletteHTTPException
@app.exception_handler(StarletteHTTPException)
async def http_exception_handler(request, exc):
    return PlainTextResponse(str(exc.detail), status_code=exc.status_code)

# 覆盖请求验证异常 RequestValidationError
@app.exception_handler(RequestValidationError)
async def validation_exception_handler(request, exc):
    return PlainTextResponse(str(exc), status_code=400)


@app.get("/items/{item_id}")
async def read_item(item_id: int):
    if item_id == 3:
        raise HTTPException(status_code=418, detail="Nope! I don't like 3.")
    return {"item_id": item_id}
```

#### 覆盖请求验证异常

请求中包含无效数据时，**FastAPI** 内部会触发 `RequestValidationError`。

该异常也内置了默认异常处理器。

覆盖默认异常处理器时需要导入 `RequestValidationError`，并用 `@app.excption_handler(RequestValidationError)` 装饰异常处理器。

这样，异常处理器就可以接收 `Request` 与异常。

访问 `/items/foo`，可以看到默认的 JSON 错误信息：

```json
{
    "detail": [
        {
            "loc": [
                "path",
                "item_id"
            ],
            "msg": "value is not a valid integer",
            "type": "type_error.integer"
        }
    ]
}
```

被替换为了以下文本格式的错误信息：

```
1 validation error
path -> item_id
  value is not a valid integer (type=type_error.integer)
```

#### 覆盖 `HTTPException` 错误处理器

同理，也可以覆盖 `HTTPException` 处理器。

### 使用 `RequestValidationError` 的请求体

`RequestValidationError` 包含其接收到的无效数据请求的 `body` 。

开发时，可以用这个请求体生成日志、调试错误，并返回给用户。

```python
from fastapi import FastAPI, Request, status
from fastapi.encoders import jsonable_encoder
from fastapi.exceptions import RequestValidationError
from fastapi.responses import JSONResponse
from pydantic import BaseModel

app = FastAPI()


@app.exception_handler(RequestValidationError)
async def validation_exception_handler(request: Request, exc: RequestValidationError):
    return JSONResponse(
        status_code=status.HTTP_422_UNPROCESSABLE_ENTITY,
        content=jsonable_encoder({"detail": exc.errors(), "body": exc.body}),
    )


class Item(BaseModel):
    title: str
    size: int


@app.post("/items/")
async def create_item(item: Item):
    return item
```

现在试着发送一个无效的 `item`，例如：

```
{
  "title": "towel",
  "size": "XL"
}
```

收到的响应包含 `body` 信息，并说明数据是无效的：

```
{
  "detail": [
    {
      "loc": [
        "body",
        "size"
      ],
      "msg": "value is not a valid integer",
      "type": "type_error.integer"
    }
  ],
  "body": {
    "title": "towel",
    "size": "XL"
  }
}
```



## 异步支持

FastAPI 支持异步请求处理：

```python
@app.get("/async-example")
async def read_async_data():
    data = await some_async_function()
    return {"data": data}
```

# 高级功能

## 依赖注入

FastAPI 的依赖注入系统可以简化代码并提高可重用性：

```python
from fastapi import Depends

def common_parameters(q: str = None, skip: int = 0, limit: int = 100):
    return {"q": q, "skip": skip, "limit": limit}

@app.get("/items/")
def read_items(commons: dict = Depends(common_parameters)):
    return commons
```

## 中间件

中间件可以在请求和响应的生命周期中执行额外操作：

```python
@app.middleware("http")
async def add_process_time_header(request: Request, call_next):
    start_time = time.time()
    response = await call_next(request)
    process_time = time.time() - start_time
    response.headers["X-Process-Time"] = str(process_time)
    return response
```

## 异常处理

自定义异常处理可以返回特定的错误响应：

```python
from fastapi import HTTPException

@app.get("/items/{item_id}")
def read_item(item_id: int):
    if item_id not in items:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"item_id": item_id}
```



## 安全性

FastAPI 支持多种安全机制，如 OAuth2 和 JWT：

```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.get("/users/me")
def read_current_user(token: str = Depends(oauth2_scheme)):
    return {"token": token}
```

## 调试与测试

### 调试

使用 `uvicorn` 的 `--reload` 参数可以启用热重载，方便调试：

```bash
uvicorn main:app --reload
```

### 测试

FastAPI 支持通过 `TestClient` 编写测试：

```python
from fastapi.testclient import TestClient

client = TestClient(app)

def test_read_root():
    response = client.get("/")
    assert response.status_code == 200
    assert response.json() == {"message": "Hello, FastAPI!"}
```

# 部署 FastAPI 应用

FastAPI 应用可以通过 ASGI 服务器（如 Uvicorn、Hypercorn）部署到生产环境：

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

## 使用 Docker 部署

创建 `Dockerfile`：

```dockerfile
FROM python:3.9

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

构建并运行容器：

```bash
docker build -t fastapi-app .
docker run -d -p 8000:8000 fastapi-app
```

# 总结

FastAPI 是一个高性能、易用且功能丰富的 Python Web 框架，适合构建现代 API。它的自动文档生成、类型安全和异步支持使其成为开发者的首选工具。通过本文的介绍，你可以快速上手 FastAPI 并开始构建自己的 API 应用。