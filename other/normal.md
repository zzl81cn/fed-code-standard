为了规范前端团队的开发模式，提高代码质量及协作效率，优化前端性能及用户体验，特制定该前端技术规范文档，其中包括了前端技术栈，HTML，JavaScript，CSS/LESS/SCSS等几个部分。供前端同事参考及开发践行。

---

### 一般规范

以下列举了一些可应用在 HTML，JavaScript 和 CSS/LESS/SCSS 上的通用规则。

1. #### 文件和资源命名

* 在前端项目中，所有的文件名应该遵循统一命名约定。以可读性而言，减号（-）是用来分隔文件名的不二之选。同时它也是常见的 URL 分隔符，如：
```
example.com/my-blog-entry 
img.example.com/big-black-background.jpg
```
所以，请使用减号用来分隔资源名称。

* 请确保文件命名总是以字母开头而不是数字。

* 资源的字母名称必须全为小写。这是因为在某些对大小写字母敏感的操作系统中，当文件通过工具压缩混淆后，或者人为修改过后，大小写不同而导致引用文件不同的错误，很难被发现。

* 在某些情况下，需要对资源文件增加后缀或特定的扩展名（比如 .min.js, .min.css）。这种情况下，建议使用点分隔符来进行处理。

不推荐：
```
MyScript.js 
myCamelCaseName.css
i_love_react.html
1001-scripts.js
my-file-min.css
```

推荐：
```
my-script.js
my-camel-case-name.css
i-love-react.html
thousand-and-one-scripts.js
my-file.min.css
```

2. #### 协议
不要指定引入资源所带的具体协议。

当引入图片或其他媒体文件，或者样式和脚本时，url 所指向的具体路径，不要指定协议部分（http:，https:），除非这两者协议都不可用。

不指定协议使得 URL 从绝对的获取路径转变为相对的，在请求资源协议无法确定时非常好用，而且还能为文件大小节省几个字节。

不推荐：
```
<script src="http://apps.bdimg.com/libs/accounting.js/0.3.2/accounting.min.js"></script>
```

推荐：
```
<script src="//apps.bdimg.com/libs/accounting.js/0.3.2/accounting.min.js"></script>
```

不推荐：
```
.example {
  background: url(http://static.example.com/images/bg.jpg);
}
```

推荐：
```
.example {
  background: url(//static.example.com/images/bg.jpg);
}
```

3. #### 缩进

由于广为人知的兼容性，请避免使用tab进行代码缩进。推荐使用空格进行缩进，一次缩进两个空格。

推荐：
```
<ul>
  <li>Fantastic</li>
  <li>Great</li>
  <li>
    <a href="#">Test</a>
  </li>
</ul>
```

```
@media screen and (min-width: 1100px) {
  body {
    font-size: 100%;
  }
}
```

```
(function(){
  var x = 10;
  function y(a, b) {
    return {
      result: (a + b) * x
    }
  }
}());
```

4. #### 注释

编写自解释代码只是一个传说，没有任何代码是可以完全自解释的。而代码注释，则是永远也不嫌多。

注释的目的，不是描述你的代码都干了些什么，而是你的代码为什么要这么写，以及背后的考量是什么。当然，也可以加入所思考问题或是解决方案的链接地址。

不推荐：
```
var offset = 0;
if(includeLabels) {
  // 添加20px的偏移量。这是废话
  offset = 20;
}
```

推荐：
```
var offset = 0;
if(includeLabels) {
  //如果内部包含了label标签，我们需要设置最小20px的偏移量。
  //参考以下bug链接: http://somebrowservendor.com/issue-tracker/ISSUE-1
  offset = 20;
}
```

5. #### 文件备注

每个文件的头部，建议用备注的方式，说明以下信息：版权、作者、创建时间、功能简介等。

推荐：
```
/**
 * Copyright (c) 2015-present, Brc, Inc.
 * All rights reserved.
 *
 * Author: Togayther
 * Date  : 2017-08-14 12:31:56
 * Descr : 这里是一些简单的功能描述文字
 */
```

6. #### 代码检查
这里的代码检查，主要针对JavaScript。由于JavaScript是一种相对宽松和自由的编程语言，因此严格遵循编码规范和格式化风格指南就显得极为重要。建议使用 JSLint 或 JSHint 自动化工具，确保JavaScript编程风格的统一。