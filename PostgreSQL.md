# Win7 安装 PostgreSQL Postgis 记录
**软件说明：** postgresql-9.3.3-1-windows-binaries 自解压版本，没有选择 exe 安装版本；操作系统 win7 64位，postgis-pg93-setup-2.1.exe；

----

1. 下载 postgresql-9.3.3-1-windows-binaries 自解压版本
  
2. 首先解压postgresql：解压到你想要的安装目录，主要最好不要有中文或者空格，我的目录是

		e:\application;
	
3. 初始化数据库：开始-》dos窗口，cd到你的解压目录bin文件夹下，会自动创建postgres数据库，执行下面命令：

	    e:\Application\pgsql\bin>initdb.exe -D e:\Application\pgsql\data -E UTF8 --locale=C
	
	-D 设置数据文件目录，-E,数据库编码；
	
4. 启动数据库：两种方式，一是注册为windows服务，具体操作为：

			e:\Application\pgsql\bin>pg_ctl.exe register -D E:\Application\pgsql\data -Npgsql
			
	-N表示windows服务名称为pgsql；

		e:\Application\pgsql\bin>net start pgsql
	如果你的安装没有错误，现在就应该可以起来了。	
	二是直接启动，具体操作为：
	
		e:\Application\pgsql\bin>pg_ctl.exe start -w -D E:\Application\pgsql\data
5. 卸载服务：

    	e:\Application\pgsql\bin>pg_ctl.exe unregister -D d:\Application\pgsql\data -Npgsql
		
6. 创建数据库：

        e:\Application\pgsql\bin>createdb.exe -E UTF8 testdb
7. 创建用户：

        e:\Application\pgsql\bin>createuser.exe postgre
会有是否创建superuser的选项，创建一个名为postgre的超级用户；
8. 修改用户密码：

        e:\Application\pgsql\bin>psql.exe postgres
		
		psql (8.4.2)
		Type "help" for help.
		postgres=# alter user postgre with password 'postgre'
		postgres-#
第二种方式为使用pgAdmin修改，具体就不演示了，用pgAdmin连接到服务器，可以直接修改密码；
9. 安装postgis：
双击安装文件，选择postgre的安装目录，这个地方我搞错了，一开始以为是postgis的安装目录，其实不是，是选择postgre的目录，也就是你解压的目录才对，填写超级用户名称和密码，一路next下去，安装成功。


Title: Win7 安装 PostgreSQL Postgis 记录
Date: 2014-03-07 22:30
Modified: 2014-03-08 22:30
Category: Database
Tags: postgresql
Slug: postgresql-windows
Authors: Shan