为了规范前端团队的开发模式，提高代码质量及协作效率，优化前端性能及用户体验，特制定该前端技术规范文档，其中包括了前端技术栈，HTML，JavaScript，CSS/LESS/SCSS等几个部分。供前端同事参考及开发践行。

---

### JavaScript规范

1. #### es5 语言规范

* 命名
> 变量使用Camel命名法。

推荐： 

```
var loadingModules = {};
```

> 常量使用全部字母大写，单词间下划线分隔的命名方式。

推荐：

```
var HTML_ENTITY = {};  
```

> 函数使用Camel命名法。

推荐： 

```
var TargetState = {
  READING: 1,
  READED: 2,
  APPLIED: 3,
  READY: 4
};
```

> 命名空间使用Camel命名法。

推荐： 

```
equipments.heavyWeapons = {};
```

> 类名使用名词。

推荐： 

```
function Engine(options) {
  ...
}
```

> 函数名使用动宾短语。

推荐：

```
function getStyle(element) {
  ...
}
```

> boolean类型的变量使用is或has开头。

推荐： 

```
var isReady = false;
var hasMoreCommands = false;
```

> Promise对象用动宾短语的进行时表达。

推荐：

```
var loadingData = ajax.get('url');
loadingData.then(callback);
```

* 语言特性

> 变量、函数在使用前必须先定义（不通过 var 定义变量将导致变量污染全局环境。）

推荐：
```
var name = 'MyName';
```

不推荐：
```
name = 'MyName';
```

> 变量即用即声明，不推荐在函数或其它形式的代码块起始位置统一声明所有变量。（变量声明与使用的距离越远，出现的跨度越大，代码的阅读与维护成本越高。虽然JavaScript的变量是函数作用域，还是应该根据编程中的意图，缩小变量出现的距离空间。）

推荐：

```
function kv2List(source) {
  var list = [];
  for (var key in source) {
    if (source.hasOwnProperty(key)) {
      var item = {
        k: key,
        v: source[key]
      };

      list.push(item);
    }
  }
  return list;
}
```

不推荐：
```
function kv2List(source) {
  var list = [];
  var key;
  var item;
  for (key in source) {
    if (source.hasOwnProperty(key)) {
      item = {
        k: key,
        v: source[key]
      };
      list.push(item);
    }
  }
  return list;
}
```

> 使用类型严格的条件判断===。

推荐：
```
if (age === 30) {
  ...
}
```

不推荐：
```
if (age == 30) {
  ...
}
```

> 尽可能使用简洁的表达式。

推荐：
```
if (!name) {
  ...
}
```

不推荐：
```
if (name === '') {
  ...
}
```

推荐：
```
if (name) {
  ...
}
```

不推荐：
```
if (name !== '') {
  ...
}
```

推荐：
```
if (collection.length) {
  ...
}
```

不推荐：
```
if (collection.length > 0) {
  ...
}
```

> 如果函数或全局中的 else 块后没有任何语句，可以删除 else。

推荐：
```
function getName() {
  if (name) {
    return name;
  }

  return 'unnamed';
}
```

不推荐：
```
function getName() {
  if (name) {
    return name;
  }
  else {
    return 'unnamed';
  }
}
```

> 不要在循环体中包含函数表达式，事先将函数提取到循环体外。(循环体中的函数表达式，运行过程中会生成循环次数个函数对象。)

推荐：
```
function clicker() {
  ...
}

for (var i = 0, len = elements.length; i < len; i++) {
    var element = elements[i];
    addListener(element, 'click', clicker);
}
```

不推荐：
```
for (var i = 0, len = elements.length; i < len; i++) {
  var element = elements[i];
  addListener(element, 'click', function () {});
}
```

> 对有序集合进行遍历时，缓存 length。

推荐：
```
for (var i = 0, len = elements.length; i < len; i++) {
  var element = elements[i];
}
```

不推荐：
```
for (var i = 0; i < elements.length; i++) {
  var element = elements[i];
}
```

> 类型检测优先使用 typeof。对象类型检测使用 instanceof。null 或 undefined 的检测使用 == null。

推荐：
```
// string
typeof variable === 'string'

// number
typeof variable === 'number'

// boolean
typeof variable === 'boolean'

// Function
typeof variable === 'function'

// Object
typeof variable === 'object'

// RegExp
variable instanceof RegExp

// Array
variable instanceof Array

// null
variable === null

// null or undefined
variable == null

// undefined
typeof variable === 'undefined'  
```

> 转换成 string 时，使用 + ''。
推荐：
```
num + '';
```

不推荐：
```
new String(num);
num.toString();
String(num);  
```

> 转换成 number 时，通常使用 +。

推荐：
```
+str;
```

不推荐：
```
Number(str);
```

> string 转换成 number，要转换的字符串结尾包含非数字并期望忽略时，使用 parseInt。

推荐：
```
var width = '200px';
parseInt(width, 10);
```

> 使用 parseInt 时，必须指定进制。

推荐：
```
parseInt(str, 10);
```

不推荐：
```
parseInt(str);
```

> 字符串开头和结束使用单引号 '。(1.输入单引号不需要按住 shift，方便输入。2.实际使用中，字符串经常用来拼接 HTML。为方便 HTML 中包含双引号而不需要转义写法。)

推荐：
```
var str = '我是一个字符串';
var html = '<div class="cls">拼接HTML可以省去双引号转义</div>';
```

> 使用对象字面量 {} 创建新 Object。

推荐：
```
var obj = {};
```

不推荐：
```
var obj = new Object();
```

> for in 遍历对象时, 使用 hasOwnProperty 过滤掉原型中的属性。

推荐：
```
var newInfo = {};
for (var key in info) {
    if (info.hasOwnProperty(key)) {
        newInfo[key] = info[key];
    }
}
```

> 使用数组字面量 [] 创建新数组。

推荐：
```
var arr = [];
```

不推荐：
```
var arr = new Array();
```

> 尽量避免使用直接 eval 函数。

> 尽量不要使用 with。（使用 with 可能会增加代码的复杂度，不利于阅读和管理。也会对性能有影响。）

> 尽量避免使用 switch 语句，建议用 if else 来替换。 

> 尽量在脚本中启用严格模式，但避免在脚本第一行启用，这可能会导致所有脚本都启动了严格模式，从而引发一些第三方类库的问题。

推荐：
```
(function(){
  'use strict';
 
  // Your code starts here
 
}());
```

不推荐：
```
'use strict';
 
(function(){
 
  // Your code starts here
 
}());
```

> 用三元操作符判断或返回结果。但切勿在复杂的情况下使用。

推荐：
```
return x === 10 ? 'valid' : 'invalid';
```

不推荐：
```
if (x === 10) {
  return 'valid';
} else {
  return 'invalid';
}
```
2. #### es6 语言规范

当前es6主要应用于react/react-native等新型前端开发框架上，需要结合babel转码器进行转码。相关的语言参考：[ECMAScript 6 入门](http://es6.ruanyifeng.com/ "")

* let 完全取代 var

推荐：
```
'use strict';

if (true) {
  let x = 'hello';
}

for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

不推荐：
```
'use strict';

if (true) {
  var x = 'hello';
}

for (var i = 0; i < 10; i++) {
  console.log(i);
}
```

* 在let和const之间，建议优先使用const，尤其是在全局环境，不应该设置变量，只应设置常量。

推荐：
```
const a = 1;
const b = 2;
const c = 3;
```

不推荐：
```
var a = 1, 
  b = 2, 
  c = 3;
```

* 静态字符串一律使用单引号或反引号，不使用双引号。动态字符串使用反引号。

推荐：
```
const a = 'foobar';
const b = `foo${a}bar`;
const c = 'foobar';
```

不推荐：
```
const a = "foobar";
const b = 'foo' + a + 'bar';
```

* 使用数组成员对变量赋值时，优先使用解构赋值。

推荐：
```
const arr = [1, 2, 3, 4];
const [first, second] = arr;
```

不推荐：
```
const arr = [1, 2, 3, 4];
const first = arr[0];
const second = arr[1];
```

* 函数的参数如果是对象的成员，优先使用解构赋值。

推荐：
```
function getFullName(obj) {
  const { firstName, lastName } = obj;
}
```

推荐:
```
function getFullName({ firstName, lastName }) {
  ...
}
```

不推荐：
```
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;
}
```

* 如果函数返回多个值，优先使用对象的解构赋值，而不是数组的解构赋值。这样便于以后添加返回值，以及更改返回值的顺序。

推荐：
```
function processInput(input) {
  return { left, right, top, bottom };
}
const { left, right } = processInput(input);
```

不推荐：
```
function processInput(input) {
  return [left, right, top, bottom];
}
const { left, right } = processInput(input);

```

* 单行定义的对象，最后一个成员不以逗号结尾。多行定义的对象，最后一个成员以逗号结尾。

推荐：
```
const a = { k1: v1, k2: v2 };
const b = {
  k1: v1,
  k2: v2,
};
```
不推荐：
```
const a = { k1: v1, k2: v2, };
const b = {
  k1: v1,
  k2: v2
};
```

* 对象的属性和方法，尽量采用简洁表达法，这样易于描述和书写。

推荐：
```
var ref = 'some value';
const atom = {
  ref,

  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

不推荐：
```
var ref = 'some value';
const atom = {
  ref: ref,

  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};
```

* 使用扩展运算符（...）拷贝数组。

推荐：
```
const itemsCopy = [...items];
```

不推荐：
```
const itemsCopy = [];
for (let i = 0, len = items.length; i < len; i++) {
  itemsCopy[i] = items[i];
}
```

* 使用Array.from方法，将类似数组的对象转为数组。

推荐：
```
const foo = document.querySelectorAll('.foo');
const nodes = Array.from(foo);
```

* 立即执行函数可以写成箭头函数的形式。

推荐：
```
(() => {
  console.log('halo world.');
})();
```

* 那些需要使用函数表达式的场合，尽量用箭头函数代替。因为这样更简洁，而且绑定了this。

推荐：
```
[1, 2, 3].map((x) => {
  return x * x;
});
```

推荐：
```
[1, 2, 3].map(x => x * x);
```

不推荐：
```
[1, 2, 3].map(function (x) {
  return x * x;
});
```

* 简单的、单行的、不会复用的函数，建议采用箭头函数。如果函数体较为复杂，行数较多，还是应该采用传统的函数写法。

* 所有配置项都应该集中在一个对象，放在最后一个参数，布尔值不可以直接作为参数。

推荐：
```
function divide(a, b, { option = false } = {}) {
  ...
}
```

不推荐：
```
function divide(a, b, option = false ) {
  ...
}

```

* 不要在函数体内使用arguments变量，使用rest运算符（...）代替。因为rest运算符显式表明你想要获取参数，而且arguments是一个类似数组的对象，而rest运算符可以提供一个真正的数组。

推荐：
```
function concatenateAll(...args) {
  return args.join('');
}
```

不推荐：
```
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}
```

* 使用默认值语法设置函数参数的默认值。

推荐：
```
function doSomething(opts = {}) {
  ...
}
```

不推荐：
```
function doSomething(opts) {
  opts = opts || {};
}
```

* 尽量使用Class，取代需要prototype的操作。因为Class的写法更简洁，更易于理解。

推荐：
```
class Queue {
  constructor(contents = []) {
    this._queue = [...contents];
  }
  pop() {
    const value = this._queue[0];
    this._queue.splice(0, 1);
    return value;
  }
}
```

不推荐：
```
function Queue(contents = []) {
  this._queue = [...contents];
}
Queue.prototype.pop = function() {
  const value = this._queue[0];
  this._queue.splice(0, 1);
  return value;
}
```

* 使用extends实现继承。

* 使用import取代require。

推荐：
```
import { func1, func2 } from 'moduleA';
```

不推荐：
```
const moduleA = require('moduleA');
const func1 = moduleA.func1;
const func2 = moduleA.func2;
```

* 使用export取代module.exports。

推荐：
```
import React from 'react';

class Breadcrumbs extends React.Component {
  render() {
    return <nav />;
  }
};

export default Breadcrumbs;
```

不推荐：
```
// 这是commonJS的写法
var React = require('react');

var Breadcrumbs = React.createClass({
  render() {
    return <nav />;
  }
});

module.exports = Breadcrumbs;
```

* 如果模块默认输出一个函数，函数名的首字母应该小写。如果模块默认输出一个对象，对象名的首字母应该大写。

推荐：
```
function makeStyleGuide() {
}

export default makeStyleGuide;
```

推荐：
```
const StyleGuide = {
  es6: {
  }
};

export default StyleGuide;
```

最后，推荐使用eslint对es6的代码风格进行自动化检查。用来保证写出语法正确、风格统一的代码。