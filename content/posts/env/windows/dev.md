---
title: 'Windows'
date: 2025-01-18
tags: ['环境', 'windows']
description: windows 环境配置
---

**_!注：安装、日志等目录可根据自己的实际情况创建，不一定下面相同_**

# go

[国内下载（推荐）](https://golang.google.cn/dl) [官网下载](https://go.dev/dl)

> 下载完成并解压至 `D:\env\go` 并创建 `D:\proj\go`

```
go env -w GO111MODULE=on
go env -w GOCACHE=D:\logs\go\go-build
go env -w GOMODCACHE=D:\logs\go\pkg\mod
go env -w GOPROXY=https://proxy.golang.com.cn,direct
go env -w GOPATH=D:\proj\go
```

# mysql

> 需要创建：`D:\logs\mysql` `D:\data\mysql` 示例： mysql-8.0.40

[mysql 下载](https://dev.mysql.com/downloads/mysql/)

## 准备

解压至 `D:\env\mysql` 并新建 `my.ini` 文件

```ini
[mysqld]
# 数据库目录
datadir=D:\\data\\mysql

# 端口
port=3306

# 默认字符集
character-set-server=utf8mb4
collation-server=utf8mb4_general_ci

# 默认存储引擎
default-storage-engine=INNODB

# INNODB 引擎配置
innodb_buffer_pool_size=512M
innodb_log_file_size=128M
innodb_file_per_table=1
innodb_flush_method=normal

# 新的 redo log 容量配置，替代废弃项 innodb_log_file_size 和 innodb_log_files_in_group
innodb_redo_log_capacity=268435456

# 日志
log_error=D:\\logs\\mysql\\error.log

# 记录慢查询
slow_query_log=1
slow_query_log_file=D:\\logs\\mysql\\slow.log

# 其他配置
tmp_table_size=64M
max_heap_table_size=64M
max_connections=150
thread_cache_size=10
table_open_cache=2000
open_files_limit=5000

# 启用 TLS 支持（如果有 SSL 证书）
# ssl-ca=D:/path_to_your_ca.pem
# ssl-cert=D:/path_to_your_cert.pem
# ssl-key=D:/path_to_your_key.pem

# MySQL 连接加密
# 注意：如果你使用 TLS 连接，确保正确配置证书
# 默认情况下会使用自签名证书，可以忽略警告，也可以替换为受信任证书
ssl=1

[client]
# 客户端端口配置
port=3306

# 客户端默认字符集
default-character-set=utf8mb4

# 启用连接重试
# 用于客户端遇到连接问题时重新连接
reconnect=1
```

## 安装

> 使用 `管理员` 打开命令窗口

```
# 初始化并获取默认密码
D:\env\mysql\bin> .\mysqld.exe --initialize --console

# 安装到服务中 --install [自定义服务名称]，可以在服务中设置开机自动启动
D:\env\mysql\bin> .\mysqld.exe --install mysqld --defaults-file="D:\env\mysql\my.ini"

# 连接 MySQL 并初始化密码
D:\env\mysql\bin>.\mysql.exe -u root -P 3306 -p
Enter password: 这里输入上面的密码

...

# mysql8 修改密码
ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'your_password';
FLUSH PRIVILEGES;

```

# php

> 示例：PHP 8.4 (8.4.3) VS17 x64 Non Thread Safe (2025-Jan-15 11:07:36)

[php 下载](https://windows.php.net)

## 问题

```
PS D:\> php -v
PHP Warning:  'C:\Windows\SYSTEM32\VCRUNTIME140.dll' 14.15 is not compatible with this PHP build linked with 14.42 in Unknown on line 0
```

[问题解决](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)

```
PS D:\> php -v
PHP 8.4.3 (cli) (built: Jan 15 2025 11:02:41) (NTS Visual C++ 2022 x64)
Copyright (c) The PHP Group
Zend Engine v4.4.3, Copyright (c) Zend Technologies
```

## 配置

```
# 763~764行
On windows:
extension_dir = "D:\env\php\ext"

# 801行
cgi.fix_pathinfo=1

# 964 行
date.timezone = "Asia/Shanghai"

# extension，根据实际开发需求
extension=curl
extension=openssl
extension=pdo_mysql
extension=mbstring
extension=gd
extension=zip
extension=exif
extension=intl
extension=mysqli
extension=pgsql
extension=odbc
extension=xdebug   ; 如果你使用调试工具
```

## Composer 安装

[下载安装](https://pkg.xyz/#how-to-install-composer)

```
PS D:\env\composer> php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
PS D:\env\composer> php composer-setup.php
All settings correct for using Composer
Downloading...

Composer (version 2.8.4) successfully installed to: D:\env\composer\composer.phar
Use it: php composer.phar

PS D:\env\composer> php .\composer.phar --version
Composer version 2.8.4 2024-12-11 11:57:47
PHP version 8.4.3 (D:\env\php\php.exe)
Run the "diagnose" command to get more detailed diagnostics output.
```

### composer.bat

> 新建 `D:\env\composer\composer.bat` 文件并配置 `D:\env\composer` 到环境变量中

```
@php "%~dp0composer.phar" %*
```

```
PS D:\> composer --version
Composer version 2.8.4 2024-12-11 11:57:47
PHP version 8.4.3 (D:\env\php\php.exe)
Run the "diagnose" command to get more detailed diagnostics output.
```

# openresty

[官网](https://openresty.org/cn/) [github latest](https://github.com/openresty/openresty/releases)

下载 `openresty-1.27.1.1-win64.zip` 并解压至 `D:\env\openresty`

## 使用

```
# 启动
PS D:\env\openresty> .\nginx.exe

# 停止（需在另一个命令窗口中）
PS D:\env\openresty> .\nginx.exe -s stop

# 测试配置（需在另一个命令窗口中）
PS D:\env\openresty> .\nginx.exe -t
nginx: the configuration file ./conf/nginx.conf syntax is ok
nginx: configuration file ./conf/nginx.conf test is successful

# 重载（需在另一个命令窗口中），需要先执行启动
PS D:\env\openresty> .\nginx.exe -s reload
```

## openresty + php

推荐使用 `phpstudy`

> 创建 `D:\env\openresty\conf\conf.d` 目录，并创建 `php.conf` 文件

```
# openresty + php 测试
server {
    listen 2025;
    server_name localhost;

    location / {
        root   D:\\proj\\php\\demo;
        index  index.php index.html index.htm;
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
    	root D:\\proj\\php\\demo;
        include fastcgi_params;
        fastcgi_pass 127.0.0.1:9008;  # 确保 PHP-FPM 监听端口正确
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param  PATH_INFO $fastcgi_script_name;
    }


    # 配置错误日志和访问日志
    error_log D:\\logs\\php\\demo-error.log;
    access_log D:\\logs\\php\\demo-access.log;
}
```

> 修改 `D:\env\openresty\conf\nginx.conf` ，在 http {...} 中添加一行

```
include conf.d\\php.conf;
```

> 测试

```
# php-cgi 启动
PS D:\env\php> .\php-cgi.exe -b 9000
```

```
# 重新加载 openresty
PS D:\env\openresty> .\nginx.exe -s reload
```

`D:\proj\php\demo` 中添加 `index.php` `url-test\test.php`

```
# index.php
<?php

echo phpinfo();


# url-test/test.php
<?php

echo 'url-test';
```

> 访问 [http://localhost:2025](http://localhost:2025) [http://localhost:2025/url-test/test.php](http://localhost:2025/url-test/test.php)
