<h2 style="color:#000;background:rgba(64,116,52,1);line-height:60px;padding-left:10px;">组件周期</h2>
- 在调度过程中，有4个生命周期函数会被触发：
	- ```componentWillMount```和``` componentWillReceiveProps```是在Mounted阶段被触发，这个阶段React Component解析生成对应的DOM节点，并被插入到浏览器的DOM结构的一个过程。 ```componentWillMount```——> render ——>``` componentWillReceiveProps```
	- ```shouldComponentUpdate```和```componentWillUpdate```发生在Update阶段，一个mounted的React Component被重新render的过程，当state发生改变并影响了DOM结构的时候react才会去改变对应的DOM结构
- 在执行过程中，有3个生命周期函数会被触发：
	- componentDidMount
	- componentDidUpdate
	- componentWillUnmount ： unmounted是一个mounted的React Component对应的DOM节点被从DOM结构中移除的一个过程。

###shouldComponentUpdate
- shouldComponentUpdate是一个很特殊的函数，它默认会返回ture，但假如这个函数返回false的话，更新流程就会被跳过，render也不会继续被触发。假如你想要提升你应用的性能，可以在这个函数中自定义一些判断来跳过不需要被更新的组件。组件在初次渲染流程或者使用forceUpdate方法时是不会触发这个函数的。
- 当state发生改变时，会触发componentWillUpdate（）--> render --> componentDidUpdate（）
```
generarePhotoData = (photoDataObj) => {
    let fileLists = Object.keys(photoDataObj).map((item, index) => {
      return {
        uid: -index-1,
        name: item,
        status: 'done',
        url: photoDataObj[item],
        thumbUrl: photoDataObj[item]
      }
    })
    return fileLists
  }
```
<h2 style="color:#000;background:rgba(64,116,52,1);line-height:60px;padding-left:10px;">@connect</h2>
- It is in fact a part of react-redux which is used to connects a React component to a Redux store.这是react-redux的一部分，连接React组件和react store
- Decorators make it possible to annotate and modify classes and properties at design time. 装饰器让在design time时注释和更改类和属性成为可能
- connect([mapStateToProps], [mapDispatchToProps], [mergeProps],[options]) 。connect和@装饰器，connect是通过options将class传入到connect中，将store中的数据和dispatch中的数据绑定到组件中，@connect直接连接了react组件和react store

<h2 style="color:#000;background:rgba(64,116,52,1);line-height:60px;padding-left:10px;">REF</h2>
- REF字符串属性可以附加到任何render（）输出的组件上
```javascript
- 给从 render 返回的东西分配 ref 属性，如：
"<input ref="myInput" />"
- 在其他一些代码(典型的是事件处理程序的代码)，通过 this.refs 访问 backing instance，如：
this.refs.myInput
你可以通过调用 React.findDOMNode(this.refs.myInput) 直接访问组件的 DOM 节点。
```
- ref回调属性：ref 属性可以是一个回调函数，而不是一个名字。这个回调函数在组件安装后立即执行。被引用的组件作为一个参数传递，且回调函数可以立即使用这个组件，或保存供以后使用(或实现这两种行为)。
- 好处：
	- 你可以在组件类中定义任何公共方法(如在 Typeahead 中的复位方法)，并通过 refs(如 this.refs.myTypeahead.reset())调用这些公共方法。
	- 执行 DOM 测量几乎总是需要接触“本地”组件，如 ```<input/ >```，并通过 ```React.findDOMNode(this.refs.myInput) ```访问它的底层 DOM 节点。Refs 是可行的可靠的方法之一。
	- refs 自动为你 book-kept!如果子组件被摧毁，那么它的 ref 也被摧毁了。在这里不必担心内存(除非你为保留自己的 reference 做了一些疯狂的事)。
- 注意事项：
	- 永远不要访问组件的 render 方法内部的 refs——或任何组件的 render 方法正在 call satck 中运行时，也不要访问 refs。
	- 如果你想保存 Google Closure Compiler Crushing 的弹性，确保永远不要访问作为字符串被指定的属性。这意味着如果你的 ref 被定义为``` ref =“myRefString”```，你必须使用 this.refs['myRefString'] 来访问。
	- 如果你还没有用 React 给几个应用程序编程，那么你通常首先会倾向于尝试使用 refs 来“让事情发生”在你的应用程序中。如果是这样的话，花点时间，更为慎重的思考一下 state 应该属于组件层次结构的什么位置。通常情况下，你会清楚地发现，“拥有”那个 state 的适当的位置是更高的层次结构中。把 state 放置在那里通常可以消除任何想要使用 ref 来“让事情发生”的现象——相反，数据流通常会实现你的目标
<h2 style="color:#000;background:rgba(64,116,52,1);line-height:60px;padding-left:10px;">state</h2>

- 有时需要对用户输入、服务器请求或者时间变化等作出响应，这时才需要使用 State。</br>
- 常用的模式是创建多个只负责渲染数据的无状态（stateless）组件，在它们的上层创建一个有状态（stateful）组件并把它的状态通过 props 传给子级。这个有状态的组件封装了所有用户的交互逻辑，而这些无状态组件则负责声明式地渲染数据。
- State 应该包括那些可能被组件的事件处理器改变并触发用户界面更新的数据。 真实的应用中这种数据一般都很小且能被 JSON 序列化。当创建一个状态化的组件时，想象一下表示它的状态最少需要哪些数据，并只把这些数据存入 this.state。在 render() 里再根据 state 来计算你需要的其它数据
- ```props```几乎可以传递所有的内容，包括变量、函数、甚至是组件本身。组件只能根据传入的props渲染界面，而不能在其内部对props进行修改。
<h2 style="color:#000;background:rgba(64,116,52,1);line-height:60px;padding-left:10px;">thunk</h2>
- A thunk is a function that wraps an expression to delay its evaluation. thunk是一个覆盖一个表达式以延迟它的求值的函数
<h2 style="color:#000;background:rgba(64,116,52,1);line-height:60px;padding-left:10px;">bindActionCreators</h2>
- Redux中的bindActionCreators，是通过dispatch将action包裹起来，这样可以通过bindActionCreators创建的方法，直接调用dispatch(action)(隐式调用）。
- 主要用处：一般情况下，我们可以通过Provider将store通过React的connext属性向下传递，bindActionCreators的唯一用处就是需要传递action creater到子组件，并且改子组件并没有接收到父组件上传递的store和dispatch。
- 惟一使用 bindActionCreators 的场景是当你需要把 action creator 往下传到一个组件上，却不想让这个组件觉察到 Redux 的存在，而且不希望把 Redux store 或 dispatch 传给它。
<h2 style="color:#000;background:rgba(64,116,52,1);line-height:60px;padding-left:10px;">compose(...functions)</h2>
- 从右到左来组合多个函数。这是函数式编程中的方法，为了方便，被放到了 Redux 里。当需要把多个 store 增强器 依次执行的时候，需要用到它。compose 做的只是让你不使用深度右括号的情况下来写深度嵌套的函数。
- 参数
	- (arguments): 需要合成的多个函数。每个函数都接收一个函数作为参数，然后返回一个函数。
返回值
	- (Function): 从右到左把接收到的函数合成后的最终函数。

<h2 style="color:#000;background:rgba(64,116,52,1);line-height:60px;padding-left:10px;">扩展运算符和Rest运算符</h2>
- 扩展运算符用三个点号表示，功能是把数组或类数组对象展开成一系列用逗号隔开的值
- rest运算符也是三个点号，不过其功能与扩展运算符恰好相反，把逗号隔开的值序列组合成一个数组

<h2 style="color:#000;background:rgba(64,116,52,1);line-height:60px;padding-left:10px;">遍历对象的六种方式</h2>
- for ... in 循环遍历对象自身的和继承的可枚举属性(不含Symbol属性).

- Obejct.keys(obj),返回一个数组,包括对象自身的(不含继承的)所有可枚举属性(不含Symbol属性).

- Object.getOwnPropertyNames(obj),返回一个数组,包含对象自身的所有属性(不含Symbol属性,但是包括不可枚举属性).

- Object.getOwnPropertySymbols(obj),返回一个数组,包含对象自身的所有Symbol属性.

- Reflect.ownKeys(obj),返回一个数组,包含对象自身的所有属性,不管属性名是Symbol或字符串,也不管是否可枚举.

- Reflect.enumerate(obj),返回一个Iterator对象,遍历对象自身的和继承的所有可枚举属性(不含Symbol属性),与for ... in 循环相同.



