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

1.挂载阶段
    getDefaultProps\getIniteState\componentWillMount\render\compoentDidMount
2.更新阶段
    componentWillRecieveProps\shouldCompoentUpdate\componentWillUpdate\render\compoentDidUpdate
3.卸载阶段
    componentWillUnMount

1.挂载阶段有：`getDefaultProps`这个方法只会调用一次。返回来默认的属性值。`getInitialState`用来初始化每个实例的state。`componentWillMount`的该方法在首次渲染之前调用，也是在render方法调用之前修改state的最后一次机会。`render`创建一个虚拟DOM，标示组件的输出。对于一个组件来说，这个方法是必须的。`componentDidMount`该方法被调用时，已经渲染出真是的DOM了。一般用来调后台接口。   
2.更新阶段：`componentWillReceiveProps`组件的props属性可以通过付组件来更改。在这里可以更新state,触发render方法重新渲染组件。`shouldComponentUpdate`如果确定组件的props或state的改变不需要重新渲染，可以返回false来阻止组件重新渲染。`componentWillUpdate`，在组件接收到新的props或state即将渲染前。此时不要更新props或state.`componentDidUpdate`表示更新之后，相当于compoentDIdMount，可以获得DOM.    
3.卸载阶段：`componentWillUnmount`卸载销毁时执行，完成所有的清理和销毁工作。主要用于取消定时器或事件监听器。

2.state
-----------------------

[具体情况参考](https://juejin.im/post/5a155f906fb9a045284622b4)     
1.setState不会立刻改变React组件中state的值    
2.setState通过引发一次组件的更新过程来引发重新绘制    
3.多次setState函数调用产生的效果会合并



3.虚拟dom
---------------------

[虚拟DOM介绍](http://www.alloyteam.com/2015/10/react-virtual-analysis-of-the-dom/)虚拟DOM是render方法返回来的一个轻量级javascript对象。虚拟DOM具有batching(批处理)和diff算法。

4.diff算法
--------------------------

[参考资料](https://zhuanlan.zhihu.com/p/20346379)

>1.三个策略

传统diff算法，复杂度是o(n的三次方)，通过改进变成o(n)，主要用到的三个策略是    
1.Web UI中DOM节点跨层级的移动操作很少，可以忽略不计     
2.拥有相同类的两个组件将会生成相似的树形结构，拥有不同类的两个组件将会生成不同的树形结构     
3.对于同以层级的一组子节点，它们可以通过唯一id进行区分

基于这三个策略对tree diff\component diff\element diff做了优化。tree diff只进行统一层级比较。component diff不同类型的组件，删除组件，再新建组件。element diff设置key

5.react和vue区别
---------------------------
1.相同点：虚拟DOM/组件化／属性／构建工具    
2.不同点：JSX-模版／状态管理-对象属性／双向数据绑定

6.react中遇到的困难
------------------------------
1.动态表单中列表的key，必须是固定的，不然会出问题。    
2.当导航切换特别快的时候，之前请求的数据出现了setState(…):Can only update a mounted or mounting component……的错误。出现这个问题时，这个主要是发生在异步处理的情况下，例如事件或者异步请求的情况     
3.添加给DOM元素的监听事件，组件卸载时，手动清除。     
4.表单校验问题      
5.