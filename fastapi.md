# FastAPI

**文章参考**：[FastAPI官方文档](https://fastapi.tiangolo.com/)，[Oauth2](https://juejin.cn/post/6859572307505971213)

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

#### 更新数据

##### 用 `PUT` 更新数据

更新数据请用 [HTTP `PUT`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/PUT) 操作。

把输入数据转换为以 JSON 格式存储的数据（比如，使用 NoSQL 数据库时），可以使用 `jsonable_encoder`。例如，把 `datetime` 转换为 `str`。

```python
class Item(BaseModel):
    name: Union[str, None] = None
    description: Union[str, None] = None
    price: Union[float, None] = None
    tax: float = 10.5
    tags: List[str] = []

items = {
    "foo": {"name": "Foo", "price": 50.2},
    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},
    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []},
}

@app.put("/items/{item_id}", response_model=Item)
async def update_item(item_id: str, item: Item):
    update_item_encoded = jsonable_encoder(item)
    items[item_id] = update_item_encoded
    return update_item_encoded
```

`PUT` 用于接收替换现有数据的数据。

##### 关于更新数据的警告

用 `PUT` 把数据项 `bar` 更新为以下内容时：

```
{
    "name": "Barz",
    "price": 3,
    "description": None,
}
```

因为上述数据未包含已存储的属性 `"tax": 20.2`，新的输入模型会把 `"tax": 10.5` 作为默认值。

因此，本次操作把 `tax` 的值「更新」为 `10.5`。

##### 用 `PATCH` 进行部分更新

[HTTP `PATCH`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/PATCH) 操作用于更新 *部分* 数据。

即，只发送要更新的数据，其余数据保持不变。

> `PATCH` 没有 `PUT` 知名，也怎么不常用。
>
> 很多人甚至只用 `PUT` 实现部分更新。
>
> **FastAPI** 对此没有任何限制，可以**随意**互换使用这两种操作。

### 路径操作配置

#### `status_code` 状态码

`status_code` 用于定义*路径操作*响应中的 HTTP 状态码。

可以直接传递 `int` 代码， 比如 `404`。

如果记不住数字码的涵义，也可以用 `status` 的快捷常量

```python
@app.post("/items/", response_model=Item, status_code=status.HTTP_201_CREATED)
async def create_item(item: Item):
    return item
```

#### `tags` 参数

`tags` 参数的值是由 `str` 组成的 `list` （一般只有一个 `str` ），`tags` 用于为*路径操作*添加标签：

```python
@app.post("/items/", response_model=Item, tags=["items"])
async def create_item(item: Item):
    return item
```

OpenAPI 概图会自动添加标签，供 API 文档接口使用：

#### `summary` 和 `description` 参数

路径装饰器还支持 `summary` 和 `description` 这两个参数：

```python
@app.post(
    "/items/",
    response_model=Item,
    summary="Create an item",
    description="Create an item with all the information, name, description, price, tax and a set of unique tags",
)
async def create_item(item: Item):
    return item
```

#### 文档字符串 `docstring`

描述内容比较长且占用多行时，可以在函数的 docstring 中声明*路径操作*的描述，**FastAPI** 支持从文档字符串中读取描述内容。

文档字符串支持 [Markdown](https://en.wikipedia.org/wiki/Markdown)，能正确解析和显示 Markdown 的内容，但要注意文档字符串的缩进。

```python
@app.post("/items/", response_model=Item, summary="Create an item")
async def create_item(item: Item):
    """
    Create an item with all the information:

    - **name**: each item must have a name
    - **description**: a long description
    - **price**: required
    - **tax**: if the item doesn't have tax, you can omit this
    - **tags**: a set of unique tag strings for this item
    """
    return item
```

#### 响应描述

`response_description` 参数用于定义响应的描述说明：

```python
@app.post(
    "/items/",
    response_model=Item,
    summary="Create an item",
    response_description="The created item",
)
async def create_item(item: Item):
    """
    Create an item with all the information:

    - **name**: each item must have a name
    - **description**: a long description
    - **price**: required
    - **tax**: if the item doesn't have tax, you can omit this
    - **tags**: a set of unique tag strings for this item
    """
    return item
```

> 注意，`response_description` 只用于描述响应，`description` 一般则用于描述*路径操作*。



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





# 高级功能

## JSON 兼容编码器

在某些情况下，您可能需要将数据类型（如Pydantic模型）转换为与JSON兼容的数据类型（如`dict`、`list`等）。

比如，如果您需要将其存储在数据库中。

对于这种要求， **FastAPI**提供了`jsonable_encoder()`函数。

### 使用`jsonable_encoder`

让我们假设你有一个数据库名为`fake_db`，它只能接收与JSON兼容的数据。

例如，它不接收`datetime`这类的对象，因为这些对象与JSON不兼容。

因此，`datetime`对象必须将转换为包含[ISO格式化](https://en.wikipedia.org/wiki/ISO_8601)的`str`类型对象。

同样，这个数据库也不会接收Pydantic模型（带有属性的对象），而只接收`dict`。

对此你可以使用`jsonable_encoder`。

它接收一个对象，比如Pydantic模型，并会返回一个JSON兼容的版本：

```python
from datetime import datetime

from fastapi import FastAPI
from fastapi.encoders import jsonable_encoder
from pydantic import BaseModel

fake_db = {}


class Item(BaseModel):
    title: str
    timestamp: datetime
    description: str | None = None


app = FastAPI()


@app.put("/items/{id}")
def update_item(id: str, item: Item):
    json_compatible_item_data = jsonable_encoder(item)
    fake_db[id] = json_compatible_item_data
```

在这个例子中，它将Pydantic模型转换为`dict`，并将`datetime`转换为`str`。

调用它的结果后就可以使用Python标准编码中的[`json.dumps()`](https://docs.python.org/3/library/json.html#json.dumps)。

这个操作不会返回一个包含JSON格式（作为字符串）数据的庞大的`str`。它将返回一个Python标准数据结构（例如`dict`），其值和子值都与JSON兼容。





## 异步支持

FastAPI 支持异步请求处理：

```python
@app.get("/async-example")
async def read_async_data():
    data = await some_async_function()
    return {"data": data}
```



## 依赖注入

FastAPI 提供了简单易用，但功能强大的**依赖注入**系统。

这个依赖系统设计的简单易用，可以让开发人员轻松地把组件集成至 **FastAPI**。

依赖注入常用于以下场景：

- 共享业务逻辑（复用相同的代码逻辑）
- 共享数据库连接
- 实现安全、验证、角色权限
- 等……

上述场景均可以使用**依赖注入**，将**代码重复最小化**。

**依赖项**是 FastAPI 提供的一种机制，用于在请求处理之前执行一些通用的逻辑。依赖项可以是一个函数、一个类或者一个可调用对象，它会在请求处理之前被调用。

### 函数依赖项

依赖项就是一个函数，且可以使用与*路径操作函数*相同的参数：

```python
from typing import Union

from fastapi import Depends, FastAPI # 导入 `Depends`

app = FastAPI()


async def common_parameters(
    q: Union[str, None] = None, skip: int = 0, limit: int = 100
):
    return {"q": q, "skip": skip, "limit": limit}

# 声明依赖项
@app.get("/items/")
async def read_items(commons: dict = Depends(common_parameters)):
    return commons


@app.get("/users/")
async def read_users(commons: dict = Depends(common_parameters)):
    return commons
```

依赖项函数的形式和结构与*路径操作函数*一样。

因此，可以把依赖项当作**没有「装饰器」**（即，没有 `@app.get("/some-path")` ）**的路径操作函数**。

你只能传给 Depends **一个参数**。且该参数必须是**可调用对象**，比如函数。该函数接收的参数和*路径操作函数*的参数一样。

### 简单用法

观察一下就会发现，只要*路径* 和*操作*匹配，就可以使用声明的路径操作函数。然后，**FastAPI** 会用正确的参数调用函数，并提取请求中的数据。

实际上，所有（或大多数）网络框架的工作方式都是这样的。

开发人员永远都不需要直接调用这些函数，这些函数是由框架调用的。

通过依赖注入系统，只要告诉 **FastAPI** *路径操作函数* 还要「依赖」其他在*路径操作函数*之前执行的内容，**FastAPI** 就会执行函数代码，并「注入」函数返回的结果。

其他与「依赖注入」概念相同的术语为：

- 资源（Resource）
- 提供方（Provider）
- 服务（Service）
- 可注入（Injectable）
- 组件（Component）

虽然，**层级式依赖注入系统**的定义与使用十分简单，但它却非常强大。

比如，可以定义依赖其他依赖项的依赖项。

最后，依赖项层级树构建后，**依赖注入系统**会处理所有依赖项及其子依赖项，并为每一步操作提供（注入）结果。

比如，下面有 4 个 API 路径操作（*端点*）：

- `/items/public/`
- `/items/private/`
- `/users/{user_id}/activate`
- `/items/pro/`

开发人员可以使用依赖项及其子依赖项为这些路径操作添加不同的权限：

![image-20250606160754402](images/image-20250606160754402.png)

### 类依赖项

```python
from fastapi import Depends, FastAPI

app = FastAPI()


fake_items_db = [{"item_name": "Foo"}, {"item_name": "Bar"}, {"item_name": "Baz"}]


class CommonQueryParams:
    def __init__(self, q: str | None = None, skip: int = 0, limit: int = 100): # 创建类实例的 __init__ 方法
        self.q = q
        self.skip = skip
        self.limit = limit


@app.get("/items/")
async def read_items(commons: CommonQueryParams = Depends(CommonQueryParams)):
    response = {}
    if commons.q:
        response.update({"q": commons.q})
    items = fake_items_db[commons.skip : commons.skip + commons.limit]
    response.update({"items": items})
    return response
```

#### 类型注解 vs `Depends`

注意，我们在上面的代码中编写了两次`CommonQueryParams`：

```python
commons: CommonQueryParams = Depends(CommonQueryParams)
```

最后的 `CommonQueryParams`:

```
... = Depends(CommonQueryParams)
```

...实际上是 **Fastapi** 用来知道依赖项是什么的。

FastAPI 将从依赖项中提取声明的参数，这才是 FastAPI 实际调用的。

------

在本例中，第一个 `CommonQueryParams` ：

```
commons: CommonQueryParams ...
```

...对于 **FastAPI** 没有任何特殊的意义。FastAPI 不会使用它进行数据转换、验证等 (因为对于这，它使用 `= Depends(CommonQueryParams)`)。

你实际上可以只这样编写:

```python
commons = Depends(CommonQueryParams)
```

但是声明类型是被鼓励的，因为那样你的编辑器就会知道将传递什么作为参数 `commons` ，然后它可以帮助你完成代码，类型检查，等等。所以你该这样简写：

```python
commons: CommonQueryParams = Depends()
```

### 子依赖项

FastAPI 支持创建含**子依赖项**的依赖项。

并且，可以按需声明任意**深度**的子依赖项嵌套层级。

**FastAPI** 负责处理解析不同深度的子依赖项。

```python
from typing import Union

from fastapi import Cookie, Depends, FastAPI

app = FastAPI()


def query_extractor(q: Union[str, None] = None): # 第一层依赖项(子依赖项)
    return q


def query_or_cookie_extractor(
    q: str = Depends(query_extractor),
    last_query: Union[str, None] = Cookie(default=None),
): # 第二层依赖项
    if not q:
        return last_query
    return q


@app.get("/items/")
async def read_query(query_or_default: str = Depends(query_or_cookie_extractor)):
    return {"q_or_cookie": query_or_default}
```

![image-20250606170825859](images/image-20250606170825859.png)

#### 多次使用同一个依赖项

如果在同一个*路径操作* 多次声明了同一个依赖项，例如，多个依赖项共用一个子依赖项，**FastAPI** 在处理同一请求时，只调用一次该子依赖项。

FastAPI 不会为同一个请求多次调用同一个依赖项，而是把依赖项的返回值进行「缓存」，并把它传递给同一请求中所有需要使用该返回值的「依赖项」。

在高级使用场景中，如果**不想使用「缓存」值**，而是为需要在同一请求的每一步操作（多次）中都实际调用依赖项，可以把 `Depends` 的参数 `use_cache` 的值设置为 `False` :

```python
async def needy_dependency(fresh_value: str = Depends(get_value, use_cache=False)):
    return {"fresh_value": fresh_value}
```

### 路径操作装饰器依赖项

有时，我们并不需要在*路径操作函数*中使用依赖项的返回值。

或者说，**有些依赖项不返回值**，但仍要执行或解析该依赖项。

对于这种情况，不必在声明*路径操作函数*的参数时使用 `Depends`，而是可以在*路径操作装饰器*中添加一个由 `dependencies` 组成的 `list`。

```python
from fastapi import Depends, FastAPI, Header, HTTPException

app = FastAPI()

async def verify_token(x_token: str = Header()):
    if x_token != "fake-super-secret-token":
        raise HTTPException(status_code=400, detail="X-Token header invalid")

async def verify_key(x_key: str = Header()):
    if x_key != "fake-super-secret-key":
        raise HTTPException(status_code=400, detail="X-Key header invalid")
    return x_key

@app.get("/items/", dependencies=[Depends(verify_token), Depends(verify_key)])
async def read_items():
    return [{"item": "Foo"}, {"item": "Bar"}]
```

路径操作装饰器依赖项（以下简称为**“路径装饰器依赖项”**）的执行或解析方式和普通依赖项一样，但就算这些依赖项会返回值，它们的**值也不会传递给*路径操作函数***。

### 全局依赖项

有时，我们要为整个应用添加依赖项。

通过与定义[*路径装饰器依赖项*](https://fastapi.tiangolo.com/zh/tutorial/dependencies/dependencies-in-path-operation-decorators/) 类似的方式，可以把依赖项添加至整个 `FastAPI` 应用。

这样一来，就可以为所有*路径操作*应用该依赖项：

```python
app = FastAPI(dependencies=[Depends(verify_token), Depends(verify_key)])
```

### 使用yield的依赖项

FastAPI支持在完成后执行一些额外步骤的依赖项.

为此，你需要使用 `yield` 而不是 `return`，然后再编写这些额外的步骤（代码）。

> 确保在每个依赖中只使用一次 `yield`。

例如，你可以使用这种方式创建一个数据库会话，并在完成后关闭它。

在发送响应之前，只会执行 `yield` 语句及之前的代码：

```python
async def get_db():
    db = DBSession()
    try:
        yield db
    finally:
        db.close()
```

同样，你可以混合使用带有 `yield` 或 `return` 的依赖。

你也可以声明一个依赖于多个带有 `yield` 的依赖，等等。

![image-20250606190643852](images/image-20250606190643852.png)

…没学懂



## 安全性

FastAPI 支持多种安全机制，如 OAuth2 和 JWT。

### OAuth2

OAuth2是一个规范，它定义了几种处理身份认证和授权的方法。

它是一个相当广泛的规范，涵盖了一些复杂的使用场景。

它包括了使用「第三方」进行身份认证的方法。

这就是所有带有「使用 Facebook，Google，Twitter，GitHub 登录」的系统背后所使用的机制。

#### OAuth 1

有一个 OAuth 1，它与 OAuth2 完全不同，并且更为复杂，因为它直接包含了有关如何加密通信的规范。

如今它已经不是很流行，没有被广泛使用了。

OAuth2 没有指定如何加密通信，它期望你为应用程序使用 **HTTPS** 进行通信。

### 简单的验证

#### 创建 `main.py`

```python
from typing import Annotated

from fastapi import Depends, FastAPI
from fastapi.security import OAuth2PasswordBearer

app = FastAPI()

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")


@app.get("/items/")
async def read_items(token: Annotated[str, Depends(oauth2_scheme)]):
    return {"token": token}
```

运行并打开文档，点击 **Authorize** 按钮，弹出授权表单，输入 `username` 与 `password` 及其它可选字段

![hhh](images/image01.png)

#### 密码流

现在，我们回过头来介绍这段代码的原理。

`Password` **流**是 OAuth2 定义的，用于处理安全与身份验证的方式（**流**）。

OAuth2 的设计目标是为了让后端或 API 独立于服务器验证用户身份。

但在本例中，**FastAPI** 应用会处理 API 与身份验证。

下面，我们来看一下简化的运行流程：

- 用户在前端输入 `username` 与`password`，并点击**回车**
- （用户浏览器中运行的）前端把 `username` 与`password` 发送至 API 中指定的 URL（使用 `tokenUrl="token"` 声明）
- API 检查 `username` 与`password`，并用令牌（`Token`） 响应（即，承载者令牌 “Bearer Token”）：
- 令牌只是用于验证用户的**字符串**
- 一般来说，令牌会在一段时间后过期
    - 过时后，用户要再次登录
    - 这样一来，就算令牌被人窃取，风险也较低。因为它与永久密钥不同，**在绝大多数情况下**不会长期有效
- **前端临时将令牌存储在某个位置**
- 用户点击前端，前往前端应用的其它部件
- 前端需要从 API 中提取更多数据：
    - 为指定的端点（Endpoint）进行身份验证
    - 因此，用 API 验证身份时，要发送值为 `Bearer` + 令牌的请求头 `Authorization`（即，`Authorization: Bearer <token>`）
    - 假如令牌为 `foobar`，`Authorization` 请求头就是： `Bearer foobar`

### 获取当前用户

创建 Pydantic 用户模型。

```python
from typing import Union

from fastapi import Depends, FastAPI
from fastapi.security import OAuth2PasswordBearer
from pydantic import BaseModel

app = FastAPI()

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")


class User(BaseModel):
    username: str
    email: Union[str, None] = None
    full_name: Union[str, None] = None
    disabled: Union[bool, None] = None

# fake_decode_token（伪）工具函数 ，该函数接收 str 类型的令牌，并返回 Pydantic 的 User 模型
def fake_decode_token(token):
    return User(
        username=token + "fakedecoded", email="john@example.com", full_name="John Doe"
    )


async def get_current_user(token: str = Depends(oauth2_scheme)): # get_current_user 依赖项
    user = fake_decode_token(token)
    return user


@app.get("/users/me")
async def read_users_me(current_user: User = Depends(get_current_user)):
    return current_user
```

### OAuth2 实现简单的 Password 和 Bearer 验证

首先，导入 **`OAuth2PasswordRequestForm`**，然后，在 `/token` *路径操作* 中，用 `Depends` 把该类作为依赖项。

```python
from typing import Union

from fastapi import Depends, FastAPI, HTTPException, status
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
from pydantic import BaseModel

fake_users_db = {
    "johndoe": {
        "username": "johndoe",
        "full_name": "John Doe",
        "email": "johndoe@example.com",
        "hashed_password": "fakehashedsecret",
        "disabled": False,
    },
    "alice": {
        "username": "alice",
        "full_name": "Alice Wonderson",
        "email": "alice@example.com",
        "hashed_password": "fakehashedsecret2",
        "disabled": True,
    },
}

app = FastAPI()


def fake_hash_password(password: str):
    return "fakehashed" + password


oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")


class User(BaseModel):
    username: str
    email: Union[str, None] = None
    full_name: Union[str, None] = None
    disabled: Union[bool, None] = None


class UserInDB(User):
    hashed_password: str


def get_user(db, username: str):
    if username in db:
        user_dict = db[username]
        return UserInDB(**user_dict)


def fake_decode_token(token):
    # This doesn't provide any security at all
    # Check the next version
    user = get_user(fake_users_db, token)
    return user


async def get_current_user(token: str = Depends(oauth2_scheme)):
    user = fake_decode_token(token)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Invalid authentication credentials",
            headers={"WWW-Authenticate": "Bearer"},
        )
    return user


async def get_current_active_user(current_user: User = Depends(get_current_user)):
    if current_user.disabled:
        raise HTTPException(status_code=400, detail="Inactive user")
    return current_user


@app.post("/token")
async def login(form_data: OAuth2PasswordRequestForm = Depends()):
    user_dict = fake_users_db.get(form_data.username)
    if not user_dict:
        raise HTTPException(status_code=400, detail="Incorrect username or password")
    user = UserInDB(**user_dict)
    hashed_password = fake_hash_password(form_data.password)
    if not hashed_password == user.hashed_password:
        raise HTTPException(status_code=400, detail="Incorrect username or password")

    return {"access_token": user.username, "token_type": "bearer"}


@app.get("/users/me")
async def read_users_me(current_user: User = Depends(get_current_active_user)):
    return current_user
```

#### 1. 客户端请求令牌

客户端通过向 `tokenUrl` 发送 POST 请求来获取令牌。请求通常包含以下参数：

- `username`: 用户的用户名。

- `password`: 用户的密码。

- `scope`: 常用于声明指定安全权限。

    > 虽然表单字段的名称是 `scope`（单数），但实际上，它是以空格分隔的，由多个**scope**组成的长字符串。

    - 常见用例为，`users:read` 或 `users:write`
    - 脸书和 Instagram 使用 `instagram_basic`
    - 谷歌使用 `https://www.googleapis.com/auth/drive`

- `grant_type`: 指定授权类型，对于密码模式，通常是 `password`。
- `client_id` 和 `client_secret`（可选）: 如果客户端需要身份验证，可以提供这些参数。

```http
POST /token HTTP/1.1
Host: yourdomain.com
Content-Type: application/x-www-form-urlencoded

grant_type=password&username=johndoe&password=secret
```

#### 2. 授权服务器响应

如果授权服务器验证成功，它会返回一个 JSON 响应，包含访问令牌和其他信息：

```json
{
    "access_token": "example_access_token",
    "token_type": "bearer",
    "expires_in": 3600,
    "refresh_token": "example_refresh_token"
}
```

如果验证失败，授权服务器会返回一个错误响应：

```json
{
    "error": "invalid_grant",
    "error_description": "The provided authorization grant is invalid, expired, or revoked"
}
```

#### 3. FastAPI 的依赖项处理

在 FastAPI 中，`OAuth2PasswordBearer` 依赖项会自动处理令牌的验证逻辑。它会从请求的 `Authorization` 头部中提取令牌，并调用指定的验证函数（如 `fake_decode_token`）来**验证令牌的有效性**。

> 使之仅在当前用户为激活状态时，才能获取 `current_user`。
>
> 为此，要再创建一个依赖项 `get_current_active_user`，此依赖项以 `get_current_user` 依赖项为基础。

如果令牌无效，会抛出一个 `HTTPException`，并返回 401 状态码。

> 如果用户不存在，或状态为未激活，这两个依赖项都会返回 HTTP 错误。

```python
async def get_current_user(token: str = Depends(oauth2_scheme)):
    user = fake_decode_token(token)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Invalid authentication credentials",
            headers={"WWW-Authenticate": "Bearer"},
        )
    return user

async def get_current_active_user(current_user: User = Depends(get_current_user)):
    if current_user.disabled:
        raise HTTPException(status_code=400, detail="Inactive user")
    return current_user
```

使用 `/users/me` 路径的 `GET` 操作。

可以提取如下当前用户数据：

```json
{
  "username": "johndoe",
  "email": "johndoe@example.com",
  "full_name": "John Doe",
  "disabled": false,
  "hashed_password": "fakehashedsecret"
}
```

### OAuth2 实现密码哈希与 Bearer JWT 令牌验证

```python
from datetime import datetime, timedelta, timezone
from typing import Annotated

import jwt
from fastapi import Depends, FastAPI, HTTPException, status
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
from jwt.exceptions import InvalidTokenError
from passlib.context import CryptContext
from pydantic import BaseModel

# 配置 JWT
# to get a string like this run:
# 生成安全的随机密钥: openssl rand -hex 32
SECRET_KEY = "09d25e094faa6ca2556c818166b7a9563b93f7099f6f0f4caa6cf63b88e8d3e7"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30

# 模拟数据库
fake_users_db = {
    "johndoe": {
        "username": "johndoe",
        "full_name": "John Doe",
        "email": "johndoe@example.com",
        "hashed_password": "$2b$12$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36WQoeG6Lruj3vjPGga31lW",
        "disabled": False,
    }
}

# 定义模型
class Token(BaseModel):
    access_token: str
    token_type: str

class TokenData(BaseModel):
    username: str | None = None

class User(BaseModel):
    username: str
    email: str | None = None
    full_name: str | None = None
    disabled: bool | None = None

class UserInDB(User):
    hashed_password: str

# 初始化密码上下文
pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")
# 初始化 OAuth2PasswordBearer
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

app = FastAPI()

# 密码哈希和验证
def verify_password(plain_password, hashed_password):
    return pwd_context.verify(plain_password, hashed_password)

def get_password_hash(password):
    return pwd_context.hash(password)

def get_user(db, username: str):
    if username in db:
        user_dict = db[username]
        return UserInDB(**user_dict)

def authenticate_user(fake_db, username: str, password: str):
    user = get_user(fake_db, username)
    if not user:
        return False
    if not verify_password(password, user.hashed_password):
        return False
    return user

# 生成JWT令牌
def create_access_token(data: dict, expires_delta: timedelta | None = None):
    to_encode = data.copy()
    if expires_delta:
        expire = datetime.now(timezone.utc) + expires_delta
    else:
        expire = datetime.now(timezone.utc) + timedelta(minutes=15)
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
    return encoded_jwt

# JWT令牌验证
async def get_current_user(token: Annotated[str, Depends(oauth2_scheme)]):
    credentials_exception = HTTPException(
        status_code=status.HTTP_401_UNAUTHORIZED,
        detail="Could not validate credentials",
        headers={"WWW-Authenticate": "Bearer"},
    )
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username = payload.get("sub")
        if username is None:
            raise credentials_exception
        token_data = TokenData(username=username)
    except InvalidTokenError:
        raise credentials_exception
    user = get_user(fake_users_db, username=token_data.username)
    if user is None:
        raise credentials_exception
    return user

async def get_current_active_user(
    current_user: Annotated[User, Depends(get_current_user)],
):
    if current_user.disabled:
        raise HTTPException(status_code=400, detail="Inactive user")
    return current_user

# 令牌端点
@app.post("/token")
async def login_for_access_token(
    form_data: Annotated[OAuth2PasswordRequestForm, Depends()],
) -> Token:
    user = authenticate_user(fake_users_db, form_data.username, form_data.password)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect username or password",
            headers={"WWW-Authenticate": "Bearer"},
        )
    access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
    access_token = create_access_token(
        data={"sub": user.username}, expires_delta=access_token_expires
    )
    return Token(access_token=access_token, token_type="bearer")

# 保护的路由
@app.get("/users/me/", response_model=User)
async def read_users_me(
    current_user: Annotated[User, Depends(get_current_active_user)],
):
    return current_user

@app.get("/users/me/items/")
async def read_own_items(
    current_user: Annotated[User, Depends(get_current_active_user)],
):
    return [{"item_id": "Foo", "owner": current_user.username}]
```

#### 实现流程

1. **密码哈希**：使用 `passlib` 的 `CryptContext` 对密码进行哈希处理，确保存储在数据库中的密码是安全的。
2. **JWT 令牌**：使用 `PyJWT` 生成和验证 JWT 令牌，令牌中包含用户信息和过期时间。
3. **OAuth2PasswordBearer**：使用 FastAPI 的 `OAuth2PasswordBearer` 来处理令牌验证，确保只有持有有效令牌的用户才能访问受保护的路由。
4. **令牌端点**：提供一个 `/token` 端点，用户可以通过用户名和密码获取 JWT 令牌。
5. **保护的路由**：使用依赖项来验证用户是否已通过 JWT 令牌认证，从而保护特定的路由。

#### JWT 简介

JWT 即**JSON 网络令牌**（JSON Web Tokens）。

JWT 是一种将 JSON 对象编码为没有空格，且难以理解的长字符串的标准。JWT 的内容如下所示：

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

JWT 字符串没有加密，任何人都能用它恢复原始信息。

但 JWT 使用了签名机制。接受令牌时，可以用签名校验令牌。

使用 JWT 创建**有效期为一周的令牌**。第二天，用户持令牌再次访问时，仍为登录状态。

令牌于一周后过期，届时，用户身份验证就会失败。只有再次登录，才能获得新的令牌。如果用户（或第三方）篡改令牌的过期时间，因为签名不匹配会导致身份验证失败。

如需深入了解 JWT 令牌，了解它的工作方式，请参阅 [https://jwt.io](https://jwt.io/)。

> 安装 **`PyJWT`**，在 Python 中生成和校验 JWT 令牌：

```
pip install pyjwt
```

##### JWT `sub` 的技术细节

JWT 规范还包括 `sub` 键，值是令牌的主题。

该键是可选的，但要把用户标识放在这个键里，所以本例使用了该键。

除了识别用户与许可用户在 API 上直接执行操作之外，JWT 还可能用于其它事情。

例如，识别**汽车**或**博客**。

接着，为实体添加权限，比如**驾驶**（汽车）或**编辑**（博客）。

然后，把 JWT 令牌交给用户（或机器人），他们就可以执行驾驶汽车，或编辑博客等操作。无需注册账户，只要有 API 生成的 JWT 令牌就可以。

同理，JWT 可以用于更复杂的场景。

在这些情况下，多个实体的 ID 可能是相同的，以 ID `foo` 为例，用户的 ID 是 `foo`，车的 ID 是 `foo`，博客的 ID 也是 `foo`。

为了避免 ID 冲突，在给用户创建 JWT 令牌时，可以为 `sub` 键的值加上前缀，例如 `username:`。因此，在本例中，`sub` 的值可以是：`username:johndoe`。

注意，划重点，`sub` 键在整个应用中应该只有一个唯一的标识符，而且应该是字符串。

#### 密码哈希

**哈希**是指把特定内容（本例中为密码）转换为乱码形式的字节序列（其实就是字符串）。

每次传入完全相同的内容时（比如，完全相同的密码），返回的都是完全相同的乱码。

但这个乱码无法转换回传入的密码。

**为什么使用密码哈希**

原因很简单，假如数据库被盗，窃贼无法获取用户的明文密码，得到的只是哈希值。

这样一来，窃贼就无法在其它应用中使用窃取的密码（要知道，很多用户在所有系统中都使用相同的密码，风险超大）。

> 安装 **`passlib`**，处理密码哈希的 Python 包，支持很多安全哈希算法及配套工具：

```
# 推荐的算法是 Bcrypt, 安装附带 Bcrypt 的 PassLib
pip install passlib[bcrypt]
```



## 中间件

中间件可以在**请求和响应的生命周期中**执行**额外操作**：

- 它接收你的应用程序的每一个**请求**.
- 然后它可以对这个**请求**做一些事情或者执行任何需要的代码.
- 然后它将**请求**传递给应用程序的其他部分 (通过某种*路径操作*).
- 然后它获取应用程序生产的**响应** (通过某种*路径操作*).
- 它可以对该**响应**做些什么或者执行任何需要的代码.
- 然后它返回这个 **响应**.

### 创建中间件

要创建中间件你可以在函数的顶部使用装饰器 `@app.middleware("http")`.

中间件参数接收如下参数:

- `request`.
- 一个函数 `call_next` 它将接收 `request` 作为参数.
    - 这个函数将 `request` 传递给相应的 *路径操作*.
    - 然后它将返回由相应的*路径操作*生成的 `response`.
- 然后你可以在返回 `response` 前进一步修改它.

```python
import time
from fastapi import FastAPI, Request

app = FastAPI()

@app.middleware("http")
async def add_process_time_header(request: Request, call_next):
    start_time = time.perf_counter()
    response = await call_next(request)
    process_time = time.perf_counter() - start_time
    response.headers["X-Process-Time"] = str(process_time)
    return response
```



### CORS（跨域资源共享）

[CORS 或者「跨域资源共享」](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) 指浏览器中运行的前端拥有与后端通信的 JavaScript 代码，而后端处于与前端不同的**「源」**的情况。

#### 源

源是协议（`http`，`https`）、域（`myapp.com`，`localhost`，`localhost.tiangolo.com`）以及端口（`80`、`443`、`8080`）的组合。

因此，这些都是不同的源：

- `http://localhost`
- `https://localhost`
- `http://localhost:8080`

即使它们都在 `localhost` 中，但是它们使用不同的协议或者端口，所以它们都是不同的「源」。

#### 步骤

假设你的浏览器中有一个前端运行在 `http://localhost:8080`，并且它的 JavaScript 正在尝试与运行在 `http://localhost` 的后端通信（因为我们没有指定端口，浏览器会采用默认的端口 `80`）。

然后，浏览器会向后端发送一个 HTTP `OPTIONS` 请求，如果后端发送适当的 headers 来授权来自这个不同源（`http://localhost:8080`）的通信，浏览器将允许前端的 JavaScript 向后端发送请求。

为此，后端必须有一个「允许的源」列表。

在这种情况下，它必须包含 `http://localhost:8080`，前端才能正常工作。

#### 通配符

也可以使用 `"*"`（一个「通配符」）声明这个列表，表示全部都是允许的。

但这仅允许某些类型的通信，不包括所有涉及凭据的内容：像 Cookies 以及那些使用 Bearer 令牌的授权 headers 等。

因此，为了一切都能正常工作，最好显式地指定允许的源。

#### 使用 `CORSMiddleware`

你可以在 **FastAPI** 应用中使用 `CORSMiddleware` 来配置它。

- 导入 `CORSMiddleware`。
- 创建一个允许的源列表（由字符串组成）。
- 将其作为「中间件」添加到你的 **FastAPI** 应用中。

你也可以指定后端是否允许：

- 凭证（授权 headers，Cookies 等）。
- 特定的 HTTP 方法（`POST`，`PUT`）或者使用通配符 `"*"` 允许所有方法。
- 特定的 HTTP headers 或者使用通配符 `"*"` 允许所有 headers。

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

origins = [
    "http://localhost.tiangolo.com",
    "https://localhost.tiangolo.com",
    "http://localhost",
    "http://localhost:8080",
]

app.add_middleware(
    CORSMiddleware,
    allow_origins=origins,
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)


@app.get("/")
async def main():
    return {"message": "Hello World"}
```

默认情况下，这个 `CORSMiddleware` 实现所使用的默认参数较为保守，所以你需要显式地启用特定的源、方法或者 headers，以便浏览器能够在跨域上下文中使用它们。

支持以下参数：

- `allow_origins` - 一个允许跨域请求的源列表。例如 `['https://example.org', 'https://www.example.org']`。你可以使用 `['*']` 允许任何源。
- `allow_origin_regex` - 一个正则表达式字符串，匹配的源允许跨域请求。例如 `'https://.*\.example\.org'`。
- `allow_methods` - 一个允许跨域请求的 HTTP 方法列表。默认为 `['GET']`。你可以使用 `['*']` 来允许所有标准方法。
- `allow_headers` - 一个允许跨域请求的 HTTP 请求头列表。默认为 `[]`。你可以使用 `['*']` 允许所有的请求头。`Accept`、`Accept-Language`、`Content-Language` 以及 `Content-Type` 请求头总是允许 CORS 请求。
- `allow_credentials` - 指示跨域请求支持 cookies。默认是 `False`。另外，允许凭证时 `allow_origins` 不能设定为 `['*']`，必须指定源。
- `expose_headers` - 指示可以被浏览器访问的响应头。默认为 `[]`。
- `max_age` - 设定浏览器缓存 CORS 响应的最长时间，单位是秒。默认为 `600`。

中间件响应两种特定类型的 HTTP 请求……

##### CORS 预检请求

这是些带有 `Origin` 和 `Access-Control-Request-Method` 请求头的 `OPTIONS` 请求。

在这种情况下，中间件将拦截传入的请求并进行响应，出于提供信息的目的返回一个使用了适当的 CORS headers 的 `200` 或 `400` 响应。

##### 简单请求

任何带有 `Origin` 请求头的请求。在这种情况下，中间件将像平常一样传递请求，但是在响应中包含适当的 CORS headers。



# 大型应用

如果你正在开发一个应用程序或 Web API，很少会将所有的内容都放在一个文件中。

**FastAPI** 提供了一个方便的工具，可以在保持所有灵活性的同时构建你的应用程序。

> 这将相当于 Flask 的 Blueprints

## 多个文件

假设你的文件结构如下：

```
.
├── app
│   ├── __init__.py
│   ├── main.py
│   ├── dependencies.py
│   └── routers
│   │   ├── __init__.py
│   │   ├── items.py
│   │   └── users.py
│   └── internal
│       ├── __init__.py
│       └── admin.py
```

> 上面有几个 `__init__.py` 文件：每个目录或子目录中都有一个。
>
> 这就是能将代码从一个文件导入到另一个文件的原因。
>
> 例如，在 `app/main.py` 中，你可以有如下一行：
>
> ```python
> from app.routers import items
> ```

![img](https://fastapi.tiangolo.com/img/tutorial/bigger-applications/package.drawio.svg)

带有注释的同一文件结构：

```
.
├── app                  # 「app」是一个 Python 包
│   ├── __init__.py      # 这个文件使「app」成为一个 Python 包
│   ├── main.py          # 「main」模块，例如 import app.main
│   ├── dependencies.py  # 「dependencies」模块，例如 import app.dependencies
│   └── routers          # 「routers」是一个「Python 子包」
│   │   ├── __init__.py  # 使「routers」成为一个「Python 子包」
│   │   ├── items.py     # 「items」子模块，例如 import app.routers.items
│   │   └── users.py     # 「users」子模块，例如 import app.routers.users
│   └── internal         # 「internal」是一个「Python 子包」
│       ├── __init__.py  # 使「internal」成为一个「Python 子包」
│       └── admin.py     # 「admin」子模块，例如 import app.internal.admin
```

### `routers` 子包

#### `APIRouter`

假设专门用于处理用户逻辑的文件是位于 `/app/routers/users.py` 的子模块。

你希望将与用户相关的*路径操作*与其他代码分开，以使其井井有条。

但它仍然是同一 **FastAPI** 应用程序/web API 的一部分（它是同一「Python 包」的一部分）。

你可以使用 `APIRouter` 为该模块创建*路径操作*。

##### 导入 `APIRouter`

我们知道此模块中的所有*路径操作*都有相同的：

- 路径 `prefix`：`/items`。
- `tags`：（仅有一个 `items` 标签）。
- 额外的 `responses`。
- `dependencies`：它们都需要我们创建的 `X-Token` 依赖项。

因此，我们可以将其添加到 `APIRouter` 中，而不是将其添加到每个路径操作中。

你可以导入它并通过与 `FastAPI` 类相同的方式创建一个「实例」：

```python
# app/routers/items.py
from fastapi import APIRouter, Depends, HTTPException

from ..dependencies import get_token_header # 通过 .. 对依赖项使用了相对导入

router = APIRouter(
    prefix="/items",
    tags=["items"],
    dependencies=[Depends(get_token_header)],
    responses={404: {"description": "Not found"}},
)

fake_items_db = {"plumbus": {"name": "Plumbus"}, "gun": {"name": "Portal Gun"}}

@router.get("/")
async def read_items():
    return fake_items_db

@router.get("/{item_id}")
async def read_item(item_id: str):
    if item_id not in fake_items_db:
        raise HTTPException(status_code=404, detail="Item not found")
    return {"name": fake_items_db[item_id]["name"], "item_id": item_id}

@router.put(
    "/{item_id}",
    tags=["custom"],
    responses={403: {"description": "Operation forbidden"}},
)
async def update_item(item_id: str):
    if item_id != "plumbus":
        raise HTTPException(
            status_code=403, detail="You can only update the item: plumbus"
        )
    return {"item_id": item_id, "name": "The great Plumbus"}
```

##### 相对导入

一个单点 `.`，例如：

```python
from .dependencies import get_token_header
```

表示：

- 从该模块（`app/routers/items.py` 文件）所在的同一个包（`app/routers/` 目录）开始...
- 找到 `dependencies` 模块（一个位于 `app/routers/dependencies.py` 的虚构文件）...
- 然后从中导入函数 `get_token_header`。

两个点 `..`，在`app/`里找：

```python
from ..dependencies import get_token_header
```

三个点 `...`，在`app/`的父包下找，但该父包并不存在，`app` 已经是最顶层的包



### `dependencies.py` 模块

我们了解到我们将需要一些在应用程序的好几个地方所使用的依赖项。

因此，我们将它们放在它们自己的 `dependencies` 模块（`app/dependencies.py`）中。

现在我们将使用一个简单的依赖项来读取一个自定义的 `X-Token` 请求首部：

```python
# app/dependencies.py
from fastapi import Header, HTTPException

async def get_token_header(x_token: str = Header()):
    if x_token != "fake-super-secret-token":
        raise HTTPException(status_code=400, detail="X-Token header invalid")

async def get_query_token(token: str):
    if token != "jessica":
        raise HTTPException(status_code=400, detail="No Jessica token provided")
```

### `main.py` FastAPI 主体

在这里你导入并使用 `FastAPI` 类。

这将是你的应用程序中将所有内容联结在一起的主文件。

#### 导入 `FastAPI`

你可以像平常一样导入并创建一个 `FastAPI` 类。

我们甚至可以声明[全局依赖项](https://fastapi.tiangolo.com/zh/tutorial/dependencies/global-dependencies/)，它会和每个 `APIRouter` 的依赖项组合在一起：

```python
from fastapi import Depends, FastAPI

from .dependencies import get_query_token, get_token_header
from .internal import admin
from .routers import items, users

app = FastAPI(dependencies=[Depends(get_query_token)])

# 包含 users 和 items 的 APIRouter
app.include_router(users.router)
app.include_router(items.router)
# 包含一个有自定义 prefix、tags、responses 和 dependencies 的 APIRouter
app.include_router(
    admin.router,
    prefix="/admin",
    tags=["admin"],
    dependencies=[Depends(get_token_header)],
    responses={418: {"description": "I'm a teapot"}},
)

@app.get("/")
async def root():
    return {"message": "Hello Bigger Applications!"}
```

使用 `app.include_router()`，我们可以将每个 `APIRouter` 添加到主 `FastAPI` 应用程序中。

## 后台任务

你可以定义在返回响应后运行的后台任务。

这对需要在请求之后执行的操作很有用，但客户端不必在接收响应之前等待操作完成。

包括这些例子：

- 执行操作后发送的电子邮件通知：
    - 由于连接到电子邮件服务器并发送电子邮件往往很“慢”（几秒钟），您可以立即返回响应并在后台发送电子邮件通知。
- 处理数据：
    - 例如，假设您收到的文件必须经过一个缓慢的过程，您可以返回一个"Accepted"(HTTP 202)响应并在后台处理它。

### 使用 `BackgroundTasks`

首先导入 `BackgroundTasks` 并在 *路径操作函数* 中使用类型声明 `BackgroundTasks` 定义一个参数：

```python
from typing import Annotated

from fastapi import BackgroundTasks, Depends, FastAPI

app = FastAPI()

# 创建一个任务函数
def write_log(message: str):
    with open("log.txt", mode="a") as log:
        log.write(message)

# 
def get_query(background_tasks: BackgroundTasks, q: str | None = None):
    if q:
        message = f"found query: {q}\n"
        background_tasks.add_task(write_log, message)
    return q

@app.post("/send-notification/{email}")
async def send_notification(
    email: str, background_tasks: BackgroundTasks, q: Annotated[str, Depends(get_query)]
):
    message = f"message to {email}\n"
    # 添加后台任务
    background_tasks.add_task(write_log, message)
    return {"message": "Message sent"}
```

`.add_task()` 接收以下参数：

- 在后台运行的任务函数(`write_notification`)。
- 应按顺序传递给任务函数的任意参数序列(`email`)。
- 应传递给任务函数的任意关键字参数(`message="some notification"`)。

> 该示例中，信息会在响应发出 *之后* 被写到 `log.txt` 文件。
>
> 如果请求中有查询，它将在后台任务中写入日志。
>
> 然后另一个在 *路径操作函数* 生成的后台任务会使用路径参数 `email` 写入一条信息。



## 部署

### 手动运行服务器

简而言之，使用 `fastapi run` 来运行您的 FastAPI 应用程序

```
fastapi run main.py
```

这在大多数情况下都能正常运行。😎

例如，您可以使用该命令在容器、服务器等环境中启动您的 **FastAPI** 应用。

你也可以在你的 FastAPI 应用中直接导入 `uvicorn` 并运行：

```python
# myapp.py
import uvicorn
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def root():
    a = "a"
    b = "b" + a
    return {"hello world": b}


if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

如果你这样运行：

```
python myapp.py
```

那么文件中由 Python 自动创建的内部变量 `__name__`，会将字符串 `"__main__"` 作为值。

所以，下面这部分代码才会运行：

```python
uvicorn.run(app, host="0.0.0.0", port=8000)
```

### ASGI 服务器

FastAPI 使用了一种用于构建 Python Web 框架和服务器的标准，称为 ASGI（Asynochronous Server Gateway Interface）。FastAPI 本质上是一个 ASGI Web 框架。

请确保您创建并激活一个[虚拟环境](https://fastapi.tiangolo.com/zh/virtual-environments/)，然后再安装服务器应用程序。

```
pip install "uvicorn[standard]"
```

FastAPI 应用可以通过 ASGI 服务器（如 Uvicorn、Hypercorn）部署到生产环境：

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

命令 `uvicorn main:app` 的含义如下：

- `main`：指的是 `main.py` 文件（即 Python “模块”）。

- `app`：指的是 `main.py` 文件中通过 `app = FastAPI()` 创建的对象。

它等价于以下导入语句：

```python
from main import app
```

> Uvicorn 和其他服务器支持 `--reload` 选项，该选项在开发过程中非常有用。
>
> ```bash
> uvicorn main:app --reload
> ```
>
> 但 `--reload` 选项会消耗更多资源，且相对不稳定。
>
> 它对于**开发阶段**非常有帮助，但在**生产环境**中**不应该**使用。

### 使用 Docker 部署

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

