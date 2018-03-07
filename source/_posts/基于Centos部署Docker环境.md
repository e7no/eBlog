---
title: 基于Centos部署Docker环境
date: 2017-03-02 14:11:59
categories: Docker
tags: [docker,centos]
copyright: true
photos: 
    - "http://omdfpjss7.bkt.clouddn.com/17-3-6/88149926-file_1488780731850_b1c8.jpg"
---
#### 拉取镜像 
```
docker pull centos:6.8
```
#### 将这个镜像启动成为一个容器,并映射端口
```
docker run -it -d --name www -p 33060:3306 -p 220:22 -p 8080:80 centos：6.8 /bin/bash
```
#### 查看创建的镜像
```
docker ps
```
#### 进入创建的镜像容器
```
docker exec -it <container ID> bash 
```
#### 安装ifconfig
```
yum install net-tools –y
```
#### 安装ssh服务
```
yum install openssh*
```
#### 安装压缩解压缩
```
yum install -y unzip zip
```
#### 修改密码
```
passwd
```
#### 创建SSH服务目录
```
mkdir -p /var/run/sshd
```
#### 设置秘钥
```
  ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
  ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
```
#### 启动服务
```
/usr/sbin/sshd -D &
```
#### 查看SSH监听端口使用情况
```
netstat -tunlp
```
#### 取消pam登录限制
```
sed -ri 's/session required pam_loginuid.so/#session required pam_loginuid.so/g' /etc/pam.d/ssh
```
#### 本地创建公钥（非docker环境）,已有则不需要创建
```
ssh-keygen -t rsa
```
#### 创建授权目录
```
mkdir root/.ssh
```
#### 编辑授权文件,复制本地.ssh目录中的id_rsa.pub里面的密钥到授权文件中
```
vim /root/.ssh/authorized_keys
```
#### 创建自动启动SSH服务器的可执行文件run.sh,并添加可执行权限
```
  vim /run.sh
  chmod +x run.sh
```
#### 编辑run.sh
```
  #!/bin/bash
  /usr/sbin/sshd -D
```
#### 通过Xshell登录该镜像,地址为docker的IP，端口号为220,账号为：root,密码为上面设置的密码

---

