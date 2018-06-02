# vue

## 基础

## 安装

### 引入

直接下载并用 `<script>` 标签引入，`Vue` 会被注册为一个全局变量。 

```
//本地引入
<script src='vue.js'></script>
//
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

### npm

>```
>npm install vue
>```



## vue实例

### 创建一个实例

每个 Vue 应用都是通过用 Vue 函数创建一个新的 Vue 实例开始的：

```
new Vue({
    //content
})
```

### 数据与方法

- 当一个 Vue 实例被创建时，它向 Vue 的**响应式系统**中加入了其 `data` 对象中能找到的所有的属性 。
- 只有当实例被创建时 data 中存在的属性才是响应式的。
- 除了数据属性，Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 `$`，以便与用户定义的属性区分开来 

### 实例生命周期钩子

每个 Vue 实例在被创建时都要经过一系列的初始化过程，同时在这个过程中也会运行一些叫做生命周期钩子的函数。生命周期钩子的 `this `上下文指向调用它的 Vue 实例



## 模版语法

### 插值

#### 文本

数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

```
<span>Message: {{ msg }}</span>
```

Mustache 标签将会被替代为对应数据对象上 msg 属性的值。

#### 原始html

双大括号中数据包含html代码，会被解释为普通文本，而非 HTML 代码。要输出真正的html代码，使用`v-html`指令：

```
<span v-html="..."></span>
```

#### 使用js表达式

```
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}
```

这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含**单个表达式** 

### 指令

#### 参数

一些指令能够接收一个“参数”，在指令名称之后以冒号表示。 

```
<a v-bind:href="url">...</a>
```

在这里 `href` 是参数，告知 `v-bind` 指令将该元素的 `href` 特性与表达式 `url` 的值绑定。 

#### 修饰符

修饰符 (Modifiers) 是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。 

```
<form v-on:submit.prevent="onSubmit">...</form>
```

`.prevent` 修饰符告诉 `v-on` 指令对于触发的事件调用`event.preventDefault()` 。

### 缩写

```
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>
```

```
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>
```



## 计算属性和侦听器

### 计算属性

在vue实例中添加`computed`属性，在属性中定义方法用于处理任何复杂逻辑。

```
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
})
```

### 方法属性

在vue实例中添加`methods`属性，在属性中定义相应方法。

```
var vm = new Vue({
    el: 'example',
    data: {
        message: 'Hello'
    }
    methods:{
       reversedMessage: function () {
       return this.message.split('').reverse().join('') 
    }
})
```

计算属性和方法属性能达到同样的效果。

- 计算属性只有在它的相关依赖发生改变时才会重新求值。
- 若相关依赖未改变，计算属性会立即返回之前的计算结果，而不必再次执行函数。
- 每当触发重新渲染时，调用方法将**总会**再次执行函数。 

### 侦听属性

在vue实例中添加 `watch`属性,在属性中定义方法用于观察和响应 Vue 实例上的数据变动。

```
var vm = new Vue({
    el: 'example'
    data: {
        
    }
    watch:{
        
    }
})
```



## Class 与 Style 绑定

### 绑定 HTML Class

#### 对象语法

- 给 v-bind:class 一个对象，以动态地切换 class：

```
<div v-bind:class="{ active: isActive }"></div>
```

active 这个 class 存在与否将取决于数据属性 isActive。

- v-bind:class 指令也可以与普通的 class 属性共存。

```
<div class="static" v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>
// Vue实例中的data
data: {
  isActive: true,
  hasError: false
}
//结果
<div class="static active"></div>
```

- 绑定的数据对象不必内联定义在模板里。

```
<div v-bind:class="classObject"></div>
//Vue实例中的data
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
```

#### 数组语法

- 可以把一个数组传给 v-bind:class，以应用一个 class 列表。

```
<div v-bind:class="[activeClass, errorClass]"></div>
//Vue实例中的data
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
//结果
<div class="active text-danger"></div>
```

- 根据条件切换列表中的 class，可以用三元表达式。

```
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```

- 在数组语法中也可以使用对象语法.

```
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```

#### 用在组件上

在一个自定义组件上使用 `class` 属性时，这些类将被添加到该组件的根元素上面。这个元素上已经存在的类不会被覆盖。 

```
<my-component class="baz boo"></my-component>
//js
Vue.component('my-component', {
  template: '<p class="foo bar">Hi</p>'
})
//结果
<p class="foo bar baz boo">Hi</p>
```

###绑定内联样式

#### 对象语法

`v-bind:style `的对象语法十分直观，看着非常像 CSS，但其实是一个 JavaScript 对象。 

```
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
//Vue实例中的data属性
data: {
  activeColor: 'red',
  fontSize: 30
}
```

- 直接绑定到一个样式对象.

```
<div v-bind:style="styleObject"></div>
// Vue实例中的data属性
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```

#### 数组语法

v-bind:style 的数组语法可以将多个样式对象应用到同一个元素上。

```
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```

- 自动添加前缀：当 `v-bind:style` 使用需要添加`浏览器引擎前缀`的 CSS 属性时，Vue.js 会自动侦测并添加相应的前缀。 
- 为 `style` 绑定中的属性提供一个包含多个值的数组，常用于提供多个带前缀的值:

```
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```

只会渲染数组中最后一个被浏览器支持的值，如果浏览器支持不带浏览器前缀的 flexbox，那么就只会渲染 display: flex。



## 条件渲染

### v-if

v-if 是一个指令，所以必须将它添加到一个元素上。

```
<h1 v-if="ok">Yes</h1>
<h1 v-else>No</h1>
```

#### 渲染分组

切换多个元素可以把一个 `<template>` 元素当做不可见的包裹元素，并在上面使用 `v-if`。 最终的渲染结果将不包含 <template>元素。

```
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

#### v-else

`v-else` 元素必须紧跟在带 `v-if` 或者 `v-else-if` 的元素的后面，否则它将不会被识别。 

#### v-if-else

充当 v-if 的“else-if 块”，可以连续使用。

```
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

#### 用key管理可复用元素

Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。

添加一个具有唯一值的 key 属性，元素是完全独立的，不要复用它们。

```
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>

<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>
```

注意，<label> 元素仍然会被高效地复用，因为它们没有添加 key 属性.

### v-show

带有 `v-show` 的元素始终会被渲染并保留在 DOM 中。`v-show` 只是简单地切换元素的 CSS 属性 `display`。 

### v-fi v-show

- `v-if` 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被**销毁**和**重建**。 
- `v-if` 也是**惰性的**：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。 
- `v-show` 不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。 
- v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。



## 列表渲染

### v-for

`v-for` 指令需要使用`item in items` 形式的特殊语法，`items` 是源数据数组，并且 `item` 是数组元素迭代的别名。 

```
<ul id="example-1">
  <li v-for="item in items">
    {{ item.message }}
  </li>
</ul>
// vue实例中的data
 data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
```

- `v-for` 还支持一个可选的**第二个参数**为当前项的**索引**。 

```
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

- 可以用 `of` 替代 `in` 作为分隔符，因为它是最接近 JavaScript 迭代器的语法 .

```
<div v-for="item of items"></div>
```

### 对象的v-for

```
  <li v-for="value in object">
    {{ value }}
  </li>
// vue实例中的data
 data: {
    object: {
      firstName: 'John',
      lastName: 'Doe',
      age: 30
    }
  }
```

- 可以提供第二个的参数为键名

```
<div v-for="(value, key) in object">
  {{ key }}: {{ value }}
</div>
```

- 第三个参数为索引

```
<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }}: {{ value }}
</div>
```

### key

- 当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用“就地复用”策略。
- 如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。

为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，需要为每项提供一个唯一 key 属性。需要用 v-bind 来绑定动态值。

```
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```

### 数组更新检测

#### 变异方法

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

调用这些方法将会触发视图更新。但会改变被这些方法调用的原始数组。

#### 替换数组

不会改变原始数组，但**总是返回一个新数组**。当使用非变异方法时，可以用新数组替换旧数组： 

```
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```

#### 注意

由于 JavaScript 的限制，Vue 不能检测以下变动的数组：

- 利用索引直接设置一个项时，例如：`vm.items[indexOfItem] = newValue`
- 修改数组的长度时，例如：`vm.items.length = newLength`

```
var vm = new Vue({
  data: {
    items: ['a', 'b', 'c']
  }
})
vm.items[1] = 'x' // 不是响应性的
vm.items.length = 2 // 不是响应性的
```

两种方式都可以实现和 `vm.items[indexOfItem] = newValue` 相同的效果，同时也将触发状态更新： 

```
Vue.set(vm.items, indexOfItem, newValue)
```

```
vm.items.splice(indexOfItem, 1, newValue)
```

也可以使用 `vm.$set `实例方法，该方法是全局方法 Vue.set 的一个别名：

```
vm.$set(vm.items, indexOfItem, newValue)
```

### 对象更新注意事项

由于 JavaScript 的限制，Vue 不能检测对象属性的添加或删除：

```
var vm = new Vue({
  data: {
    a: 1
  }
})
// `vm.a` 现在是响应式的

vm.b = 2
// `vm.b` 不是响应式的
```

- 对于已经创建的实例，Vue 不能动态添加根级别的响应式属性。

- 但是，可以使用`Vue.set(object, key, value)` 方法向嵌套对象添加响应式属性 。

  ```
  var vm = new Vue({
    data: {
      userProfile: {
        name: 'Anika'
      }
    }
  })
  ```

  + 添加一个新的 age 属性到嵌套的 userProfile 对象：

  ```
  Vue.set(vm.userProfile, 'age', 27)
  ```

  + 还可以使用 vm.$set 实例方法，它只是全局 Vue.set 的别名：

  ```
  vm.$set(vm.userProfile, 'age', 27)
  ```

### 显示过滤/排序结果

想要显示一个数组的过滤或排序副本，而不实际改变或重置原始数据。可以创建返回过滤或排序数组的计算属性。

```
<li v-for="n in evenNumbers">{{ n }}</li>
//
data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
computed: {
  evenNumbers: function () {
    return this.numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```

- 在计算属性不适用的情况下 (例如，在嵌套 `v-for` 循环中) 可以使用一个 method 方法： 

  ```
  <li v-for="n in even(numbers)">{{ n }}</li>
  //
  data: {
    numbers: [ 1, 2, 3, 4, 5 ]
  },
  methods: {
    even: function (numbers) {
      return numbers.filter(function (number) {
        return number % 2 === 0
      })
    }
  }
  ```

  

### template中的v-for

利用带有 v-for 的 <template> 渲染多个元素.

```
 <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider"></li>
  </template>
```

### v-if v-for

- 当它们处于同一节点，v-for 的优先级比 v-if 更高，意味着 v-if 将分别重复运行于每个 v-for 循环中。

```
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
</li>
```

- 如果是有条件地跳过循环的执行，那么可以将 `v-if` 置于外层元素 (或<template>)上 。

  ```
  <ul v-if="todos.length">
    <li v-for="todo in todos">
      {{ todo }}
    </li>
  </ul>
  <p v-else>No todos left!</p>
  ```

### 组件的v-for

任何数据都不会被自动传递到组件里，因为组件有自己独立的作用域。为了把迭代数据传递到组件里，我们要用 `props` 。

```
<my-component
  v-for="(item, index) in items"
  v-bind:item="item"
  v-bind:index="index"
  v-bind:key="item.id"
></my-component>
```



## 事件处理

### 监听事件

可以用 `v-on` 指令监听 DOM 事件，并在触发时运行一些 JavaScript 代码。

> ```
> <button v-on:click="counter += 1">Add 1</button>
> ```

### 事件处理方法

直接把 JavaScript 代码写在 v-on 指令中是不可行的，因此 v-on 还可以接收一个需要调用的方法名称。

> ```
> <button v-on:click="greet">Greet</button>
> //
>   methods: {
>     greet: function (event) {
>       // `this` 在方法里指向当前 Vue 实例
>       alert('Hello ' + this.name + '!')
>       // `event` 是原生 DOM 事件
>       if (event) {
>         alert(event.target.tagName)
>       }
>     }
> ```

### 内联处理器中的方法

- 除了直接绑定到一个方法，也可以在内联 JavaScript 语句中调用方法： 

>```
><button v-on:click="say('hi')">Say hi</button>
><button v-on:click="say('what')">Say what</button>
> //
>   methods: {
>    say: function (message) {
>      alert(message)
>    }
>```

- 有时也需要在内联语句处理器中访问原始的 DOM 事件。可以用特殊变量 `$event` 把它传入方法： 

> ```
> <button v-on:click="warn('Form cannot be submitted yet.', $event)">Submit</button>
> //
> methods: {
>   warn: function (message, event) {
>     // 现在我们可以访问原生事件对象
>     if (event) event.preventDefault()
>     alert(message)
>   }
> }
> ```

### 事件修饰符

修饰符是由点开头的指令后缀来表示的。

- `.stop`，阻止单击事件继续传播
- `.prevent`，提交事件不再重载页面
- `.capture`，添加事件监听器时使用事件捕获模式 
- `.self`，当在 event.target 是当前元素自身时触发处理函数
- `.once`，点击事件将只会触发一次
- `.passive`，滚动事件的默认行为 (即滚动行为) 将会立即触发

```
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

### 按键修饰符

Vue 允许为 v-on 在监听键盘事件时添加按键修饰符：

```
<!-- 只有在 `keyCode` 是 13 时调用 `vm.submit()` -->
<input v-on:keyup.13="submit">
```

Vue 为最常用的按键提供了别名：

```
<input @keyup.enter="submit">
```

全部的按键别名：

- `.enter`
- `.tab`
- `.delete` (捕获“删除”和“退格”键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

可以通过全局 config.keyCodes 对象自定义按键修饰符别名：

```
// 可以使用 `v-on:keyup.f1`
Vue.config.keyCodes.f1 = 112
```

#### 自动匹配按键修饰符

可直接将 `KeyboardEvent.key`暴露的任意有效按键名转换为 kebab-case 来作为修饰符： 

```
<input @keyup.page-down="onPageDown">
```

### 系统修饰符

用如下修饰符来实现仅在按下相应按键时才触发鼠标或键盘事件的监听器。

- `.ctrl`
- `.alt`
- `.shift`
- `.meta`

```
<!-- Alt + C -->
<input @keyup.alt.67="clear">

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

#### .exact修饰符

.exact 修饰符允许你控制由精确的系统修饰符组合触发的事件。

```
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```

#### 鼠标按钮修饰符

这些修饰符会限制处理函数仅响应特定的鼠标按钮。

- `.left`
- `.right`
- `.middle`



## 表单输入绑定

### 基本用法

- 用 `v-model` 指令在表单 `<input>` 及 `<textarea>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。 
- `v-model` 会忽略所有表单元素的 `value`、`checked`、`selected` 特性的初始值而总是将 Vue 实例的数据作为数据来源。 

#### 文本

```
<input v-model="message" placeholder="edit me">
<p>Message is: {{ message }}</p>
```

#### 复选框

- 单个复选框，绑定到布尔值：

```
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
```

- 多个复选框，绑定到同一个数组：

```
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames">
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
  <label for="mike">Mike</label>
  <br>
  <span>Checked names: {{ checkedNames }}</span>
  //js
    data: {
    checkedNames: []
  }
```

#### 选择框

- 单选时： 

```
 <select v-model="selected">
    <option disabled value="">请选择</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ selected }}</span>
  //
   data: {
    selected: ''
  }
```

- 多选时 (绑定到一个数组)：

```
 <select v-model="selected" multiple style="width: 50px;">
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <br>
  <span>Selected: {{ selected }}</span>
  //
    data: {
    selected: []
  }
```

- 用 v-for 渲染的动态选项：

```
<select v-model="selected">
  <option v-for="option in options" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<span>Selected: {{ selected }}</span>
//js
data: {
    selected: 'A',
    options: [
      { text: 'One', value: 'A' },
      { text: 'Two', value: 'B' },
      { text: 'Three', value: 'C' }
    ]
  }
```

### 值绑定

对于单选按钮，复选框及选择框的选项，`v-model` 绑定的值通常是静态字符串 (对于复选框也可以是布尔值)： 

```
<!-- 当选中时，`picked` 为字符串 "a" -->
<input type="radio" v-model="picked" value="a">

<!-- `toggle` 为 true 或 false -->
<input type="checkbox" v-model="toggle">

<!-- 当选中第一个选项时，`selected` 为字符串 "abc" -->
<select v-model="selected">
  <option value="abc">ABC</option>
</select>
```

把值绑定到 Vue 实例的一个动态属性上，这时可以用 `v-bind` 实现，并且这个属性的值可以不是字符串。 

#### 复选框

```
<input  type="checkbox"  v-model="toggle"  true-value="yes"  false-value="no">
// 当选中时
vm.toggle === 'yes'
// 当没有选中时
vm.toggle === 'no'
```

`true-value` 和 `false-value` 特性并不会影响输入控件的 `value` 特性，因为浏览器在提交表单时并不会包含未被选中的复选框。 

### 修饰符

#### .lazy

默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步。 添加 lazy 修饰符，从而转变为使用 change 事件进行同步：

```
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg" >
```

#### .number

即使在 `type="number" `时，HTML 输入元素的值也总会返回字符串。自动将用户的输入值转为数值类型，可以给 v-model 添加 number 修饰符：

```
<input v-model.number="age" type="number">
```

#### .trim

要自动过滤用户输入的首尾空白字符，可以给 v-model 添加 trim 修饰符：

```
<input v-model.trim="msg">
```



## 组件基础

### 组件示例

```
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

组件是可复用的**Vue 实例**，且带有一个名字：在这个例子中是 <button-counter>。

通过 new Vue 创建的 Vue 根实例中，把这个组件作为自定义元素来使用。

```
<div id="components-demo">
  <button-counter></button-counter>
</div>
//js
new Vue({ el: '#components-demo' })
```

因为组件是可复用的 Vue 实例，所以它们与 new Vue 接收相同的选项。

### 组件复用

```
<div id="components-demo">
  <button-counter></button-counter>
  <button-counter></button-counter>
  <button-counter></button-counter>
</div>
```

每用一次组件，就会有一个它的新实例被创建。

#### data必须是一个函数

**一个组件的 data 选项必须是一个函数**，因此每个实例可以维护一份被返回对象的独立的拷贝： 

```
data: function () {
  return {
    count: 0
  }
}
```

### 组件的组织

- 为了能在模板中使用，这些组件必须先注册以便 Vue 能够识别。

- 有两种组件的注册类型：**全局注册**和**局部注册**。

- 组件都只是通过 Vue.component 全局注册的：

  ```
  Vue.component('my-component-name', {
    // ... options ...
  })
  ```

  + **全局注册**的组件可以用在其被注册之后的任何 (通过 `new Vue`) 新创建的 Vue 根实例，也包括其组件树中的所有子组件的模板中。 

### 向子组件传递数据

- Prop 是可以在组件上注册的一些自定义特性。

- 当一个值传递给一个 prop 特性的时候，它就变成了那个组件实例的一个属性。

- 用一个`props` 选项将其包含在该组件可接受的 prop 列表中： 

  ```
  Vue.component('blog-post', {
    props: ['title'],
    template: '<h3>{{ title }}</h3>'
  })
  ```

- 一个组件默认可以拥有任意数量的 prop，任何值都可以传递给任何 prop。 

- 在组件实例中访问值，就像访问 data 中的值一样。

### 单个根元素

将模板的内容包裹在一个父元素内，来修复显示错误 (**每个组件必须只有一个根元素**)。

```
<div class="blog-post">
  <h3>{{ post.title }}</h3>
  <div v-html="post.content"></div>
</div>
```

### 向父组件发送消息

调用内建的 `$emit` 方法并传入事件的名字，来向父级组件触发一个事件：

```
<button v-on:click="$emit('enlarge-text')">
  Enlarge text
</button>
```

然后可以用 `v-on` 在博文组件上监听这个事件，就像监听一个原生 DOM 事件一样： 

```
<blog-post
  ...
  v-on:enlarge-text="postFontSize += 0.1"
></blog-post>
```

#### 实用组件抛出一个值

可以使用 $emit 的第二个参数来提供抛出一个特定的值：

```
<button v-on:click="$emit('enlarge-text', 0.1)">
  Enlarge text
</button>
```

然后当在父级组件监听这个事件的时候，通过 `$event` 访问到被抛出的这个值： 

```
<blog-post
  ...
  v-on:enlarge-text="postFontSize += $event"
></blog-post>
```

如果这个事件处理函数是一个方法，那么这个值将会作为第一个参数传入这个方法：

```
<blog-post
  ...
  v-on:enlarge-text="onEnlargeText"
></blog-post>
//js
methods: {
  onEnlargeText: function (enlargeAmount) {
    this.postFontSize += enlargeAmount
  }
}
```

#### 在组件上使用v-model

自定义事件也可以用于创建支持 v-model 的自定义输入组件。

```
<input v-model="searchText">
```

等价于：

```
<input
  v-bind:value="searchText"
  v-on:input="searchText = $event.target.value"
>
```

#### 通过插槽分发内容

Vue 自定义的 <slot> 元素可以向一个组件传递内容。

```
Vue.component('alert-box', {
  template: `
    <div class="demo-alert-box">
      <strong>Error!</strong>
      <slot></slot>
    </div>
  `
})
```

### 动态组件

在不同组件之间进行动态切换是非常有用的，通过 Vue 的 <component> 元素加一个特殊的 is 特性来实现。

```
<!-- 组件会在 `currentTabComponent` 改变时改变 -->
<component v-bind:is="currentTabComponent"></component>
```

### 解析Dom模版注意事项

如 `<li>`、`<tr>` 和 `<option>`，只能出现在其它某些特定的元素内部。 导致使用这些有约束条件的元素时遇到一些问题。

```
<table>
  <blog-post-row></blog-post-row>
</table>
```

这个自定义组件 `<blog-post-row>` 会被作为无效的内容提升到外部，并导致最终渲染结果出错。 

特殊的 `is` 特性提供了办法： 

```
<table>
  <tr is="blog-post-row"></tr>
</table>
```



## 深入组件

## 组件注册

### 组件名

在注册一个组件的时候，始终需要给它一个名字。 组件名就是` Vue.component `的第一个参数。

```
Vue.component('my-component-name', { /* ... */ })
```

### 全局注册

通过 Vue.component 来创建组件，这些组件是全局注册的。它们在注册之后可以用在任何新创建的 Vue 根实例 (new Vue) 的模板中。

### 局部注册

通过一个普通的 JavaScript 对象来定义组件：

```
var ComponentA = { /* ... */ }
var ComponentB = { /* ... */ }
var ComponentC = { /* ... */ }
```

然后在 `components` 选项中定义要使用的组件： 

```
new Vue({
  el: '#app'
  components: {
    'component-a': ComponentA,
    'component-b': ComponentB
  }
})
```

- 对于 `components` 对象中的每个属性来说，其属性名就是自定义元素的名字，其属性值就是这个组件的选项对象。 
- **局部注册的组件在其子组件中不可用**。 

希望 ComponentA 在 ComponentB 中可用：

```
var ComponentA = { /* ... */ }

var ComponentB = {
  components: {
    'component-a': ComponentA
  },
  // ...
}
```

### 模块系统

#### 在模块系统中局部注册

在局部注册之前导入每个想使用的组件。 如ComponentB.js 或 ComponentB.vue 文件中：

```shell
import ComponentA from './ComponentA'
import ComponentC from './ComponentC'

export default {
  components: {
    ComponentA,
    ComponentC
  },
  // ...
}
```

#### 自动化全局注册

在各个组件中被频繁的用到的相对通用组件,把它们称为**基础组件**。



## prop

### 静态和动态Prop

像这样给 prop 传入一个静态的值： 

```
<blog-post title="My journey with Vue"></blog-post>
```

通过 `v-bind` 动态赋值 :

```
<blog-post v-bind:title="post.title"></blog-post>
```

任何类型的值都可以传给一个 prop。

#### 传入一个数字

```html
<!-- 即便 `42` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:likes="42"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:likes="post.likes"></blog-post>
```

#### 传入一个布尔值

```html
<!-- 包含该 prop 没有值的情况在内，都意味着 `true`。-->
<blog-post favorited></blog-post>

<!-- 即便 `false` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<base-input v-bind:favorited="false">

<!-- 用一个变量进行动态赋值。-->
<base-input v-bind:favorited="post.currentUserFavorited">
```

#### 传入一个数组

```html
<!-- 即便数组是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:comment-ids="[234, 266, 273]"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:comment-ids="post.commentIds"></blog-post>
```

#### 传入一个对象

```html
<!-- 即便对象是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:comments="{ id: 1, title: 'My Journey with Vue' }"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:post="post"></blog-post>
```

#### 传入一个对象的所有属性

将一个对象的所有属性都作为 prop 传入， 使用不带参数的 v-bind (取代 v-bind:prop-name)。

```html
<blog-post v-bind="post"></blog-post>
//js
post: {
  id: 1,
  title: 'My Journey with Vue'
}
//等价于
<blog-post  v-bind:id="post.id"  v-bind:title="post.title"></blog-post>
```

### 单项数据流

- 所有的 prop 都使得其父子 prop 之间形成了一个**单向下行绑定**：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。 防止从子组件意外改变父级组件的状态。
- 每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。

两种常见的试图改变一个 prop 的情形：

1. **这个 prop 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 prop 数据来使用。** 最好定义一个本地的 data 属性并将这个 prop 用作其初始值： 

   ```js
   props: ['initialCounter'],
   data: function () {
     return {
       counter: this.initialCounter
     }
   }
   ```

2. **这个 prop 以一种原始的值传入且需要进行转换**。最好使用这个 prop 的值来定义一个计算属性： 

   ```js
   props: ['size'],
   computed: {
     normalizedSize: function () {
       return this.size.trim().toLowerCase()
     }
   }
   ```

   

