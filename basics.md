Date: 2011-09-18
Title: Markdown 一分钟快速入门
Category:Tools
Tags: markdown
Slug: markdown-quickly-start
Authors:Shan

**声明：** 本文来源于对[Markdown官方](http://daringfireball.net/projects/markdown/)文档学习过程中的总结，在此记录，是为了方便自己快速查阅，同时也希望提供markdown初学者快速起步的便利。

## 概述
 * 哲学
 * 行内 HTML
 * 特殊字符自动转换

Markdown 是一套书写 *标记* 规则，目标是为了快速书写用于网络发表的文档。标记语法来源于电子邮件，非常接近纯文本，所以便于阅读。发布时需要 Markdown 转换工具将文档转换为 Html 或者其他格式。

Markdown 区别于 Html 的是：markdown 偏向于写作而 html 偏向于发布，所以markdown的源文件很好阅读，但表现力者弱于html。


***
## 语法

* 块元素
    * 段落和换行
    * 标题
    * 区块引言
    * 列表
    * 程序代码区块
    * 分隔线

* 段元素
    * 链接
    * 强调
    * 程序代码
    * 图片
	
* 其它
    * 转义字符
    * 自动链接

### 段落

**加入一个空行：**一段连续的文字构成一个段落，段落与段落之间的划分是通过 *在段落间加入一个空行* 。

**句尾加两个空格再回车：**一个段落中间 markdown 是不会在句尾回车后自动断行，要想强制断行就需要 *在句尾加两个空格再回车* 。



### 列表

无序列表使用星号 `*`、加号 `+` 和减号 `-` 来做为列表的项目标记，这些符号是都可以使用的，使用星号：

	* Candy.
	* Gum.
	* Booze.

加号：

	+ Candy.
	+ Gum.
	+ Booze.

和减号

	- Candy.
	- Gum.
	- Booze.

都会输出 HTML 为：

	<ul>
	<li>Candy.</li>
	<li>Gum.</li>
	<li>Booze.</li>
	</ul>

有序的列表则是使用一般的数字接着一个英文句点作为项目标记，这个数字是多少不会影响实际html输出效果。比如你可以按1、2、3排也可以3、2、1甚至1、1、1输出结果都是一样：

	1. Red
	2. Green
	3. Blue

输出 HTML 为：

	<ol>
	<li>Red</li>
	<li>Green</li>
	<li>Blue</li>
	</ol>

如果你在项目之间插入空行，那项目的内容会用 `<p>` 包起来，你也可以在一个项目内放上多个段落，只要在它前面缩排 4 个空白或 1 个 tab 。

	* A list item.
	
		With multiple paragraphs.

	* Another item in the list.

输出 HTML 为：

	<ul>
	<li><p>A list item.</p>
	<p>With multiple paragraphs.</p></li>
	<li><p>Another item in the list.</p></li>
	</ul>

### 链接

Markdown 支援两种形式的链接语法： *行内* 和 *参考* 两种形式，两种都是使用角括号来把文字转成连结。

行内形式是直接在后面用括号直接接上链接：

	This is an [example link](http://example.com/).

输出 HTML 为：

	<p>This is an <a href="http://example.com/">
	example link</a>.</p>

你也可以选择性的加上 title 属性：

	This is an [example link](http://example.com/ "With a Title").

输出 HTML 为：

	<p>This is an <a href="http://example.com/" title="With a Title">
	example link</a>.</p>

参考形式的链接让你可以为链接定一个名称，之后你可以在文件的其他地方定义该链接的内容：

	I get 10 times more traffic from [Google][1] than from
	[Yahoo][2] or [MSN][3].
	
	[1]: http://google.com/ "Google"
	[2]: http://search.yahoo.com/ "Yahoo Search"
	[3]: http://search.msn.com/ "MSN Search"

输出 HTML 为：

	<p>I get 10 times more traffic from <a href="http://google.com/"
	title="Google">Google</a> than from <a href="http://search.yahoo.com/"
	title="Yahoo Search">Yahoo</a> or <a href="http://search.msn.com/"
	title="MSN Search">MSN</a>.</p>

title 属性是选择性的，链接名称可以用字母、数字和空格，但是不分大小写：

	I start my morning with a cup of coffee and
	[The New York Times][NY Times].

	[ny times]: http://www.nytimes.com/

输出 HTML 为：

	<p>I start my morning with a cup of coffee and<a href="http://www.nytimes.com/">The New York Times</a>.</p>


### 图片 ###

图片的语法和链接很像。

行内形式（title 是选择性的）：

	![alt text](/path/to/img.jpg "Title")

参考形式：

	![alt text][id]

	[id]: /path/to/img.jpg "Title"

上面两种方法都会输出 HTML 为：

	<img src="/path/to/img.jpg" alt="alt text" title="Title" />

### 代码 ###
在一般的段落文字中，你可以使用反引号 `` ` `` 来标记代码区段，区段内的 `&`、`<` 和 `>` 都会被自动的转换成 HTML 实体，这项特性让你可以很容易的在代码区段内插入 HTML 码：

	I strongly recommend against using any `<blink>` tags.

	I wish SmartyPants used named entities like `&mdash;`
	instead of decimal-encoded entites like `&#8212;`.

输出 HTML 为：

	<p>I strongly recommend against using any
	<code>&lt;blink&gt;</code> tags.</p>
	<p>I wish SmartyPants used named entities like
	<code>&amp;mdash;</code> instead of decimal-encoded
	entites like <code>&amp;#8212;</code>.</p>

如果要建立一个已经格式化好的代码区块，只要每行都缩进 4 个空格或是一个 tab 就可以了，而 `&`、`<` 和 `>` 也一样会自动转成 HTML 实体。

Markdown 语法:

	If you want your page to validate under XHTML 1.0 Strict,
	you've got to put paragraph tags in your blockquotes:

	<blockquote>
	<p>For example.</p>
	</blockquote>

输出 HTML 为：

	<p>If you want your page to validate under XHTML 1.0 Strict,
	you've got to put paragraph tags in your blockquotes:</p>
	<pre><code>&lt;blockquote&gt;
	&lt;p&gt;For example.&lt;/p&gt;
	&lt;/blockquote&gt;
	</code></pre>

