# HTML
<h4 align=right>by 1x0</h4>

## 简述：什么是html
- **H**yper**t**ext **M**arkup **L**anguage（超文本标记语言）
- 不是编程语言（不做逻辑处理）
- 告诉浏览器怎么构造网页

[浙大轻首页](zjuers.com)
## html元素
标准的html文件由html元素组成
格式为 开始标签-内容-结束标签
```html
<p>我要女装</p>
```
## html格式
```html
<!DOCTYPE html>
<!--解释一下这是一个h5文档-->
<html>
    <head>
        <meta charset="UTF-8">
        <title>浙江大学求是潮</title>
    </head>
    <!--head部分放一些不渲染在网页页面的东西，比如标题-->
    <body>
        <h1>谁要女装</h1>
        <p>我是不灵</p>
        <p>我是仙人掌</p>
    </body>
    <!--body部分放渲染在页面上的内容-->
</html>
```
## html元素
### 块级元素
- 在页面以块的形式呈现
- 占父元素全部宽度
#### `<h1>`-`<h6>`
`<h1>`,`<h2>`,...,`<h6>` 
heading 标题元素，分为六级
#### `<p>`
paragraph 段落元素
#### `<div>`
Division 内容划分元素
`<div>` HTML元素是通用容器。它对内容或布局没有影响。
（可以理解为一个盒子）
#### `<ul>`、`<ol>`和`<li>`
```html
<ul>
    <li>我是不灵</li>
    <li>我是1x0</li>
    <li>我是Qwant</li>
    <li>我是仙人掌</li>
</ul>
```
`<ul>`是无序列表，`<ol>`是有序列表，`<li>`是list item，列表中的元素
#### 其他
表格`<table>`
### 内联元素
- 通常在块级元素内
- 只占父元素部分宽度
#### `<a>`
`<a>` 元素可以通过它的 href 属性创建通向其他网页、文件、同一页面内的位置或任何其他 URL 的超链接。
```html
<div>以下是
<a href="https://zjuers.com" target="_blank">zjuers轻首页</a>
的链接
</div>
```
这里的href被称为html元素的属性，写在起始tag上。属性之间以空格隔开
#### `<img>`
```html
<img src="./img/atri.jpg" alt="atri">
```
`src`属性代表图片的位置。可以是url（网址）也可以是本地路径
##### 绝对路径和相对路径
在URL中，斜杠是标准的路径分隔符。Web浏览器期望在URL中看到斜杠。
绝对路径：`"H:/desktop/Atri Studio Code.exe"`
相对路径：`"./Atri Studio Code.exe"`
`./`表示该文件所在的目录下
`../`表示上一级文件夹下
`../../`表示上上一级文件夹下
以此类推
#### 其他
输入`<input>`、交互控件`<form>`
