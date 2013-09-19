
PHP应用程序安全编程
============================

## 六 文件系统访问
    如果允许用户上传文件，必须考虑放在特定的目录中，并将文件路径封装，防止用户访问系统文件，如：
        /etc/passwd，处理/www/uploaded_files/etc/passwd，不存在
    防止远程文件系统漏洞：禁用php.ini的allow_url_fopen。
    如果需要访问远程文件：使用FTP获取文件，保存后使用文件数据

## 网上资料
[linux](http://www.linux.org/ "linux")

