# Javascript 代码格式

### 1. 整体格式（个人常用的一套js代码结构）
只是提供了一个模块，大家可以发挥自己强大的逻辑，写出更好的框架出来；
```javascript
// 创建viewContent
var vc = {};

// 创建模块
vc.module = {};

// 全局变量定义
vc.content = {};

// dom拾取
vc.doms = {};

// 渲染模块 and 数据验证模块
vc.module.render = function(){

  var $render = function(){
    ...
  }
  
  return {
    render: $render,
  }
}();

// 事件模块
vc.module.bindEvent = function(){

  var _initEvent = function(){
    ...
  }

  return {
    init: _initEvent,
  }
}();

// 服务模块
vc.module.service = function(){
  
  var _getServiceData = function(){
    ...
  }
  
  return {
    getServiceData: _getServiceData,
  }
}();

// 初始化
var _initialize = function(){
  vc.module.render.render();
  vc.module.bindEvent.init();
  vc.module.service.getServiceData();
}

_initialize();
```

###### 优缺点：
1. 不适合新手使用，需要一段时间接受；
2. 每个页面只有一个对象，一个方法，比ES6的写法更加的让开发者看懂，可读性高，方便二次开发；
3. 模块里方法命名的规则，渲染数据和验证数据使用$开头加上方法命名，获取数据和绑定事件使用_开头加上方法命名；

### 2. 命名规范
尽可能的使用英文来命名，单词一定要拼全，命名长度过长的话，可以使用单词缩写，缩写的单词，一定要让别人看得懂，当然了可以加注释；
```javascript
// 构造函数命名 大驼峰命名
function StructureFunction(){
  ...
}

StructureFunction.prototype.__name__ = function(){
  ...
}

// 函数命名 和数据有关的使用_开头命名，和渲染有关使用$开头命名
function _commonFunction = function(){
  ...
}

function $commonFunction = function(){
  ...
}

// 全局变量 尽量避免少写全局变量，能在方法里面解决的就不要拿到外面来
vc.content = {
  userId: '',
  userName: '',
};

// dom拾取 统一使用id来拾取元素 id的命名和dom命名一样
vc.doms = {
  btn: $("#btn"),
};
```

### 3. 方法调用
这里面有个很精髓的地方就是 `vc.module.service = function(){}();` 的使用，但是方法里面一定要 `return {}`,不然调不到；
```javascript
vc.module.service = function(){
  
  var _getServiceData = function(){
    ...
  }
  
  return {
    getServiceData: _getServiceData,
  }
}();

vc.module.service.getServiceData();
```

### 5. 代码细节方面
##### 1 变量书写
```javascrtip
vc.content =  {
  name:'aa', // error
  name: 'aa', // ok
};
```
##### 2 判断书写
```javascrtip
if(name){
  ...
}else{
  ...
} // ok
```
> ##### 2.1 这种写法为后端代码写法，也不能说这种写法错误，结合整体的代码风格来决定
```javascrtip
if(name)
{
  ...
}
else
{
  ...
}
```
> ##### 2.2 ES6写法，书写方面会简单很多
```javascrtip
if(name) console.log(...) // ok

if(name) 
console.log(...) //error
```
##### 3. 赋值书写
避免重复书写
```javascript
function name(n){
  n = n ? n : ''; // error
  
  n = n || ''; // ok
}
```
