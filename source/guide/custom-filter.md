title: 自定义过滤器
type: guide
order: 10
---

## 基本用法

和自定义指令类似，你可以用全局方法 `Vue.filter()`，传递一个**过滤器 ID**和一个**过滤器函数**，来注册一个自定义过滤器。过滤器函数会接受一个参数值并返回将其转换后的值：

``` js
Vue.filter('reverse', function (value) {
  return value.split('').reverse().join('')
})
```

``` html
<!-- 'abc' => 'cba' -->
<span v-text="message | reverse"></span>
```

过滤器函数也接受任何内联的参数：

``` js
Vue.filter('wrap', function (value, begin, end) {
  return begin + value + end
})
```

``` html
<!-- 'hello' => 'before hello after' -->
<span v-text="message | wrap 'before' 'after'"></span>
```

## 双向过滤器

现在我们已经在展示到视图之前用过滤器把模型里的值进行了转换。其实我们也可以定义一个过滤器在值从视图 (input 元素) 写回模型之前进行转换：

``` js
Vue.filter('check-email', {
  // read is optional in this case, it's here
  // just for demo purposes.
  read: function (val) {
    return val
  },
  // this will be invoked before writing to
  // the model.
  write: function (val, oldVal) {
    return isEmail(val) ? val : oldVal
  }
})
```

## 动态参数

如果一个过滤器参数没有被单引号所围住，它会在vm的数据上下文里被动态地认定。此外，过滤器总是调用当前vm作为它的`this`上下文。

``` html
<input v-model="userInput">
<span>{{msg | concat userInput}}</span>
```

``` js
Vue.filter('concat', function (value, input) {
  // here `input` === `this.userInput`
  return value + input
})
```

在上面这个例子中，你用表达式即可完成相同的结果。但是面对更复杂的处理时，如果需要不止一个声明，你就得把它们放到一个可可计算的设定中或一个自定义过滤器中。

内建的 `filterBy` 和 `orderBy` 过滤器都是根据传入的数组以及所属 Vue 实例状态而运行的过滤器。

很好！是时候了解[组件系统](../guide/components.html)的工作方式了。
