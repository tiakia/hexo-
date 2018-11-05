---
title: react拾遗
date: 2018-10-23 14:39
categories: react
tags: [react]
keywords:
- react
clearReading: true
thumbnailImage:
thumbnailImagePosition: left  //缩略图显示的位置，上下左右都可以
autoThumbnailImage: true
metaAlignment: center  //文章页图片上的文字居中显示
coverImage: http://ostu98x74.bkt.clouddn.com/cover/cover.jpg
coverCaption:
coverMeta: in
coverSize: full
comments: true
---

总结一些 react 中常见的面试题吧，同时也是让自己多学习学习 react 相关的知识。查漏补缺。

<!-- more -->
##### 组件的命名
基于路径命名的方式，举个例子，组件的路径如果是 `components/User/List.jsx`，那么它就被命名为 `UserList`。

#### !!()
!!(a)的作用是将a强制转换为布尔类型
{% tabbed_codeblock test.js  %}
<!-- tab js -->
let a = 123;
console.log(!!a); // true

let b = '';
console.log(!!b); //false

let c = 'null';
console.log(!!c); //true

let d = null;
console.log(!!d); //false
<!-- endtab -->
{% endtabbed_codeblock %}


#### PureComponent
`React.PureComponent` 相较于 `React.Component` 做了一个`shouldComponentupdate()`的浅比较，避免了重复更新

#### props 和 state
props 更多的类似是 函数 的 参数
state 类似函数内部声明的变量，在函数内部使用，控制函数状态

#### setState 的 callback()
{% tabbed_codeblock  test.js  %}
<!-- tab js -->
this.setState({
    name: 'Tian'
}, () => {
    console.log(this.state.name)
});
<!-- endtab -->
{% endtabbed_codeblock %}

`setState`是异步的，但是可以在回调函数中获取`setState`后的 `state`

#### HTML 和 React 中的事件处理有什么区别
- `react` 事件名称大写，eg: `onClick`/`onChange`
- 在HTML中阻止事件可以`return false`,在 `react` 中 必须使用 `e.preventDefault()`

#### react 中 函数绑定 this 的方法
- 在 构造函数中
{% tabbed_codeblock test.js  %}
<!-- tab js -->
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.handleClick = this.handleClick.bind(this);
    }
    handleClick(){
        console.log('click');
    }
}
<!-- endtab -->
{% endtabbed_codeblock %}

- 箭头函数
{% tabbed_codeblock  test.js  %}
<!-- tab js -->
handleClick = () => {
    console.log('click');
}
<!-- endtab -->
{% endtabbed_codeblock %}
> react中函数的使用

- `<button onCLick={this.handleClick}>Click</button>`
- `<input onChange={e => this.handleChange(e)}/>`

#### ref 的使用
{% tabbed_codeblock  test.js  %}
<!-- tab js -->
class MyComponent extends React.Component {
    constructor(props) {
       super(props);
       this.myRef = React.createRef();
    }
    render() {
       return <div ref={this.myRef}/>;
    }
}
<!-- endtab -->
<!-- tab js -->
class SearchBar extends Component {
   constructor(props) {
      super(props);
      this.txtSearch = null;
      this.state = { term: '' };
      this.setInputSearchRef = e => {
         this.txtSearch = e;
      }
   }
   onInputChange(event) {
      this.setState({ term: this.txtSearch.value });
   }
   render() {
      return (
         <input
            value={this.state.term}
            onChange={this.onInputChange.bind(this)}
            ref={this.setInputSearchRef} />
      );
   }
}
<!-- endtab -->
{% endtabbed_codeblock %}

#### 受控组件 和 非受控组件

使用 `setState` 控制内部状态的组件称为受控组件，
##### controlled
{% tabbed_codeblock  test.js %}
<!-- tab js -->
class NameForm extends React.Component {
    constructor(props) {
        super(props);
        this.state = {name: ''};
        this.handleNameChange = this.handleNameChange.bind(this);
    }

    handleNameChange(event) {
        this.setState({ name: event.target.value });
    };

    render() {
        return (
            <div>
                <input type="text"
                       value={this.state.name}
                       onChange={this.handleNameChange}
                       />
            </div>
        );
    }
}
<!-- endtab -->
{% endtabbed_codeblock %}

> tip

当注释 `this.setState({value: event.target.value});` 这行代码，文本框再次输入时，页面不会重新渲染，所产生效果即是文本框输入不了值，即文本框值的改变受到 `setState()` 方法的控制，在未执行时，不重新渲染组件


##### uncontrolled
表单数据由DOM本身处理。即不受`setState()`的控制，与传统的HTML表单输入相似，input输入值即显示最新值（使用 `ref` 从DOM获取表单值）
{% tabbed_codeblock  test.js %}
<!-- tab  js -->
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.input = null;
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={input => this.input = input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
<!-- endtab -->
{% endtabbed_codeblock %}

#### React16 生命周期

[react16生命周期](http://www.tiankai.party/react16.html)


#### React 高阶组件

在组件内部对旧的组件进行封装，返回一个新的组件。
{% tabbed_codeblock  test.js %}
<!-- tab js -->
function HOC(WrappedComponent) {
    return class Test extends Component {
        render() {
            const newProps = {
                title: "New Header",
                footer: false,
                showFeatureX: false,
                showFeatureY: true
            }

            return <WrappedComponent {...this.props} {...newProps}/>
        }
    }
}
<!-- endtab -->
{% endtabbed_codeblock %}

#### React Context
{% tabbed_codeblock  test.js  %}
<!-- tab js -->
const { Provider, Consumer } = React.createContext("light");

class App extends Component {
    render() {
        reutrn (
            <Provider value={"dark"}>
                <ToolBar/>
            </Provider>
        )
    }
}

functoin ToolBar() {
    reutrn (
        <Consumer>
            {
                value => (
                    <button>{value}</button>
                )
            }
        </Consumer>
    )
}

<!-- endtab -->
{% endtabbed_codeblock %}

#### react 16.6 lazy

{% tabbed_codeblock  test.js %}
<!-- tab js -->
import React, {lazy, Suspense} from 'react';
const OtherComponent = lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <OtherComponent />
    </Suspense>
  );
}
<!-- endtab -->
{% endtabbed_codeblock %}


#### componentDitCatch()

#### static getDerivedStateFromError()

#### static getDerivedStateFromProps()

#### getSnapshotBeforeUpdate()
