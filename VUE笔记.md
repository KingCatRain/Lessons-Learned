# VUE笔记

# 组件

## DOM模板的 `is` 属性
有些元素限制能被他包裹的元素 例如： `ul` ， `ol` ， `table` ， `select` ， 等，如果在这些元素中使用模板，例如：

~~~
<table>
  <my-row>...</my-row>
</table>
~~~

自定义组件 `my-row` 会被认为是无效的内容，因此在渲染的时候会导致错误。变通的方案是使用特殊的 `is` 属性:

~~~
<table>
  <tr is="my-row"></tr>
</table>
~~~

应当注意，如果您使用来自以下来源之一的字符串模板，这些限制将不适用：

* `<script type="text/x-template">`
* JavaScript内联模版字符串
* `.vue` 组件

因此，有必要的话请使用字符串模版。

## 组件的 `data` 必须是函数

~~~
Vue.component('my-component', {
  template: '<span>{{ message }}</span>',
  data: {
    message: 'hello'
  }
})
~~~

为了保证组件在多个地方被使用时 ***data*** 里的数据保持独立，最好用：

~~~
data() {
	return {
		message: 'hello'	
	};
}
~~~

## 构成组件

组件的解耦很重要，保证组件可以在相对隔离的环境中书写和理解，也大幅度提高了组件的可维护性和可重用性。

在 ***Vue.js*** 中，父子组件的关系可以总结为 ***props down, events up***， 父组件通过 ***props*** 向下传递数据给子组件，子组件通过 ***events*** 给父组件发送消息。如下图 ![图片](http://cn.vuejs.org/images/props-events.png)

## Props

### 使用Props传递数据

组件实例的作用域是 ***孤立的*** 。这意味着并不能且不应该在子组件的模板内直接引用父组件的数据。可以使用 ***Props*** 把数据传给子组件。
***Props** 是父组件用来传递数据的一个自定义属性，子组件需要显示的用 `props` 选项来声明 “prop”：

~~~
Vue.component('chilid', {
	// 声明props
	props: ['message'],
	// 就像 data 一样，prop 可以用在模板内
	// 同样也可以在 vm 实例中像 ”this.message“ 这样使用
	template: '<span> {{ message }} </span>',
});
~~~

在父组件像它传入一个值：

~~~
<child message="hello!"></child>
~~~

结果：

~~~
hello！
~~~

### camelCase vs. kebab-case

HTML特性不区分大小写，当使用非字符串模板时，***prop*** 的名字形式会从 ***camelCase*** （驼峰）转成 ***kebab-case*** （短横线隔开）

~~~
Vue.component('child', {
	// camelCase in javascript
	props: ['myMessage'],
	template: '<span>{{ myMessage }}</span>'
});
~~~

~~~
// kebab-case in HTML
<child my-message=""></child>
~~~

再次说明，如果你使用的字符串模板，不用在意这些限制

### 动态props

类似于用 `v-bind` 绑定HTML特性到一个表达式，也可以用 `v-bind` 动态绑定 ***props*** 的值到父组件的数据中，每当父组件中的值变化时，该变化也会传导给子组件：

~~~
<div>
	<input v-model="parentMsg">
	<br>
	<child v-bind:my-message="parentMsg"></child>
</div>
~~~

### 字面量语法 vs 动态语法

初学者常犯的一个错误是使用字面量语法传递数值：

~~~
<!-- 传递了一个字符串”1“ -->
<comp some-prop="1"></comp>
~~~

因为它是一个字面prop，它的值以字符串 `”1“` 而不是实际的数字传下去。如果想传一个实际的JavaScript数字，需要使用 `v-bind` ,从而让它的值被当做JavaScript的表达式来计算：

~~~
<!-- 传递实际的数字 -->
<comp v-bind:some-prop="1"></comp
~~~

### 单向数据流

***prop*** 是单向绑定的，当父组件属性变化时，将传到给子组件，但不会反过来。这是防止子组件无意修改了父组件的状态，--这会让应用的数据流难以理解。

另外，每次父组件更新时，子组件的 ***prop*** 都会更新到最新的值，这意味着你***不应该***在子组件内部改变***prop***，如果改变了，***Vue*** 会在控制台给出警告。

通常有两种改变prop的情况
1. ***prop*** 作为初始值传入，子组件之后只是将它的初始值当做本地数据的初始值使用。
2. ***prop*** 作为需要被转变的初始值传入。

### prop验证

组件可以为 ***props*** 指定验证要求，如果未指定验证要求，***Vue*** 会发出警告。当组件给其他人使用时，这很有用。

***prop*** 是一个对象而不是字符串数组时，它包含验证要求：

~~~
Vue.compenent('example', {
	props: {
		// 基础类型检测，（‘null’ 意思是任何类型都可以）
		propA: Number,
		// 支持多种类型
		propB: [String, Number],
		// 必传且是字符串
		propC: {
			type: String,
			required: true
		},
		// 数字，有默认值
		propD: {
			type: Number,
			default: 100
		},
		// 数组/对象应该由一个共产函数返回
		propE: {
			type: Object,
			default: function() {
				return {message: 'hello'};
			}
		},
		// 自定义验证函数
		propF: {
			validator: function(vaule) {
				return value > 10;
			}
		}
	}
});
~~~

`type` 可以是下面的原声构造器

* String
* Number
* Boolean
* Function
* Object
* Array
 
`type` 也可以是自定义构造器，用 `instanceof` 检测。

当 ***prop*** 验证失败了，***Vue*** 将拒绝在子组件上设置此值，如果使用的是开发版本将抛出一条错误。

## 自定义事件

我们知道父组件是通过 ***props*** 传递数据给子组件，但如果子组件需要把数据传递回去，应该怎么做？那就是自定义事件。

### 使用 v-on 绑定自定义事件

每个 ***Vue*** 实例都实现了 ***事件接口（event interface）*** ,即：

* 使用 `$on(eventName)` 监听事件
* 使用 `$emit(eventName)` 触发事件

> ***Vue*** 事件系统分离自浏览器的 ***EventTarget API*** 。尽管他们的运行类似，但 `$on` 和 `$emit` 不是 `addEventListener` 和 `dispatchEvent` 的别名。

另外父组件可以在使用子组件的地方直接用 `v-on` 来监听子组件触发的事件，下边是一个例子：

~~~
<div id="counter-event-example">
	<span>{{ total }}</span>
	<button-counter v-on:increment="incrementTotal"></button-counter>
	<button-counter v-on:increment="incrementTotal"></button-counter>
</div
~~~

子组件：

~~~
Vue.component('buttonCounter', {
	template: "<span v-on:click="increment">{{ counter }}</span>",
	data() {
		return {
			counter: 0,
		};
	},
	methods: {
		increment() {
			this.counter += 1;
			this.$emit('increment');
		},
	},
});
~~~

父组件

~~~
new Vue(
	data() {
		return {
			countTotal: 0,
		};
	},
	methods: {
		incrementTotal() {
			this.counterTotal += 1;
		},
	},
);
~~~

### 给组件绑定原生事件

有时候你可能想在一个组件的根元素上监听一个原生事件，这是可以用 `.native` 修饰 `v-on` 。例如：

~~~
<my-component v-on:click.native="doTheThing"></my-component>
~~~

## 使用自定义的表单输入组件

自定义事件也可以用来创建自定义表单输入组件，使用 `v-model` 来实现数据的双向绑定。牢记：

~~~
<input v-model="somthing">
~~~

仅仅是一个语法糖

### Slots分发内容分发

为了让组件可以组合，我们需要一种方式来混合父组件的内容和子组件自己的模板，这个过程被称为 ***内容分发*** （或 ***translution*** AngularJS里边的）

#### 编辑作用域

# 深入响应式原理

## 如何追踪变化

