---
title: laravel
date: 2017-09-26 10:55:15
tags:
---
有关mac laravel项目的搭建
### 1.服务器环境
```html
PHP >= 7.0.0
PHP OpenSSL 扩展
PHP PDO 扩展
PHP Mbstring 扩展
PHP Tokenizer 扩展
PHP XML 扩展
```
### 2.环境安装
```html
安装依赖 PHP7
     brew tap homebrew/php（如能搜到php71可忽略）
     brew install  php71  php71-mcrypt
     brew link php71 （设置当前环境所有 php 使用 php7）
 
启动 PHP-FPM
     brew services start php71
安装 Nginx
     brew  install nginx  （已有忽略）
安装 Composer (依赖包管理器)
     brew install composer
```
### 3.安装 Laravel 安装器
```html
composer global require "laravel/installer"
```
### 4.添加环境变量
```html
 export PATH="$HOME/.composer/vendor/bin:$PATH"
```
### 5.新建项目
```html
 laravel new blog    (新建项目名称叫 blog 并且在当前目录下生成 blog 文件夹)
```
### 6.Copy 项目目录下的 .env.example 文件为 .env
```html
 cp .env.example .env
```
### 7.设置应用程序密钥
```html
在你安装完 Laravel 后，首先需要做的事情是设置一个随机字符串的密钥。假设你是通过 Composer 或是 Laravel 安装工具安装的 Laravel，那么这个密钥已经通过 key:generate 命令帮你设置完成。通常这个密钥会有 32 字符长。这个密钥可以被设置在 .env 环境文件中。如果你还没将 .env.example 文件重命名为 .env，那么你现在应该去设置下。
如果应用程序密钥没有被设置的话，你的用户 Session 和其它的加密数据都是不安全的！
命令：php artisan key:generate
```
### 8.Nginx 配置规则
```base
server
{
    # 端口  80 小端口需要 root 启动 Nginx ，大端口 如 8080 不需要 root
    listen          80;
    # host  域名
    server_name     admin.cloud.51idc.com;
    # 目录 (注意：是项目目录下的 public 目录)
    root            /Users/eagle/workspace/ xx/public;
    index           index.php;
    # 伪静态规则（必须含有）
    try_files       $uri /index.php$is_args$query_string;
    location ~ \.php$ {
        try_files                   $uri = 404;
        fastcgi_split_path_info     ^(.+\.php)(/.+)$;
        fastcgi_connect_timeout     30s;
        fastcgi_read_timeout        100s;
        fastcgi_pass                127.0.0.1:9000;
        fastcgi_param               SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        fastcgi_param               SCRIPT_NAME $fastcgi_script_name;
        include                     fastcgi_params;
    }
}
```
### 9.启动 Nginx 或者 重启 Nginx
```base
sudo nginx -s reload
or
brew services start nginx
or
brew services restart nginx

```
### 10.修改hosts
### 11.浏览域名
### 12.[模板使用说明](http://laravelacademy.org/post/5919.html)
### 13.[视图调用方法](http://laravelacademy.org/post/5908.html)
### 14.[安装说明](http://laravelacademy.org/post/5744.html)
### 15.安装问题说明
```html
cross-env: command not found
解决方案：
cross-env是跨平台的环境变量，需要安装这个环境
npm install cross-env --save-dev
```
### 16配置出现问题
```html
.events.js:160
      throw er; // Unhandled 'error' event
      ^

Error: spawn node_modules/webpack/bin/webpack.js ENOENT
    at exports._errnoException (util.js:1026:11)
    解决方案：
    rm -rf node_modules
    rm package-lock.json
    cnpm cache clear --force
    cnpm install
```
