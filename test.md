# React代码规范
---

<!-- TOC depthFrom:2 depthTo:3 withLinks:1 updateOnSave:1 orderedList:0 -->

- [基本规范](#基本规范)
- [命名规范](#命名规范)
- [组件规范](#组件规范)
	- [class、React.createClass 与 stateless](#classreactcreateclass-与-stateless)
	- [代码对齐](#代码对齐)
	- [JSX语法](#jsx语法)

<!-- /TOC -->

## 基本规范

- 每个文件应该只包含单个组件
- 组件内部使用 `jsx` 语法。
- js部分推荐使用 `ES6` 语法，目前项目采用 `ES5`书写，后面会逐步替换。(这里规范以 `ES6`为主，但大部分规范一致)

## 命名规范

- 扩展名：目前项目使用 js
- 文件名：采用驼峰命名规则
- 模块名：采用帕斯卡命名规则
- 实例名：采用驼峰命名规则
- 属性名：采用驼峰命名规则，避免使用DOM相关的属性来用作其他的用途，如 style、className

  > 如果整个文件夹是一个模块，使用 `index.js` 作为入口文件，然后直接使用 `index.js` 或者文件夹名作为模块的名称。

如，文件结构：

```
login
    ├──index.js
    ├──index.less
```

```javascript
// bad
const Login = require('./login/login.js');
var Login = require('./login/index.js');

// bad
var login = require('./login');

// good
var Login = require('./login');

// bad
var Login = <Login />;

// good
var login = <Login />;
```

## 组件规范

### class、React.createClass 与 stateless

- 推荐使用 `ES6` 的语法，除非必要，避免使用 `Mixin` （官方已不推荐使用 `Mixin`, 并且 `ES6` 不支持 `Mixin`) [详情](https://facebook.github.io/react/docs/react-without-es6.html#mixins) [推荐方案](https://zhuanlan.zhihu.com/p/20361937?columnSlug=purerender)

  ```javascript
  // ES5
    var Hello = React.createClass({
      // ...
      render: function() {
        return <div>{'hello'}</div>;
      }
    });

    // ES6
    class Hello extends React.Component {
        // ...
        render() {
            return <div>{' hello'}</div>;
        }
    }
  ```

- 如果你的模块没有状态或是没有引用refs， 推荐使用普通函数（非箭头函数）而不是类:

  ```javascript
  // bad
    class Hello extends React.Component {
        render() {
            return <div>{this.props.hello}</div>;
        }
    }

    // bad (relying on function name inference is discouraged)
    const Hello = ({ hello }) => (
        <div>{hello}</div>
    );

    // good
    function Hello({ hello }) {
        return <div>{hello}</div>;
    }
  ```

### 代码对齐

- 目前项目中代码缩进为4个空格
- 习惯使用 tab 的话，请将自己的编辑器 tab 长度设置为4个空格

  > 不推荐使用 tab, 不同编辑器 tab 长度不一致，易造成代码缩进混乱

### JSX语法

- 缩进

  ```javascript
  // good 单个属性直接写成一行
    <Custom attrA="123" />

    // bad
    <Custom attrA="123" attrB="123" />

    // bad
    <Custom attrA="123"
            attrB="123" />

    // good 多个属性采用多行编写，新建一行关闭标签
    <Custom
        attrA="123"
        attrB="123"
    />

    // 子元素按照常规方式缩进
    <Custom
      attrA="123"
      attrB="123"
    >
        <Label>123</lable>
    </Custom>
  ```

- 空格：总是在自动关闭的标签前加一个空格，正常情况下也不需要换行

  ```javascript
  // bad 少空格
    <Custom/>

    // bad 空格多了
    <Custom    />

    // bad 不用换行
    <Custom
    />

    //good
    <Custom />
  ```
