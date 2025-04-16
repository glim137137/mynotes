# Vue2

本文参考：[vue2](https://v2.cn.vuejs.org/v2/guide/)

[TOC]

# Vue实例

## 创建一个 Vue 实例

每个 Vue 应用都是通过用 `Vue` 函数创建一个新的 **Vue 实例**开始的：

```js
var vm = new Vue({
  // 选项
})
```

虽然没有完全遵循 [MVVM 模型](https://zh.wikipedia.org/wiki/MVVM)，但是 Vue 的设计也受到了它的启发。因此在文档中经常会使用 `vm` (ViewModel 的缩写) 这个变量名表示 Vue 实例。

当创建一个 Vue 实例时，你可以传入一个**选项对象**。这篇教程主要描述的就是如何使用这些选项来创建你想要的行为。

## 响应式数据

当一个 Vue 实例被创建时，它将 `data` 对象中的所有的 property 加入到 Vue 的**响应式系统**中。当这些 property 的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

```js
// 我们的数据对象
var data = { a: 1 }

// 该对象被加入到一个 Vue 实例中
var vm = new Vue({
  data: data
})

// 获得这个实例上的 property
// 返回源数据中对应的字段
vm.a == data.a // => true

// 设置 property 也会影响到原始数据
vm.a = 2
data.a // => 2

// ……反之亦然
data.a = 3
vm.a // => 3
```

当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时就已经存在于 `data` 中的 property 才是**响应式**的。也就是说如果你添加一个新的 property，比如：

```js
vm.b = 'hi'
```

那么对 `b` 的改动将不会触发任何视图的更新。如果你知道你会在晚些时候需要一个 property，但是一开始它为空或不存在，那么你仅需要设置一些初始值。比如：

```js
data: {
  newTodoText: '',
  visitCount: 0,
  hideCompletedTodos: false,
  todos: [],
  error: null
}
```

这里唯一的例外是使用 `Object.freeze()`，这会阻止修改现有的 property，也意味着响应系统无法再*追踪*变化。

```js
var obj = {
  foo: 'bar'
}

Object.freeze(obj)

new Vue({
  el: '#app',
  data: obj
})
```

```HTML
<div id="app">
  <p>{{ foo }}</p>
  <!-- 这里的 `foo` 不会更新！ -->
  <button v-on:click="foo = 'baz'">Change it</button>
</div>
```

除了数据 property，Vue 实例还暴露了一些有用的实例 property 与方法。它们都有前缀 `$`，以便与用户定义的 property 区分开来。例如：

```js
var data = { a: 1 }
var vm = new Vue({
  el: '#example',
  data: data
})

vm.$data === data // => true
vm.$el === document.getElementById('example') // => true

// $watch 是一个实例方法
vm.$watch('a', function (newValue, oldValue) {
  // 这个回调将在 `vm.a` 改变后调用
})
```



### DOM 更新时机 `tick`

当你修改了响应式状态时，DOM 会被自动更新。但是需要注意的是，DOM 更新不是同步的。Vue 会在“next tick”更新周期中缓冲所有状态的修改，以确保不管你进行了多少次状态修改，每个组件都只会被更新一次。

`nextTick()` 可以在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。

```js
// 修改数据
vm.msg = 'Hello'
// DOM 还没有更新
Vue.nextTick(function () {
  // 这里可以访问到更新后的 DOM
  console.log('DOM 更新了!');
  
  // 举个例子，修改某个元素的样式
  document.querySelector('#someElement').style.color = 'red';
})

// 作为一个 Promise 使用 (2.1.0 起新增，详见接下来的提示)
Vue.nextTick()
  .then(function () {
    // DOM 更新了
  })
```





## 生命周期图示

每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。Vue 实例的**生命周期**被划分为不同阶段，下图展示了实例的生命周期：

![Vue 实例生命周期](https://v2.cn.vuejs.org/images/lifecycle.png)



# 模板语法

## 声明式渲染

Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统：

```vue
<div id="app">
  {{ message }}
</div>
```

```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

`Hello Vue!`

我们已经成功创建了第一个 Vue 应用！看起来这跟渲染一个字符串模板非常类似，但是 Vue 在背后做了大量工作。现在数据和 DOM 已经被建立了关联，所有东西都是**响应式的**。我们要怎么确认呢？打开你的浏览器的 JavaScript 控制台 (就在这个页面打开)，并修改 `app.message` 的值，你将看到上例相应地更新。

注意我们不再和 HTML 直接交互了。一个 Vue 应用会将其挂载到一个 DOM 元素上 (对于这个例子是 `#app`) 然后对其进行完全控制。那个 HTML 是我们的入口，但其余都会发生在新创建的 Vue 实例内部。

### 数据绑定

#### 对象形式

它直接返回一个对象，该对象会成为组件的响应式数据。

```js
data: {
  message: 'Hello Vue!'
}
```

**注意：** 这种方式是不可用于组件的实例（如在 Vue 组件中），而是用于 Vue 根实例的 `data` 选项。

#### 函数方式

```js
data() {
  return {
    message: 'Hello Vue!'
  };
}
```

这种方式用于组件内的 `data` 选项，是 Vue 组件**最推荐**的方式。

**为什么要用函数？** 在 Vue 组件中，每个组件实例都应该有自己的数据副本。如果直接使用对象形式（像第一种方式），则会造成所有实例共享相同的数据（因为对象是引用类型）。通过函数返回数据，可以确保每个实例都有独立的数据副本。



## 插值表达式

### 文本

数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

```html
<span>Message: {{ msg }}</span>
```

Mustache 标签将会被替代为对应数据对象上 `msg` property 的值。无论何时，绑定的数据对象上 `msg` property 发生了改变，插值处的内容都会更新。

通过使用 [v-once 指令](https://v2.cn.vuejs.org/v2/api/#v-once)，你也能执行一次性地插值，当数据改变时，插值处的内容不会更新。但请留心这会影响到该节点上的其它数据绑定：

```html
<span v-once>这个将不会改变: {{ msg }}</span>
```

### 原生html

双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用 [`v-html` 指令](https://v2.cn.vuejs.org/v2/api/#v-html)：

```html
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

>  Using mustaches: \<span style="color: red">This should be red.\</span>
>
> Using v-html directive: <span style="color: red">This should be red.</span>

这个 `span` 的内容将会被替换成为 property 值 `rawHtml`，直接作为 HTML——会忽略解析 property 值中的数据绑定。注意，你不能使用 `v-html` 来复合局部模板，因为 Vue 不是基于字符串的模板引擎。反之，对于用户界面 (UI)，组件更适合作为可重用和可组合的基本单位。

> 你的站点上动态渲染的任意 HTML 可能会非常危险，因为它很容易导致 [XSS 攻击](https://en.wikipedia.org/wiki/Cross-site_scripting)。请只对可信内容使用 HTML 插值，**绝不要**对用户提供的内容使用插值。

### JS表达式

迄今为止，在我们的模板中，我们一直都只绑定简单的 property 键值。但实际上，对于所有的数据绑定，Vue.js 都提供了完全的 JavaScript 表达式支持。

```html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```

这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含**单个表达式**，所以下面的例子都**不会**生效。

```html
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
```

> 模板表达式都被放在沙盒中，只能访问[全局变量的一个白名单](https://github.com/vuejs/vue/blob/v2.6.10/src/core/instance/proxy.js#L9)，如 `Math` 和 `Date` 。你不应该在模板表达式中试图访问用户定义的全局变量。



## 指令

Vue 提供了多个指令用于在 DOM 中绑定数据、控制渲染等。指令通常以 `v-` 开头。

### 参数与动态参数

#### 参数

一些指令能够接收一个“参数”，在指令名称之后以冒号表示。例如，`v-bind` 指令可以用于响应式地更新 HTML attribute：

```html
<a v-bind:href="url">...</a>
```

在这里 `href` 是参数，告知 `v-bind` 指令将该元素的 `href` attribute 与表达式 `url` 的值绑定。

#### 动态参数

从 2.6.0 开始，可以用**方括号**括起来的 JavaScript 表达式作为一个指令的参数：

```html
<!--
注意，参数表达式的写法存在一些约束，如之后的“对动态参数表达式的约束”章节所述。
-->
<a v-bind:[attributeName]="url"> ... </a>
```

这里的 `attributeName` 会被作为一个 JavaScript 表达式进行动态求值，求得的值将会作为最终的参数来使用。例如，如果你的 Vue 实例有一个 `data` property `attributeName`，其值为 `"href"`，那么这个绑定将等价于 `v-bind:href`。

同样地，你可以使用动态参数为一个动态的事件名绑定处理函数：

```html
<a v-on:[eventName]="doSomething"> ... </a>
```

在这个示例中，当 `eventName` 的值为 `"focus"` 时，`v-on:[eventName]` 将等价于 `v-on:focus`。

##### 对动态参数的值的约束

动态参数预期会求出一个字符串，异常情况下值为 `null`。这个特殊的 `null` 值可以被显性地用于移除绑定。任何其它非字符串类型的值都将会触发一个警告。

```js
data() {
  return {
    attr1: 'src',
    attr2: null,
    attr3: 123
  };
}
```

##### 对动态参数表达式的约束

动态参数表达式有一些语法约束，因为某些字符，如空格和引号，放在 HTML attribute 名里是无效的。例如：

```html
<!-- 这会触发一个编译警告 -->
<a v-bind:['foo' + bar]="value"> ... </a>
```

变通的办法是使用没有空格或引号的表达式，或用计算属性替代这种复杂表达式。

在 DOM 中使用模板时 (直接在一个 HTML 文件里撰写模板)，还需要避免使用大写字符来命名键名，因为浏览器会把 attribute 名全部强制转为小写：

```html
<!--
在 DOM 中使用模板时这段代码会被转换为 `v-bind:[someattr]`。
除非在实例中有一个名为“someattr”的 property，否则代码不会工作。
-->
<a v-bind:[someAttr]="value"> ... </a>
```

### 动态绑定属性 `v-bind` 

`v-bind` 依然用于动态绑定 HTML 属性：

```html
<img v-bind:src="imageSrc" alt="Vue logo">
```

你还可以使用简写 `:src` 来代替：

```html
<img :src="imageSrc" alt="Vue logo">
```

### Class 与 Style 绑定

Vue 支持动态绑定样式和类。

#### 绑定 HTML Class

##### 对象语法

我们可以传给 `v-bind:class` 一个对象，以动态地切换 class：

```html
<div v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>
```

```js
data: {
  isActive: true,
  hasError: false
}
```

上面的语法表示 `active` 这个 class 存在与否将取决于数据 property `isActive` 的布尔值。

> class `text-danger` 因为是 kebab-case (短横线分隔命名) 所以必须加上单引号。实际书写中推荐所有的 `class` 都加上单引号。

绑定的数据对象不必内联定义在模板里：

```vue
<div v-bind:class="classObject"></div>
```

```js
data: {
  classObject: {
    'active': true,
    'text-danger': false
  }
}
```

绑定一个返回对象的**计算属性**：

```js
data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      'active': this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}
```

##### 数组语法

我们可以把一个数组传给 `v-bind:class`，以应用一个 class 列表：

```vue
<div v-bind:class="[activeClass, errorClass, 'post']"></div>
```

```js
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
```

如果你也想根据条件切换列表中的 class，可以用**三元表达式**：

```vue
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```

在数组语法中也可以使用对象语法：

```vue
<div v-bind:class="[{ 'active': isActive }, errorClass]"></div>
```

#### 绑定内联样式

##### 对象语法

`v-bind:style` 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。

```html
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">
</div>
```

> CSS property 名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名。但其实与HTML class 一样，更推荐使用 `kebab-case`+单引号 的形式。

直接绑定到一个样式对象通常更好，这会让模板更清晰：

```vue
<div v-bind:style="styleObject"></div>
```

```js
data: {
  activeColor: 'red',
  fontSize: 30,
}
computed: {
  styleObject: function () {
    return {
      'color': this.activeColor,
      // 涉及像素的不要忘了后面加'px', 例如 'font-size', 'padding', 'width'...
      'font-size': this.fontSize + 'px'
    }
  }
}
```

##### 数组语法

`v-bind:style` 的数组语法可以将多个样式对象应用到同一个元素上：

```vue
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```

在数组语法中也可以使用对象语法：

```vue
<div v-bind:class="[{ 'color': activeColor }, baseStyles]"></div>
```

### 条件渲染 `v-if` 

`v-if` , `v-else-if`, `v-else`用于条件渲染：

```html
<ul>
  	<p v-if="condition1">Condition 1 is true</p>
	<p v-else-if="condition2">Condition 2 is true</p>
	<p v-else>If no condition is true</p>
</ul>
```

`v-show`：不同之处在于 `v-show` 会在 DOM 渲染中保留该元素；`v-show` 仅切换了该元素上名为 `display` 的 CSS 属性。

```html
<h1 v-show="ok">Hello!</h1>
```

#### `v-if` vs. `v-show`

`v-if` 是“真实的”按条件渲染，因为它确保了在切换时，条件区块内的事件监听器和子组件都会被销毁与重建。

`v-if` 也是**惰性**的：如果在初次渲染时条件值为 false，则不会做任何事。条件区块只有当条件首次变为 true 时才被渲染。

相比之下，`v-show` 简单许多，元素无论初始条件如何，始终会被渲染，只有 CSS `display` 属性会被切换。

总的来说，`v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要频繁切换，则使用 `v-show` 较好；如果在运行时绑定条件很少改变，则 `v-if` 会更合适。

### 列表渲染 `v-for` 

 `v-for` 里使用范围值

```html
<span v-for="n in 10">{{ n }}</span>
```

`v-for` 用于遍历数组并渲染列表项：

```html
<li v-for="item in items">
  {{ item.message }}
</li>
<!-- v-for 也支持使用可选的第二个参数表示当前项的位置索引。 -->
<li v-for="(item, index) in items">
  {{ parentMessage }} - {{ index }} - {{ item.message }}
</li>

<!-- 使用 of 作为分隔符来替代 in，这更接近 JavaScript 的迭代器语法 -->
<div v-for="item of items"></div>

<!-- 也可以在定义 v-for 的变量别名时使用解构，和解构函数参数类似 -->
<li v-for="({ message }, index) in items">
  {{ message }} {{ index }}
</li>
```

`v-for` 用于遍历对象并渲染列表项：

```html
<ul>
  <li v-for="value in myObject">
    {{ value }}
  </li>
</ul>

<li v-for="(value, key) in myObject">
  {{ key }}: {{ value }}
</li>

<li v-for="(value, key, index) in myObject">
  {{ index }}. {{ key }}: {{ value }}
</li>
```

#### `v-for` 和 `v-if`

当 `v-if` 和 `v-for` 同时存在于一个元素上的时候，`v-if` 会首先被执行。

**注意**

> 同时使用 `v-if` 和 `v-for` 是**不推荐的**，因为这样二者的优先级不明显。
>
> 两种常见的情况可能导致这种用法：
>
> - 过滤列表中的项目 (例如，`v-for="user in users" v-if="user.isActive"`)。在这种情况下，可以用一个新的计算属性来替换 `users`，该属性返回过滤后的列表 (例如 `activeUsers`)。
> - 避免渲染应该隐藏的列表 (例如 `v-for="user in users" v-if="shouldShowUsers"`)。在这种情况下，将 `v-if` 移至容器元素 (如 `ul`、`ol`)。

#### 通过 key 管理状态

Vue 默认按照“就地更新”的策略来更新通过 `v-for` 渲染的元素列表。当数据项的顺序改变时，Vue 不会随之移动 DOM 元素的顺序，而是就地更新每个元素，确保它们在原本指定的索引位置上渲染。

默认模式是高效的，但**只适用于列表渲染输出的结果不依赖子组件状态或者临时 DOM 状态 (例如表单输入值) 的情况**。

为了给 Vue 一个提示，以便它可以跟踪每个节点的标识，从而重用和重新排序现有的元素，你需要为每个元素对应的块提供一个唯一的 `key` attribute：

```html
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```

### 双向数据绑定 `v-model` 

`v-model` 用于实现表单元素和数据的双向绑定：

```html
<input v-model="message" placeholder="输入内容">
<p>你输入的内容是：{{ message }}</p>
```

`v-model` 绑定了一个输入框的值和 Vue 实例中的 `message` 数据，实现了双向绑定。

### 事件绑定

可以用 `v-on` 指令监听 DOM 事件，并在触发时运行一些 **JavaScript 代码**。你可以使用简写 `@` 来绑定事件：

```html
<div id="example-1">
  <button v-on:click="counter += 1">Add 1</button>
  <p>The button above has been clicked {{ counter }} times.</p>
</div>
```

```js
var example1 = new Vue({
  el: '#example-1',
  data: {
    counter: 0
  }
})
```

#### 事件处理方法

然而许多事件处理逻辑会更为复杂，所以直接把 JavaScript 代码写在 `v-on` 指令中是不可行的。因此 `v-on` 还可以接收一个需要调用的方法名称。

示例：

```vue
<div id="example-2">
  <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet">Greet</button>
</div>
```

```js
var example2 = new Vue({
  el: '#example-2',
  data: {
    name: 'Vue.js'
  },
  // 在 `methods` 对象中定义方法
  methods: {
    greet: function (event) {
      // `this` 在方法里指向当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
})

// 也可以用 JavaScript 直接调用方法
example2.greet() // => 'Hello Vue.js!'
```

#### 在内联事件处理器中访问事件参数

有时我们需要在内联事件处理器中访问原生 DOM 事件。你可以向该处理器方法传入一个特殊的 `$event` 变量，或者使用内联箭头函数：

```vue
<!-- 使用特殊的 $event 变量 -->
<button @click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

<!-- 使用内联箭头函数 -->
<button @click="(event) => warn('Form cannot be submitted yet.', event)">
  Submit
</button>
```

```js
function warn(message, event) {
  // 这里可以访问原生事件
  if (event) {
    console.log(event.target)
  }
  alert(message)
}
```

#### 修饰符

修饰符 (modifier) 是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，`.prevent` 修饰符告诉 `v-on` 指令对于触发的事件调用 `event.preventDefault()`：

```html
<form v-on:submit.prevent="onSubmit">...</form>
```

在接下来对 [`v-on`](https://v2.cn.vuejs.org/v2/guide/events.html#事件修饰符) 和 [`v-for`](https://v2.cn.vuejs.org/v2/guide/forms.html#修饰符) 等功能的探索中，你会看到修饰符的其它例子。

##### 事件修饰符

| 修饰符     | 作用                                                         | 使用场景                 |
| ---------- | ------------------------------------------------------------ | ------------------------ |
| `.prevent` | 阻止事件的默认行为（如阻止表单提交、链接跳转等）             | 例如：阻止表单提交等     |
| `.stop`    | 阻止事件冒泡，防止事件传递到父元素                           | 例如：阻止点击事件冒泡   |
| `.once`    | 事件处理函数只会执行一次，执行后自动解除绑定                 | 例如：点击只触发一次事件 |
| `.capture` | 事件在捕获阶段触发（即父元素先于子元素触发事件）             | 例如：优先捕获父元素事件 |
| `.passive` | 不调用 `preventDefault()`，优化性能（主要用于滚动等事件）    | 例如：提高滚动性能       |
| `.self`    | 用于避免父元素的事件被触发。仅当事件在绑定元素本身触发时才有效。 |                          |

```html
<!-- 单击事件将停止传递 -->
<a @click.stop="doThis"></a>

<!-- 提交事件将不再重新加载页面 -->
 <form @submit.prevent="onSubmit"></form>
 
<!-- 修饰语可以使用链式书写 -->
 <a @click.stop.prevent="doThat"></a>
 
<!-- 也可以只有修饰符 -->
 <form @submit.prevent></form>
 
<!-- 仅当 event.target 是元素本身时才会触发事件处理器 -->
 <!-- 例如：事件处理器不来自子元素 -->
 <div @click.self="doThat">...</div>
 
<!-- 添加事件监听器时，使用 `capture` 捕获模式 -->
 <!-- 例如：指向内部元素的事件，在被内部元素处理前，先被外部处理 -->
 <div @click.capture="doThis">...</div>
 
<!-- 点击事件最多被触发一次 -->
 <a @click.once="doThis"></a>
```

##### 按键修饰符

**keyup, keydown, keypress**

```html
<!-- 仅在 `key` 为 `Enter` 时调用 `submit` -->
<input @keyup.enter="submit" />
```

 Vue 为一些常用的按键提供了别名：

`.enter` 

`.tab` 

`.delete` (捕获“Delete”和“Backspace”两个按键) 

`.esc` 

`.space` 

`.up` / `.down` / `.left` / `.right`

##### 鼠标修饰符

**click**

`.left`

`.right`

`.middle`

**`.exact` 修饰符**

此外还有 `.exact` 修饰符，允许控制触发一个事件所需的确定组合的系统按键修饰符：

```html
<!-- 当按下 Ctrl 时，即使同时按下 Alt 或 Shift 也会触发 -->
<button @click.ctrl="onClick">A</button>
 
<!-- 仅当按下 Ctrl 且未按任何其他键时才会触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>
 
<!-- 仅当没有按下任何系统按键时触发 -->
<button @click.exact="onClick">A</button>
```







# 选项式 API

## 挂载元素

- **类型**：`string | Element`

- **限制**：只在用 `new` 创建实例时生效。

- **详细**：

    提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标。可以是 CSS 选择器，也可以是一个 HTMLElement 实例。

```js
new Vue({
  el: '#app',  // 将 Vue 实例挂载到 id 为 "app" 的 DOM 元素上
  data: {
    message: 'Hello, Vue!'
  }
});

```

## 响应式数据

- **类型**：`Object | Function`
- **限制**：组件的定义只接受 `function`。

如果 `data` 是一个对象，那么它会被视为 Vue 实例或组件的初始数据：

```js
new Vue({
  data: {
    message: 'Hello, Vue!'
  }
});
```

但是，这种方式在组件中容易出现问题，多个组件实例会共享同一个 `data` 对象，因此通常不推荐在组件中直接使用这种方式。

在组件中，`data` 应该是一个返回数据对象的 **函数**，以确保每个组件实例都有自己的数据副本：

```js
new Vue({
  data() {
    return {
      message: 'Hello, Vue!'
    };
  }
});
```

在这种情况下，每个 Vue 实例（或组件实例）都会调用 `data` 函数，返回一个新的数据对象，从而确保数据的隔离性。

## 方法

你可以通过 `methods` 来处理事件或执行其他操作。

- **类型**：`{ [key: string]: Function }`

- **详细**：

    methods 将被混入到 Vue 实例中。可以直接通过 VM 实例访问这些方法，或者在指令表达式中使用。方法中的 `this` 自动绑定为 Vue 实例。

> :exclamation:注意，**不应该使用箭头函数来定义 method 函数** (例如 `plus: () => this.a++`)。理由是箭头函数绑定了父级作用域的上下文，所以 `this` 将不会按照期望指向 Vue 实例，`this.a` 将是 undefined。

```html
<div id="app">
  <button @click="greet">点击我</button>
</div>

<script>
  new Vue({
    el: '#app',
    methods: {
      // 两种写法等价
      greet() {
          alert('你好，Vue!');
      },
      // 推荐写法
      greet: function() {
          alert('你好，Vue!');
      }
    }
  });
</script>
```

## 侦听器

当你希望在数据变化时执行某些操作（如异步请求、DOM 操作、外部库的调用等）时，可以使用侦听器。Vue 会在数据发生变化时触发回调函数。

- **类型**：`{ [key: string]: string | Function | Object | Array }`

- **详细**：

    一个对象，键是需要观察的表达式，值是对应回调函数。值也可以是方法名，或者包含选项的对象。Vue 实例将会在实例化时调用 `$watch()`，遍历 watch 对象的每一个 property。

```js
new Vue({
    el: '#app',
    data() {
  		return {
      		searchQuery: ''
  		};
	},
	watch: {
        // 两种写法等价
  		searchQuery(newQuery, oldQuery) {
      		// 当 searchQuery 变化时，发送请求
      		this.fetchData(newQuery);
  		},
        // 推荐写法
  		searchQuery: function(newQuery, oldQuery) {
      		this.fetchData(newQuery);
  		}
	},
	methods: {
  		fetchData(query) {
      		// 假设通过 Ajax 获取数据
      		console.log('Fetching data for:', query);
  		}
	}
});
```

## 计算属性

计算属性是基于其依赖进行**缓存**的，并且在**相关依赖发生变化**时才会**重新计算**。

- **类型**：`{ [key: string]: Function | { get: Function, set: Function } }`

- **详细**：

    计算属性将被混入到 Vue 实例中。所有 getter 和 setter 的 this 上下文自动地绑定为 Vue 实例。

```html
<div id="app">
  <p>{{ reversedMessage }}</p>
</div>

<script>
  new Vue({
    el: '#app',
    data: {
      message: 'Hello, Vue!'
    },
    computed: {
      reversedMessage: function() {
        return this.message.split('').reverse().join('');
      }
    }
  });
</script>
```

在这个例子中，`reversedMessage` 会返回 `message` 的反转值，且只有当 `message` 改变时，`reversedMessage` 才会重新计算。

### get() 与 set()

计算属性的类型可以是一个带有 `get` 方法的简单函数，或者包含 `get` 和 `set` 的对象，后者用于实现可读写的计算属性。

```js
new Vue({
  el: '#app',
  data() {
    return {
      firstName: 'John',
      lastName: 'Doe'
    };
  },
  computed: {
    // 完整的 get 和 set
    fullName: {
      // get 方法，返回计算的值
      get() {
        return `${this.firstName} ${this.lastName}`;
      },
      // set 方法，允许修改数据
      set(newFullName) {
        const names = newFullName.split(' ');
        this.firstName = names[0];
        this.lastName = names[1] || '';
      }
    }
  }
});

```

### 计算属性缓存 vs 方法

你可能已经注意到我们可以通过在表达式中调用方法来达到同样的效果：

```html
<p>Reversed message: "{{ reversedMessage() }}"</p>
// 在组件中
<script>
	methods: {
 	 reversedMessage: function () {
  	  		return this.message.split('').reverse().join('')
  		}
	}
</script>
```

我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，不同的是**计算属性是基于它们的响应式依赖进行缓存的**。只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 `message` 还没有发生改变，多次访问 `reversedMessage` 计算属性会立即返回之前的计算结果，而不必再次执行函数。

这也同样意味着下面的计算属性将不再更新，因为 `Date.now()` 不是响应式依赖：

```js
computed: {
  now: function () {
    return Date.now()
  }
}
```

相比之下，每当触发重新渲染时，调用方法将**总会**再次执行函数。

我们为什么需要缓存？假设我们有一个性能开销比较大的计算属性 **A**，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算属性依赖于 **A**。如果没有缓存，我们将不可避免的多次执行 **A** 的 getter！如果你不希望有缓存，请用方法来替代。

### 计算属性 vs 侦听属性

Vue 提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：**侦听属性**。当你有一些数据需要随着其它数据变动而变动时，你很容易滥用 `watch`。然而，通常更好的做法是使用计算属性而不是命令式的 `watch` 回调。细想一下这个例子：

```html
<div id="demo">{{ fullName }}</div>
```

```js
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
})
```

上面代码是命令式且重复的。将它与计算属性的版本进行比较：

```js
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```

好得多了，不是吗？

## 生命周期钩子

每个 Vue 组件实例在创建时都需要经历一系列的初始化步骤，比如设置好数据侦听，编译模板，挂载实例到 DOM，以及在数据改变时更新 DOM。在此过程中，它也会运行被称为生命周期钩子的函数，让开发者有机会在特定阶段运行自己的代码。

Vue 实例提供了多种生命周期钩子，在不同的阶段执行不同的操作。

```js
new Vue({
  el: '#app',
  data: {
    message: 'Hello, Vue!'
  },
  beforeCreate() {
    console.log('beforeCreate: 实例初始化');
  },
  created() {
    console.log('created: 实例创建完成');
  },
  beforeMount() {
    console.log('beforeMount: 即将挂载');
  },
  mounted() {
    console.log('mounted: 挂载完成');
  },
  beforeUpdate() {
    console.log('beforeUpdate: 数据更新前');
  },
  updated() {
    console.log('updated: 数据更新后');
  },
  beforeDestroy() {
    console.log('beforeDestroy: 销毁前');
  },
  destroyed() {
    console.log('destroyed: 销毁后');
  }
});
```

:star: ​**created** 和 **mounted** 是**最常用**的生命周期钩子。`created` 用于初始化数据和请求数据，`mounted` 用于需要操作 DOM 或依赖于 DOM 完成的任务。

**beforeDestroy** 和 **destroyed** 用于组件销毁时的清理工作，避免内存泄漏。



## vue2 中的 this

在 **Vue 2** 中，`this` 是指向 Vue 实例的对象。通过 `this`，你可以访问 Vue 实例的各种属性和方法，包括：

- **数据 (data)**: 通过 `this` 访问和修改 Vue 实例中的响应式数据。
- **方法 (methods)**: 通过 `this` 调用 Vue 实例中的方法。
- **计算属性 (computed)**: 通过 `this` 访问计算属性。

```js
new Vue({
  el: '#app',
  data() {
    return {
      message: 'Hello, Vue!',
    };
  },
  methods: {
      logMessage(curMessage) {
        console.log(curMessage);
      },
  },
  computed: {
      reversedMessage: function() {
        return this.message.split('').reverse().join('');
      },
  },
  created() {
    this.logMessage(this.message);
  },
  mounted() {
    this.logMessage(this.reversedMessage);
  }
});
```



# 组件



## 组件入门

### 基本示例

这里有一个 Vue 组件的示例：

```js
// 定义一个名为 button-counter 的新组件
Vue.component('button-counter', {
  data: function () {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})
```

组件是可复用的 Vue 实例，且带有一个名字：在这个例子中是 `<button-counter>`。我们可以在一个通过 `new Vue` 创建的 Vue 根实例中，把这个组件作为自定义元素来使用：

```html
<div id="components-demo">
  <button-counter></button-counter>
</div>

<scrpit>
    new Vue({ el: '#components-demo' })
</scrpit>
```

因为组件是可复用的 Vue 实例，所以它们与 `new Vue` 接收相同的选项，例如 `data`、`computed`、`watch`、`methods` 以及生命周期钩子等。仅有的例外是像 `el` 这样根实例特有的选项。

### 组件复用

你可以将组件进行任意次数的复用：

```html
<div id="components-demo">
  <button-counter></button-counter>
  <button-counter></button-counter>
  <button-counter></button-counter>
</div>
```

You clicked me 0 times. You clicked me 0 times. You clicked me 0 times.

注意当点击按钮时，每个组件都会各自独立维护它的 `count`。因为你每用一次组件，就会有一个它的新**实例**被创建。

#### data 必须是一个函数

当我们定义这个 `<button-counter>` 组件时，你可能会发现它的 `data` 并不是像这样直接提供一个对象：

```js
data: {
  count: 0
}
```

取而代之的是，**一个组件的 `data` 选项必须是一个函数**，因此每个实例可以维护一份被返回对象的独立的拷贝：

```js
data: function () {
  return {
    count: 0
  }
}
```

### 组件的组织

通常一个应用会以一棵嵌套的组件树的形式来组织：

![Component Tree](https://v2.cn.vuejs.org/images/components.png)

例如，你可能会有页头、侧边栏、内容区等组件，每个组件又包含了其它的像导航链接、博文之类的组件。

为了能在模板中使用，这些组件必须先注册以便 Vue 能够识别。这里有两种组件的注册类型：**全局注册**和**局部注册**。至此，我们的组件都只是通过 `Vue.component` 全局注册的：

```js
Vue.component('my-component-name', {
  // ... options ...
})
```

全局注册的组件可以用在其被注册之后的任何 (通过 `new Vue`) 新创建的 Vue 根实例，也包括其组件树中的所有子组件的模板中。

到目前为止，关于组件注册你需要了解的就这些了，如果你阅读完本页内容并掌握了它的内容，我们会推荐你再回来把[组件注册](https://v2.cn.vuejs.org/v2/guide/components-registration.html)读完。

### 监听子组件事件

在我们开发 `<blog-post>` 组件时，它的一些功能可能要求我们和父级组件进行沟通。例如我们可能会引入一个辅助功能来放大博文的字号，同时让页面的其它部分保持默认的字号。

在其父组件中，我们可以通过添加一个 `postFontSize` 数据 property 来支持这个功能：

```js
new Vue({
  el: '#blog-posts-events-demo',
  data: {
    posts: [/* ... */],
    postFontSize: 1
  }
})
```

它可以在模板中用来控制所有博文的字号：

```html
<div id="blog-posts-events-demo">
  <div :style="{ fontSize: postFontSize + 'em' }">
    <blog-post
      v-for="post in posts"
      :key="post.id"
      :post="post"
    ></blog-post>
  </div>
</div>
```

现在我们在每篇博文正文之前添加一个按钮来放大字号：

```js
Vue.component('blog-post', {
  props: ['post'],
  template: `
    <div class="blog-post">
      <h3>{{ post.title }}</h3>
      <button>
        Enlarge text
      </button>
      <div v-html="post.content"></div>
    </div>
  `
})
```

问题是这个按钮不会做任何事，这时候我们需要用到自定义事件：

```html
<button>
  Enlarge text
</button>
```

#### 自定义事件

当点击这个按钮时，我们需要告诉父级组件放大所有博文的文本。Vue 实例提供了一个**自定义事件**的系统来解决这个问题。父级组件可以像处理 native DOM 事件一样通过 `v-on` 监听子组件实例的任意事件：

```html
<blog-post
  ...
  @enlarge-text="postFontSize += 0.1"
>
</blog-post>
```

>事件后面往往是 **一个方法** 或 **一个有效的 JavaScript 表达式**

同时子组件可以通过调用内建的 [**`$emit`** 方法](https://v2.cn.vuejs.org/v2/api/#vm-emit)并传入事件名称来触发一个事件：

```html
<button @click="$emit('enlarge-text')">
  Enlarge text
</button>
```

有了这个 `v-on:enlarge-text="postFontSize += 0.1"` 监听器，父级组件就会接收该事件并更新 `postFontSize` 的值。

##### 使用自定义事件抛出一个值

例如我们可能想让 `<blog-post>` 组件决定它的文本要放大多少。这时可以使用 `$emit` 的第二个参数来提供这个值：

```html
<button @click="$emit('enlarge-text', 0.1)">
  Enlarge text
</button>
```

如果这个事件处理函数是**一个 JS 表达式**，然后当在父级组件监听这个事件的时候，我们可以通过 **`$event`** 访问到被抛出的这个值：

```html
<blog-post
  ...
  @enlarge-text="postFontSize += $event"
></blog-post>
```

如果这个事件处理函数是**一个方法**：

```html
<blog-post
  ...
  @enlarge-text="onEnlargeText"
></blog-post>
```

那么这个值将会作为第一个参数传入这个方法：

```js
methods: {
  onEnlargeText: function (enlargeAmount) {
    this.postFontSize += enlargeAmount
  }
}
```



#### 在组件上使用 `v-model`

自定义事件也可以用于创建支持 `v-model` 的自定义输入组件。记住：

```html
<input v-model="searchText">
```

等价于：

```html
<input
  :value="searchText"
  @input="searchText = $event.target.value"
>
```

当用在组件上时，`v-model` 则会这样：

```html
<custom-input
  v-bind:value="searchText"
  v-on:input="searchText = $event"
></custom-input>
```

为了让它正常工作，这个组件内的 `<input>` 必须：

- 将其 `value` attribute 绑定到一个名叫 `value` 的 prop 上
- 在其 `input` 事件被触发时，将新的值通过自定义的 `input` 事件抛出

写成代码之后是这样的：

```js
Vue.component('custom-input', {
  props: ['value'],
  template: `
    <input
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
    >
  `
})
```

现在 `v-model` 就应该可以在这个组件上完美地工作起来了：

```html
<custom-input v-model="searchText"></custom-input>
```

### 组件插槽

和 HTML 元素一样，我们经常需要向一个组件传递内容，像这样：

```html
<alert-box>
  Something bad happened.
</alert-box>
```

可能会渲染出这样的东西：

<div class="demo-alert-box">
     <strong>Error!</strong>
     <slot>Something bad happened.</slot>
</div>

Vue 允许你在父组件中定义插槽，并将子组件内容传递给父组件的插槽。幸好，Vue 自定义的 `<slot>` 元素让这变得非常简单：

```js
Vue.component('alert-box', {
  template: `
    <div class="demo-alert-box">
      <strong>Error!</strong>
      <slot></slot>
    </div>
  `
})
```

如你所见，我们只要在需要的地方加入插槽就行了——就这么简单！

### 动态组件

有的时候，在不同组件之间进行动态切换是非常有用的，比如在一个[多标签的界面](https://v2.cn.vuejs.org/v2/guide/components.html#动态组件)里。

上述内容可以通过 Vue 的 `<component>` 元素加一个特殊的 `is` attribute 来实现：

```html
<!-- 组件会在 `currentTabComponent` 改变时改变 -->
<component v-bind:is="currentTabComponent"></component>
```

`:is` 用于绑定当前组件的名称（字符串）或组件对象。`currentTabComponent` 是一个变量，用于存储当前显示的组件的名称。

在上述示例中，`currentTabComponent` 可以包括

- 已注册组件的名字，或
- 一个组件的选项对象

### 单文件组件

很多 Vue 项目中，我们使用 `Vue.component` 来定义全局组件，紧接着用 `new Vue({ el: '#container '})` 在每个页面内指定一个容器元素。

这种方式在很多中小规模的项目中运作的很好，在这些项目里 JavaScript 只被用来加强特定的视图。但当在更复杂的项目中，或者你的前端完全由 JavaScript 驱动的时候，下面这些缺点将变得非常明显：

- **全局定义 (Global definitions)** 强制要求每个 component 中的命名不得重复
- **字符串模板 (String templates)** 缺乏语法高亮，在 HTML 有多行的时候，需要用到丑陋的 `\`
- **不支持 CSS (No CSS support)** 意味着当 HTML 和 JavaScript 组件化时，CSS 明显被遗漏
- **没有构建步骤 (No build step)** 限制只能使用 HTML 和 ES5 JavaScript，而不能使用预处理器，如 Pug (formerly Jade) 和 Babel

文件扩展名为 `.vue` 的 **single-file components (单文件组件)** 为以上所有问题提供了解决方法，并且还可以使用 webpack 或 Browserify 等构建工具。

这是一个文件名为 `Hello.vue` 的简单实例：

[![单文件组件的示例 (点击查看文本版的代码](https://v2.cn.vuejs.org/images/vue-component.png)](https://codesandbox.io/s/github/vuejs/v2.vuejs.org/tree/master/src/v2/examples/vue-20-single-file-components)

**SFC**将组件的模板、脚本和样式封装在一个文件中，以便更好地组织和维护代码。一个文件内包含了三部分内容：

1. **模板 (template)** - 用于定义组件的结构（HTML）。
2. **脚本 (script)** - 用于定义组件的逻辑和数据（JavaScript）。
3. **样式 (style)** - 用于定义组件的样式（CSS）。



## 组件注册

### 组件名

在注册一个组件的时候，我们始终需要给它一个名字。

```js
Vue.component('my-component-name', { /* ... */ })
```

该组件名就是 `Vue.component` 的第一个参数。

你给予组件的名字可能依赖于你打算拿它来做什么。当直接在 DOM 中使用一个组件 (而不是在字符串模板或[单文件组件](https://v2.cn.vuejs.org/v2/guide/single-file-components.html)) 的时候，我们强烈推荐遵循 [W3C 规范](https://html.spec.whatwg.org/multipage/custom-elements.html#valid-custom-element-name)中的自定义组件名 (字母全小写且必须包含一个连字符)。这会帮助你避免和当前以及未来的 HTML 元素相冲突。

#### 组件名大小写

定义组件名的方式有两种：

##### 使用 kebab-case

```js
Vue.component('my-component-name', { /* ... */ })
```

当使用 kebab-case (短横线分隔命名) 定义一个组件时，你也必须在引用这个自定义元素时使用 kebab-case，例如 `<my-component-name>`。

##### 使用 PascalCase

```js
Vue.component('MyComponentName', { /* ... */ })
```

当使用 PascalCase (首字母大写命名) 定义一个组件时，你在引用这个自定义元素时两种命名法都可以使用。也就是说 `<my-component-name>` 和 `<MyComponentName>` 都是可接受的。注意，尽管如此，直接在 **DOM (即非字符串的模板)** 中使用时**只有 kebab-case 是有效的。**

所以，推荐遵循kebab-case (字母全小写且必须包含一个连字符) 的写法。

### 全局注册

到目前为止，我们只用过 `Vue.component` 来创建组件：

```js
Vue.component('my-component-name', {
  // ... 选项 ...
})
```

这些组件是**全局注册的**。也就是说它们在注册之后可以用在任何新创建的 Vue 根实例 (`new Vue`) 的模板中。比如：

```js
Vue.component('component-a', { /* ... */ })
Vue.component('component-b', { /* ... */ })
Vue.component('component-c', { /* ... */ })

new Vue({ el: '#app' })
```

```html
<div id="app">
  <component-a></component-a>
  <component-b></component-b>
  <component-c></component-c>
</div>
```

在所有子组件中也是如此，也就是说这三个组件*在各自内部*也都可以相互使用。

### 局部注册

全局注册往往是不够理想的。比如，如果你使用一个像 webpack 这样的构建系统，全局注册所有的组件意味着即便你已经不再使用一个组件了，它仍然会被包含在你最终的构建结果中。这造成了用户下载的 JavaScript 的无谓的增加。

在这些情况下，你可以通过一个普通的 JavaScript 对象来定义组件：

```js
var ComponentA = { /* ... */ }
var ComponentB = { /* ... */ }
var ComponentC = { /* ... */ }
```

然后在 **`components`** 选项中定义你想要使用的组件：

```js
new Vue({
  el: '#app',
  components: {
    'component-a': ComponentA,
    'component-b': ComponentB
  }
})
```

对于 `components` 对象中的每个 property 来说，其 property 名就是自定义元素的名字，其 property 值就是这个组件的选项对象。

注意**局部注册的组件在其子组件中\*不可用\***。例如，如果你希望 `ComponentA` 在 `ComponentB` 中可用，则你需要这样写：

```js
var ComponentA = { /* ... */ }

var ComponentB = {
  components: {
    'component-a': ComponentA
  },
  // ...
}
```

或者如果你通过 Babel 和 webpack 使用 ES2015 模块，那么代码看起来更像：

```js
import ComponentA from './ComponentA.vue'

export default {
  components: {
    ComponentA
  },
  // ...
}
```

注意在 ES2015+ 中，在对象中放一个类似 `ComponentA` 的变量名其实是 `ComponentA: ComponentA` 的缩写，即这个变量名同时是：

- 用在模板中的自定义元素的名称
- 包含了这个组件选项的变量名



## Props

**Prop** 是在组件上注册的一些自定义属性。这种机制实现了**父组件向子组件传递数据**。

- 父组件通过 **HTML 属性（attribute）** 的方式传递数据给子组件。

- 子组件需要在 `props` 选项中声明它可以接收哪些数据。

### Prop 是什么 ?

早些时候，我们提到了创建一个博文组件的事情。问题是如果你不能向这个组件传递某一篇博文的标题或内容之类的我们想展示的数据的话，它是没有办法使用的。这也正是 prop 的由来。

Prop 是你可以在组件上注册的一些**自定义 attribute**。当一个值传递给一个 prop attribute 的时候，它就变成了那个组件实例的一个 property。为了给博文组件传递一个标题，我们可以用一个 `props` 选项将其包含在该组件可接受的 prop 列表中：

```js
Vue.component('blog-post', {
  props: ['title'],
  template: '<h3>{{ title }}</h3>'
})
```

一个组件默认可以拥有**任意数量**的 prop，任何值都可以传递给任何 prop。在上述模板中，你会发现我们能够在组件实例中访问这个值，就像访问 `data` 中的值一样。

一个 prop 被注册之后，你就可以像这样把数据作为一个自定义 attribute 传递进来：

```vue
<blog-post title="My journey with Vue"></blog-post>
<blog-post title="Blogging with Vue"></blog-post>
<blog-post title="Why Vue is so fun"></blog-post>
```

### 父传子

我们继续以博文为例，

数据在父组件中： 

```vue
<template>
	<blog-post
	  v-for="post in posts"
	  :key="post.id"
	  :post="post"
	></blog-post>
</template>

<script>
new Vue({
  data: {
    post: {
        id: 1,
        title: "Study Props",
        content: "We are learning Props.",
    },
  }
});
</script>
```

Props 声明在子组件中：

```js
Vue.component('blog-post', {
  props: ['post'],
  template: `
    <div class="blog-post">
      <h3>{{ post.title }}</h3>
      <div v-html="post.content"></div>
    </div>
  `
})
```

### Prop 的大小写

HTML 中的 attribute 名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名：

```js
Vue.component('blog-post', {
  // 在 JavaScript 中是 camelCase 的
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
```

```html
<!-- 在 HTML 中是 kebab-case 的 -->
<blog-post post-title="hello!"></blog-post>
```

重申一次，如果你使用字符串模板，那么这个限制就不存在了。

```html
<!-- BlogPost.vue -->
<template>
  <!-- 可以直接用 camelCase，不需要转成 kebab-case -->
  <blog-post :postTitle="title"></blog-post>
</template>
```

或者

```js
new Vue({
  el: '#app',
  template: '<blog-post :postTitle="title"></blog-post>',
  data: {
    title: 'Hello!'
  }
});
```

### Prop 的类型

以字符串数组形式列出的 prop：

```js
props: ['title', 'likes', 'isPublished', 'commentIds', 'author']
```

以对象形式列出 prop，这些 property 的名称和值分别是 prop 各自的名称和类型：

```js
props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // or any other constructor
}
```

### 传递静态或动态 Prop

像这样，你已经知道了可以像这样给 prop 传入一个静态的值：

```html
<blog-post title="My journey with Vue"></blog-post>
```

你也知道 prop 可以通过 `v-bind` 动态赋值，例如：

```html
<!-- 动态赋予一个变量的值 -->
<blog-post v-bind:title="post.title"></blog-post>

<!-- 动态赋予一个复杂表达式的值 -->
<blog-post
  v-bind:title="post.title + ' by ' + post.author.name"
></blog-post>
```

在上述两个示例中，我们传入的值都是字符串类型的，但实际上*任何*类型的值都可以传给一个 prop。

prop 的值可以是数字，布尔值，数组，对象，但是它们作为**一个 JavaScript 表达式**都需要用双引号 `“”` 括起来。

```html
<blog-post v-bind:likes="42"></blog-post>
<blog-post v-bind:is-published="false"></blog-post>
<blog-post v-bind:comment-ids="[234, 266, 273]"></blog-post>
<blog-post
  v-bind:author="{
    name: 'Veronica',
    company: 'Veridian Dynamics'
  }"
></blog-post>
```

#### 传入一个对象的所有 property

如果你想要将一个对象的所有 property 都作为 prop 传入，你可以使用不带参数的 `v-bind` (取代 `v-bind:prop-name`)。例如，对于一个给定的对象 `post`：

```js
post: {
  id: 1,
  title: 'My Journey with Vue'
}
```

下面的模板：

```html
<blog-post v-bind="post"></blog-post>
```

等价于：

```html
<blog-post
  :id="post.id"
  :title="post.title"
></blog-post>
```

### 单向数据流

所有的 prop 都使得其父子 prop 之间形成了一个**单向下行绑定**：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外变更父级组件的状态，从而导致你的应用的数据流向难以理解。

额外的，每次父级组件发生变更时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你**不**应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。

这里有两种常见的试图变更一个 prop 的情形：

1. **这个 prop 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 prop 数据来使用。**在这种情况下，最好定义一个本地的 data property 并将这个 prop 用作其初始值：

    ```js
    props: ['initialCounter'],
    data: function () {
      return {
        counter: this.initialCounter
      }
    }
    ```

2. **这个 prop 以一种原始的值传入且需要进行转换。**在这种情况下，最好使用这个 prop 的值来定义一个计算属性：

    ```js
    props: ['size'],
    computed: {
      normalizedSize: function () {
        return this.size.trim().toLowerCase()
      }
    }
    ```

> :exclamation:注意在 JavaScript 中对象和数组是通过引用传入的，所以对于一个数组或对象类型的 prop 来说，在子组件中改变变更这个对象或数组本身**将会**影响到父组件的状态。



## 自定义事件

在 Vue 中，自定义事件是一种在组件之间传递信息的方式，特别是在父子组件之间。**当子组件需要向父组件**传递数据时，通常使用自定义事件。

#### 自定义事件是什么 ?

当点击这个按钮时，我们需要告诉父级组件放大所有博文的文本。Vue 实例提供了一个**自定义事件**的系统来解决这个问题。父级组件可以像处理 native DOM 事件一样通过 `v-on` 监听子组件实例的任意事件：

```html
<blog-post
  ...
  @enlarge-text="postFontSize += 0.1"
>
</blog-post>
```

>事件后面往往是 **一个方法** 或 **一个有效的 JavaScript 表达式**

同时子组件可以通过调用内建的 [**`$emit`** 方法](https://v2.cn.vuejs.org/v2/api/#vm-emit)并传入事件名称来触发一个事件：

```html
<button @click="$emit('enlarge-text')">
  Enlarge text
</button>
```

有了这个 `v-on:enlarge-text="postFontSize += 0.1"` 监听器，父级组件就会接收该事件并更新 `postFontSize` 的值。

##### 使用自定义事件抛出一个值

例如我们可能想让 `<blog-post>` 组件决定它的文本要放大多少。这时可以使用 `$emit` 的第二个参数来提供这个值：

```html
<button @click="$emit('enlarge-text', 0.1)">
  Enlarge text
</button>
```

如果这个事件处理函数是**一个 JS 表达式**，然后当在父级组件监听这个事件的时候，我们可以通过 **`$event`** 访问到被抛出的这个值：

```html
<blog-post
  ...
  @enlarge-text="postFontSize += $event"
></blog-post>
```

如果这个事件处理函数是**一个方法**：

```html
<blog-post
  ...
  @enlarge-text="onEnlargeText"
></blog-post>
```

那么这个值将会作为第一个参数传入这个方法：

```js
methods: {
  onEnlargeText: function (enlargeAmount) {
    this.postFontSize += enlargeAmount
  }
}
```



### 子传父

我们以一个发送消息的按钮为例，

数据在子组件中：

```vue
<button @click="sendMessage"></button>

<script>
export default {
  methods: {
    sendMessage() {
      // 使用 $emit 触发自定义事件 'message-sent'
      this.$emit('message-sent', 'Hello, World");
    }
  }
}
</script>
```

事件定义在父组件中：

```vue
<child-component @message-sent="receiveMessage"></child-component>

<script>
// 引入子组件
import ChildComponent from './ChildComponent.vue';

export default {
  components: {
    ChildComponent
  },
  data() {
    return {
      message: ''
    };
  },
  methods: {
    // 监听 'message-sent' 事件并处理接收到的数据
    receiveMessage(msg) {
      this.message = msg;
    }
  }
}
</script>
```





### 事件名

不同于组件和 prop，事件名不存在任何自动化的大小写转换。而是触发的事件名需要**完全匹配**监听这个事件所用的名称。举个例子，如果触发一个 camelCase 名字的事件：

```js
this.$emit('myEvent')
```

则监听这个名字的 kebab-case 版本是不会有任何效果的：

```html
<!-- 没有效果 -->
<my-component v-on:my-event="doSomething"></my-component>
```

不同于组件和 prop，事件名不会被用作一个 JavaScript 变量名或 property 名，所以就没有理由使用 camelCase 或 PascalCase 了。并且 `v-on` 事件监听器在 **DOM 模板**中会被自动转换为全小写 (因为 HTML 是大小写不敏感的)，所以 `v-on:myEvent` 将会变成 `v-on:myevent`——导致 `myEvent` 不可能被监听到。

因此，我们推荐你**始终使用 kebab-case 的事件名**。

### 将原生事件绑定到组件

你可能有很多次想要在一个**组件的根元素**上直接监听一个原生事件。

> :star:在 Vue 中，**一个组件的根元素**指的是组件模板中最外层的 HTML 元素。这个元素是 Vue 渲染组件时的最外层容器，其他所有元素都在这个元素内部。

这时，你可以使用 `v-on` 的 `.native` 修饰符：

```html
<base-input v-on:focus.native="onFocus"></base-input>
```



## 组件的 `v-model`

一个组件上的 `v-model` 默认会利用名为 `value` 的 prop 和名为 `input` 的事件，但是像单选框、复选框等类型的输入控件可能会将 `value` attribute 用于[不同的目的](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox#Value)。

`model` 选项可以用来避免这样的冲突：

```js
Vue.component('base-checkbox', {
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    checked: Boolean
  },
  template: `
    <input
      type="checkbox"
      v-bind:checked="checked"
      v-on:change="$emit('change', $event.target.checked)"
    >
  `
})
```

现在在这个组件上使用 `v-model` 的时候：

```html
<base-checkbox v-model="lovingVue"></base-checkbox>
```

这里的 `lovingVue` 的值将会传入这个名为 `checked` 的 prop。同时当 `<base-checkbox>` 触发一个 `change` 事件并附带一个新的值的时候，这个 `lovingVue` 的 property 将会被更新。

> :exclamation:注意你仍然需要在组件的 `props` 选项里声明 `checked` 这个 prop。



## 插槽

### 插槽内容

插槽允许你像这样合成组件：

```html
<navigation-link url="/profile">
  Your Profile
</navigation-link>
```

然后你在 `<navigation-link>` 的模板中可能会写为：

```html
<a
  v-bind:href="url"
  class="nav-link"
>
  <slot></slot>
</a>
```

当组件渲染的时候，`<slot></slot>` 将会被替换为“Your Profile”。插槽内可以包含任何模板代码，包括 HTML：

```html
<navigation-link url="/profile">
  <!-- 添加一个 Font Awesome 图标 -->
  <span class="fa fa-user"></span>
  Your Profile
</navigation-link>
```

甚至其它的组件：

```html
<navigation-link url="/profile">
  <!-- 添加一个图标的组件 -->
  <font-awesome-icon name="user"></font-awesome-icon>
  Your Profile
</navigation-link>
```

如果 `<navigation-link>` 的 `template` 中**没有**包含一个 `<slot>` 元素，则该组件起始标签和结束标签之间的任何内容都会被抛弃。

### 后备内容

有时为一个插槽设置具体的后备 (也就是默认的) 内容是很有用的，它只会在没有提供内容的时候被渲染。

```html
<button type="submit">
  <slot>Submit</slot>
</button>
```

现在当我在一个父级组件中使用 `<submit-button>` 并且不提供任何插槽内容时：

```html
<submit-button></submit-button>
```

后备内容“Submit”将会被渲染：

```html
<button type="submit">
  Submit
</button>
```

但是如果我们提供内容：

```html
<submit-button>
  Save
</submit-button>
```

则这个提供的内容将会被渲染从而取代后备内容：

```html
<button type="submit">
  Save
</button>
```

### 具名插槽

有时我们需要多个插槽。例如对于一个带有如下模板的 `<base-layout>` 组件：

```html
<div class="container">
  <header>
    <!-- 我们希望把页头放这里 -->
  </header>
  <main>
    <!-- 我们希望把主要内容放这里 -->
  </main>
  <footer>
    <!-- 我们希望把页脚放这里 -->
  </footer>
</div>
```

对于这样的情况，`<slot>` 元素有一个特殊的 attribute：`name`。这个 attribute 可以用来定义额外的插槽：

```html
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```

一个不带 `name` 的 `<slot>` 出口会带有**隐含的名字“default”**。

在向具名插槽提供内容的时候，我们可以在一个 `<template>` 元素上使用 **`v-slot`** 指令，并以 `v-slot` 的参数的形式提供其名称：

```html
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```

现在 **`<template>` 元素中的所有内容**都将会被传入**相应的插槽**。任何没有被包裹在带有 `v-slot` 的 `<template>` 中的内容都会被视为默认插槽的内容。

然而，如果你希望更明确一些，仍然可以在一个 `<template>` 中包裹默认插槽的内容：

```html
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <template v-slot:default>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </template>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```

任何一种写法都会渲染出：

```html
<div class="container">
  <header>
    <h1>Here might be a page title</h1>
  </header>
  <main>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </main>
  <footer>
    <p>Here's some contact info</p>
  </footer>
</div>
```

注意 **`v-slot` 只能添加在 `<template>` 上** (只有[一种例外情况](https://v2.cn.vuejs.org/v2/guide/components-slots.html#独占默认插槽的缩写语法))，这一点和已经废弃的 [`slot` attribute](https://v2.cn.vuejs.org/v2/guide/components-slots.html#废弃了的语法) 不同。

### 作用域插槽

#### 编译作用域

```html
<navigation-link url="/profile">
  Clicking here will send you to: {{ url }}
  <!--
  这里的 `url` 会是 undefined，因为其 (指该插槽的) 内容是
  _传递给_ <navigation-link> 的而不是
  在 <navigation-link> 组件*内部*定义的。
  -->
</navigation-link>
```

作为一条规则，请记住：

> 父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。

#### 插槽 prop

有时让插槽内容能够访问子组件中才有的数据是很有用的。例如，设想一个带有如下模板的 `<current-user>` 组件：

```html
<span>
  <slot>{{ user.lastName }}</slot>
</span>
```

我们可能想换掉备用内容，用名而非姓来显示。如下：

```html
<current-user>
  {{ user.firstName }}
</current-user>
```

然而上述代码不会正常工作，因为只有 `<current-user>` 组件可以访问到 `user`，而我们提供的内容是在父级渲染的。

为了让 `user` 在父级的插槽内容中可用，我们可以将 `user` 作为 `<slot>` 元素的一个 attribute 绑定上去：

```html
<span>
  <slot v-bind:user="user">
    {{ user.lastName }}
  </slot>
</span>
```

绑定在 `<slot>` 元素上的 attribute 被称为**插槽 prop**。现在在父级作用域中，我们可以使用带值的 `v-slot` 来定义我们提供的插槽 prop 的名字，以便使用父级的值：

```html
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>
```

在这个例子中，我们选择将包含所有插槽 prop 的对象命名为 `slotProps`，但你也可以使用任意你喜欢的名字。

##### 独占默认插槽的缩写语法

在上述情况下，当被提供的内容***只有***默认插槽时，组件的标签才可以被当作插槽的模板来使用。这样我们就可以把 `v-slot` 直接用在组件上：

```html
<current-user v-slot:default="slotProps">
  {{ slotProps.user.firstName }}
</current-user>
```

这种写法还可以更简单。就像假定未指明的内容对应默认插槽一样，不带参数的 `v-slot` 被假定对应默认插槽：

```html
<current-user v-slot="slotProps">
  {{ slotProps.user.firstName }}
</current-user>
```

注意默认插槽的缩写语法**不能**和具名插槽混用，因为它会导致作用域不明确：

```html
<!-- 无效，会导致警告 -->
<current-user v-slot="slotProps">
  {{ slotProps.user.firstName }}
  <template v-slot:other="otherSlotProps">
    slotProps is NOT available here
  </template>
</current-user>
```

只要出现多个插槽，请始终为***所有的***插槽使用完整的基于 `<template>` 的语法：

```html
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>

  <template v-slot:other="otherSlotProps">
    ...
  </template>
</current-user>
```

##### 解构插槽 prop

作用域插槽的内部工作原理是将你的插槽内容包裹在一个拥有单个参数的函数里：

```js
function (slotProps) {
  // 插槽内容
}
```

这意味着 `v-slot` 的值实际上可以是任何能够作为函数定义中的参数的 JavaScript 表达式。所以在支持的环境下 ([单文件组件](https://v2.cn.vuejs.org/v2/guide/single-file-components.html)或[现代浏览器](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#浏览器兼容))，你也可以使用 [ES2015 解构](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#解构对象)来传入具体的插槽 prop，如下：

```html
<current-user v-slot="{ user }">
  {{ user.firstName }}
</current-user>
```

这样可以使模板更简洁，尤其是在该插槽提供了多个 prop 的时候。它同样开启了 prop 重命名等其它可能，例如将 `user` 重命名为 `person`：

```html
<current-user v-slot="{ user: person }">
  {{ person.firstName }}
</current-user>
```

你甚至可以定义后备内容，用于插槽 prop 是 undefined 的情形：

```html
<current-user v-slot="{ user = { firstName: 'Guest' } }">
  {{ user.firstName }}
</current-user>
```

## 动态组件 & 异步组件

### 在动态组件上使用 `keep-alive`

我们之前在一个多标签的界面中使用 `is` attribute 来切换不同的组件：

```html
<component v-bind:is="currentTabComponent"></component>
```

当在这些组件之间切换的时候，你有时会想保持这些组件的状态，以避免反复重新渲染导致的性能问题。例如我们来展开说一说这个[多标签界面](https://v2.cn.vuejs.org/v2/guide/components-dynamic-async.html)：

你会注意到，如果你选择了一篇文章，切换到 *Archive* 标签，然后再切换回 *Posts*，是不会继续展示你之前选择的文章的。这是因为你每次切换新标签的时候，Vue 都创建了一个新的 `currentTabComponent` 实例。

重新创建动态组件的行为通常是非常有用的，但是在这个案例中，我们更希望那些标签的组件实例能够被在它们第一次被创建的时候缓存下来。为了解决这个问题，我们可以用一个 `<keep-alive>` 元素将其动态组件包裹起来。

```html
<!-- 失活的组件将会被缓存！-->
<keep-alive>
  <component v-bind:is="currentTabComponent"></component>
</keep-alive>
```

### 异步组件

在大型应用中，我们可能需要将应用分割成小一些的代码块，并且只在需要的时候才从服务器加载一个模块。为了简化，Vue 允许你以一个工厂函数的方式定义你的组件，这个工厂函数会异步解析你的组件定义。Vue 只有在这个组件需要被渲染的时候才会触发该工厂函数，且会把结果缓存起来供未来重渲染。例如：

```js
Vue.component('async-example', function (resolve, reject) {
  setTimeout(function () {
    // 向 `resolve` 回调传递组件定义
    resolve({
      template: '<div>I am async!</div>'
    })
  }, 1000)
})
```

如你所见，这个工厂函数会收到一个 `resolve` 回调，这个回调函数会在你从服务器得到组件定义的时候被调用。你也可以调用 `reject(reason)` 来表示加载失败。这里的 `setTimeout` 是为了演示用的，如何获取组件取决于你自己。一个推荐的做法是将异步组件和 [webpack 的 code-splitting 功能](https://webpack.js.org/guides/code-splitting/)一起配合使用：

```js
Vue.component('async-webpack-example', function (resolve) {
  // 这个特殊的 `require` 语法将会告诉 webpack
  // 自动将你的构建代码切割成多个包，这些包
  // 会通过 Ajax 请求加载
  require(['./my-async-component'], resolve)
})
```

你也可以在工厂函数中返回一个 `Promise`，所以把 webpack 2 和 ES2015 语法加在一起，我们可以这样使用动态导入：

```js
Vue.component(
  'async-webpack-example',
  // 这个动态导入会返回一个 `Promise` 对象。
  () => import('./my-async-component')
)
```

当使用[局部注册](https://v2.cn.vuejs.org/v2/guide/components-registration.html#局部注册)的时候，你也可以直接提供一个返回 `Promise` 的函数：

```js
new Vue({
  // ...
  components: {
    'my-component': () => import('./my-async-component')
  }
})
```



## 递归组件

### 骨架屏

#### 介绍

在网络较慢，需要长时间等待加载的情况下，骨架屏可以在详细页面元素未展现时，把 DOM 结构通过简单的方块或圆形勾勒出来，相对于传统的转圈等待与白屏来说，用户体验更好。下面请根据题目要求，使用 Vue 封装一个灵活的骨架屏组件。

#### 准备

开始答题前，需要先打开本题的项目代码文件夹，目录结构如下：

```js
├── components
│   ├── List
│   │   ├── content.js
│   │   └── index.js
│   └── Skeleton
│       ├── index.js
│       └── item.js
├── css
│   └── style.css
├── effect.gif
├── index.html
└── lib
    └── vue.min.js
```

其中：

- `index.html` 是主页面。
- `components/list` 是提供的列表组件。
- `components/Skeleton` 是骨架屏组件。
- `lib` 是存放项目依赖的文件夹。
- `css` 是存放项目样式的文件夹。
- `effect.gif` 是项目目标完成效果图。

#### 目标

找到 `Skeleton/item.js` 中的 TODO 部分，完成以下目标：

1. 使用 `index.html` 中传递过去的数据 `paragraph`，并结合 **Vue 递归组件**的知识，完成骨架屏组件的编写。

**`paragraph` 中的属性说明如下：**

| 属性名     | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| `type`     | 骨架屏的容器类型，其属性值共有 `row`（行）、`col`（列）、`rect`（矩形）和 `circle`（圆形）四种类型。 |
| `style`    | 容器类型 `type` 为 `rect`（矩形）或 `circle`（圆形）对应的样式。 |
| `rowStyle` | 容器类型 `type` 为 `row`（行）时对应的样式。                 |
| `colStyle` | 容器类型 `type` 为 `col`（列）时对应的样式。                 |
| `rows`     | 类型 `type` 为 `row`（行）的容器数组，里面的每一个对象都是嵌套的子模块，即，`row`（行）容器。 |
| `cols`     | 类型 `type` 为 `col`（列）的容器数组，里面的每一个对象都是嵌套的子模块，即 `col`（列）容器。 |

**本题中的骨架屏结构图及说明如下：**

![骨架屏结构示例图](https://doc.shiyanlou.com/courses/16666/1777363/e1f5c351cf2a60d70b31d2d3960ce781-0)

- 第一行（标记 1）为 1 个矩形占位。
- 第二行（标记 2）分为两列（蓝色框），左边一列为三行组成，右边一列为 1 个矩形占位。
- 第二行左边一列分别为如下构成：第一行（标记 ①）为 1 个矩形占位，第二行（标记 ②）为 2 个矩形占位，第三行（标记 ③）为 4 个圆形+1 个矩形占位。

**`type` 和 `DOM` 结构的对应关系如下：**

```html
<div class="ske-${type}-container">
  <div class="ske ske-${type}" :style="style">
    <!-- ...... 根据类型判断此处是否需要添加元素。TIPS: row 里面可以继续嵌套 row -->
  </div>
</div>
```

在上面的示例中：

- `${type}` 的值为对应的容器类型 `row`、`col`、`rect` 或 `circle`。
- `style` 表示 `class="ske ske-${type}"` 的元素对应的样式：

如果 `${type}` 是 `rect` 或 `circle` 则使用 `style` 属性。其 DOM 结构如下：

```html
<div class="ske-rect-container">
  <div class="ske ske-rect" :style="style"></div>
</div>
```

如果 `${type}` 是 `row` 或 `col`，则使用 `rowStyle` 或者 `colStyle` 属性。其 DOM 结构如下：

```html
<!-- rowStyle/colStyle 使用示例  -->
<div class="ske ske-row" :style="row.rowStyle" v-for="row in paragraph.rows">
  <!--此处代码省略...-->
</div>
```

2. 使用 `index.html` 中传递过去的数据 `active` 完成骨架屏组件的闪烁功能：如果 `active` 为 `true`, 则给容器类型 `type` 为 `rect`（矩形）或 `circle`（圆形）的组件内层 `class="ske ske-rect"` 或 `class="ske ske-circle"` 的元素添加类名 `.ske-ani`；否则不添加。

`index.js`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <script src="./lib/vue.min.js"></script>
    <link rel="stylesheet" href="./css/style.css" />
  </head>
  <body>
    <script src="./components/List/index.js"></script>
    <script src="./components/List/content.js"></script>
    <script src="./components/Skeleton/item.js"></script>
    <script src="./components/Skeleton/index.js"></script>
    <div id="app">
      <List v-for="i in 5">
        <div v-show="loading">
          <!-- 骨架屏组件 -->
          <Skeleton :active="active" :paragraph="paragraph" />
        </div>
        <!-- 渲染真正的列表内容 -->
        <List-content v-show="!loading" />
      </List>
    </div>
    <script>
      var app = new Vue({
        el: "#app",
        data() {
          return {
            loading: true,
            active: true,
            paragraph: {
              // 骨架屏组件对应数据
              type: "row",
              rows: [
                {
                  rowStyle: {
                    margin: "10px 0 14px 14px",
                  },
                  type: "rect",
                  style: {
                    width: "170px",
                    height: "14px",
                  },
                },
                {
                  type: "col",
                  cols: [
                    {
                      colStyle: {
                        marginLeft: "15px",
                        width: "80%",
                      },
                      type: "row",
                      rows: [
                        {
                          type: "row",
                          rowStyle: {
                            marginTop: "12px",
                          },
                          rows: [
                            {
                              type: "rect",
                              style: {
                                width: "200px",
                                height: "24px",
                              },
                            },
                            {
                              type: "rect",
                              style: {
                                width: "90%",
                                height: "14px",
                                borderRadius: "3px",
                                marginTop: "18px",
                              },
                            },
                            {
                              type: "rect",
                              style: {
                                width: "65%",
                                height: "14px",
                                borderRadius: "3px",
                                marginTop: "6px",
                              },
                            },
                          ],
                        },
                        {
                          type: "col",
                          rowStyle: {
                            marginTop: "28px",
                          },
                          cols: [
                            {
                              type: "circle",
                              style: {
                                width: "25px",
                                height: "25px",
                                marginRight: "4px",
                              },
                            },
                            {
                              type: "circle",
                              style: {
                                width: "25px",
                                height: "25px",
                                marginRight: "4px",
                              },
                            },
                            {
                              type: "circle",
                              style: {
                                width: "25px",
                                height: "25px",
                                marginRight: "4px",
                              },
                            },
                            {
                              type: "circle",
                              style: {
                                width: "25px",
                                height: "25px",
                              },
                            },
                            {
                              type: "rect",
                              style: {
                                width: "150px",
                                height: "25px",
                                marginLeft: "12px",
                                borderRadius: "100px",
                              },
                            },
                          ],
                        },
                      ],
                    },
                    {
                      type: "row",
                      rows: [
                        {
                          type: "rect",
                          style: {
                            width: "135px",
                            height: "135px",
                          },
                        },
                      ],
                    },
                  ],
                },
              ],
            },
          };
        },
        mounted() {
          // 为了代码简洁此处不请求真实数据，使用定时器模拟请求的延迟
          setTimeout(() => {
            // ......当请求到数据时，开始渲染，loading状态结束
            this.loading = false;
          }, 5000);
        },
        methods: {},
      });
    </script>
  </body>
</html>
```

`Skeleton/index.js`

```js
/*
 * 骨架屏组件
 */
const SkeletonTemplate = `<div class="skeleton-wrapper">
    <div class="skeleton-content">
      <item :paragraph="paragraph" :active="active"></item>
    </div>
  </div>
`;
Vue.component("Skeleton", {
  name: "Skeleton",
  template: SkeletonTemplate,
  props: {
    active: {
      default: false,
    },
    paragraph: {},
  },
  data() {},
  watch: {},
  mounted() {},
  methods: {},
});
```

`item.js`

```js
/*
 * 骨架屏渲染组件
 */
let ItemTemplate = ``;
// TODO 请补充完整Template，完成组件代码编写
ItemTemplate += `
<div :class="'ske-'+paragraph.type+'-container'">
  <div v-for="item in arrIs(paragraph)" :class="classIs(item)" :style="styleIs(item)" >
    <item :paragraph="item" :active="active"></item>
  </div>
</div>
`;

Vue.component("item", {
  name: "item",
  template: ItemTemplate,
  props: ["paragraph", "active"],
  data() {
    return {
      typeList: ["rect", "circle"],
      classPrefix: "ske ske-",
      activeClass: " ske-ani",
    };
  },
  watch: {},
  methods: {
    // 判断是 rows or cols
    arrIs(obj) {
      if (obj?.rows) return obj.rows;
      else if (obj?.cols) return obj.cols;
      else return [];
    },
    // 判断class类
    classIs(obj) {
      if (this.typeList.includes(obj.type)) {
        return (
          this.classPrefix + obj.type + (this.active ? this.activeClass : "")
        );
      } else {
        return this.classPrefix + obj.type;
      }
    },
    // 判断样式
    styleIs(obj) {
      if (obj?.style && obj?.rowStyle) return { ...obj.style, ...obj.rowStyle };
      else if (obj?.style) return obj.style;
      else if (obj?.rowStyle) return obj.rowStyle;
      else if (obj?.colStyle) return obj.colStyle;
      else return {};
    },
  },
});
```





# 技巧



## 使用index作为key

```vue
<a
            style="background-color: #f6edd4"
            class="iconfont"
            :class="{ 'icon-selected': currentIndex == index }"
            :style="{ 'background-color': item }"
            v-for="(item, index) in bgList"
            :key="index"
            @click="changeColor(index)"
></a>
