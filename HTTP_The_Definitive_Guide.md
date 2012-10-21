
HTTP权威指南
============================

## 第一章 HTTP概述

### 客户端与服务器端如何通信？
    客户端（一般是浏览器）向服务器发送HTTP请求，服务器寻找期望的资源对象，
    如果成功，就将对象、对象类型、对象长度以及其它信息一并发还。

### 资源

    Web服务器上保存的静态文件及程序动态生成的Web内容,以媒体类型（MIME type）区分不同的类型
    
    + URI (统一资源标识符：Uniform Resource Identifier)
        1. URL: 统一资源定位符，分为方案（scheme协议类型）、网址和资源名称
        2. URN: 统一资源名，唯一名称，与资源所在地无关，这样资源可以随意移动而不影响访问。
       处于实验阶段

### 事务

    由一条请求命令和响应结果组成。通信通过名为HTTP报文的格式化数据块进行。

    * 方法：HTTP支持几种不同的请求命令，常见的如get,post,put,delete,head
    * 状态码：描述响应结果的数字码
    * 报文：纯文本
        1. 起始行
        2. 首部（head）
        3. 主体

### 连接
    
    报文通过TCP连接进行传输。

### Web系统结构组件
    * 代理
    * 缓存
    * 网关
    * 隧道
    * Agent代理


## 第二章 URL与资源

URL格式：

    scheme://user:password@host:port/path;params?query#frag
    最重要的是 方案://服务器位置/路径

URL快捷方式：相对URL

字符问题：

## 第三章 HTTP报文

HTTP报文是传递信息的包

HTTP报文像河水一样流动。术语流入（inbound）和流出（outbound），上游（upstream）和下游（downstream）用来描述流动的方向。

### 报文的组成部分

简单的文本格式。分为三个部分

    1. start line : HTTP/1.0 200 ok
    2. header     : Content-type:text/plain Content-length:19   
    3. body       : Hi! I'm a message!

每个部分间用一个回车符（ASCII 13）和一个换行符（ASCII 10）结束。但要注意老的HTTP应用可能并不发送结束符。

### 报文的语法

所有报文都可以分为请求报文（request message）和响应报文（response message）。两者结构相同。
 
    请求报文
    GET /specials/saw-blade.gif HTTP/1.0
    Host: www.xxxx.com

    响应报文
    HTTP/1.0 200 OK
    Content-Type: image/gif
    Content-Length: 8888

这里面包含了：方法（method）、请求URL（request-URL）、版本（version）、状态码（status-code）、原因短语（reason-phrase）、首部（header）、实体的主体部分（entity-body）

### 起始行（start line）

请求报文的起始行说明了__要做什么__，而响应报文的起始行说明了__发生了什么__

1. 



  