# my-react-demos
this is demos for react starter  refer to https://gitee.com/wlhy/react-demos

<script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
<script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
<script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>

>上面三个链接分别是React核心库；提供与DOM相关的功能；将ES6代码转化为ES5代码。



### introduce

##### demo01 Render JSX

在React中模板句法被称为JSX,JSX允许将HTML标签写在JS代码中。ReactDOM.render()是将JSX转变为HTML，并将其渲染到标记的DOM节点。

首先需要在script标签中type需要声明为text/babel,用来声明这是JSX句法。

React.DOM.render()接受两个参数，第一个参数是JSX编写的模板，第二个参数是模板渲染的目标节点，将被渲染成目标节点的子节点。如果目标节点(id="example")有其他节点(<h3>将被忽略</h3>)。

##### demo02 Use Javascript in JSX

在JSX中,HTML句法以( < )开始,JS句法以( { )开始

##### demo03 在JSX中使用array

arr是一个数组，该数组的每个元素是一个html标签，这个数组的每个元素在页面上将会渲染成对应的HTML标签。

##### demo04 定义一个组件

这里使用ES6 class声明一个React组件，一般套路是

```javascript
Class TemplateName extends React.Component {
  constructor() {
  	super()
  }
  render() {
  	...
  }
}
```

>注意React.Component中Component首字母要大写，如果在templateName非constructor方法中使用this,需要在constructor方法中super(),ES6子类没有自己的this，需要调用super()方法继承父class 的this.
>
>声明组件的类的首字母需要大写，否则会报错。
>
>组件有自己的属性，可以通过this.props.[attribute]来获取他们。
>
>render方法返回的JSX只有一个顶层HTML节点。如果有嵌套的节点可以使用小括号（）包括。



