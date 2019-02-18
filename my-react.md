# my-react

## 类 组件 继承 Component

构造器constructor(props)

超类super(props)

```jsx
import React, { Component, Fragment } from 'react';
import '../style.css';
import Sonsss from './Sonsss';
class Son extends Component {
    constructor(props){
        super(props);
        this.state = {
            inputValue: 'hello!!!!!',
            list: []
        }
    }
    render() {
        //JSX
        return (
            <Fragment>
                <div>
                    <label htmlFor="itext">输入内容</label>
                    <input 
                        className="inputtext" 
                        id='itext' 
                        type="text" 
                        value={this.state.inputValue} 
                        onChange={this.handleInputChange.bind(this)}/>
                    <input type="button" value="提交" onClick={this.handleBtnClick.bind(this)}/>
                </div>
                <ul>
                    {
                        this.state.list.map((item, index) => {
                            return <Todoitem 
                                        content={item} 
                                        index={index} 
                                        deleteItem={this.handleItemDelete.bind(this)}
                                        key={index}
                                    >
                                    </Todoitem>
                        })
                    }
                </ul>
            </Fragment>
        );
    }
    addfn(){}
    delete(){}
}
export default Son;
```

## index.js引入各组件

import TodoList from './TodoList'

## 3-5父传子 与 子传父

```js
父传子
父组件渲染子组件
<Son content={item} index={index} deleteFn={this.deleteItem.bind(this)} />

子组件-Son
return <div>{this.props.content}<div>
    
=============================
子传父
子组件定义某方法里面执行调用父组件的方法【通过父传子（方法有参数也通过父传子）】，从而修改父组件的数据
父fnFather(a)
子fnSon()
步骤：先 父传子｛传父的方法 + 传父的方法里的参数
	 后 子方法执行（父方法) 即：fnSon(this.props.属性名（this.props.属性名）)
```

## 4-2父传子高级指南-PropTypes

https://reactjs.org/docs/typechecking-with-proptypes.html

```
import React, { Component, Fragment } from 'react';
import PropTypes from 'prop-types';
class Son extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

//组件名.propTypes = {
Son.propTypes = {
  name: PropTypes.string
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string.isRequired
};
//设置默认值
//组件名.defaultProps = {
Son.defaultProps = {
  name: 'Stranger'
};
```



## 3-6优化-引用框架、组件、样式

一般先引用组件，再引用样式

一般把样式放在所有组件后面

```jsx
import React, { Component, Fragment } from 'react';
import Sonsss from './Sonsss';
import '../style.css';
```



## 优化-函数this指向的绑定

一般 this 指向的绑定放在顶部

组件初始化的时候就把 this 指向改好

this.addFn = this.addFn.bind(this)

```jsx
class Son extends Component {   
	constructor(props){
        super(props);
        this. addFn = this.addFn.bind(this);
        this.deleteFn = deleteFn.bind(this);
        this.state = {
            inputValue: 'hello!!!!!',
            list: []
        }
    }
    render() {
        //JSX
        return (
            <Fragment>
                <div>
                    <label htmlFor="itext">输入内容</label>
                    <input 
                        className="inputtext" 
                        id='itext' 
                        type="text" 
                        value={this.state.inputValue} 
                        onChange={this.addFn}/>
                    <input type="button" value="提交" onClick={this.deleteFn}/>
                </div>
            </Fragment>
        );
    }
    addFn(){}
    deleteFn(){}
}
export default Son;
```

## 优化-JSX的html结构

JSX过长且融合长逻辑的代码 如以下ul 里的语句

应定义一个方法getTodoItemHtml(){return }

该方法一定要有return

```jsx
 render() {
        //JSX
        return (
            <Fragment>
                <div>
                    <label htmlFor="itext">输入内容</label>
                    <input 
                        className="inputtext" 
                        id='itext' 
                        type="text" 
                        value={this.state.inputValue} 
                        onChange={this.handleInputChange.bind(this)}/>
                    <input type="button" value="提交" onClick={this.handleBtnClick.bind(this)}/>
                </div>
                <ul>
                    {
                        this.state.list.map((item, index) => {
                            return <Todoitem 
                                        content={item} 
                                        index={index} 
                                        deleteItem={this.handleItemDelete.bind(this)}
                                        key={index}
                                    >
                                    </Todoitem>
                        })
                    }
                </ul>
            </Fragment>
        );
    }
    addfn(){}
    delete(){}
}
export default Son;

==================================================
//优化后
				<ul>
                    {this.getTodoItemHtml()}
                </ul>
            </Fragment>
        );
    }
    addfn(){}
    delete(){}
    getTodoItemHtml(){
        this.state.list.map((item, index) => {
                            return <Todoitem 
                                        content={item} 
                                        index={index} 
                                        deleteItem={this.handleItemDelete.bind(this)}
                                        key={index}
                                    >
                                    </Todoitem>
                        })
    }
}
```

## 优化-数据修改this.setState()

```
//原来this.setState函数里面是对象
handleInputChange(e){
    this.setState({
        inputValue:e.target.value
    })
}
//优化后，this.setState函数里面是方法【形成异步，由于异步，故e.target.value要在外层提出来保存】，有return 返回一个对象
handleInputChange(e){
	const value = e.target.value;
    this.setState(()=>{
        return{
            inputValue:value
        }
    })
}
//可以选择再优化后ES6的写法，只有一个return,且return一个值
handleInputChange(e){
	const value = e.target.value;
    this.setState(()=>({
            inputValue:e.target.value
        })
    )
}
//===========================================
通版的优化模板
xxxxFn(){
    this.setState(() => ({ 对象}))
}
```

## prevState修改数据前的数据

this.setState((prevState)=>({}))

prevState指修改数据前的数据是什么

prevState等价于修改前的this.state

```
//没prevState
bandleBtnClick(){
    this.setState(()=>({
        list:[..this.state.list,this.state.inputValue],
        inputValue:''
    }))
}

//有prevState
bandleBtnClick(){
    this.setState((prevState)=>({
        list:[..prevState.list,this.state.inputValue],
        inputValue:''
    }))
}
```



## 优化-组件传递

```
//父传子的方法优化
//原来
deleteFn(){
    this.props.deleteItem(this.props.index)
}
//优化后
deleteFn(){
    const{ deleteItem，index } = this.props
    deleteItem(index)
}
```

## 4-3props,state与render函数的关系

当组件的props或者state发生改变的时候，render函数就会重新执行

当父组件的render函数被运行时，它的子组件的render都将被重新运行

## 虚拟DOM为什么提高性能

减少对真是DOM的创建、以及真实DOM的对比，

取而代之创建的都是JS对象，对比的也是JS对象

虚拟DOM本质上就是一个JS对象

之所以提高性能的原因是JS里面比较JS的对象，不损耗性能；比较真实的DOM损耗性能

JSX -> createElement -> 虚拟DOM（JS对象）-> 真实的DOM

## diff算法

1、原始虚拟DOM和新的虚拟DOM的对比

​	同层比对，一层一层比对

​	当某一层不一样时，下一层不会再比，下面的直接原始替换

2、循环数组，key值	

​	没有key值时，要二层循环的比较，比较起来麻烦且耗性能

​	设置key值后，以前的abcde节点还是叫abcde节点，这时候的虚拟DOM的比对会根据key值作为关联

## key值选什么比较合适

不要用索引值，可以用key={item}

## 获取元素对应的DOM节点e.target 或ref

1、事件获取元素对应的DOM节点

2、ref【一般情况下不用、复杂业务如动画才有ref】

```
<input ref={(input) => {this.input=input}｝>
//意思为：构建了一个ref的引用，这个引用叫this.input
```



## 4-8生命周期

概念：`生命周期函数`指在`某一个时刻`组件`会自动调用执行的函数`

只会被执行一次的生命周期：componentWillMount(){}、componentDidMount(){ajax的请求发送}

```
//1
//在组件即将被挂载到页面的时刻自动执行
componentWillMount(){}
//当组件的state或者peops发生改变的时候，render函数就会重新执行
render(){}
//在组件被挂载之后到页面的时刻自动执行
componentDidMount(){ajax的请求发送}

//2
//在组件将更新之前，会自动执行
shouldComponentUpdate(nextProps,nextState){
	if(nextProps.content !== this.props.content){
        return true;//一般都是些放回true
	}else{
        return false;//false的意思是我不需要更改这个的组件，不需要更新;且后面的生命周期也不会执行了
	}
}
//在组件将更新之前，会自动执行，但是他在shouldComponentUpdate返回true之后被执行
componentWillUpdate(){}
//input重新输入内容,再次执行render页面重新渲染
render()
//组件更新完成之后
componentDidUpdate(){}

//3
//组件存在父组件传递过来的props时执行
//条件：当一个组件从父组件接受了参数
//如果这个组件第一次父组件中显示，不会执行
//如果这个组件之前已经存在于父组件中，才会执行
componentWillReceiveProps(){}

//4
//当组件即将从页面中剔除的时候，会被执行(先执行，后移除)
componentWillUnmount(){}
```

## 优化-避免无谓的组件render函数的运行

借助shouldComponentUpdate方法提高react组件的性能

```
//在组件将更新之前，会自动执行
shouldComponentUpdate(nextProps,nextState){
	if(nextProps.content !== this.props.content){
        return true;//一般都是些放回true
	}else{
        return false;//false的意思是我不需要更改这个的组件，不需要更新;且后面的生命周期也不会执行了
	}
}
```

## ajax的请求发送

安装第三方模块 npm i axios / yarn add axios

重新启动服务器 npm run start

```jsx
import React, { Component, Fragment } from 'react';
import Sonsss from './Sonsss';
inport axios from 'axios'
import '../style.css';

componentDidMount(){
    //ajax的请求发送
    axios.get('/api/todolist')
    .then((res)=>{
        this.setState(()=>{
            console.log(res.data)
            return {
                list:
            }
        })
    })
    .catch(()=>{})

```

## 使用Chaeles工具进行接口数据模拟

前端数据的模拟:作用是抓到浏览器向外发送的请求，然后对一些请求进行处理

图标样子：长成一个陶瓷花瓶的样子

点进去，上面图标的【黄色扫把】为清除

选择工具栏里的Tools-Map Local…

​	弹出对应的框，点击白的框Add

​	点击后又弹出一个配置项的框

| Map from |               |
| -------- | ------------- |
| Protocol | http          |
| Host     | localhost     |
| Port     | 3000          |
| Path     | /api/todolist |
| Query    |               |

//只要请求Map from上面的地址

//就把Map to里面的内容返回给你

| Map to     |                                 |        |
| ---------- | ------------------------------- | ------ |
| Loxal path | 选择路径为自己建立的.json文件后 | choose |

✔选Enable Map Local

✔选接口路径 | 自选路径

按下OK

## 动画react-transition-group第三方模块

github搜react-transition-group

看到Docunmentation-点击Main documentation进入主文档

安装npm install react-transition-group --save，再点击下面有个CSSTransition

### 单元素动画效果

```
import React, { Component, Fragment } from 'react';
//引用动画组件
import { CSSTransition } from 'react-transition-group';

class Son extend Component{
constructor(props){
    super(props);
    this.state = {
        show:true
    }
    this.handleToggle = this.handleToggle.bind(this);
}

render(){
    return(
    	<Fragment>
    		<CSSTransition 
                in={this.state.show}==========让其知道是true/false，是入场状态还是出场状态
                timeout={300}=================动画执行多久
                classNames='fade'
                unmountOnExit=================false的时候会移除动画元素
                appear={true}=================首次默认（刷新）出现入场动画
            >
				<div>包裹需要动画效果的标签<div>
			</CSSTranstion>
			<button onClick={this.handleToggle}>切换</buttom>
    	</Fragment>
    )
}
}
```

类名

刚要入场的一瞬间【开始】，入场动画执行到动画完成之前（动画完成之后不再存在该类名）【过程】，【结束】

fade-enter, fade-enter-active, fade-enter-done, 
fade-exit, fade-exit-active, fade-exit-done
fade-appear, and fade-appear-active

```css
.fade-enter,fade-appear{
    opacity:0;
}
.fade-enter-active,fade-appear-active{
    opacity:1;
    transition:opacity 1s ease-in;
}
.fade-enter-done{
    opacity:1;
}

.fade-exit{
    opactity:1;
}
.fade-exit-active{
   	opacity:0;
    transition:opacity 1s ease-i
}
.fade-exit-done{
    opactity:0
}
```

### 4-14列表元素动画效果

import { CSSTransition,TransitionGroup } from 'react-transition-group';
外层TransitionGroup标签，内层CSSTransition标签+key值

## redux

redux实际上是数据层的框架，它把所有的数据放在Store当中

公用存储区域Store

Redux = Reducer + Flux

## UI框架

### Ant Design

https://ant.design/index-cn

项目使用 npm 或 yarn 安装====npm install antd --save 

重启服务器=================npm run start

引入样式===================import 'antd/dist/antd.css' 

接着需要什么组件就引入什么组件

查找ctrl+F查找所需

点击 <> show code