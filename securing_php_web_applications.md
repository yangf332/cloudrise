
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

## 变量覆盖漏洞
    变量如果未初始化，且能被用户所控制，可能会有安全问题。在PHP中，register_globals为ON时尤其严重。
    extract(array, [EXTR_OVERWRITE|EXTR_SKIP]),使用EXTR_SKIP以确保变量不被覆盖
    import_request_variables()
    parse_str(), mb_parse_str()

## 认证与会话
    认证 Authentication
    授权 Authorization
    认证的目的是为了认出用户是谁，而授权的目的是为了决定用户能够做什么。
    单因素/多因素认证
    Session Fixation攻击：解决方法是，在登录完成之后，重写SessionID。
    Session保持攻击：
    单点登录：Single Sign On，用户只需要登录一次，就可以访问所有的系统。

## 访问控制
    在Web应用中，分为三种访问控制：
        基于URL
        基于方法
        基于数据
    OAuth：是一个在不提供用户名和密码的情况下，授权第三方应用访问Web资源的安全协议。

## Web框架安全
    

## 网上资料
[linux](http://www.linux.org/ "linux")

