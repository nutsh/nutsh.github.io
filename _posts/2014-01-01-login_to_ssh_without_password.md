---
layout: post
title: 密钥(无需密码)方式实现SSH访问
category: ops
tag: [linux]
shortinfo: 使用密钥方式实现SSH远程访问
---


# 密钥(无需密码)方式实现SSH访问
如果想通过SSH方式,访问远程server的时候,并且不需要密码(方便统一管理密码)
```shell
ssh username@remote_server
```
可通过以下步骤


1. 打开本地termail.
2. 创建~/.ssh文件件
```shell
mkdir -p ~/.ssh
```
3. 通过ssh-keygen生成RSA密钥对
```shell
ssh-keygen -t rsa
```
4. 讲本机的公钥上传到远程主机
```
scp id_rsa.pub username@remote_server:~/.ssh/
```

5. 登陆到远程主机
```shell
ssh username@remote_server
```
6. 拷贝公钥信息拷贝到远程主机的`authorized_keys`
```shell
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```
7. 删除从本地机器上传的公钥
```shell
rm ~/.ssh/id_rsa.pub
```
8. 退出后重新登陆,就可以使用密钥(无密码)登陆远程主机了.




相关链接:
[How to SSH into Terminals without entering the password?](http://www.finiteloops.com/weblog/?p=259)
