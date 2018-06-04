为了规范前端团队的开发模式，提高代码质量及协作效率，优化前端性能及用户体验，特制定该前端技术规范文档，其中包括了前端技术栈，HTML，JavaScript，CSS/LESS/SCSS等几个部分。供前端同事参考及开发践行。

---

## HTML规范

1. ### 文档规范
推荐使用 HTML5 的文档类型申明： <!DOCTYPE html>。

2. ### 脚本加载
出于性能考虑，脚本异步加载很关键。一段脚本放置在 <head> 内，比如  
``` html
<head>
  ...
  <script src="main.js"></script>
</head>
```
其加载会一直阻塞DOM解析，直至它完全地加载和执行完毕。这会造成页面显示的延迟。

推荐：
``` html
<html>
  <head>
    <link rel="stylesheet" href="main.css">
  </head>
  <body>
    <!-- main content -->
 
    <script src="main.js" async></script>
  </body>
</html>
```

3. ### 语义化
应该根据当前的渲染场景，使用正确的html标签。比如用 heading 标签来定义头部标题，用p标签来定义文字段落，用a标签来定义链接锚点，等等。

有目的地使用html标签，对于页面的可访问性、代码重用、代码效率来说，有重大的意义。

不推荐：
``` html
<b>My page title</b>
<div class="top-navigation">
  <div class="nav-item"><a href="#home">Home</a></div>
  <div class="nav-item"><a href="#news">News</a></div>
  <div class="nav-item"><a href="#about">About</a></div>
</div>
 
<div class="news-page">
  <div class="page-section news">
    <div class="title">All news articles</div>
    <div class="news-article">
      <h2>Bad article</h2>
      <div class="intro">Introduction sub-title</div>
      <div class="content">This is a very bad example for HTML semantics</div>
      <div class="article-side-notes">I think I'm more on the side and should not receive the main credits</div>
      <div class="article-foot-notes">
        This article was created by David <div class="time">2014-01-01 00:00</div>
      </div>
    </div>
 
    <div class="section-footer">
      Related sections: Events, Public holidays
    </div>
  </div>
</div>
 
<div class="page-footer">
  Copyright 2014
</div>
```

推荐：
``` html
<header>
  <h1>My page title</h1>
</header>
 
<nav class="top-navigation">
  <ul>
    <li class="nav-item"><a href="#home">Home</a></li>
    <li class="nav-item"><a href="#news">News</a></li>
    <li class="nav-item"><a href="#about">About</a></li>
  </ul>
</nav>
 
<main class="news-page" role="main">
  <section class="page-section news">
    <header>
      <h2 class="title">All news articles</h2>
    </header>
 
    <article class="news-article">
      <header>
        <div class="article-title">Good article</div>
        <small class="intro">Introduction sub-title</small>
      </header>
 
      <div class="content">
        <p>This is a good example for HTML semantics</p>
      </div>
      <aside class="article-side-notes">
        <p>I think I'm more on the side and should not receive the main credits</p>
      </aside>
      <footer class="article-foot-notes">
        <p>This article was created by David <time datetime="2014-01-01 00:00" class="time">1 month ago</time></p>
      </footer>
    </article>
 
    <footer class="section-footer">
      <p>Related sections: Events, Public holidays</p>
    </footer>
  </section>
</main>
 
<footer class="page-footer">
  Copyright 2014
</footer>
```

4. ### 行为与表现分离

前端开发过程中，应严格的保证结构（HTML）、表现（CSS）、行为（JavaScript）三者分离，并尽量使三者之间没有太多的交互和联系。也就是说，尽量在文档和模板中只包含结构性的HTML，将所有控制表现的代码，移入到样式表中，将所有控制动作行为的代码，移入到脚本之中。

* 合并及压缩样式、脚本文件。
* 尽量避免使用行内样式（``` <style>.no-good {}</style> ```）
* 尽量避免在元素上使用 style 属性（``` <hr style="border-top: 5px solid black"> ```）
* 尽量避免使用行内脚本（``` <script>alert('no good')</script> ```）
* 不使用表象元素（如：``` <b>, <u>, <center>, <font>, <b> ``` 等）

不推荐：
``` html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="base.css">
  <link rel="stylesheet" href="grid.css">
  <link rel="stylesheet" href="type.css">
  <link rel="stylesheet" href="modules/teaser.css">
</head>
<body>
  <h1 style="font-size: 3rem"></h1>
  <b>I'm a subtitle and I'm bold!</b>
  <center>Dare you center me!</center>
  <script>
    alert('Just dont...');
  </script>
  <div class="red">I'm important!</div>
</body>
</html>
```

推荐：
``` html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="main.css">
</head>
<body>
  <h1 class="title"></h1>
  <div class="sub-title">I'm a subtitle and I'm bold!</div>
  <span class="comment">Dare you center me!</span>
  <div class="important">I'm important!</div>
  <script async src="main.js"></script>
</body>
</html>
```

5. ### type属性

根据 HTML5 规范，在引入css和JavaScript文件时一般不需要指定type属性，因为 text/css 和 text/javascript 分别是它们的默认值。

不推荐：
``` html
<link rel="stylesheet" href="main.css" type="text/css">
<script src="main.js" type="text/javascript"></script>
```

推荐：
``` html
<link rel="stylesheet" href="main.css">
<script src="main.js"></script>
```

6. ### 引号
使用双引号(“”) 而不是单引号(”) 。

不推荐：
``` html
<div class='news-article'></div>
```

推荐：
``` html
<div class="news-article"></div>
```

7. ### IE兼容模式
IE浏览器支持通过特定的 <meta> 标签来确定绘制当前页面所应该采用的IE 版本。除非有强烈的特殊需求，否则最好是设置为 edge mode，从而通知 IE 采用其所支持的最新的模式。

推荐：
``` html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

8. ### 字符编码
通过明确声明字符编码，能够确保浏览器快速并容易的判断页面内容的渲染方式。一般采用 UTF-8 编码。

推荐：
``` html
<head>
  <meta charset="UTF-8">
</head>
```

9. ### 布尔型属性
布尔型属性可以在声明时不赋值。

推荐：
``` html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

10. ### 减少标签的数量
编写 HTML 代码时，尽量避免多余的父元素。

不推荐：
``` html
<span class="avatar">
  <img src="...">
</span>
```

推荐：
``` html
<img class="avatar" src="...">
```

11. ### 标签正确嵌套
最应该恪守的一条规则是，块元素不能放在行内元素之中。

不推荐：
``` html
<a href="index.html">
  <h1>首页</h1>
</a>
```

推荐：
``` html
<h1>
  <a href="index.html">首页</a>
</h1>
```

备注：关于块元素与行内元素，可参考：
[html中行内元素有哪些？块级元素有哪些？](http://www.cnblogs.com/Jackie0714/p/4923639.html)

12. ### 空的资源引用

空的资源引用，包括常见的a标签的href=""，以及img标签的src=""。出现此类代码，浏览器解析的时候，实际上会默认加载当前页面，这对前端性能有不好的影响。编码时应极力避免出现此类空资源引用的代码。

13. ### 图片资源

* 一般情况下，png格式的图片的体积，相较jpg格式的图片的体积，都更大。所以，如若未应用到png格式的透明特性，都推荐使用jpg格式的图片。另外，由于png是一种可压缩的图像格式，正式应用时，可通过工具进行优化处理，推荐：[png压缩神器](http://www.tinypng.com/ "")

* 尽可能使用字体图标，替换传统的图像小图标。字体图标的大小、颜色，状态等，可通过css进行控制，其可定制化能力更强，相较传统的图像图标，其扩展、维护性也更高。后续会通过阿里的iconfont库，创建专门的字体图标仓库，供设计及前端开发人员使用。
