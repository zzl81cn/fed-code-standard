为了规范前端团队的开发模式，提高代码质量及协作效率，优化前端性能及用户体验，特制定该前端技术规范文档，其中包括了前端技术栈，HTML，JavaScript，CSS/LESS/SCSS等几个部分。供前端同事参考及开发践行。

---

### CSS-LESS-SCSS规范

1. #### 代码风格

* 使用2个空格作为一个缩进层级，不要使用tab字符。
* 选择器与 { 之间，必须包含一个空格。

推荐：
```
.selector {
  ...
}
```

* 属性名与之后的 : 之间不允许包含空格， : 与 属性值 之间必须包含空格。

推荐：
```
margin: 0;
```

* 列表型属性值书写在单行时，,后必须跟一个空格。

推荐：
```
font-family: Arial, sans-serif;
```

* 当一个规则包含多个 selector 时，每个选择器声明必须独占一行。

推荐：
```
.post,
.page,
.comment {
  line-height: 1.5;
}
```

不推荐：
```
.post, .page, .comment {
  line-height: 1.5;
}
```

* >、+、~ 选择器的两边各保留一个空格。

推荐：
```
main > nav {
  padding: 10px;
}

label + input {
  margin-left: 5px;
}

input:checked ~ button {
  background-color: #69C;
}
```

不推荐：
```
main>nav {
  padding: 10px;
}

label+input {
  margin-left: 5px;
}

input:checked~button {
  background-color: #69C;
}
```

* 属性选择器中的值必须用双引号包围。

推荐：
```
article[character="juliet"] {
  voice-family: "Vivien Leigh", victoria, female
}
```

不推荐：
```
article[character='juliet'] {
  voice-family: "Vivien Leigh", victoria, female
}
```

* 属性的定义必须另起一行。

推荐：
```
.selector {
  margin: 0;
  padding: 0;
}
```

不推荐：
```
.selector { margin: 0; padding: 0; }
```

* 属性定义后必须以分号结尾。

推荐：
```
.selector {
  margin: 0;
}
```

不推荐：
```
.selector {
  margin: 0
}
```

2. #### 通用

* 如无必要，不得为 id、class 选择器添加类型选择器进行限定。

推荐：
```
#error,
.danger-message {
  font-color: #c00;
}
```

不推荐：
```
dialog#error,
p.danger-message {
  font-color: #c00;
}
```

* 选择器的嵌套层级应不大于 3 级，位置靠后的限定条件应尽可能精确。

推荐：
```
#username input {
  ...
}
.comment .avatar {
  ...
}
```

不推荐：
```
.page .header .login #username input {
  ...
}
.comment div * {
  ...
}
```

* 在可以使用缩写的情况下，尽量使用属性缩写。

推荐：
```
.post {
  font: 12px/1.5 arial, sans-serif;
}
```

不推荐：
```
.post {
  font-family: arial, sans-serif;
  font-size: 12px;
  line-height: 1.5;
}
```

3. #### 数值

* 当数值为 0 - 1 之间的小数时，省略整数部分的 0。

推荐：
```
panel {
  opacity: .8
}

```

不推荐：
```
panel {
  opacity: 0.8
}
```

4. #### url
* url() 函数中的路径不加引号。

推荐：
```
body {
  background: url(bg.png);
}
```

* url() 函数中的绝对路径省去协议名。

推荐：
```
body {
  background: url(//baidu.com/img/bg.png) no-repeat 0 0;
}
```

5. #### 长度单位
* 长度为 0 时须省略单位。 (也只有长度单位可省)

推荐：
```
body {
  padding: 0 5px;
}
```

不推荐：
```
body {
  padding: 0px 5px;
}
```

6. #### 颜色
* RGB颜色值必须使用十六进制记号形式 #rrggbb。不允许使用 rgb()。

推荐：
```
.success {
  box-shadow: 0 0 2px rgba(0, 128, 0, .3);
  border-color: #008000;
}
```

不推荐：
```
.success {
  box-shadow: 0 0 2px rgba(0,128,0,0.3);
  border-color: rgb(0, 128, 0);
}
```

* 颜色值可以缩写时，必须使用缩写形式。

推荐：
```
.success {
  background-color: #aca;
}
```

不推荐：
```
.success {
  background-color: #aaccaa;
}
```

* 颜色值不允许使用命名色值。

推荐：
```
.success {
  color: #90ee90;
}
```

不推荐：
```
.success {
  color: lightgreen;
}
```

7. #### 字体

* font-family 属性中的字体名称应使用字体的英文 family name。
推荐：
```
h1 {
  font-family: "Microsoft YaHei";
}
```

不推荐：
```
h1 {
  font-family: "微软雅黑";
}
```

* font-family 按：西文字体在前，中文字体在后；效果佳 (质量高/更能满足需求) 的字体在前，效果一般的字体在后的顺序编写，最后必须指定一个通用字体族(serif/sans-serif)。

推荐：
```
h1 {
  font-family: "Helvetica Neue", Arial, "Hiragino Sans GB", "WenQuanYi Micro Hei", "Microsoft YaHei", sans-serif;
}
```

8. #### 字号

* 需要在 Windows 平台显示的中文内容，其字号应不小于12px。

9. #### 响应式

* media query 不得单独编排，必须与相关的规则一起定义。

推荐：
```
@media (...) {
  /* header styles */
}

@media (...) {
  /* main styles */
}

@media (...) {
  /* footer styles */
}

```

不推荐：
```
@media (...) {
  /* header styles */
  /* main styles */
  /* footer styles */
}
```

* media query 如果有多个逗号分隔的条件时，应将每个条件放在单独一行中。

推荐：
```
@media
(-webkit-min-device-pixel-ratio: 2),
(min--moz-device-pixel-ratio: 2),
(min-resolution: 2dppx),
(min-resolution: 192dpi) {
  ...
}
```

10. #### 属性前缀

* 带私有前缀的属性由长到短排列，按冒号位置对齐。

推荐：
```
.box {
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
}
```

11. #### 样式重置
* 推荐使用 normalize.css，对浏览器默认的呈现规则进行重置处理。参考：
[github normalize.css](https://github.com/necolas/normalize.css "）")

12. #### 自动化（参考自动化规范说明）
* 推荐使用 autoprefixer 工具，对css代码进行浏览器前缀自动化处理。
* 推荐使用 csscomb 工具，对css代码进行格式处理。
* 推荐使用 cssmin 工具，对css代码进行合并压缩处理。