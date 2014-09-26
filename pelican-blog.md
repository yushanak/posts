Title: 博客正式在 GitHub 安家
Category:Tools
Tags: pelican,python,github
Slug: pelican-blog
Authors:Shan
Date: 2014-08-17


###醒悟
* * *
###Geek是什么
Geek更多的是一种精神，一种态度，一种对技术的理解与信念。他们无法忍受丑陋的代码，拙劣的技术。他们思路开阔，技术娴熟，他们不甘平庸，追求完美。他们不会囿于常识，他们敢于突破。在常人眼中，他们不走寻常路，享受各种非主流的技术。但在他们自己眼中，这些又是那么得自然与优美。他们用自己的行为诠释着自己对于技术的理解，用那份固执传达着自己的信念。

他们掌握并热爱着技术，叛逆、执着，崇尚自由。

###为什么不选择CSDN、Wordpress、Jekyll等技术
CSDN上发表博文虽然方便，但没有归属感，自己的博客还是应该自己做主。

Wordpress上手容易、功能强大、插件丰富。但是在我看来，这些优点同时也是它的缺点：太笨重、太无脑、不够酷、无用功能太多、可定制的粒度不够小。我更喜欢简洁快速粗暴的博客系统。

Jekyll非常棒，可惜它基于Ruby。对于Python爱好者而言，基于Python的Pelican显然更加可口。

###探寻
* * *
我在搭建这个博客的过程中学到了很多很多有意思的技术。

搭建环境为 Linux，Windows下可能会麻烦一些。

搭建过程中会涉及到的技术名词如下：

* Linux
* Python
* Pip
* Pelican
* Jinja2
* Github 
* Git
* Makefile
* Markdown
* Mou
* Google Analytics
* Google Custom Search
* Google Webmasters
* Picasa
* Disqus
* Rss
* Sitemap
* Godaddy
* Dnspod
* A记录

若对任何一个技术名词有疑问，请翻墙[Google](https://www.google.com/ncr) it.

###初见
* * *
开始动手。
###Github入门指南
There are two types of GitHub Pages: Project Pages and User Pages. GitHub Pages 提供一种简洁高效的发布Pelican页面的方法。两者都支持Pelican页面发布。
请参考<http://blog.csdn.net/duxinfeng2010/article/details/8654690>

###使用Github Pages创建个人博客
Github为每一个用户分配了一个二级域名username.github.io，用户为自己的二级域名创建主页很简单，只需要在Github下创建一个名为username.github.io的版本库，并向其master分支提交网站静态页面即可。

* 登陆Github，创建一个名为username.github.io的版本库（将username替换成自己的Github账户名）。
* 点击Setting，选择一个自己喜欢的模板，最后点击发布public按钮。
* 耐心等待一段时间（不超过10分钟），登陆http://username.github.io，会发现自己的个人博客已经生成。

###安装Pelican、Markdown、ghp-import 
    pip install pelican
    pip install markdown
    pip install ghp-import 

**注意：**ghp-import在python2下工作正常，但在python3x下不能工作

###搭建骨架
    mkdir blog
    cd blog
    pelican-quickstart

根据提示一步步输入相应的配置项，不知道如何设置的接受默认即可，后续可以通过编辑pelicanconf.py文件更改配置)

以下是生成的目录结构：
    
    blog/
    ├── content              # 存放输入的源文件
    │   └── (pages)          # 存放手工创建的静态页面
    ├── output               # 生成的输出文件
    ├── develop_server.sh    # 方便开启测试服务器
    ├── Makefile             # 方便管理博客的Makefile
    ├── pelicanconf.py       # 主配置文件
    └── publishconf.py       # 主发布文件，可删除

把自己刚刚建好的username.github.io版本库clone下来：
    
    git init
    git remote add origin git@github.com:username/username.github.io.git
    git pull origin
    
###开始写博文
在content目录下用Markdown语法来写一篇文章，最好选择专业的Markdown编辑器，喜欢哪一种请Google。

写完后，执行以下命令，即可在本机<http://127.0.0.1:8000>看到效果。

    make html
    make serve

若要一键上传到Github，执行 `make github` 就可以一键部署：
    


###添翼
* * *
我们已经能成功地用markdown写出博文并部署到github了，但这远远不够。

###管理图片
我觉得使用云相册比本地图片要方便的多，我使用[Picasa](https://picasaweb.google.com?noredirect=1)来维护blog的所有图片。[微博相册](http://photo.163.com/)也是一个不错的选择。

###挑选主题
安装主题，比如 pelican-bootstrap3：

    git clone https://github.com/getpelican/pelican-themes.git
    cd pelican-themes
    pelican-themes -i  pelican-bootstrap3

选择主题，在pelicanconf.py中添加
    
    THEME = ' pelican-bootstrap3'

###安装第三方评论系统
在[Disqus](https://disqus.com/admin/signup)上申请一个站点，记牢Shortname。
在pelicanconf.py添加
    
    DISQUS_SITENAME = Shortname

 
###添加Google Analytics
去[Google Analytics](http://www.google.com/analytics)申请账号，记下跟踪ID。
在pelicanconf.py添加
    
    GOOGLE_ANALYTICS = 跟踪ID

Google Analytics极其强悍，截图说明一切：
![2](https://lh6.googleusercontent.com/-9vXmIT6vXDo/Ug5wTSu4wMI/AAAAAAAAALM/5-VSrnXNGUU/w958-h599-no/%25E5%25B1%258F%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-08-17+%25E4%25B8%258A%25E5%258D%25882.31.26.png)

![3](https://lh6.googleusercontent.com/-a4ZAnTD7F0I/Ug5wTX0w9nI/AAAAAAAAALI/x9J0atK3lpU/w958-h599-no/%25E5%25B1%258F%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-08-17+%25E4%25B8%258A%25E5%258D%25882.31.54.png)

###使用Google Webmasters
在[Google Webmasters](http://www.google.com/webmasters)上注册即可。

这个就是Google站长工具，使用它的目的是为了让博客被Google更好的收录，比如手动让Googlebot抓取、提交Robots、更新Sitemap等等，各方面完爆百度站长工具。

截图如下：
![3](https://lh3.googleusercontent.com/-tYrEbXyx_5o/UhGS1C_lcYI/AAAAAAAAALk/H7X7MBjNkVY/w958-h599-no/%25E5%25B1%258F%25E5%25B9%2595%25E5%25BF%25AB%25E7%2585%25A7+2013-08-19+%25E4%25B8%258A%25E5%258D%258811.36.32.png)

###添加插件
    git clone git://github.com/getpelican/pelican-plugins.git
比如我要使用sitemap，在pelicanconf.py里配置如下
    
    PLUGIN_PATH = u"pelican-plugins"
    PLUGINS = ["sitemap"]
    SITEMAP = {
        "format": "xml",
        "priorities": {
            "articles": 0.7,
            "indexes": 0.5,
            "pages": 0.3,
        },
        "changefreqs": {
            "articles": "monthly",
            "indexes": "daily",
            "pages": "monthly",
        }
    }

###使用Google站内搜索
请参考<http://www.codenut.net/post/2013-06-30-cse>

###申请独立域名
* 在[Godaddy](https://www.godaddy.com)上用支付宝花购买为期一年的顶级域名，并去修改Nameservers为这两个地址：f1g1ns1.dnspod.net、f1g1ns2.dnspod.net。
* 在[Dnspod](https://www.dnspod.cn)上添加新域名，并申请一条A记录指向Github Pages的ip:207.97.227.245；
* 在Pelican主目录新建CNAME文件，添上刚刚申请的域名，如我的www.lizherui.com

###登峰
* * *
最后，如果感觉还不够味儿，可以参考Pelican官方文档、研究源代码和设计自己的博客主题。

Pelican : <http://docs.getpelican.com/en/3.4>

###makefile 进阶
熟悉几个参数：

* make html 这个是生成你的静态博客站点，你可以在本地预览你的静态博客。它使用 pelicanconf.py 配置文件来生成站点。
* make publish 这个是生成准备发布的静态博客站点，会加入你网站的 URL。它使用 publishconf.py 配置文件来生成站点。
* make serve 建立一个开发服务器提供本地的预览，在windows环境使用 Python3X 的，要注意makefile文件开头的 PY?=python3 的设置，将它改过来：PY?=python 否则会报错。因为windows环境没有 python3 这个命令。
* [ghp-import](https://github.com/davisp/ghp-import) 工具：使用 pip 安装。Pelican默认使用这个工具，它可以帮助你简化更新 GitHub Page。
* make regenerate 它可以自动实时更新你的文章输出。使用时，它在后台监控你的 input 文件夹，你修改完并文章保存后，它自动重新生成你的博客到输出目录。这样你就不需要每次改完文章后再去手动输入命令生成。