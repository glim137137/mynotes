# Flask

**文章参考**：[Flask官方文档](https://flask.palletsprojects.com/)

[TOC]

# Flask 框架

## 介绍

Flask 是一个轻量级的 Python Web 框架，基于 Werkzeug WSGI 工具箱和 Jinja2 模板引擎。它被设计为易于扩展，核心简单但功能强大，适合从小型项目到复杂应用程序的开发。

### Flask 的特点

1. **轻量级**：Flask 核心功能简洁，没有默认的数据库、表单验证等组件，开发者可以根据需求自由选择扩展。
2. **灵活**：不强制项目结构，开发者可以按自己的方式组织代码。
3. **易扩展**：通过丰富的扩展库（如 Flask-SQLAlchemy、Flask-Login）可以轻松添加功能。
4. **开发友好**：内置开发服务器和调试器，支持热重载。
5. **文档丰富**：拥有完善的官方文档和活跃的社区支持。

## 安装 Flask

使用 pip 安装 Flask：

```bash
pip install flask
```

## 最小应用

一个最简单的 Flask 应用只需要几行代码：

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()
```

### 代码解析

1. `Flask(__name__)`：创建 Flask 应用实例，`__name__` 让 Flask 知道在哪里寻找静态文件等资源。
2. `@app.route('/')`：路由装饰器，将 URL `/` 映射到 `hello_world` 函数。
3. `app.run()`：启动开发服务器，默认监听 `http://127.0.0.1:5000/`。

运行应用：

```bash
python app.py
```

访问 `http://127.0.0.1:5000/` 即可看到 "Hello, World!"。

## 核心概念

### 路由

Flask 使用 `@app.route()` 装饰器定义路由：

```python
@app.route('/user/<username>')
def show_user_profile(username):
    return f'User {username}'
```

路由可以包含变量部分（用 `<variable_name>` 标记），这些部分会作为关键字参数传递给函数。

#### HTTP 方法

默认路由只响应 GET 请求，可以通过 `methods` 参数指定其他方法：

```python
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        return do_login()
    else:
        return show_login_form()
```

### 请求对象

Flask 的 `request` 对象包含所有客户端发送的请求信息：

```python
from flask import request

@app.route('/search')
def search():
    query = request.args.get('q', '')  # 获取查询参数
    return f'Search results for: {query}'
```

常用属性：
- `request.args`：GET 请求的参数
- `request.form`：POST 请求的表单数据
- `request.files`：上传的文件
- `request.json`：JSON 数据

### 响应

视图函数可以返回多种类型的响应：

1. **字符串**：自动转换为响应对象
2. **元组**：`(response, status_code)` 或 `(response, headers)`
3. **Response 对象**：更灵活的控制

```python
from flask import make_response

@app.route('/custom')
def custom_response():
    response = make_response('Custom Response')
    response.headers['X-Custom-Header'] = 'Value'
    return response
```

### 模板渲染

Flask 使用 Jinja2 模板引擎：

```python
from flask import render_template

@app.route('/hello/<name>')
def hello(name):
    return render_template('hello.html', name=name)
```

模板文件 `templates/hello.html`：

```html
<!doctype html>
<html>
<head><title>Hello</title></head>
<body>
    <h1>Hello, {{ name }}!</h1>
</body>
</html>
```

### 静态文件

静态文件（CSS, JavaScript, 图片）放在 `static` 目录下，可以通过 `url_for` 生成 URL：

```html
<link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
```

## 进阶功能

### 蓝图

蓝图（Blueprint）用于组织大型应用：

```python
from flask import Blueprint

auth = Blueprint('auth', __name__)

@auth.route('/login')
def login():
    return 'Login Page'

# 注册蓝图
app.register_blueprint(auth, url_prefix='/auth')
```

### 数据库集成

使用 Flask-SQLAlchemy 扩展：

```python
from flask_sqlalchemy import SQLAlchemy

app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///db.sqlite'
db = SQLAlchemy(app)

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)

@app.route('/users')
def list_users():
    users = User.query.all()
    return render_template('users.html', users=users)
```

### 用户会话

Flask 提供 `session` 对象来存储用户特定的信息：

```python
from flask import session

@app.route('/login', methods=['POST'])
def login():
    session['username'] = request.form['username']
    return redirect(url_for('index'))

@app.route('/logout')
def logout():
    session.pop('username', None)
    return redirect(url_for('index'))
```

### 错误处理

自定义错误页面：

```python
@app.errorhandler(404)
def page_not_found(error):
    return render_template('404.html'), 404
```

## 配置

Flask 应用可以通过多种方式配置：

```python
app = Flask(__name__)
app.config['SECRET_KEY'] = 'dev'  # 开发环境密钥
app.config.from_pyfile('config.py')  # 从文件加载
app.config.from_envvar('APP_SETTINGS')  # 从环境变量指定文件加载
```

## 部署

### 开发服务器

Flask 内置的开发服务器不适合生产环境：

```bash
flask run  # 或 python app.py
```

### 生产部署

推荐使用 WSGI 服务器部署：

1. **Gunicorn**：
   ```bash
   pip install gunicorn
   gunicorn -w 4 -b 127.0.0.1:8000 app:app
   ```

2. **uWSGI**：
   ```bash
   pip install uwsgi
   uwsgi --http 127.0.0.1:8000 --module app:app
   ```

3. **使用 Nginx 反向代理**：
   ```nginx
   server {
       listen 80;
       server_name example.com;
       
       location / {
           proxy_pass http://127.0.0.1:8000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
       }
   }
   ```

## 扩展推荐

Flask 生态系统有许多优秀扩展：

1. **Flask-SQLAlchemy**：SQLAlchemy 集成
2. **Flask-Login**：用户认证
3. **Flask-WTF**：表单处理
4. **Flask-RESTful**：构建 REST API
5. **Flask-Migrate**：数据库迁移
6. **Flask-Caching**：缓存支持

## 最佳实践

1. **项目结构**：
   ```
   /project
      /app
         /static
         /templates
         __init__.py
         views.py
         models.py
      config.py
      requirements.txt
   ```

2. **环境隔离**：
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   venv\Scripts\activate  # Windows
   ```

3. **配置管理**：
   ```python
   class Config:
       SECRET_KEY = os.environ.get('SECRET_KEY') or 'dev-key'
       SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL') or \
           'sqlite:///' + os.path.join(basedir, 'app.db')
   ```

4. **错误处理**：
   ```python
   @app.errorhandler(500)
   def internal_error(error):
       db.session.rollback()
       return render_template('500.html'), 500
   ```

## 总结

Flask 是一个灵活、轻量级的 Python Web 框架，适合从简单应用到复杂系统的开发。通过核心简洁的设计和丰富的扩展生态系统，Flask 让开发者可以按需构建功能完善的 Web 应用。本文介绍了 Flask 的核心概念和基本用法，帮助你快速上手 Flask 开发。