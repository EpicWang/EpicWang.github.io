---
layout:     post
title:      MySql免安装版配置
subtitle:   Windows MySQL 5.7.19【免安装版】配置
date:       2017-09-14
author:     EpicWang
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - mysql
	- windows
---

Windows下Mysql有各种版本，今天这里安装的是 mysql-5.7.19-winx64.zip（.zip Archive版【免安装版】，非.msi Installer安装版）

## 安装

相应操作系统版本的mysql，如果你是是windows X64版本，可以点击下载[mysql-5.7.19-winx64.zip](https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.19-winx64.zip)

### 1、下载windows 64位 .zip格式MySQL：mysql-5.7.19-winx64.zip

我这里直接解压到C:\Program Files\mysql-5.7.19-winx64

### 2、进入这个目录，创建my.ini文件并添加以下内容：

```java
[client]

default-character-set=utf8

[mysqld]

#port=3306

character-set-server=utf8

basedir=C:\\Program Files\\mysql-5.7.19-winx64

datadir=C:\\Program Files\\mysql-5.7.19-winx64\\data
```

### 3、进入C:\\Program Files\\mysql-5.7.19-winx64\\bin目录打开cmd（选中文件夹地址栏按一下删除键清空后再输入cmd敲回车）执行以下命令：

```java
mysqld --initialize        #初始化（初始化data仓库）

mysqld --install            #添加到系统service服务（若需删除服务则mysqld --remove）

net start mysql             #启动mysql服务（停止：net stop mysql）
```

### 4、用初始化时产生的随机密码登录（初始随机密码在data目录下面的.err日志文件中）：

```java
mysql -u root -p
```

### 5、修改密码(标准的改密方式)：

```java
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
```

## 以下为可选步骤：

### 6、查看编码：

```java
show variables like '%character%';
```

### 7、查看用户及允许访问的主机（localhost只允许本机访问，%表示任意ip均可访问）：

```java
use mysql;

select host,user from user;
```

### 8、如果不想每次打开mysql命令行都进入mysq解压目录的bin目录启动，那就添加到path随时随地可以使用mysql命令：

```java
C:\Program Files\mysql-5.7.19-winx64\bin
path前面加上英文分号再追加上上面这一串。

可在命令行通过echo命令查看：

echo %PATH%
试试WIN+R输入cmd打开命令行：mysql -u root -p （不会报找不到命令的错误了）。
```

### 9、退出：

```java
mysql> quit

或者

mysql> exit
完事。
```

### 附windows查看端口是否占用命令：

```java
netstat -ano | findstr 3306
```




