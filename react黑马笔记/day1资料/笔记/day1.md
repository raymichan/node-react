# React.js - 第1天[直接跳到第6点操作]

## 1. React简介
+ React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram（照片交友） 的网站。做出来以后，发现这套东西很好用，**就在2013年5月开源了**。
+ Angular1 2009 年  谷歌    MVC  不支持 组件化开发
+ 由于 React 的**设计思想极其独特**，属于革命性创新，性能出众，代码逻辑却非常简单。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。
+ 清楚两个概念：
  + library（库）：小而巧的库，只提供了特定的API；优点就是 船小好掉头，可以很方便的从一个库切换到另外的库；但是代码几乎不会改变；
  + Framework（框架）：大而全的是框架；框架提供了一整套的解决方案；所以，如果在项目中间，想切换到另外的框架，是比较困难的；




## 2. 前端三大主流框架

> 三大框架一大抄

+ Angular.js：出来**较早**的前端框架，学习曲线比较陡，NG1学起来比较麻烦，NG2 ~ NG5开始，进行了一系列的改革，也提供了组件化开发的概念；从NG2开始，也支持使用TS（TypeScript）进行编程；
+ Vue.js：**最火**（关注的人比较多）的一门前端框架，它是中国人开发的，对我我们来说，文档要友好一些；
+ React.js：**最流行**（用的人比较多）的一门框架，因为它的设计很优秀；




## 3. React与vue的对比
### 组件化方面
1. **什么是模块化：**是从**代码**的角度来进行分析的；把一些可复用的代码，抽离为单个的模块；便于项目的维护和开发；
2. **什么是组件化：** 是从 **UI 界面**的角度 来进行分析的；把一些可服用的UI元素，抽离为单独的组件；便于项目的维护和开发；
3. **组件化的好处：**随着项目规模的增大，手里的组件越来越多；很方便就能把现有的组件，拼接为一个完整的页面；
4. **Vue是如何实现组件化的：** 通过 `.vue` 文件，来创建对应的组件；
   + template  结构
   + script        行为
   + style           样式


5. **React如何实现组件化**：大家注意，React中有组件化的概念，但是，并没有像vue这样的组件模板文件；React中，一切都是以 JS 来表现的；因此要学习React，JS要合格；ES6 和 ES7 （async  和 await） 要会用；
### 开发团队方面
+ React是由FaceBook前端官方团队进行维护和更新的；因此，React的维护开发团队，技术实力比较雄厚；
+ Vue：第一版，主要是有作者 尤雨溪 专门进行维护的，当 Vue更新到 2.x 版本后，也有了一个以 尤雨溪 为主导的开源小团队，进行相关的开发和维护；

### 社区方面
+ 在社区方面，React由于诞生的较早，所以社区比较强大，一些常见的问题、坑、最优解决方案，文档、博客在社区中都是可以很方便就能找到的；
+ Vue是近两年才火起来的，所以，它的社区相对于React来说，要小一些，可能有的一些坑，没人踩过；

### 移动APP开发体验方面
+ Vue，结合 Weex 这门技术，提供了 迁移到 移动端App开发的体验（Weex，目前只是一个 小的玩具， 并没有很成功的 大案例；都是阿里自己在用）
+ React，结合 ReactNative，也提供了无缝迁移到 移动App的开发体验（RN用的最多，也是最火最流行的）；



## 4. 为什么要学习React
1. 和Angular1相比，React设计很优秀，一切基于JS并且实现了组件化开发的思想；
2. 开发团队实力强悍，不必担心断更的情况；
3. 社区强大，很多问题都能找到对应的解决方案；
4. 提供了无缝转到 ReactNative 上的开发体验，让我们技术能力得到了拓展；增强了我们的核心竞争力；
5. 很多企业中，前端项目的技术选型采用的是React.js；





## 5. React中几个核心的概念
### 虚拟DOM（Virtual Document Object Model）
 + **DOM的本质是什么**：`浏览器中的概念`（除了浏览器没有DOM了，node里面没有DOM），用JS对象来表示 页面上的元素，并提供了操作 DOM 对象的API；
 + **什么是React中的虚拟DOM**：`是框架中的概念`，是程序员 用JS对象来模拟 页面上的 DOM 和 DOM嵌套；
 + **为什么要实现虚拟DOM（虚拟DOM的目的）：**为了实现页面中， DOM 元素的高效更新
 + **DOM和虚拟DOM的区别**：
    + **DOM：**浏览器中，提供的概念；用JS对象，表示页面上的元素，并提供了操作元素的API；

    + **虚拟DOM：**是框架中的概念；而是开发框架的程序员，手动用JS对象来模拟DOM元素和嵌套关系；

      + 本质： 用JS对象，来模拟DOM元素和嵌套关系；
      + 目的：就是为了实现页面元素的高效更新；

### 通过例子解析虚拟DOM

如：有一个需求：点击列头，实现对应表格数据的排序

1. 表格中的数据从哪**来**的：从数据库中查询回来的；

2. 这些查询到的数据，**存**放在哪？这些数据在浏览器的内存中存放着，而且是以**对象数组**的形式来表示的；

3. 这些数据，是怎么**渲染**到页面上的？

   ​	方案1：手动for循环整个数组，然后手动拼接字符串 `str+='<tr></tr>'`

   ​	方案2：使用模板引擎，art-template

4. 思考：上述的方案，有没有性能上的问题？

5. 如果用户点击了【时间】，想按照时间从大到小排序

   1. 触发点击事件，在事件中，把内存中的对象数组，重新排序；
   2. 当排序完后，页面是旧页面，但是内存中的对象数组是新数组；
   3. 想办法，把最新的数组重新渲染到页面上；【思考有没有性能上的问题】

6. **分析总结** ：上述方案，只是实现了把数据渲染到页面上的能力；但是并没有把性能做到最优；

7. 最优方案：**按需渲染**页面【只重新渲染更新的数据所对应的页面元素】

8. 如何实现按需更新？获取内存中的新旧两颗DOM树，进行对比，得到需要被按需更新的DOM元素

   ```
   回顾DOM树的概念
   一个网页呈现的过程：
   1、浏览器请求服务器获取页面HTML代码
   2、浏览器要现在内存中，解析DOM结构，并在浏览器内存中，渲染出一颗DOM树；
   3、浏览器把DOM树，呈现到页面上；
   ```

9. 如何获取到新旧DOM树，从而实现DOM树的对比？

    ![](images\2DOM树.png)

   ```
   分析：浏览器中，并没有直接提供获取DOM 树的API；因此，我们无法拿到浏览器内存中的DOM树；
   ```

10. 程序员可以手动模拟新旧两颗DOM树；就是React中虚拟DOM的概念

11. 程序员如果手动模拟DOM树？如何模拟一个DOM元素

    ![](images\1模拟一个dom元素.png)

12. **总结**:什么是虚拟DOM：用JS对象的形式，来模拟页面上DOM嵌套关系：【虚拟DOM是以JS对象的形式存在的；】

    这就是React中虚拟DOM的概念;

    **本质**：用JS对象的形式，来模拟页面上DOM嵌套关系；

    **目的**：就是为了实现页面元素的高效更新；

![虚拟DOM - 表格排序案例](images/虚拟DOM引入图片.png)

### Diff算法

> Diff算法，提供新旧DOM树对比的最优方案】

【different不同、差异】

 - **tree diff:**新旧两棵DOM树，逐层对比的过程，就是 Tree Diff； 当整颗DOM逐层对比完毕，则所有需要被按需更新的元素，必然能够找到；

 - **component diff：**在进行Tree Diff的时候，每一层中，组件级别的对比，叫做 Component Diff；

    - 如果对比前后，组件的类型相同，则**暂时**认为此组件不需要被更新；
    - 如果对比前后，组件类型不同，则需要移除旧组件，创建新组件，并追加到页面上；

 - **element diff:**在进行组件对比的时候，如果两个组件类型相同，则需要进行 元素级别的对比，这叫做 Element Diff；

   ![Diff算法图](images/Diff.png)

## 6. 创建基本的webpack4.x项目

1. ![1547122331947](C:\Users\ADMINI~1\AppData\Local\Temp\1547122331947.png)

2. 操作 运行`npm init -y` 快速初始化项目

3. 操作 在项目根目录创建`src`源代码目录和`dist`产品目录

4. 操作 在 src 目录下创建 `index.html`

5. 操作 使用 cnpm 安装 webpack ，运行`npm i webpack webpack-cli -D`
   + 如何安装 `cnpm`: 全局运行 `npm i cnpm -g`

6. 注意了解：webpack 4.x 提供了 约定大于配置的概念；目的是为了尽量减少 配置文件的体积；
   + 默认约定了：
   + 打包的entry入口是`src` -> `index.js`
   + 打包的output输出文件是`dist` -> `main.js`
   + 4.x 中 新增了 `mode` 选项(为必选项)，可选的值为：`development` 和 `production`;

7. 操作 新建`webpack.config.js`配置文件

   ```javascript
   //向外暴露一个打包的配置对象   属于Node语法，因为webpack是基于Node构建的，所以webpack支持所有Node API 和语法
   module.exports = {
       mode:'development';，//开发者模式未压缩'development' or 生产模式压缩了'production'
       // 在 webpack 4.x 中，有一个很大的特性，就是 约定大于配置约定，
       // 默认的打包入口路径是src -> index.js
   }
   
   
   
   // 行不行 ？  Node和webpack目前不行； // 这是 ES6 中 向外导出模块的API 与之对应的 是  import ** from '标识符'
   // export default {}
   //  Node 支持哪些 特性呢？  如果 chrome 浏览器支持哪些，则 Node 就支持哪些；
   ```

    Node 支持哪些 特性呢？  如果 chrome 浏览器支持哪些，则 Node 就支持哪些；

   ![](images\3Node 支持哪些 特性.png)

   

8. 【`webpack-dev-server` 】作用：【内存：快】在内存中实时编译打包main.js到项目更目录

   - `npm i webpack-dev-server -D` 把这个工具**安装到项目**的本地开发依赖【不等于全局安装】

   - 解决非全局安装使用webpack-dev-server的操作+更改package.json里的配置

     - 【确认】使用webpack-dev-server前提是webpack一定有**安装到本地项目**`npm i webpack -D`

     - 由于webpack-dev-server没有全局安装，所以在 `package.json` 里的“scripts”中添加 配置`"dev": "webpack-dev-server --open --port 2323 --contentBase src --hot --host 127.0.0.1"`

       - --open firefox
       - --open iexplore
       - --progress打包记录
       - --compress压缩
       - [Webpack系列——关于Webpack-dev-server配置的点点滴滴](https://www.jianshu.com/p/5dd1a6ae1de9)

     - 最后命令窗口输入`npm run dev`或`npm run ***`

     - 现在引入script后，到时安装了`html-webpack-plugin`插件也会删除该引用

       ![](D:\用户目录\我的文档\myNode\react黑马笔记\day1资料\笔记\images\4修改引用main js.png)

9. 【`html-webpack-plugin`】作用：在内存中，根据指定的模板页面，生成一份内存中的首页；同时自动把打包好的main.js追加到页面底部

   - 安装`npm i html-webpack-plugin -D`

   - 引入 修改webpack.config.js配置

     ```
     const path = require('path');// 导入处理路径的模块
     const htmlWebpackPlugin = require('html-webpack-plugin');//导入在内存中自动生成index页面的插件
     ```

   - 主要是插件，都一定要在导入的对象中，把对象挂载一个plugins节点

     ```
     plugins:[  //插件
             new htmlWebpackPlugin({ // 创建一个在内存汇总生成html页面的插件的实例对象
             	template:path.join(__dirname,'./src/index.html'),//指定源文件模板页面
                 //template:path.resolve('./src/index.html'),//指定源文件模板页面
                 filename:'index.html',//生成内存中页面的名称
             })
         ],
     ```

   - 命令窗口运行`npm run dev`

10. ……



## 7. 在项目中使用 react

1. 运行 `npm i react react-dom -S` 安装两个包      -S代表从开发到上线都用这个包  -D工具

   + react： 专门用于创建组件和虚拟DOM的，同时组件的生命周期都在这个包中
   + react-dom： 专门进行DOM操作的，最主要的应用场景，就是`ReactDOM.render()`

2. 在`index.html`页面中，创建容器：

   ```html
   <!-- 容器，将来，使用 React 创建的虚拟DOM元素，都会被渲染到这个指定的容器中 -->
   <div id="app"></div>
   ```

3. 在`index.js`导入 包：

   ```js
   import React from 'react';//创建组件、虚拟DOM元素，生命周期
   import ReactDOM from 'react-dom';//把创建好的组件 和 虚拟DOM 放到页面上展示
   ```

4. 创建虚拟DOM元素：

   ```jsx
   // 这是 创建虚拟DOM元素的 API    <h1 title="啊，五环" id="myh1">你比四环多一环</h1>
   //  第一个参数： 标签的类型：字符串类型的参数，表示要创建的标签的名称
   //  第二个参数： 标签的属性节点：对象或null类型的参数， 表示 创建的DOM元素的属性节点
   //  第三个参数： 标签的子元素：子节点(包括其他虚拟DOM 获取文本子节点)
   //  第 N个参数： 其他子节点
   const myh1 = React.createElement('h1', { title: '啊，五环', id: 'myh1' }, '你比四环多一环')
   const myh1 = React.createElement('h1', null, '你比四环多一环')
   ```
   注意：React.createElement(）方法的调用一般都有返回值，上面例子用const myh1接收，接收后只在内存中


5. 渲染：使用 ReactDOM把虚拟DOM渲染到页面上

   ```js
   // 3. 渲染虚拟DOM元素
   // 参数1： 哪里来：表示要渲染的虚拟DOM对象
   // 参数2： 哪里去：指定容器,注意：这里不能直接放 容器元素的Id字符串，需要放一个容器的DOM对象
   ReactDOM.render(myh1, document.getElementById('app'))
   ```

   ​

## 8. JSX语法

> 什么是JSX语法：就是符合 xml 规范的 JS 语法；（语法格式相对来说，要比HTML严谨很多）
>
> // HTML 是最优秀的标记语言；
> // 注意： 在 JS 文件中，默认不能写 这种 类似于 HTML 的标记；否则 报错+打包会失败；
> // 可以使用 `babel` 来转换 这些 JS 中的标签；
> // 大家注意：这种 在 JS 中，混合写入类似于 HTML 的语法，叫做 JSX 语法； 符合 XML 规范的 JS ；
> // 注意： JSX 语法的本质，仍然是 在运行的时候，被转换成了 React.createElement 形式来执行的；
> `const myh1 = <h1 id="myh1" title="啊，五环">你比四环多一环</h1>；`
>
> ![](images\5babel JSX语法.png)

1. **如何启用 jsx 语法？**
   + 安装 `babel` 插件 [从babel7升级到babel8](http://kacoro.lofter.com/post/188bab_12c5d909d#)

     [babel从入门到入门](https://www.cnblogs.com/lsgxeva/p/7758184.html)

     - 运行`npm i babel-core babel-loader@7.1.5 babel-plugin-transform-runtime -D`
     - 运行`npm i babel-preset-env babel-preset-stage-0 -D`
       - `babel-loader` 是安装的8.x[版本](https://blog.csdn.net/wulala_hei/article/details/84768071)

   + 安装能够识别转换jsx语法转换为React.createElement(）语法的包 `babel-preset-react` 

     + 运行`npm i babel-preset-react -D`

   + 在项目根目录中添加 `.babelrc` json配置文件【要符合json语法，不能单引号，不能注释，3个语法+一个插件】

     ```json
     {
       "presets": ["env", "stage-0", "react"],
       "plugins": ["transform-runtime"]
     }
     ```

   + webpack.config.js添加babel-loader配置项：

     > // webpack 默认只能打包处理 .js 后缀名类型的文件； 像 .png .vue 无法主动处理，所以要配置第三方的loader；

     ```js
     module: { //要打包的第三方模块
         rules: [//第三方 模块的配置规则
           { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ },// 千万别忘记添加 exclude 排除项
         ]
     }
     ```

     ​

2. **jsx 语法的本质：**并不是直接把 jsx 渲染到页面上，而是 内部先转换成了 createElement 形式，再渲染的；

3. **在 jsx 中混合写入 js 表达式**：在 jsx 语法中，要把 JS代码写到 `{ }` 中

   + 渲染数字`let a=10`											 `{a+2}`
   	 渲染字符串`let str = '你好'`                   		                                         `{str}`
   + 渲染布尔值`let boo = false`                                                                      `{boo ? '条件为真' ：'条件为假'}`
   + 为属性绑定值`let title='999'`                                                                  `<p title={title}>这是p标签</p>`
   + 渲染jsx元素`const h1=<h1>我是h1</h1>`                                                     `{h1}`
   + 渲染jsx元素数组`const arr = [<h1>我是h2</h2>,<h3>我是h3</h3>]`    `{arr}`
   + 将普通字符串数组，转为jsx数组并渲染到页面上【两种方案】
     + 方案一`{nameArr}`
     + 方案二`{arrStr.map(item=><h3 key={item}>{item}</h3>)}`
     + 注意：React 中，数组要把`key` 添加给被forEach 或 map 或 for 循环直接控制的元素

4. **在 jsx 中 写注释**：推荐使用`{ /* 这是注释 */ }`

5. **为 jsx 中的元素添加class类名**：需要使用`className` 来替代 `class`；`htmlFor`替换label的`for`属性

6. 在JSX创建DOM的时候，所有的节点，必须有唯一的根元素进行包裹；

7. 在 jsx 语法中，标签必须 成对出现，如果是单标签，则必须自闭和！

> 当 编译引擎，在编译JSX代码的时候，如果遇到了`<>`那么就把它当作 HTML代码去编译，如果遇到了 `{}` 就把 花括号内部的代码当作 普通JS代码去编译；




## 9. React中创建组件

### 第1种 - 创建组件的方式

> **使用构造函数（首字母大写）来创建组件**，如果要`接收外界`传递的数据，需要在 构造函数的参数列表中使用`props`来接收；
>
> 组件中必须要向外return一个合法的JSX创建的虚拟DOM；

+ 创建组件：

  ```jsx
  function Hello () { 
  	// return null 
  	return <div>Hello 组件</div>
  }
  ```

+ 为组件传递数据：

  ```jsx
  // 在构造函数中，使用 props 形参，接收外界 传递过来的数据
  function Hello(props) {
    // props.name = 'zs'
    console.log(props)
    // 结论：不论是 Vue 还是 React，组件中的 props 永远都是只读的；不能被重新赋值；
  
    return <div>这是 Hello 组件 --- {props.name} --- {props.age} --- {props.gender}</div>
  }
  
  const dog = {
      name:'大黄',
      age:2,
      gender:'雄性'
  }
  
  // 使用组件并 为组件传递 props 数据
  ReactDOM.render(<div>
      我是渲染2号
      <Hello name={dog.name} age={dog.age} gender={dog.gender}></Hello>
      <Hello {...dog}></Hello>
  </div>,document.getElementById('app'));
  ```

  ​

1. 父组件向子组件传递数据

2. 使用{...obj}属性扩散传递数据【展开运算符】

3. 将组件封装到单独的文件中Hello.jsx

4. 注意：组件的名称首字母必须是大写，否则会报错

5. 在导入组件的时候，如何省略组件的`.jsx`后缀名：

   ```js
   // 打开 webpack.config.js ，并在导出的配置对象中，新增 如下节点：
   resolve: {
       extensions: ['.js', '.jsx', '.json'], // 表示，这几个文件的后缀名，可以省略不写
       alias: {
           '@': path.join(__dirname, './src')
       }
     }
   ```
   注意：每次修改完配置文件 webpack.config.js 文件，要重新运行`npm run dev`

6. 在导入组件的时候，配置和使用`@`路径符号

### 第2种 - 创建组件的方式

> 使用 class 关键字来创建组件
>
> ES6 中 class 关键字，是实现面向对象编程的新形式；

#### 了解ES6中 class 关键字的使用

1. class 中 `constructor` 的基本使用
2. 实例属性和实例方法
3. 静态属性和静态方法
4. 使用 `extends` 关键字实现继承

#### 基于class关键字创建组件

1. 最基本的组件结构：

   ```jsx
   class 组件名称 extends React.Component {
       render(){
           return <div>这是 class 创建的组件</div>
       }
   }
   ```




## 10. 两种创建组件方式的对比

1. 用**构造函数**创建出来的组件：叫做“无状态组件”
2. 用**class关键字**创建出来的组件：叫做“有状态组件”

> 有状态组件和无状态组件之间的**本质区别**就是：有无state属性！



## 11. 一个小案例，巩固有状态组件和无状态组件的使用

### 通过for循环生成多个组件
1. 数据：
```js
CommentList: [
    { id: 1, user: '张三', content: '哈哈，沙发' },
    { id: 2, user: '李四', content: '哈哈，板凳' },
    { id: 3, user: '王五', content: '哈哈，凉席' },
    { id: 4, user: '赵六', content: '哈哈，砖头' },
    { id: 5, user: '田七', content: '哈哈，楼下山炮' }
]
```

### 设置样式

1. 使用普通的 `style` 样式
2. 启用 css-modules
2. 使用`localIdentName`设置生成的类名称，可选的参数有：
   + [path]  表示样式表所在路径
   + [name]  表示 样式表文件名
   + [local]  表示样式的定义名称
   + [hash:length]  表示32位的hash值
4. 使用 `:local()` 和 `:global()`



## 安装 React Developer Tools 调试工具

[React Developer Tools - Chrome 扩展下载安装地址](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=zh-CN)



## 总结
理解React中虚拟DOM的概念
理解React中三种Diff算法的概念
使用JS中createElement的方式创建虚拟DOM
使用ReactDOM.render方法
使用JSX语法并理解其本质
掌握创建组件的两种方式
理解有状态组件和无状态组件的本质区别
理解props和state的区别

## 相关文章

+ [2018 年，React 将独占前端框架鳌头？](https://mp.weixin.qq.com/s/gV-w_rRfdBVAqsOpBGZaVw)
+ [前端框架三巨头年度走势对比：Vue 增长率最高](https://mp.weixin.qq.com/s/0wXWqKIigaKzMSfy4vJMVw)


+ [React数据流和组件间的沟通总结](http://www.cnblogs.com/tim100/p/6050514.html)
+ [单向数据流和双向绑定各有什么优缺点？](https://segmentfault.com/q/1010000005876655/a-1020000005876751)
+ [怎么更好的理解虚拟DOM?](https://www.zhihu.com/question/29504639?sort=created)
+ [React中文文档 - 版本较低](http://www.css88.com/react/index.html)
+ [React 源码剖析系列 － 不可思议的 react diff](http://blog.csdn.net/yczz/article/details/49886061)
+ [深入浅出React（四）：虚拟DOM Diff算法解析](http://www.infoq.com/cn/articles/react-dom-diff?from=timeline&isappinstalled=0)
+ [一看就懂的ReactJs入门教程（精华版）](http://www.cocoachina.com/webapp/20150721/12692.html)
+ [CSS Modules 用法教程](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)
+ [将MarkDown转换为HTML页面](http://blog.csdn.net/itzhongzi/article/details/66045880)
+ [win7命令行 端口占用 查询进程号 杀进程](https://jingyan.baidu.com/article/0320e2c1c9cf0e1b87507b26.html)