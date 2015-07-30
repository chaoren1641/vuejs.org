title: 常见问题
type: guide
order: 15
---

- **为什么Vue.js不支持IE8?**

  利用ECMASCript5的新特性：`Object.defineProperty`, Vue.js不借助脏检查就能提供纯正的Javascript对象语法。这一新特性在IE8里只在DOM元素上起作用，而且无法通过polyfill与JavaScript对象兼容。

- **那么Vue.js修改了我的数据喽?**

  是也不是。Vue.js只转换正常的属性到getters和setters，这样它才能在属性被访问或更改时得到通知。而序列化时，你的数据将是完全相同。当然，这里有一些注意事项：

  1. 当你使用`console.log`观察对象时你将只能看到一串getter/setters. 但你可以使用`vm.$log()`来打印出一个更直观的输出。

  2. 你不能定义数据对象的getter/setters。这不会是问题，因为数据对象都期望从纯JSON中取得，而且vue.js提供可计算的属性。

  3. Vue.js添加了一些拓展的属性或方法来观察对象: `__ob__`, `$add`, `$set`以及`$delete`. 这些属性是内部的所以它们不会显示在`for ... in ...`循环中. 但是如果你覆盖了它们这可能就破坏掉了。

  类似的东西还有一些。基于对象访问属性和以前一样,`JSON.stringify`和`for ... in ...`循环照常运行。99.9%的情况下你甚至不需要考虑它们。

- **Vue.js目前的状态怎样? 我能把它应用在生产环节么?**

  Vue.js 最新的0.12发布版本，经历了一些API变更，但这是1.0版本前的最后一个计划发布版本。在此期间，已经[在产品中使用Vue.js的公司/产品](https://github.com/yyx990803/vue/wiki/Projects-Using-Vue.js)。

- **Vue.js是免费试用的吗?**

  Vue.js遵循MIT协议是免费且完全开源的.

- **Vue.js和AngularJS之间的区别是什么?**

  下面是一些使用Vue而不是Angular的原因，当然它们可能不适合每一个人：

  1. Vue.js是一个更加灵活开放的解决方案。它允许你以希望的方式组织你的应用程序，而不是像Angular那样强迫去做。它仅仅是一个接口层，所以你可以将它作为一个页面的轻特性而不是一个大而全的SPA。在结合和匹配其他库方面它给了你更大的的空间，但你也应为更多的架构决策负责。例如，Vue.js核心默认不包含路由和ajax功能，并且通常假定你在用应用中使用了一个外部的模块管理器。这可能是最重要的区别。

  2. 在API和设计方面，Vue.js比Angular简单得多, 因此你可以快速地学习它的方方面面并投入生产.

  3. Vue.js拥有更好的性能，因为它不使用脏检查。当观察点越来越多时Angular会变得越来越慢，因为作用域内的每一次变更所有的这些观察点都需要被重新评估。Vue.js不面临这些问题，这是因为它采用了一个透明的依赖追踪的观察系统，所以所有的触发都是独立的，除非它们之间有明确的依赖关系。

  4. Vue.js指令和组件间具有一个清晰隔离。指令只意味着封装DOM操作，而组件代表一个自给自足的独立单元——它拥有自己的视图和数据逻辑。在Angular中它们两者间有不少混淆。

  但是需要指出的是Vue.js还是一个相对年轻的项目，而Angular已经久经项目验证，并且是谷歌发起的且有一个更大的社区。

- **是什么使得Vue.js不同于React.js?**

  React.js和Vue.js确实有一些相似——它们都提供响应化及可组合搭建的视图组件。然而，它们的内部实现是完全不同的。React是基于虚拟DOM —— 在内存中的表述DOM看起来应该是怎样的。React中的数据大部分是不变的，而且DOM操作通过比较来计算的。与之相反Vue.js中的数据默认情况下是可变且优雅的，变更通过事件触发。相比于虚拟DOM，Vue.js使用实际的DOM作为模板，并且保持对真实节点的引用来进行数据绑定。

  虚拟DOM的方法提供了一个功能性的方式以便在任何时候描述视图，这确实很好。因为它不使用观测值，且不需要为每个更新重新渲染整个应用，视图通过定义保证与数据保持同步。它也开辟了与JavaScript应用同构的可能性。

  总的来说我自己就是React设计理念的忠实粉丝。但React有一个问题就是你的逻辑和视图是紧密结合在一起的。对于部分开发者来说这是件让人高兴的事，但对那些像我一样设计/开发混合进行的人来说，更希望能有一个模板，它能够更容易地在视觉上考虑设计和CSS。JSX和JavaScript逻辑的混合打破了我映射代码到设计的视觉模型。相反，Vue.js扮演了一个轻量级的DSL(指令型的) 的角色，这样我们有了一个直观的扫描模板，且能够将逻辑封装进指令和过滤器中。

  React的另一个问题是：由于DOM更新完全下放给虚拟DOM，当你真的**想**自己控制DOM是就有点棘手了（虽然理论上你可以，但这样做时你本质上在对抗库原本的原则）。对于需要复杂时间控制的动画应用来说这就变成了一项很讨人厌的限制。在这方面，Vue.js允许更多的灵活性并且有不少用Vue.js构建的事例[一些FWA/Awwwards获奖站点](https://github.com/yyx990803/vue/wiki/Projects-Using-Vue.js#interactive-experiences)
  
- **What makes Vue.js different from Polymer?**

Polymer是另一个google赞助的项目，实际上也给Vue.js提供了灵感。Vue.js的components组件可以类比为Polymer的自定义元素，它们都提供类似的开发特性。最大的不同，是Polymer构建于最新的web组件特性，需要不那么简单的polyfill，以在并不能原生支持的浏览器里运行（导致性能较低）。相对的，Vue.js无需任何依赖，最低兼容到IE9。

- **是什么使得Vue.js不同于KnockoutJS?**

  首先，Vue在获取和设置虚拟属性上提供了更清晰的语法。

  从更高层次来说，Vue区别于Knockout是因为Vue的组件系统鼓励你采取自上而下，结构第一，陈述性设计的策略，而不是命令式的自下向上来建立ViewModel。在Vue中源数据是纯粹的无逻辑的对象（这些对象你可以直接JSON.stringify并扔到POST请求中），而ViewModel只是代理访问数据本身。Vue的VM实例往往连接原始数据及与其对应的DOM元素。在Knockout中，ViewModel基本**是**数据，Model和ViewModel之间的连线是很模糊的。这种分化的缺乏使得Knockout更灵活，但也更可能导致复杂的ViewModels。

- **我要提供帮助!**

  很好! 阅读 [贡献指导](https://github.com/yyx990803/vue/blob/master/CONTRIBUTING.md) 并加入<a href="https://gitter.im/yyx990803/vue" target="_blank"><img src="https://badges.gitter.im/Join%20Chat.svg"></a>上进行讨论。
