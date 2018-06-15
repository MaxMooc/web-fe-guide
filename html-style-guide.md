
# HTML编码规范

[1 前言]

[2 代码风格]

　　[2.1 缩进与换行]

　　[2.2 命名]

　　[2.3 标签]

　　[2.4 属性]

[3 通用]

　　[3.1 DOCTYPE]

　　[3.2 编码]

　　[3.3 CSS 和 JavaScript 引入]

[4 head]

　　[4.1 title]

　　[4.2 favicon]

　　[4.3 viewport]

[5 图片]

[6 表单]

　　[6.1 控件标题]

　　[6.2 按钮]

[7 多媒体]

[8 模板中的 HTML]


## 1 前言


HTML 作为描述网页结构的超文本标记语言。本文档的目标是使 HTML 代码风格保持一致，容易被理解和被维护。
本规范建议开发工具使用sublime


## 2 代码风格


### 2.1 缩进与换行


#### [强制] 使用 `4` 个空格做为一个缩进层级。

解释：
对于非 HTML 标签之间的缩进，比如 script 或 style 标签内容缩进，与 script 或 style 标签的缩进同级。

示例：

```html
<style>
/* 样式内容的第一级缩进与所属的 style 标签对齐 */
ul {
    padding: 0;
}
</style>
<ul>
    <li>first</li>
    <li>second</li>
</ul>
<script>
// 脚本代码的第一级缩进与所属的 script 标签对齐
require(['app'], function (app) {
    app.init();
});
</script>
```

### 2.2 命名


#### [强制] 请确保文件命名总是以字母开头而不是数字。

#### 代码文件命名的原则主要是名称需要表明文件对应的模块内容（重点）、对应的版本号和文件的格式等。

资源的字母名称必须全为小写，这是因为在某些对大小写字母敏感的操作系统中，当文件通过工具压缩混淆后，或者人为修改过后，大小写不同而导致引用文件不同的错误，很难被发现。

还有一些情况下，需要对文件增加前后缀或特定的扩展名（比如 .min.js, .min.css），抑或一串前缀（比如 3fa89b.main.min.css）。这种情况下，建议使用点分隔符来区分这些在文件名中带有清晰意义的元数据。

示例：
```
index.html（首页）
animation.css（动画样式）
my-camel-case-name.css
i-love-underscores.html
thousand-and-one-scripts.js
myfile.min.css     
```

#### [强制] `class` 必须单词全字母小写，单词间以 `-` 分隔。

#### [强制] `class` 必须代表相应模块或部件的内容或功能，不得以样式信息进行命名。

示例：

```html
<!-- good -->
<div class="sidebar"></div>

<!-- bad -->
<div class="left"></div>
```

#### [强制] 元素 `id` 必须保证页面唯一。

解释：

同一个页面中，不同的元素包含相同的 `id`，不符合 `id` 的属性含义。并且使用 `document.getElementById` 时可能导致难以追查的问题。


#### [建议] `id` 建议单词全字母小写，单词间以 `-` 分隔。同项目必须保持风格一致。


#### [建议] `id`、`class` 命名，在避免冲突并描述清楚的前提下尽可能短。

示例：

```html
<!-- good -->
<div id="nav"></div>
<!-- bad -->
<div id="navigation"></div>

<!-- good -->
<p class="comment"></p>
<!-- bad -->
<p class="com"></p>

<!-- good -->
<span class="author"></span>
<!-- bad -->
<span class="red"></span>
```

#### [强制] 同一页面，应避免使用相同的 `name` 与 `id`。

解释：

IE 浏览器会混淆元素的 `id` 和 `name` 属性， `document.getElementById` 可能获得不期望的元素。所以在对元素的 `id` 与 `name` 属性的命名需要非常小心。

一个比较好的实践是，为 `id` 和 `name` 使用不同的命名法。

示例：

```html
<input name="foo">
<div id="foo"></div>
<script>
// IE6 将显示 INPUT
alert(document.getElementById('foo').tagName);
</script>
````


### 2.3 标签


#### [强制] 标签名必须使用小写字母。

示例：

```html
<!-- good -->
<p>Hello StyleGuide!</p>

<!-- bad -->
<P>Hello StyleGuide!</P>
```

#### [强制]对 `HTML5` 中规定允许省略的闭合标签，不允许省略闭合标签。对于无需自闭合的标签，不允许自闭合。

解释：

常见无需自闭合标签有 `input`、`br`、`img`、`hr` 等。


示例：

```html
<!-- good -->
<input type="text" name="title">

<!-- bad -->
<input type="text" name="title" />
```
#### [建议] 标签使用必须符合标签嵌套规则。

解释：

比如 `div` 不得置于 `p` 中，`tbody` 必须置于 `table` 中。详情见


#### [建议] HTML 标签的使用应该遵循标签的语义。

解释：

下面是常见标签语义

- p - 段落
- h1,h2,h3,h4,h5,h6 - 层级标题
- strong,em - 强调
- ins - 插入
- del - 删除
- abbr - 缩写
- code - 代码标识
- cite - 引述来源作品的标题
- q - 引用
- blockquote - 一段或长篇引用
- ul - 无序列表
- ol - 有序列表
- dl,dt,dd - 定义列表


### 2.4 属性


#### [强制] 属性名必须使用小写字母。

示例：

```html
<!-- good -->
<table cellspacing="0">...</table>

<!-- bad -->
<table cellSpacing="0">...</table>
```


#### [强制] 属性值必须用双引号包围。

解释：

不允许使用单引号，不允许不使用引号。


示例：

```html
<!-- good -->
<script src="esl.js"></script>

<!-- bad -->
<script src='esl.js'></script>
<script src=esl.js></script>
```

#### [建议] 自定义属性建议以 `xxx-` 为前缀，推荐使用 `data-`。

解释：

使用前缀有助于区分自定义属性和标准定义的属性。


示例：

```html
<ol data-ui-type="Select"></ol>
```

## 3 通用


### 3.1 DOCTYPE


#### [强制] 使用 `HTML5` 的 `doctype` 来启用标准模式，建议使用大写的 `DOCTYPE`。

示例：

```html
<!DOCTYPE html>
```

#### [建议] 启用 IE Edge 模式。

示例：

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

#### [建议] 在 `html` 标签上设置正确的 `lang` 属性。

解释：

有助于提高页面的可访问性，如：让语音合成工具确定其所应该采用的发音，令翻译工具确定其翻译语言等。


示例：

```html
<html lang="zh-CN">
```


### 3.2 编码


#### [强制] 页面必须使用精简形式，明确指定字符编码。指定字符编码的    `meta` 必须是 `head` 的第一个直接子元素。


示例：

```html
<html>
    <head>
        <meta charset="UTF-8">
        ......
    </head>
    <body>
        ......
    </body>
</html>
```


### 3.3 CSS 和 JavaScript 引入


#### [强制] 引入 `CSS` 时必须指明 `rel="stylesheet"`。

示例：

```html
<link rel="stylesheet" href="page.css">
```

#### [建议] 展现定义放置于外部 `CSS` 中，行为定义放置于外部 `JavaScript` 中。

解释：

结构-样式-行为的代码分离，对于提高代码的可阅读性和维护性都有好处。


## 4 head


### 4.1 title


#### [强制] 页面必须包含 `title` 标签声明标题。

#### [强制] `title` 必须作为 `head` 的直接子元素，并紧随 `charset` 声明之后。

解释：

`title` 中如果包含 ASCII 之外的字符，浏览器需要知道字符编码类型才能进行解码，否则可能导致乱码。


示例：

```html
<head>
    <meta charset="UTF-8">
    <title>页面标题</title>
</head>
```

### 4.2 favicon


#### [强制] 保证 `favicon` 可访问。

解释：

在未指定 favicon 时，大多数浏览器会请求 Web Server 根目录下的 `favicon.ico` 。为了保证 favicon 可访问，避免 404，必须遵循以下两种方法之一：

1. 在 Web Server 根目录放置 `favicon.ico` 文件。
2. 使用 `link` 指定 favicon。


示例：

```html

<link href="/favicon.ico" rel="icon" type="image/x-icon" />（建议）
<link rel="shortcut icon" href="path/to/favicon.ico">
```

### 4.3 viewport


#### [建议] 若页面欲对移动设备友好，需指定页面的 `viewport`。

解释：

viewport meta tag 可以设置可视区域的宽度和初始缩放大小，避免在移动设备上出现页面展示不正常。

比如，在页面宽度小于 `980px` 时，若需 iOS 设备友好，应当设置 viewport 的 `width` 值来适应你的页面宽度。同时因为不同移动设备分辨率不同，在设置时，应当使用 `device-width` 和 `device-height` 变量。

另外，为了使 viewport 正常工作，在页面内容样式布局设计上也要做相应调整，如避免绝对定位等。可参考淘宝的flexible布局

## 5 图片


#### [强制] 图片最大不应超过200kb，超长图片拆分。

#### [强制] 禁止 `img` 的 `src` 取值为空。延迟加载的图片也要增加默认的 `src`。

解释：

`src` 取值为空，会导致部分浏览器重新加载一次当前页面。

#### [建议] 图片数量较多时可采用预加载和懒加载的方式优化用户体验和加载速度。

#### [建议] 添加 `width` 和 `height` 属性，以避免页面抖动。

#### [建议] 有下载需求的图片采用 `img` 标签实现，无下载需求的图片采用 CSS 背景图实现。

解释：

1. 产品 logo、用户头像、用户产生的图片等有潜在下载需求的图片，以 `img` 形式实现，能方便用户下载。
2. 无下载需求的图片，比如：icon、背景、代码使用的图片等，尽可能采用 CSS 背景图实现(css sprites)。



## 6 表单


### 6.1 控件标题


#### [强制] 有文本标题的控件必须使用 `label` 标签将其与其标题相关联。

解释：

有两种方式：

1. 将控件置于 `label` 内。
2. `label` 的 `for` 属性指向控件的 `id`。

推荐使用第一种，减少不必要的 `id`。如果 DOM 结构不允许直接嵌套，则应使用第二种。

示例：

```html
<label><input type="checkbox" name="confirm" value="on"> 我已确认上述条款</label>

<label for="username">用户名：</label> <input type="textbox" name="username" id="username">
```


### 6.2 按钮


#### [强制] 使用 `button` 元素时必须指明 `type` 属性值。

解释：

`button` 元素的默认 `type` 为 `submit`，如果被置于 `form` 元素中，点击后将导致表单提交。为显示区分其作用方便理解，必须给出 `type` 属性。


示例：

```html
<button type="submit">提交</button>
<button type="button">取消</button>
```

#### [建议] 尽量不要使用按钮类元素的 `name` 属性。

解释：

由于浏览器兼容性问题，使用按钮的 `name` 属性会带来许多难以发现的问题。


## 7 多媒体


#### [建议] 当在现代浏览器中使用 `audio` 以及 `video` 标签来播放音频、视频时，应当注意格式。

解释：

音频应尽可能覆盖到如下格式：

* MP3
* WAV
* Ogg

视频应尽可能覆盖到如下格式：

* MP4
* WebM
* Ogg

#### [建议] 在支持 `HTML5` 的浏览器中优先使用 `audio` 和 `video` 标签来定义音视频元素。

#### [建议] 使用退化到插件的方式来对多浏览器进行支持。

示例：

```html
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    <object width="100" height="50" data="audio.mp3">
        <embed width="100" height="50" src="audio.swf">
    </object>
</audio>

<video width="100" height="50" controls>
    <source src="video.mp4" type="video/mp4">
    <source src="video.ogg" type="video/ogg">
    <object width="100" height="50" data="video.mp4">
        <embed width="100" height="50" src="video.swf">
    </object>
</video>
```

#### [建议] 只在必要的时候开启音视频的自动播放。


#### [建议] 在 `object` 标签内部提供指示浏览器不支持该标签的说明。

示例：

```html
<object width="100" height="50" data="something.swf">DO NOT SUPPORT THIS TAG</object>
```



