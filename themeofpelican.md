Title: How to create themes for Pelican
Date: 2014-03-07 10:30
Modified: 2014-03-07 10:30
Category: Tools
Tags: pelican
Slug: create-themes-for-Pelican
Authors: Shan


pelican使用jinja2模板引擎来提供博客主题的渲染和输出html，jinja2 的语法很简单。如果你想创建自己的主题模板，先从简单的默认主题获取灵感吧。

##项目结构
一个主题项目必须包括下面的目录结构：

        ├── static
        │   ├── css
        │   └── images
        └── templates
            ├── archives.html         // to display archives
            ├── period_archives.html  // to display time-period archives
            ├── article.html          // processed for each article
            ├── author.html           // processed for each author
            ├── authors.html          // must list all the authors
            ├── categories.html       // must list all the categories
            ├── category.html         // processed for each category
            ├── index.html            // the index. List all the articles
            ├── page.html             // processed for each page
            ├── tag.html              // processed for each tag
            └── tags.html             // must list all the tags. Can be a tag cloud.

static 是静态文件目录，目录里的文件将会被复制到 output 目录中的 theme 目录。
templates 目录包括所有用来生成输出的模板，上面列出的是必须有的模板，你可以添加你自己的模板来丰富你的主题。
##模板和变量
所有的模板都接收你在 settings 文件中定义的变量。你定义的变量必须全部采用大写，然后你就可以直接在模板中使用它们。
###通用变量
 变量|描述
 :---------------|:---------------
 output_file|渲染出来的 html 文件名
 articles|文章列表，按照时间降序排序，所有的元素都是 article 对象，所以你可以获取它的属性值（比如 Tag，Summary等等）
 dates|日期
 tags|(tag, articles)元组列表，包括所有的 tags
 categories|(category, articles)元组列表, 包括所有的分类和对应的文章 (值)
 pages|页面列表
 
###排序
###时间格式
Pelican 通过你的设置和本地时区来格式化时间格式（通过 DATE_FORMATS/DEFAULT_DATE_FORMAT 变量） 。并提供 locale_date 属性。 date 属性是一个 datetime 对象。 如果你需要自定义一个不同于你设置的格式，你可以使用 Jinja2 的过滤器 strftime ，它将正确地使用本地设置格式化时间。

    :::python
    {{ article.date|strftime('%d %B %Y') }}

###index.html
这是你的 blog 首页。生成为 output 目录的 index.html 文件。如果分页被设置，后续的页面将为 /index`n`.html。

变量|描述
:--------|:--------
articles_paginator|  A paginator object for the list of articles
articles_page|   The current page of articles
dates_paginator|     A paginator object for the article list, ordered by date, ascending.
dates_page|  The current page of articles, ordered by date, ascending.
page_name|   ‘index’ – useful for pagination links

###author.html

 变量|描述
 :--------|:--------
 author|  The name of the author being processed
 articles|    Articles by this author
 dates|   Articles by this author, but ordered by date, ascending
 articles_paginator|  A paginator object for the list of articles
 articles_page|   The current page of articles
 dates_paginator|     A paginator object for the article list, ordered by date, ascending.
 dates_page|  The current page of articles, ordered by date, ascending.
 page_name|   AUTHOR_URL where everything after {slug} is removed – useful for pagination links

###Feeds
feed 变量明确区分 ATOM 和 RSS 。ATOM 是默认。

    FEED_ATOM
    FEED_RSS
    FEED_ALL_ATOM
    FEED_ALL_RSS
    CATEGORY_FEED_ATOM
    CATEGORY_FEED_RSS
    TAG_FEED_ATOM
    TAG_FEED_RSS
    TRANSLATION_FEED_ATOM
    TRANSLATION_FEED_RSS


