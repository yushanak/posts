Title:为手机和平板安装 Ubuntu Touch 
Category: Tools
Tags: Ubuntu,Linux
Slug: ubuntu-touch-dev
Authors: Shan
Date: 2014-09-24
Modified: 2014-09-28


## 支持的设备

目前开发所基于的设备如下：

* Nexus 4
* Nexus 7 2013 WiFi
* Nexus 10

Galaxy Nexus和Nexus 7 2012 将不会得到持续的支持，尽管可能会有社区版本。



## 准备好你的 Ubuntu 桌面系统
首先通过以下几步准备好你的桌面安装平台，这样才能识别你的设备，并且安装系统到你的设备。

* 确保你打开了 universe 软件源：

		deb http://us.archive.ubuntu.com/ubuntu/ saucy universe
		deb-src http://us.archive.ubuntu.com/ubuntu/ saucy universe
		deb http://us.archive.ubuntu.com/ubuntu/ saucy-updates universe
		deb-src http://us.archive.ubuntu.com/ubuntu/ saucy-updates universe

* 添加PPA：

		$ sudo add-apt-repository ppa:phablet-team/tools
		$ sudo apt-get update
	在12.04中，你还需要将 ubuntu SDK加上：
		$ sudo add-apt-repository ppa:ubuntu-sdk-team/ppa 

* 安装 ubuntu-device-flash 包：

		$ sudo apt-get install ubuntu-device-flash
	
	安装完成后你可以通过 man 来查看使用手册：

		$ man ubuntu-device-flash

	ubuntu-device-flash工具包提供了两个重要的 Android 工具，后面将要频繁使用它：
	- adb：提供一个命令行的设备连接工具，这个必须在设备启动后使用（Android系统你还需打开开发者模式）。
	- fastboot：当设备进入到 bootloader 模式，并使用USB链接到桌面时，使用的设备连接工具。

	阅读这两个工具的说明文档：

		$ adb help 2>&1 | less
		$ fastboot help 2>&1 | less


* 安装 phablet-tools 包

	phablet-tools 是一个很好用的桌面工具，当你你通过USB链接设备到桌面后，你可以使用
	- click-buddy 创建一键安装包，发送到设备运行。
	- phablet-screenshot 提供设备的屏幕截图，并保存到当前目录。
	- phablet-bootchart 帮你创建设备启动状态图。

	安装 phablet-tools：

		$ sudo apt-get install phablet-tools
		#查看安装的组件
		$ dpkg -L phablet-tools | grep bin
		#查看帮助 命令+ -h参数比如：
		$ phablet-config -h

## 备份原有的 Android 数据
安装 Ubuntu for devices 将会清除设备上的所有数据。

1. 打开 Android 的开发者模式
2. 打开 usb 调试模式

连接设备到电脑，你通过授权后，使用 adb 工具检查连接，看是否能够找到设备：

	$ adb devices
如果没有显示设备，先使用：`adb kill-server`。
通过这几步你的设备就已经成功连接到 ubuntu 桌面，并处于安装和开发模式。下面开始备份数据：

	$ adb backup -apk -shared -all
在你通过授权后，这将在当前的目录建立一个 Android 设备的数据备份（./backup.ab）

## 解锁 Android 的 bootloader

1. 进入Android 的 bootloader 模式

		$ adb reboot bootloader

2. 验证设备是否正确连接：

		$ fastboot devices

3. 解锁

		$ sudo fastboot oem unlock

4. 在设备上通过授权
5. 重启设备进入 Android：

		$ fastboot reboot

6. 在设备上完成初次安装的步骤，设备已解锁。

## 安装 Ubuntu

**提示：** 如果你的设备经过加密，在安装 ubuntu 之前，你首先要恢复的未加密，或恢复到出厂状态。
有两种安装源可选择 devel and stable 。同时还有不同的Channels，Channels是基于ubuntu的发行版本来命名的，要注意不同的版本名称  Ubuntu 14.04 是Trusty release。Ubuntu 13.10 是 Saucy release。每个发行版又有不同的变种，-proposed（候选） -customized（自定义）以及 -customized-proposed

	#查看当前可用安装镜像
	$ ubuntu-device-flash --list-channels
	
开始安装：

1. 关机
2. 启动进入 bootloader
3. 检查设备是否正常连接
4. 开始使用你选择的版本安装，例子是 devel 版。`--bootstrap` 选项通常只用在第一次安装 ubuntu的情况下，让设备在安装重启后回到 bootloader，而不是进入到 ubuntu。

	$ ubuntu-device-flash --channel=devel --bootstrap

5. 等待设备安装完，自动重启。
整个过程可能经历下面几个步骤：
	- 首先下载安装镜像到  `~/.cache/ubuntuimages` （可用 ubuntu-device-flash –clean-cache 来清空）。
	- 镜像文件拷贝到设备并安装 “recovery” 镜像。
	- 重启到 recovery 继续安装 ubuntu 通用系统
	- 安装完成启动进入 ubuntu。
	
## 系统手动更新
你可以在设备上使用自动更新来更新系统。你也可以自己手动更新系统：