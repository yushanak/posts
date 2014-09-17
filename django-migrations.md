Date: 2014-09-03
Title: Django1.7 新增 Migrations 功能
Category: Python 
Tags: Django,Python
Slug: django-migrantions
Authors: Shan


*本文是学习Django文档的一个概要，详细内容请阅读 [Django文档原文](https://docs.djangoproject.com/en/1.7/topics/migrations/)*

Django 1.7主要改进内容：

* 一个新的内置数据库迁移系统
* Django 应用的一个重构概念
* 改进了 Field API 模块，支持迁移，未来将会启用简单的组合键，支持 Django's ORM
* 改进了可定制的 Manager 和 QuerySet 类
* 一个可扩展的系统检测框架

更多内容请看发行说明。
***
## 简介
在Django 1.7 以前，Django 只支持添加新模型到数据库。syncdb命令（migrate命令的前身）不提供删除或更改现有的数据库结构的功能。

从 Django 1.7 开始，Django 将提供一种在你修改你的数据库结构（添加字段或删除表等）后进行数据库迁移的方法，它们大多设计成自动运行，但是你需要知道该什么时候迁移,在什么时候运行它们,以及运行中你可能遇到的常见问题。

## 工具
下面提供的数据库迁移方面的几个命令：

* migrate，负责应用迁移，执行迁移动作，更新数据库。
* makemigrations，负责在你修改的数据模型的基础上构建新的迁移，也就是说将你的更改单独打包到迁移文件。类似于提交的动作。
* sqlmigrae，负责打印出迁移的SQL语句

**注意：** 迁移是基于每一个应用级别进行的。并且有些应用是不能迁移的。你可以将它类比于一个版本控制系统（GIT）。

## 支持的数据库后台：

### PostgreSQL
PostgreSQL是所有支持的数据库中最容易迁移的，唯一的提示是使用默认值添加一个列将会导致整个表的重写，耗费的时间将与它的大小成正比。建议你添加新列时将列的 null=true 打开这样将加快迁移的速度。
### MySQL
MySql缺乏支持变更的操作，这意味着如果迁移失败，你将需要手工执行回滚以便再次尝试。此外，无论是添加或删除列，Mysql几乎会重新整个表，这在一些低档硬件平台将会导致长时间的数据库锁定。
### SQLite
SQLite 很少的变更支持，所以django通过以下方式实现：
* 使用新数据结构建立一张新表
* 拷贝数据到新表
* 删除旧表
* 将新表改回到原来的名字

这种方式效果还不错，但是执行很慢而且偶尔还会出错。不建议您在生产环境中运行和迁移SQLite,除非你非常了解风险和其局限性。这个一般是使用在开发环境。
## 工作流
迁移工具的使用很简单，更改你的数据模型后，使用 **makemigrations** 命令：

	$ python manage.py makemigrations
	Migrations for 'books':
  		0003_auto.py:
    		- Alter field author on book

在此过程中，将会扫描你的模型比较前后的变化，新建一组迁移文件，你需要仔细检查自动产生的迁移是否是你预期的结果，特别是在发生复杂的数据模型变动之后。

一旦你的迁移文件建成之后，你需要将结构改变应用到你的数据库中，确保是你预期的结果：

	$ python manage.py migrate
	Operations to perform:
  		Synchronize unmigrated apps: sessions, admin, messages, auth, staticfiles, contenttypes
 	 	Apply all migrations: books
	Synchronizing apps without migrations:
  		Creating tables...
  		Installing custom SQL...
 		Installing indexes...
	Installed 0 object(s) from 0 fixture(s)
	Running migrations:
  		Applying books.0003_auto... OK

## 依赖

## 迁移文件