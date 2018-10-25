React
===================
1.生命周期
-----------------------
    1.componentWillMount
    2.componentDidMount
    3.shuoldcomponentupdate
    4.componentwillupdate
    5.componentDidUpdate
    6.componentwillunmount
    7.componentwillreceiveprops

[具体参考](https://segmentfault.com/a/1190000004168886)

>1.挂载阶段
    getDefaultProps\getIniteState\componentWillMount\render\compoentDidMount

>2.更新阶段
    componentWillRecieveProps\shouldCompoentUpdate\componentWillUpdate\render\compoentDidUpdate

>3.卸载阶段
    componentWillUnMount


>4.1.挂载阶段有：`getDefaultProps`这个方法只会调用一次。返回来默认的属性值。`getInitialState`用来初始化每个实例的state。`componentWillMount`的该方法在首次渲染之前调用，也是在render方法调用之前修改state的最后一次机会。`render`创建一个虚拟DOM，标示组件的输出。对于一个组件来说，这个方法是必须的。`componentDidMount`该方法被调用时，已经渲染出真是的DOM了。一般用来调后台接口。   
2.更新阶段：`componentWillReceiveProps`组件的props属性可以通过付组件来更改。在这里可以更新state,触发render方法重新渲染组件。`shouldComponentUpdate`如果确定组件的props或state的改变不需要重新渲染，可以返回false来阻止组件重新渲染。`componentWillUpdate`，在组件接收到新的props或state即将渲染前。此时不要更新props或state.`componentDidUpdate`表示更新之后，相当于compoentDIdMount，可以获得DOM.    
3.卸载阶段：`componentWillUnmount`卸载销毁时执行，完成所有的清理和销毁工作。主要用于取消定时器或事件监听器。

2.state
-----------------------

[具体情况参考](https://juejin.im/post/5a155f906fb9a045284622b4)     
>1.setState不会立刻改变React组件中state的值    

>2.setState通过引发一次组件的更新过程来引发重新绘制   

>3.多次setState函数调用产生的效果会合并



3.虚拟dom
---------------------

[虚拟DOM介绍](http://www.alloyteam.com/2015/10/react-virtual-analysis-of-the-dom/)虚拟DOM是render方法返回来的一个轻量级javascript对象。虚拟DOM具有batching(批处理)和diff算法。

4.diff算法
--------------------------

[参考资料](https://zhuanlan.zhihu.com/p/20346379)

>1.三个策略

传统diff算法，复杂度是o(n的三次方)，通过改进变成o(n)，主要用到的三个策略是    
* Web UI中DOM节点跨层级的移动操作很少，可以忽略不计     
* 拥有相同类的两个组件将会生成相似的树形结构，拥有不同类的两个组件将会生成不同的树形结构     
* 对于同以层级的一组子节点，它们可以通过唯一id进行区分

基于这三个策略对tree diff\component diff\element diff做了优化。tree diff只进行统一层级比较。component diff不同类型的组件，删除组件，再新建组件。element diff设置key

5.react和vue区别
---------------------------
* 相同点：虚拟DOM/组件化／属性／构建工具    
* 不同点：JSX-模版／状态管理-对象属性／双向数据绑定

6.react中遇到的困难
------------------------------
*  动态表单中列表的key，必须是固定的，不然会出问题。    
*  当导航切换特别快的时候，之前请求的数据出现了setState(…):Can only update a mounted or mounting component……的错误。出现这个问题时，这个主要是发生在异步处理的情况下，例如事件或者异步请求的情况     
*  添加给DOM元素的监听事件，组件卸载时，手动清除。     
*  表单校验问题      

7.setState [参考](https://juejin.im/post/5b45c57c51882519790c7441)
------------------------

>1.[参考](https://www.jianshu.com/p/c6257cbef1b1)

>2.`不能直接修改state`, 例如： this.state.title = 'React';

>3.State的更新是异步的![图片](https://github.com/qingzhu1224/learn-react/blob/master/imges/state.png)

>4.如果state的类型是`不可变类型（数字，字符串，布尔值，null， undefined）`，直接给修改的状态赋一个新值就可以了。如果状态的类型是`数组`，使用`concat、slice、filter或者扩展运算符`.如果是`普通对象`，使用`Object.assgin{}或者扩展运算符`.

Immutable Data
===================================

>1.[参考](https://github.com/camsong/blog/issues/3)

>2.Immutable实现原理是持久化数据结构，也就是使用旧数据创建新数据时，要保证旧数据同时可用且不可变。同时为了避免deepCopy把所有节点都复制一遍带来的性能损耗，使用了结构共享，即如果对象数中一个节点发生变化，只修改这个节点和受它影响的父节点，其他节点则进行共享。优点：`时间旅行`和`节省内存`


虚拟DOM
=======================

>1.[参考](https://foio.github.io/virtual-dom/) 

>2.为什么用虚拟DOM？传统的MVC框架，它是将某个模版编译成模版函数，需要更新时，是自己手动将数据整体传入模版函数，得到一个字符串，使用innerHTML刷新整个容器。这里其实是可以优化的，但由于是手动，是体力活，都是直接使用innerHTML。由于整体替换，一下子销毁这么多元素（有时还绑着事件，可能导致GC出问题），又要插入这么多元素，再重新绑定事件，这个性能很差。react，首先使用编译手段（jsx的虚拟DOM转换），将这部分消耗能提前释放出去，不过将字符串（jsx模版）转换为一个个JS对象，也占不了多少内存。 然后是数据发生变动时, 由于数据变动都是需要用setState方法,因此兼容性很好, 少了Object.defineProperty或wrapper的消耗,然后对应数据通过render转换成字符串,字符串再转换虚拟DOM树 先后虚拟DOM进行比较, 更新视图.[参考](https://www.cnblogs.com/rubylouvre/p/5012458.html)

>3.两个虚拟dom,使用diff算法之后，会产生patchs，再更新dom

>4.[参考](https://github.com/KieSun/My-wheels/tree/master/Virtual%20Dom)

>5.Virtual Dom 算法的实现也就是以下三步

* 通过 JS 来模拟创建 DOM 对象
* 判断两个对象的差异
* 渲染差异url

其他
=====================

1.react的数据载体

2.后台请求接口事放在ComponentWillMount还是ComponentDidMount中？ [参考](http://react-china.org/t/react-componentdidmount-componentwillmount/15144/8)

- 一般异步加载数据放在ComponentDidMount中，因为componentWillMount里面状态改变并不会触发再次更新，而componentDidMount里面state的变化会触发更新，所以对于请求远程数据的，尽量放在componentDidMount，这样状态变化后，界面也会更新，而放在componentWillMount，有可能界面不会更新



3.react 16新增的内容 [参考](https://zhuanlan.zhihu.com/p/34604934)


