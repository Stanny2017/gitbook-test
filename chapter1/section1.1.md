# react 16.3 极客时间

- 传统web UI 开发 应用程序状态分散难以追踪和维护
- react 始终整体刷新页面

## flux 架构

- 单向数据流
- 是 react 解决关于数据模型的思路
- 不需要关心细节就可以把 store 连接到 view 上
- redux 是 fulx 架构的衍生项目（状态管理框架）

## 以组件方式考虑 UI 的构建 

## 创建一个简单的组件

- 受控组件： 表单元素状态由使用者维护
- 非受控组件： 表单元素状态由 DOM 自身维护

需要考虑：
1. 创建静态 UI
2. 考虑组件的状态组成
3. 考虑组件 

## 何时创建组件

- 每个组件只做一件事
- 如果组件变得复杂，那么应该拆分成小组件；可以提高性能，组件过大所有状态都要刷新。

## 数据状态管理： DRY 原则

1. 能计算得到的状态就不要单独存储
2. 组件尽量无状态，所需数据通过 props 获取（可以使组件性能更优，并且提高可重用性 

## JSX： 语法糖

- 在 js 中直接写 html 标记。
- jsx 的本质：动态创建组件的语法糖 

```js
const name ="stanny";
const element = <h1>Hello,{name}</h1>;// 这里实际返回的是 html 结点
//等同于：
const name = "stanny";
const element = React.createElement(
    'h1',
    null,
    'Hello',
    name
);
```

- 延展属性

```js
const props = {firstName:"Stanely",lastName:"Stanny"};
const greeting = <Greeting {...props} />;、
```

## 组件命名约定

1. React 认为小写的 tag 是原生 DOM 节点， 如'div'
2. 自定义的组件以大写字母开头
3. 属性语法？

## react 生命周期

可以分成三个阶段

1. 创建时
2. 更新时
3. 卸载时

1. render 阶段
2. pre-commit 阶段（更新 dom 结点称之为 commit）： 在此节点可以读取 DOM
3. commit 阶段： 

## Virtual DOM 

是 jsx 的运行基础

虚拟 DOM 的两个假设： 理解 DOM diff 算法（算法复杂度 优化到了 O（n））
1. 组件的 DOM 结构是相对稳定的
2. 类型相同的兄弟节点可以被唯一标识 （key 属性，提高性能）

DOM diff
- 节点跨层移动（几率小）删除父节点的所有子节点重新创建，不必考虑某个子节点是否会在其他地方用到。

## 组件复用的另外两种形式

设计模式，使用react 组件新的方法模式。
1. 高阶组件（一般不会有自己的 ui 呈现，只是负责为它自己封装的组件提供额外的功能支持，比如提供数据，  解决组件多层传递资源问题） 
2. 函数作为子组件

## contenxt   

> Context 通过组件树提供了一个传递数据的方法，从而避免了在每一个层级手动的传递 props 属性。

- 根节点 提供上下文数据 provider
- 子节点共享这些数据
- provider（是根节点）  value 设置的值通过 consumer 子节点的函数参数传入
- 不要仅仅为了避免在几个层级下的组件传递 props 而使用 context，它是被用于在多个层级的多个组件需要访问相同数据的情景。

```js
const ThemeContext = React.createContext('light');

class App extends React.Component {
    render(){
        return (
            <ThemeContext.Provider value= "dark">
                <ThemeButton>
            </ThemeContext>
        )
    } 
}
function ThemeButton(prop){
    return (
        <ThemeContext.Consumer>
            {
                theme => <Button {...props} theme={theme}></Button>
            }
        </ThemeContext.Consumer>
    )
}

```

## 脚手架

三种脚手架工具：
1. Create React App，
2. Codesandbox：在线代码编辑器，支持react、vue 以及 angular 等项目。在线脚手架
3. Rekit：基于 create-react-app

### 为什么需要脚手架

web 开发日趋复杂
1. react 管理 UI
2. Redux 状态管理
3. React/Router
4. Babel 代码转换兼容
5. eslint 代码审查

脚手架工具提前定义好典型的项目需要的类库配置。

create-react-app （facebook 推出）
- 适合学习react 或者开发小型项目时使用，内置的工具是最小化
- 整合了babel、webpack、 eslint...

create-react-app + (Redux + React Router + less/scss + feature oriented architecture + dedicated ide) = Rekit

## codesandbox 

- webpack 打包工具运行在浏览器端
- 让你不再关注业务之外端配置
- 不需搭建本地环境

## 为什么需要打包

1. 编译 es6 语法特性，编译 jsx
2. 整合资源，例如图片， less/sass
3. 优化代码体积

- webpack： 各种loader => 每种资源打包后形成可以部署的资源
- 有了脚手架工具，不需要关注太多细节，就可以得到打包结果。

## 打包注意事项

1. 设置 nodejs 环境变量为 production（开发环境和生产环境不一样）  `scripts/build.js`
2. 禁用开发时专用代码，比如logger
3. 设置应用根路径： `package.json`  "homepage" 属性指明应用会被部署在哪里

- `npm run build` 通常会 生成一个 build 目录，用这个文件夹在生产环境中 部署。