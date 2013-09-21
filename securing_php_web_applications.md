
PHP应用程序安全编程
============================

## 二 处理错误
    striptags()
	htmlentities(), htmlspecialchars()

## 三 系统调用
    exec(),system()及backtick的风险

## 四 缓冲区溢出和变量整理


## 六 文件系统访问
    如果允许用户上传文件，必须考虑放在特定的目录中，并将文件路径封装，防止用户访问系统文件，如：
        /etc/passwd，处理/www/uploaded_files/etc/passwd，不存在
    防止远程文件系统漏洞：禁用php.ini的allow_url_fopen。
    如果需要访问远程文件：使用FTP获取文件，保存后使用文件数据

## 七 身份验证

## 九 会话安全性

## 十 跨站式脚本编程
    XSS：反射式、存储式

## 文件包含漏洞
    include(), require(), include_once(), require_once()
    当这些函数包含一些新文件时，该文件将作为PHP代码执行，PHP内核并不会在意被包含的文件是什么类型。即使被包含的是txt、图片或远程URL，也都将作为PHP代码执行。
    解决方案：配置open_basedir
    1) Apache httpd.conf Directory php_admin_value open_basedir /usr/local/apache/htdocs/
    2) Apache httpd.conf VirtualHost php_admin_value open_basedir /usr/local/apache/htdocs/ 不建议
	3）php.ini open_basedir = ''


## 网上资料
[linux](http://www.linux.org/ "linux")

