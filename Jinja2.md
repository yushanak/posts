Title: Jinja2 简明教程（一）
Date: 2014-03-13 15:30
Modified: 2014-09-13 15:30
Category: Python
Tags: Jinjia2,Python
Slug: Jinjia2-how-to-1
Authors: Shan


Jinja2 简明教程（一），Jinjin2 通用模板语言，类似于 Django 的模板，但更加灵活和快速。Jinja2 需要至少 Python 2.4 版本来运行。

##Jinjia2 模板引擎中的语法和语义结构
模板仅仅是文本文件。它可以生成任何基于文本的格式（HTML、XML、CSV、LaTex 等等）。 它并没有特定的扩展名， .html 或 .xml 都可以。
模板包括：**变量**、 **表达式** 和 **tags**。语法灵感主要来自于 Django 和 Python 。{% %}用来执行语句， {{ }}用来返回一个变量的值。

###变量
变量是由你的 app 传递进模板来的。它可能有属性或者元素，这完全取决于你传递进来的是什么类型的变量。

