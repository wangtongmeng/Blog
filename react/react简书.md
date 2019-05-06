B站https://www.bilibili.com/video/av37028937/?p=1，里面有些笔记
## 第 2 章 react 初探

### react 简介

- Facebook 推出
- 2013年开源
- 函数式编程
- 使用人数最多的前端框架
- 健全的文档与完善的社区
- React Fiber（react 16 之后的统称）

**官网**：https://reactjs.org/

**与 vue 的区别**：更加灵活，适合开发复杂度较高的项目

### 开发环境搭建

**使用方式**

- 引入.js文件使用 React（古老）
- 通过脚手架工具来编码
  -  React 官方脚手架：Create-react-app
  - 脚手架是通过构建工具构建的，如，grunt、gulp、webpack

**创建项目**

1.安装 node 和 npm 后，全局安装 react 脚手架：

```shell
npm install -g create-react-app
```

创建并启动项目

```shell
create-react-app my-app
cd my-app
npm start
```

2.如果 Node >= 6 and npm >= 5.2，可运行命令安装

```shell
npx create-react-app my-app
cd my-app
npm start
```

### 工程目录文件简介

精简项目文件，只留下，index.html、index.js、App.js

### react 中的组件

组件化思想：一个页面是有很多组件组成的。

![组件化思想](./img/组件化思想.png)

**定义一个组件**

组件是通过类继承 React.Component 这个类来定义的

```js
// App.js
import React, { Component } from 'react';

class App extends Component {
  render() {
    return (
      <div>
        hellow world
      </div>
    );
  }
}

export default App;
```

**JSX 语法**

ReactDOM.render() 的第一个参数传入的是`<App />`而不是 App，而`< />`这种形式就是 JSX 语法，**使用JSX 语法就必须引入 'react'**，否则报错。

```js
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

同理，在App.js 中 render 函数中的 div 标签形式也是 JSX 语法，也需要引入 React。

```js
// App.js
import React, { Component } from 'react';

class App extends Component {
  render() {
    return (
      <div>
        hellow world
      </div>
    );
  }
}

export default App;
```

### React 中最基础的JSX语法

**使用 h5 标签**

```js
// App.js
import React, { Component } from 'react';

class App extends Component {
  render() {
    return (
      <div>hellow world</div>
    );
  }
}

export default App;
```

**使用自定义组件标签**

使用自定义组件标签是，首字母必须大写，而 h5标签和在html相同不需要大写。

```js
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

## 第3章 React 基础精讲

本章通过TodoList功能的实现，给大家完整介绍React的基础语法，设计理念以及围绕React展开的一些编程思维。

### 使用React编写TodoList功能

- 在 index.js 中引入 TodoList 组件
- 创建 TodoList 组件
  - render 中 圆括号() 的作用使得我们可以换行书写
  - 使用 Fragment 占位符作为包裹元素

**引入 TodoList 组件**

```js
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import TodoList from './TodoList';

ReactDOM.render(<TodoList />, document.getElementById('root'));

```

**创建 TodoList 组件**

```js
// TodoList.js
import React, { Component, Fragment } from 'react'

class TodoList extends Component {
	render() {
		return (
			<Fragment>
				<div>
					<input />
					<button>提交</button>
				</div>
				<ul>
					<li>学英语</li>
					<li>learn react</li>
				</ul>
			</Fragment>
		)
	}
}

export default TodoList
```

### React 中的响应式设计思想和事件绑定

实现 input 框的响应式

- state 存储数据
- 绑定数据或方法通过 `{}` 包裹
- 绑定函数时通过 bind 绑定 this
- 修改 state 数据，通过 setState 修改

```js
// TodoList.js
import React, { Component, Fragment } from 'react'

class TodoList extends Component {

  constructor (props) {
    super(props)
    this.state = {
      inputValue: '',
      list: []
    }
  }
	render() {
		return (
			<Fragment>
				<div>
					<input 
      			value={this.state.inputValue} 
  					onChange={this.handleInputChange.bind(this)} 
          />
					<button>提交</button>
				</div>
				<ul>
					<li>学英语</li>
					<li>learn react</li>
				</ul>
			</Fragment>
		)
  }
  handleInputChange (event) {
    this.setState({
      inputValue: event.target.value
    })
  }
}

export default TodoList

```

### 实现 TodoList 新增删除功能

- 通过 ... 展开运算符，展开数组，结合添加数据，完成添加功能
- 通过 bind 传入第二个参数 index ，完成定位要删除的数据
- 删除数据时，先复制原数组，完成删除操作，再通过 setState 覆盖原有数据。不要直接在原数据上操作，不利于 react 性能优化。

```js
// TodoList.js
import React, { Component, Fragment } from 'react'

class TodoList extends Component {

  constructor (props) {
    super(props)
    this.state = {
      inputValue: '',
      list: []
    }
  }
	render() {
		return (
			<Fragment>
				<div>
					<input value={this.state.inputValue} onChange={this.handleInputChange.bind(this)} />
					<button onClick={this.handleBtnClick.bind(this)}>提交</button>
				</div>
				<ul>
					{
            this.state.list.map((item, index) => {
              return (
                <li 
                  key={index} 
                  onClick={this.handleItemDelete.bind(this, index)}
                >
                  {item}
                </li>
                )
            })
          }
				</ul>
			</Fragment>
		)
  }
  
  handleInputChange (event) {
    this.setState({
      inputValue: event.target.value
    })
  }

  handleBtnClick () {
    this.setState({
      list: [...this.state.list, this.state.inputValue],
      inputValue: ''
    })
  }

  handleItemDelete (index) {
    // imumutable
    // state 不允许我们做任何改变
    const list = [...this.state.list]
    list.splice(index, 1)
    this.setState({
      list: list
    })
  }
}

export default TodoList

```

### JSX语法细节补充

### 拆分组件与组件之间的传值

### TodoList 代码优化

### 围绕 React 衍生出的思考

