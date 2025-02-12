---
title: 'Linux 初始化'
date: 2025-01-19
tags: ['环境', 'linux']
description: '测试服务器环境：Huawei Cloud EulerOS 2.0'
---

# 写在前面

> 当然，如果你使用 `docker` `宝塔` 等搭建，就不需这么麻烦的编译安装了，可以忽略

# 准备

```
#!/bin/bash
# cls 命令添加
ln -s /usr/bin/clear /usr/local/bin/cls
# 防火墙
systemctl start firewalld.service
firewall-cmd --zone=public --add-port=22/tcp --permanent
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=443/tcp --permanent
# 重启
systemctl restart firewalld
# 开机启动
systemctl enable firewalld.service
# 列表查看
# firewall-cmd --list-ports
cd /etc
# 主机名称
cp hostname hostname.bak
echo "Rengchi" > hostname
cd /etc/
cp sysctl.conf sysctl.conf.bak
sed -i '$a vm.overcommit_memory = 1' /etc/sysctl.conf
sudo sed -i '$a net.ipv4.tcp_max_syn_backlog = 4096' /etc/sysctl.conf
sudo sed -i '$a net.ipv4.tcp_fin_timeout = 15' /etc/sysctl.conf
sysctl -p
reboot
```

# .vimrc

## vim 目录

```
cd
mkdir .vim .vim/backup .vim/undo
```

```
" 让配置变更立即生效
autocmd BufWritePost $MYVIMRC source $MYVIMRC

" 基础设置
set nocompatible            " 不兼容 vi
set noswapfile              " 不生成 swap 文件
set autowrite               " 设置自动保存
set confirm                 " 未保存或只读文件时弹出确认框
set number                  " 显示行号
set autoindent              " 自动缩进
set smartindent             " 智能缩进
" set mouse=a                 " 启用鼠标支持
syntax on                   " 开启语法高亮

" Tab 和缩进设置
set tabstop=4               " 设置 Tab 为 4 个空格
set shiftwidth=4            " 设置缩进宽度为 4 个空格
set softtabstop=4           " 设置 Tab 为 4 个空格
set expandtab               " 用空格替代 Tab

" 编码设置
set fileencodings=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936
set termencoding=utf-8
set encoding=utf-8

" 自动加载
set autoread

" 文本显示设置
set linebreak               " 不换行断字
set showmatch               " 高亮匹配括号
set cursorline              " 突出显示当前行
set ruler                   " 打开状态栏标尺

" 搜索设置
set hlsearch                " 搜索时高亮匹配的词
set incsearch               " 边输入边搜索
set ignorecase              " 搜索时忽略大小写
set smartcase               " 当搜索包含大写字母时，搜索区分大小写

" 中文帮助设置
set helplang=cn             " 设置中文帮助
set ambiwidth=double        " 设置双字宽显示，防止字符不完整

" 备份与撤销文件设置
set backup                  " 开启备份文件
set backupdir=~/.vim/backup  " 设置备份文件存放路径
set undofile                " 开启撤销历史记录文件
set undodir=~/.vim/undo      " 设置撤销文件存放路径

" 快捷键映射
let mapleader = ","         " 定义 <leader> 键
nnoremap <leader>e :e ~/.vimrc<cr>           " 快速打开 vim 配置文件
nnoremap <leader>r :source $MYVIMRC<cr>      " 刷新配置
nnoremap <c-d> yyp                          " Ctrl+d 复制本行并粘贴到下一行
inoremap ;; <Esc>                           " 将 ESC 键映射为两次 ; 键
nnoremap <leader>q :q<cr>                   " <leader>+q 快速退出 vim
inoremap <leader>q <Esc>:q<cr>
nnoremap <leader>s :w<cr>                   " <leader>+s 快速保存
inoremap <leader>s <Esc>:w<cr>

" 插入模式、正常模式按 Ctrl+u 快速转换为大写
inoremap <c-u> <esc>viwUea
nnoremap <c-u> viwUe

" 文件头部签名信息管理
nmap <F6> ms:call TitleDet() <cr>'s
function AddTitle()
    call append (0,"/*********************************************************************")
    call append (1," * Author           : 仍迟")
    call append (2," * Create At        : ".strftime("%Y-%m-%d %H:%M"))
    call append (3," * Filename         : ".expand("%:t"))
    call append (4," * Description      : 知之行之，无负今日")
    call append (5," * ******************************************************************/")
    echohl WarningMsg | echo "添加成功 !!" | echohl None
endfunction
function UpdateTitle()
    normal m'
    execute '/* Last modified\s*:/s@:.*$@\=strftime(": %Y-%m-%d %H:%M")@'
    normal ''
    normal mk
    execute '/* Filename\s*:/s@:.*$@\=": ".expand("%:t")@'
    execute "noh"
    normal 'k
    echohl WarningMsg | echo "更新成功 !!" | echohl None
endfunction
function TitleDet()
    let n=1
    while n<8
       let line = getline(n)
       if line =~ '^\s*\*\s*Last\smodified\s*:\s*\S*.*$'
        call UpdateTitle()
    return
       endif
       let n = n+1
    endwhile
    call AddTitle()
endfunction

" 查找与替换
nnoremap <C-f> /
nnoremap <C-h> :%s/
nnoremap <leader>sf :!grep -ri

" 允许光标键跨行，光标可以出现在最后一个字符后
set whichwrap+=<,>,h,l
set virtualedit=block,onemore
```

# 环境安装目录

> `/data` 目录有可以使用重复，需要先查看是否存在

> `/fate ` 目录为存储配置文件目录

```
cd
mkdir /env /logs /download /third /daemon /data /proj
mkdir /logs/openresty /logs/openresty/proxy_temp /logs/redis /logs/mysql /fate
mkdir /third/mysql
mkdir /fate/openresty /fate/openresty/lua /fate/openresty/conf.d /fate/redis /fate/mysql
mkdir /daemon/openresty /daemon/redis /daemon/mysql
mkdir /data/mysql /data/mysql/data /data/mysql/mysql-files /data/openresty /data/git /data/git/repo
mkdir /proj/html /proj/go
chmod 755 /env /fate /data /download /proj
chmod -R 755 /logs/openresty /daemon /proj/html
chmod 777 /logs
```

# go（可选）

> go 项目直接把打包后的放在服务器上运行就可以，或者使用 docker

## 安装

```
cd /download
wget https://golang.google.cn/dl/go1.23.5.linux-amd64.tar.gz
tar -zxf go1.23.5.linux-amd64.tar.gz
mv /download/go /env/
rm -rf /download/go
ln -s /env/go/bin/* /usr/local/bin/
go env -w GOPATH=/proj/go
go env -w GOROOT=/env/go
go env -w GOBIN=/proj/go/bin
go env -w GOPROXY=https://goproxy.cn,direct
go env -w GOCACHE=/logs/go/go-build
go env -w GOMODCACHE=/logs/go/pkg/mod
go env -w GO111MODULE=on
```

## 命令自动补全

> 中途需要输入一个 `y`

```
go install github.com/posener/complete/gocomplete@latest
/proj/go/bin/gocomplete -install
```

## 环境变量

```
ln -s /proj/go/bin/* /usr/local/bin/
```

# git

## 安装

```
cd /download
yum install zlib-devel libcurl-devel curl-devel openssl-devel -y
wget https://www.kernel.org/pub/software/scm/git/git-2.48.1.tar.gz
tar -zxf git-2.48.1.tar.gz
cd git-2.48.1
./configure --prefix=/env/git
make -j$(nproc)
make install
ln -s /env/git/bin/* /usr/local/bin
```

## 命令自动补全

> ！注 `./root/.bashrc`

```
cd
wget https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash
mv /root/git-completion.bash /etc/bash_completion.d/
chmod o+r /etc/bash_completion.d/git-completion.bash
cat >> .bashrc << EOF
if [ -f /etc/bash_completion.d/git-completion.bash ]; then
. /etc/bash_completion.d/git-completion.bash
fi
EOF
. /root/.bashrc
```

## 扩展

### 自己搭建（不要在线下整，属于个人测试）

> 手动复制到服务器 `/home/git/.ssh/authorized_keys` 中

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
ssh-copy-id git@server
```

```
git config --global init.defaultBranch main
git config --global user.email "your_email@example.com"
git config --global user.name "username"
useradd -m -s /bin/bash git
# 密码设置，可选
passwd git

mkdir -p /home/git/.ssh
chmod 700 /home/git/.ssh
chown -R git:git /home/git/.ssh
chmod 600 /home/git/.ssh/authorized_keys
chown -R git:git /data/git/repo/test.git
chmod -R 755 /data/git/repo/test.git
```

### gitea

> ! 搭建中需要使用 `mysql` `openresty` 反代，需要在安装完成后最后配置

[github](https://github.com/go-gitea/gitea) [gitea](https://about.gitea.com/) [中文文档](https://docs.gitea.com/zh-cn/) [下载](https://dl.gitea.com/gitea/)

#### ! 请在阅读相关文档后安装，熟悉后再安装到生产环境

[签名验证](https://www.cnblogs.com/Gitea/p/install-gitea-service.html)

```
useradd -r -m -d /home/gitea -s /bin/bash gitea
su gitea
cd
wget https://github.com/go-gitea/gitea/releases/download/v1.22.5/gitea-1.22.5-linux-amd64
wget https://github.com/go-gitea/gitea/releases/download/v1.22.5/gitea-1.22.5-linux-amd64.asc
gpg --edit-key 7C9E68152594688862D62AF62D9AE806EC1592E2
gpg --keyserver hkp://pgp.mit.edu --recv 7C9E68152594688862D62AF62D9AE806EC1592E2
gpg --verify gitea-1.22.5-linux-amd64.asc gitea-1.22.5-linux-amd64
mv gitea-1.22.5-linux-amd64 gitea
chmod +x /home/gitea/gitea
./gitea web --port 3000
systemctl enable gitea
systemctl start gitea
systemctl status gitea
```

#### gitea.service

> `vim /etc/systemd/system/gitea.service`

```
[Unit]
Description=Gitea
Documentation=https://docs.gitea.io
After=network.target

[Service]
User=gitea
Group=gitea
ExecStart=/home/gitea/gitea web
RestartSec=3
Restart=always
Environment=GITEA_WORK_DIR=/home/gitea
Environment=GITEA_CUSTOM=/home/gitea/custom
WorkingDirectory=/home/gitea
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
```

#### gitea.conf

> 如果开启 `https` 的话，注意证书配置项

```
# gitea
server {
    listen       80;
    server_name  gitea.yourhost.com;
    return  301 https://$server_name$request_uri;
}

server {
    listen 443 ssl;
    server_name gitea.yourhost.com;

    # 强制浏览器使用 HTTPS
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;

    ssl_certificate      /data/openresty/cert/gitea.yourhost.com/fullchain.pem;
    ssl_certificate_key  /data/openresty/cert/gitea.yourhost.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;  # 仅支持 TLSv1.2 和 TLSv1.3
    ssl_ciphers 'TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:...';  # 选择安全的加密套件
    ssl_prefer_server_ciphers on;  # 强制服务器优先选择加密套件
    ssl_session_cache shared:SSL:1m;
    ssl_session_timeout 5m;

    access_log /logs/openresty/gitea.access.log;
    error_log /logs/openresty/gitea.error.log;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Range $http_range;
        proxy_set_header If-Range $http_if_range;
        proxy_redirect off;
        proxy_pass http://127.0.0.1:3000;
    }
}
```

# openresty

[openresty 官网](https://openresty.org/cn/)

## 安装

> 服务器不能直接使用 `yum` 安装，这里选择下载编译安装

```
yum install pcre-devel zlib-devel openssl-devel geoip-devel jemalloc-devel -y
cd /download
wget https://mirrors.huaweicloud.com/openresty/v1.25.3.2/openresty-1.25.3.2.tar.gz
tar -zxf openresty-1.25.3.2.tar.gz
cd /download/openresty-1.25.3.2
./configure --prefix=/env/openresty \
            --conf-path=/fate/openresty/nginx.conf \
            --error-log-path=/logs/openresty/error.log \
            --http-log-path=/logs/openresty/access.log \
            --pid-path=/daemon/openresty/openresty.pid \
            --with-http_v2_module \
            --with-http_realip_module \
            --with-http_stub_status_module \
            --with-luajit \
            --with-cc=gcc \
            --with-stream \
            --with-stream_ssl_module \
            --with-http_ssl_module \
            --with-http_sub_module \
            --with-http_secure_link_module \
            --with-http_gzip_static_module \
            --with-http_auth_request_module \
            --with-pcre-jit \
            --with-threads \
            --with-http_geoip_module \
            --with-poll_module \
            --with-ld-opt="-ljemalloc" \
            --with-http_dav_module \
            --with-http_flv_module \
            --with-http_mp4_module \
            --with-http_slice_module \
            --with-file-aio

gmake -j$(nproc)
gmake install
groupadd -r openresty
useradd -r -g openresty -s /sbin/nologin openresty
ln -s /env/openresty/bin/openresty /usr/local/bin/
chmod 755 /env/openresty
chown -R openresty:openresty /env/openresty /data/openresty
chmod 644 /env/openresty/lualib
chown -R openresty:openresty /env/openresty/lualib/
chmod -R 644 /env/openresty/lualib/resty
chown -R openresty:openresty /env/openresty/lualib/resty
chmod -R 755 /proj/html
chmod 755 /fate/openresty
chown -R openresty:openresty /fate/openresty
chmod -R 644 /fate/openresty/conf.d
chown -R openresty:openresty /fate/openresty/conf.d
```

## 开机自动启动

> `openresty` # chkconfig: - 60 80

```
vim /etc/init.d/openresty
chmod +x /etc/init.d/openresty
chkconfig --add openresty
chkconfig openresty on
```

```
#!/bin/bash
# chkconfig: - 60 80
# OpenResty 服务初始化脚本
# 用于在系统启动时启动 OpenResty，及在运行时进行管理

nginxd=/env/openresty/nginx/sbin/nginx
nginx_config=/fate/openresty/nginx.conf
nginx_pid=/daemon/openresty/openresty.pid
RETVAL=0
prog="OpenResty"

# 导入函数库
. /etc/rc.d/init.d/functions

# 导入网络配置
. /etc/sysconfig/network

# 检查网络是否启动
[ ${NETWORKING} = "no" ] && exit 0

# 检查 nginx 可执行文件是否存在
[ -x $nginxd ] || exit 0

# 启动 OpenResty 服务
start() {
    if [ -e $nginx_pid ]; then
        echo "$prog 已经在运行..."
        exit 1
    fi
    echo -n $"启动 $prog: "
    daemon $nginxd -c ${nginx_config}
    RETVAL=$?
    echo
    [ $RETVAL = 0 ] && touch /daemon/openresty/openresty.lock
    return $RETVAL
}

# 停止 OpenResty 服务
stop() {
    echo -n $"停止 $prog: "
    killproc $nginxd
    RETVAL=$?
    echo
    [ $RETVAL = 0 ] && rm -f /daemon/openresty/openresty.lock $nginx_pid
}

# 重新加载 OpenResty 配置
reload() {
    echo -n $"重新加载 $prog: "
    killproc $nginxd -HUP
    RETVAL=$?
    echo
}

# 根据传入的参数执行相应操作
case "$1" in
start)
    start
    ;;
stop)
    stop
    ;;
reload)
    reload
    ;;
restart)
    stop
    start
    ;;
status)
    status $nginxd
    RETVAL=$?
    ;;
*)
    echo $"用法: $prog {start|stop|status|restart|reload}"
    exit 1
esac

exit $RETVAL
```

## nginx.conf 示例

```
user  openresty;
worker_processes  auto;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

# pid
pid        /daemon/openresty/openresty.pid;

events {
    worker_connections  1024;
}

http {
    # 定义新的临时目录
    proxy_temp_path /logs/openresty/proxy_temp;

    include       mime.types;

    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for" '
                    '"$http_x_real_ip" "$http_x_forwarded_host" '
                    '"$http_x_forwarded_proto"'
                    '"$request_time" "$upstream_addr" "$upstream_response_time"';

    # access_log  /log/openresty/access.log  main;

    sendfile        on;  # 大文件处理
    tcp_nopush      on;  # 大文件处理
    # 客户端连接在 Keep-Alive 状态下保持打开的时间（秒） keepalive_timeout  30;

    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
    gzip_min_length 1024;
    gzip_proxied any;
    gzip_disable "msie6";
    gzip_vary on;

    # 隐藏服务器信息版本号
    server_tokens off;

    # 移除不需要的响应头部（需要 ngx_headers_more 模块）
    more_clear_headers "X-Powered-By";
    more_clear_headers "Server";
    more_clear_headers "X-Content-Type-Options";

    # 上传文件
    client_max_body_size 10M;
    client_body_buffer_size 8M;

    # 定义共享内存区域
    limit_conn_zone $binary_remote_addr zone=conn_limit_per_ip:10m;
    limit_req_zone $binary_remote_addr zone=req_limit_per_ip:10m rate=10r/s; # 提高速率限制

    # lua
    #access_by_lua_file "lua 文件目录";

     add_header X-HTTP-Method-Override ""; # 禁用伪造的方法
    # 可以增强浏览器的安全性，防止 XSS 攻击和其他安全漏洞
     add_header X-Content-Type-Options nosniff always; # 防止 MIME 类型嗅探
    # 禁用跨站请求伪造（CSRF）
     add_header Referrer-Policy "no-referrer";
    # 防止点击劫持，相同域名iframe引用
    # add_header X-Frame-Options SAMEORIGIN;
    add_header X-XSS-Protection "1; mode=block" always; # 防止跨站脚本攻击 (XSS)
    add_header X-Content-Type-Options "nosniff"; # 防止浏览器解读响应的MIME类型
    add_header X-Frame-Options "DENY"; # 防止点击劫持（Clickjacking）
    add_header Set-Cookie "name=value; SameSite=Strict"; # 防止跨站请求伪造 (CSRF)
    # 启用 Content Security Policy (CSP), 设置 CSP 头以防止外部脚本和资源的加载，从而防止 XSS 攻击
    add_header X-Content-Security-Policy "default-src 'self'; script-src 'self'; object-src 'none'; style-src 'self'; frame-ancestors 'none';"; # CSP 防范攻击
    add_header Content-Security-Policy "default-src 'self'; script-src 'self'; object-src 'none'; style-src 'self';";

    # cache 配置
    proxy_cache_path /logs/openresty/cache levels=1:2 keys_zone=my_cache:10m max_size=1g inactive=60m use_temp_path=off;
    proxy_cache_key "$scheme$request_method$host$request_uri";

    # www
    # include /fate/openresty/conf.d/www.conf;
}
```

## conf.d/security.conf

```
vim /fate/openresty/conf.d/security.conf
chmod -R 644 /fate/openresty/conf.d
```

```
# 限制对敏感文件的访问
location ~ /\. {
    deny all;
}

location ~ /\.git {
    deny all;
}

# 禁用不必要的 HTTP 方法
if ($request_method !~ ^(GET|POST|HEAD)$) {
    return 405;
}
```

## https 证书

```
pip config set global.cache-dir "/logs/python/pip"
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
pip install certbot certbot-nginx
certbot certonly

# letsencrypt链接，在使用certbot certonly后执行
# 也可以直接写在etc目录中的证书地址在openresty中
ln -s /etc/letsencrypt/live/ /data/openresty/cert

# 生成的证书列表
certbot certificates
# 删除生成的证书
certbot delete --cert-name <certificate_name_or_domain>
# 刷新证书
certbot renew
```

## 定时任务相关

```
crontab -e
# 输入内容
# ...

# 保存完成后重启
systemctl restart crond
```

## 日志轮转

```
vim /etc/logrotate.d/openresty
```

> 编辑文件时要 `删除#注释`

```
/logs/openresty/*.log {
    daily               # 每天轮转日志
    rotate 7            # 保留7个日志文件
    size 50M            # 当日志文件超过50MB时进行轮转
    compress            # 轮转的日志进行压缩
    missingok           # 如果日志文件不存在，则不报错
    notifempty          # 如果日志为空，不进行轮转
    create 0640 openresty openresty  # 新创建的日志文件权限
}
```

```
# 强制执行，未达到50M也会生成.gz文件
logrotate -f /etc/logrotate.d/openresty
```

# redis

[官网](https://redis.io/) [下载](https://download.redis.io/releases/)

> `redis` # chkconfig: - 50 90

## 安装 & 配置

> 自定义端口修改 `sed -i '139s/6379/1234/' redis.conf`

```
cd /download
wget https://download.redis.io/releases/redis-7.4.2.tar.gz
tar -zxf redis-7.4.2.tar.gz
cd /download/redis-7.4.2
cd deps
make hiredis lua jemalloc linenoise
cd ..
make -j$(nproc)
make PREFIX=/env/redis install
ln -s /env/redis/bin/* /usr/local/bin/
cp /download/redis-7.4.2/redis.conf /fate/redis/redis.conf.bak
cp /download/redis-7.4.2/redis.conf /fate/redis/redis.conf
cd /fate/redis
sed -i '70s/^#\s*//' redis.conf
sed -i '156s/^#\s*//' redis.conf
sed -i '156s/\/run/\/daemon\/redis/' redis.conf
sed -i '157s/^#\s*//' redis.conf
sed -i '310s/no/yes/' redis.conf
sed -i '342s/\/var\/run\/redis_6379.pid/\/daemon\/redis\/redis_6379.pid/' redis.conf
sed -i '356s/""/\/logs\/redis\/redis.log/' redis.conf
sed -i '1050s/^# requirepass foobared/requirepass redis/' redis.conf
sed -i '1085s/^#\s*//' redis.conf
sed -i '$ a\rename-command FLUSHDB ""\nrename-command FLUSHALL ""' redis.conf
```

## 开机自动启动

```
vim /etc/init.d/redis
chmod +x /etc/init.d/redis
chkconfig --add /etc/init.d/redis
chkconfig redis on
```

### /etc/init.d/redis

```
#!/bin/sh
# chkconfig: - 50 90
# description: Redis 服务初始化脚本，用于在系统启动时启动 Redis，并在运行时进行管理

# Increase file descriptor limit
# LimitNOFILE 是控制系统允许每个进程可以打开的最大文件描述符数。增加此限制可以防止 Redis 在处理大量并发连接时遇到 "too many open files" 错误。
# LimitNOFILE=10032 # 无效


# Redis 服务端口
REDISPORT=6379
# Redis 服务可执行文件路径
EXEC=/env/redis/bin/redis-server
# Redis 客户端可执行文件路径
CLIEXEC=/env/redis/bin/redis-cli

# PID 文件路径，用于记录 Redis 服务的进程 ID
PIDFILE="/daemon/redis/redis_${REDISPORT}.pid"
# Redis 配置文件路径
CONF="/fate/redis/redis.conf"
# Redis 服务密码
PASSWORD="redis"

# 根据传入的参数执行相应操作
case "$1" in
    start)
        # 启动 Redis 服务
        if [ -f $PIDFILE ]; then
            echo "$PIDFILE 已存在，进程已经在运行或崩溃"
        else
            # 设置 Redis 所需的文件描述符限制
            ulimit -n 10032
            echo "正在启动 Redis 服务器..."
            $EXEC $CONF --requirepass $PASSWORD
        fi
        ;;
    stop)
        # 停止 Redis 服务
        if [ ! -f $PIDFILE ]; then
            echo "$PIDFILE 不存在，进程未运行"
        else
            PID=$(cat $PIDFILE)
            echo "正在停止 Redis..."
            $CLIEXEC -p $REDISPORT -a $PASSWORD shutdown
            # 等待 Redis 进程完全停止
            while [ -x /proc/${PID} ]; do
                echo "等待 Redis 停止..."
                sleep 1
            done
            echo "Redis 已停止"
        fi
        ;;
    *)
        # 提示正确的使用方法
        echo "请使用 start 或 stop 作为第一个参数"
        ;;
esac
```

## 测试连接

```
redis-server /fate/redis/redis.conf
redis-cli -p 6379
127.0.0.1:6379> AUTH redis
OK
127.0.0.1:6379> ping
PONG
```

# mysql

[官网](https://www.mysql.com/cn/) [下载 8.0.41](https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.41.tar.gz)

> `mysql` # chkconfig: - 55 85

## my.cnf

```
groupadd -r mysql
useradd -r -g mysql -s /sbin/nologin mysql
vim /fate/mysql/my.cnf
```

```
[mysqld]
# performance schema配置
performance-schema = 1
performance-schema-instrument = wait/lock/metadata/sql/mdl=ON
# 启用更严格的权限检查
# 需要在 MySQL 启动时通过 --skip-grant-tables 禁用授权表
skip-grant-tables=0

# 设置 MySQL 安装目录
basedir=/env/mysql
# 设置 MySQL 数据目录
datadir=/data/mysql/data
# 设置 socket 文件路径
socket=/daemon/mysql/mysql.sock
# 限制 LOAD DATA 和 SELECT ... INTO OUTFILE 操作的目录
secure-file-priv=/data/mysql/mysql-files

# 运行 MySQL 的用户
user=mysql

# PID 文件路径
pid-file=/daemon/mysql/mysql.pid
# 最大连接数
max_connections=1000
# 设置线程缓存大小
thread_cache_size = 200  # 根据连接数设置，减少线程创建和销毁的开销
# 设置每个线程的堆栈大小
thread_stack = 192K  # 适当调整

# 设置排序操作的缓冲区大小
sort_buffer_size = 4M  # 调整排序操作的内存缓存大小
# 设置读取数据的缓冲区大小
read_buffer_size = 4M  # 用于扫描大数据表的查询
# 设置表缓存数量
table_open_cache = 1024  # 根据您的表数量和查询频率设置

# 默认字符集和校对规则
character-set-server=utf8mb4
collation-server=utf8mb4_general_ci

# 默认存储引擎
default-storage-engine=INNODB

# SQL 模式
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION

# 错误日志文件路径
log-error=/logs/mysql/mysql-error.log
# 二进制日志文件路径
log-bin=/logs/mysql/mysql-bin.log
# 二进制日志过期时间（7 天）
binlog_expire_logs_seconds=604800

# 慢查询
slow_query_log = 1
slow_query_log_file = /logs/mysql/mysql-slow.log
long_query_time = 2

# InnoDB 配置
innodb_buffer_pool_size=1G # 设置 InnoDB 缓冲池的大小，建议设置为物理内存的 70%-80%（对于数据库服务器）
# innodb_log_file_size=256M # 根据事务量进行调整，mysql8.0以上不支持了，废弃
innodb_redo_log_capacity=1073741824
innodb_flush_log_at_trx_commit=2 # 1 最强的数据安全性，但可能会影响性能，特别是在高并发的环境中 2 性能和数据安全性之间提供了一个平衡点，适合大多数应用场景 0 最高的性能，但牺牲了数据安全性，适合对数据丢失容忍度较高的环境
innodb_file_per_table=1
innodb_flush_method=O_DIRECT
innodb_read_io_threads = 4  # 增加读取线程数
innodb_write_io_threads = 4  # 增加写入线程数

# 接缓冲区的大小，适用于大数据表的连接操作
join_buffer_size = 8M
# 临时表
tmp_table_size = 64M
max_heap_table_size = 64M

default_authentication_plugin=caching_sha2_password
# 禁止root远程登录
# skip-networking # 如果你需要支持远程连接，不要启用 skip-networking
skip-name-resolve # 如果你希望避免 DNS 解析带来的性能开销，并确保所有连接基于 IP 地址，可以启用 skip-name-resolve，但要确保所有权限配置都使用 IP 地址，而不是主机名
# 读写分离
# 对于负载较重的系统，设置读写分离，主库处理写操作，从库处理读操作，可以显著提升性能。
replicate-do-db=db1
read_only=1   # 设置从库为只读
# 密钥策略
# validate-password-policy=STRONG
# validate-password-length=12
# 禁用符号链接 & 禁用 LOAD DATA LOCAL INFILE 功能
# skip-symbolic-links # 不需要显示定义了
local-infile=0
[client]
# 客户端配置
port=3306
socket=/daemon/mysql/mysql.sock

# 包含额外的配置文件
# !includedir /etc/mysql/conf.d/
```

## rpcsvc-proto

```
cd /download
wget https://github.com/thkukuk/rpcsvc-proto/releases/download/v1.4.4/rpcsvc-proto-1.4.4.tar.xz
tar xf rpcsvc-proto-1.4.4.tar.xz
cd rpcsvc-proto-1.4.4/
./configure
make -j$(nproc) && make install
```

## 安装

```
cd /third/mysql
wget https://archives.boost.io/release/1.77.0/source/boost_1_77_0.tar.bz2
tar -xjf /third/mysql/boost_1_77_0.tar.bz2 -C /third/mysql/
yum install openssl-devel rpcgen libtirpc-devel gcc-c++ ncurses-devel cmake libevent-devel lz4-devel libudev-devel bison openldap-devel cyrus-sasl-devel m4 -y
cd /download
wget https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.41.tar.gz
tar -zxf mysql-8.0.41.tar.gz
cd /download/mysql-8.0.41/
mkdir build
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/env/mysql \
         -DMYSQL_DATADIR=/data/mysql/data \
         -DSYSCONFDIR=/fate/mysql \
         -DMYSQL_UNIX_ADDR=/daemon/mysql/mysql.sock \
         -DDEFAULT_CHARSET=utf8mb4 \
         -DDEFAULT_COLLATION=utf8mb4_general_ci \
         -DWITH_MYISAM_STORAGE_ENGINE=1 \
         -DWITH_INNOBASE_STORAGE_ENGINE=1 \
         -DENABLED_LOCAL_INFILE=1 \
         -DMYSQL_TCP_PORT=3306 \
         -DWITH_DEBUG=0 \
         -DWITH_SSL=system \
         -DWITH_SYSTEMD=1 \
         -DMYSQL_MAINTAINER_MODE=0 \
         -DDOWNLOAD_BOOST=1 \
         -DWITH_BOOST=/third/mysql/boost_1_77_0 \
         -DWITH_LZ4=system \
         -DWITH_ZLIB=bundled \
         -DWITH_LIBEVENT=system
make -j$(nproc)
make install
ln -s /env/mysql/bin/* /usr/local/bin
```

## 开机自动启动

```
cp /download/mysql-8.0.41/build/scripts/mysqld.service /etc/systemd/system/mysqld.service
systemctl enable mysqld
```

## 初始化

```
chmod 755 /logs/mysql /data/mysql /data/mysql/data /fate/mysql /daemon/mysql
chown -R mysql:mysql /env/mysql /fate/mysql /data/mysql /logs/mysql /daemon/mysql /data/mysql/mysql-files
chmod 700 /data/mysql/mysql-files
chown -R mysql:mysql /env/mysql /fate/mysql /data/mysql /logs/mysql /daemon/mysql /data/mysql/mysql-files
mysqld --initialize --user=mysql --basedir=/env/mysql --datadir=/data/mysql/data
cat /logs/mysql/mysql-error.log
```

## 配置

```
systemctl start mysqld
mysql -uroot -p
systemctl restart mysqld
```

### sql

> 如何安装 `gitea` 可以创建一个 `gitea的数据库`

```
ALTER USER root@localhost IDENTIFIED WITH caching_sha2_password BY 'your_root_passwd';
update mysql.user set host = 'localhost' WHERE user = 'root' AND host != 'localhost';
create database gitea;
create user 'gitea'@'127.0.0.1' identified by 'your_gitea_passwd';
grant all privileges on gitea.* to 'gitea'@'127.0.0.1';
# 删除权限
# DROP USER 'gitea'@'127.0.0.1';
update mysql.user set Process_priv = 'Y' where user = 'gitea';
flush privileges;
quit;
```
