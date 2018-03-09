---
title: Windows下用Vagrant搭建Linux开发环境
date: 2017-09-01 15:04:58
categories: Vagrant
tags: [Vagrant,Linux]
copyright: true
photos: 
    - "https://img.e7no.com/18-3-9/43077516.jpg"
---
> Vagrant下载地址：[https://www.vagrantup.com/downloads.html](https://note.youdao.com/)

> VirtualBox下载地址：[https://www.virtualbox.org/wiki/Downloads](https://note.youdao.com/)

> VagrantBox镜像下载地址：[http://www.vagrantbox.es/
](https://note.youdao.com/)


###### 执行终端: GitBash 或者 cmd

### 1.安装软件
##### 先安装VirtualBox,然后安装Vagrant


### 2.1 直接在线拉取镜像
##### [https://www.virtualbox.org/wiki/Downloads](https://note.youdao.com/) 

备注：{title} box命名 {url} 镜像地址  （在线拉镜像速度会比较慢）

```
vagrant box add {title} {url}
```
### 2.2 或导入下载镜像

###### 把下载的centos-6.8-x86_64.box复制到本目录 D:www/box下，执行

```
vagrant box add centos6.8 centos-6.8-x86_64.box
```


### 3.初始化Box

```
vagrant init {title}
```

### 4.启动Box

```
vagrant up
```

### 5.配置Vagrantfile-常用配置

- ####  box命名

```
config.vm.box = "centos6.7"
```

- ####  端口映射 -- *可以添加多个*

```
config.vm.network "forwarded_port", guest: 80, host: 80
config.vm.network "forwarded_port", guest: 87, host: 8087
config.vm.network "forwarded_port", guest: 3306, host: 33060
```

- ####  目录映射(可以不设置，默认将Linux下的vagrant共享到当前box目录) -- *表示把本机的data目录共享到虚拟机里的/var/www目录*

```
config.vm.synced_folder "D:/www", "/var/www/html"
```

- ####  ip设置
 
```
config.vm.network "public_network",ip:"192.168.56.1"
```

### 6.重启vagrant加载新的配置项

```
vagrant reload
```

### 7.导出Box在其他机器上运行，免去重新部署

```
vagrant package
```

### 8.其他命令解释

```
vagrant box add "boxIdentity" remoteUrlorLocalFile  添加box
vagrant init "boxIdentity"  初始化box
vagrant up  启动虚拟机
vagrant ssh  登录虚拟机
vagrant box list  显示当前已添加的box列表
vagrant box remove "boxIdentity"  删除box
vagrant destroy  停止当前正在运行的虚拟机并销毁所有创建的资源
vagrant halt  关闭虚拟机
vagrant package  打包当前运行的虚拟机的环境
vagrant plugin  用于安装卸载插件
vagrant reload  重启虚拟机，主要用于重新载入配置文件
vagrant suspend  挂起虚拟机
vagrant resume  恢复挂起状态
vagrant ssh-config  输出ssh连接信息
vagrant status  输出当前虚拟机的状态
```

