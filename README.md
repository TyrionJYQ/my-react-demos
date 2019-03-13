# my-react-demos
this is demos for react starter  refer to https://gitee.com/wlhy/react-demos

- <script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>

- <script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
- <script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>

>上面三个链接分别是React核心库；提供与DOM相关的功能；将ES6代码转化为ES5代码。



### introduce

##### demo01: Render JSX

在React中模板句法被称为JSX,JSX允许将HTML标签写在JS代码中。ReactDOM.render()是将JSX转变为HTML，并将其渲染到标记的DOM节点。

首先需要在script标签中type需要声明为text/babel,用来声明这是JSX句法。

React.DOM.render()接受两个参数，第一个参数是JSX编写的模板，第二个参数是模板渲染的目标节点，将被渲染成目标节点的子节点。如果目标节点(id="example")有其他节点将被忽略。

##### demo02: Use Javascript in JSX

在JSX中,HTML句法以( < )开始,JS句法以( { )开始

##### demo03: 在JSX中使用array

arr是一个数组，该数组的每个元素是一个html标签，这个数组的每个元素在页面上将会渲染成对应的HTML标签。

##### demo04: 定义一个组件

这里使用ES6 class声明一个React组件，一般套路是

```javascript
Class TemplateName extends React.Component {
  constructor() {
  	super();
  }
  render() {
  	...
  }
}
```

>注意React.Component中Component首字母要大写，如果在templateName的constructor方法中使用this,需要在constructor方法中super(),ES6子类没有自己的this，需要调用super()方法继承父class 的this.
>
>声明组件的类的首字母需要大写，否则会报错。
>
>组件有自己的属性，可以通过this.props[attributeName]来获取他们。
>
>render方法返回的JSX只有一个顶层HTML节点。如果有嵌套的节点可以使用小括号（）包括。



##### demo05: this.props.children

this.props.children有以下三种可能性

- undefined:组件中没有子节点
- Object：组件中只插入一个子节点
- Array:组件中插入两个或两个以上子节点

使用React.Children可以让我们更加方便的遍历this.props.children而不用去关注this.props.children具体类型。



##### demo06: PropTypes

在React中类的属性被称为props，props可以是任何类型的数据，有时你需要某种方式去验证props的数据类型，因为你并不想用户可以随意输入任何类型的props到你的组件。这时你需要PropTypes.

PropTypes引入方式

```javascript
<script src="https://cdn.bootcss.com/prop-types/15.6.1/prop-types.js"></script>
```

```javascript
import PropTypes from 'prop-types';
```

​	

```javascript
  let title = 'hello world';
  class MyTitle extends React.Component {
    static propTypes = {
      title: PropTypes.string
    }
    render() {
      return (
        <h1>{this.props.title}</h1>
      )
    }
  }
  // MyTitle.propTypes = {
  //   title: PropTypes.number
  // }
  ReactDOM.render(
    <MyTitle title={title}/>,
    document.getElementById('example')
  );
```

分析：引入PropTypes后，可以通过TemplateClassName.propTypes来使用，也可以通过

```javascript
...
static propTypes = {...}
...
```

来使用（类的静态属性两种声明方式）。

```javascript
 class MyTitle extends React.Component {
    static propTypes = {
      title: PropTypes.string.isRequired
    }
    static defaultProps = {
      title: 'stranger'
    }
    render() {
      return (
        <h1>{this.props.title}</h1>
      )
    }
  }
  ReactDOM.render(
    <MyTitle/>,
    document.getElementById('example')
  );
```

- ```javascript
  propTypes[type].isRequired: //必须传值
  ```

- ```javascript
  static defaultProps = {} // 设置props的默认值
  ```


- 当props设置默认值，在组件中没有传递相关属性，如果设置了该prop是必填项，react不会报错，这时prop使用的是默认值。



##### demo07: Finding a DOM node

某些时候，你想获取组件中的DOM节点，在React中你可以通过使用ref属性来找到你想要的DOM节点。目标DOM需要有有一个ref属性，通过this.refs.[refName]来匹配到相应的DOM元素。

>这里需要注意的是，需要在组件被渲染成DOM后才能通过ref属性拿到想要的DOM属性，否则获取到的是一个null。如果多个DOM节点有想通过的ref属性名。

```javascript
class MyComponent extends React.Component {
  handleClick() {
    console.log(this.refs.spanNode) //<span>1</span>
    console.log( this.refs.myTextInput) // <input type="text" value="haha">
    this.refs.myTextInput.focus();
  }
  render() {
    return (
      <div>
        <span ref="spanNode">2</span>
        <span ref="spanNode">1</span>
        <input type="text" ref="myTextInput" />
        <input type="button" ref="myTextInput" value="Focus the text input" onClick={() =>this.handleClick()} />
        <input type="text" ref="myTextInput" value="haha" onChange = {() => false}/>  
      </div>
    )
  }
}
ReactDOM.render(
  <MyComponent/>,
  document.getElementById('example')
);
```

##### demo08: this.state

React将组件看成一个状态机，通过与用户的交互，实现不同状态，然后渲染 UI，让用户界面和数据保持一致。React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。

声明state,在组件的constructor方法中初始化state,this.setState()方法用来更新state并重新渲染视图。

```javascript
class TemplateClassName extends React.Class {
  constructor() {
    super();
  	this.state = {
  
 	}
  }
  
  handleEvent() {
  	this.setState(); //re-render
  }
}
```

##### demo09: Form

在React中,this.state用来描述组件的状态，通过与用户交互来改变this.state,是可变的，this.setState()用来改变组件的state,而this.props用来描述组件不可改变的稳定的属性。

所以：如果你在React中使用input, textarea,  option等表单元素，并且想让程序对用户的输入作出响应，你需要使用onChange事件。



```javascript
class Input  extends React.Component {
  constructor() {
    super();
    this.state = {
      value: 'Hello'
    };
  }
  handleChange(e) {
    // return;
    this.setState({
      value: e.target.value
    })
  }
  render() {
    let {value} = this.state;
    return (
      <div>
        <input type="text" value={value} onChange={e => this.handleChange(e)}></input>
      </div>
    )
  }
}
ReactDOM.render(
  <Input/>,
  document.getElementById('example')
);
```

>与Vue不同的是，在vue中，数据是双向绑定的，数据驱动视图，用户操作也会导致vue中相关数据发生变化，比如表单相关元素中使用v-model进行绑定。
>
>但在React中，使用表单元素你需要使用onChange()事件对用户输入进行处理，如果表单元素没有绑定onChange事件，会报如下错误。

```
react-dom.development.js:526 Warning: Failed prop type: You provided a `value` prop to a form field without an `onChange` handler. This will render a read-only field. If the field should be mutable use `defaultValue`. Otherwise, set either `onChange` or `readOnly`.
    in input (created by Input)
    in div (created by Input)
    in Input
```

如过把上面注释的return语句放开，就会发现无论用户如何如入页面表单上的值都不会发生变化。



##### demo10: Component Lifecycle

这是一个简单使用react组件生命周期的示例。在Clock组件的componentDidMount阶段使用this.setState改变state中time值，触发视图重新渲染,在componentWillUnmount即将卸载阶段清除定时器。



##### demo11: ajax

在React组件中如何获取从服务器或第三方API上的数据。在组件的componentDidMount阶段使用ajax获取数据，当获取到响应数据后，使用this.setState触发视图重新更新。

```javascript
let Component = React.Component;
class Prize  extends Component {
  constructor(props) {
    super(props);
    this.state = {
      prize: {}
    }
  }
  getPrize() {
    // 模拟ajax请求
    setTimeout(() => 
      this.setState({
        prize: {'name':'一等奖', 'bonus': '$10000000000'}
      }),
      2000
    )
  }
  componentDidMount() {
   this.getPrize()
  }
  render() {
    let prize = this.state.prize;
    return (
      <div>
        <span>中奖情况:</span>
        <span>{prize.name}</span>
        <span>{prize.bonus}</span>
      </div>
    )
  }
}

ReactDOM.render(
 <Prize/>,
  document.getElementById('example')
);
```

