# MySQL安装

- [MySQL安装](#mysql安装)
  - [安装](#安装)
  - [修改默认字符集](#修改默认字符集)
  - [启动](#启动)
  - [首次连接](#首次连接)

> 安装环境：
>
> - 操作系统：CentOS 7
> - MySQL版本：MySQL 5.7

## 安装

```shell
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm

yum -y install mysql57-community-release-el7-10.noarch.rpm

rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022

yum -y install mysql-community-server
```

## 修改默认字符集

```shell
vim /etc/my.cnf

[mysqld]
character-set-server=utf8
collation-server=utf8_general_ci

[client]
default-character-set=utf8
```

## 启动

```shell
systemctl start mysqld.service

systemctl enable mysqld.service
```

## 首次连接

```shell
# 查看初始密码
grep "password" /var/log/mysqld.log

# 客户端连接
mysql -uroot -p

# 修改密码
SET GLOBAL validate_password_policy = LOW;
SET GLOBAL validate_password_length = 6;
ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
GRANT ALL PRIVILEGES ON *.* TO 'root' @'%' IDENTIFIED BY '123456' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
