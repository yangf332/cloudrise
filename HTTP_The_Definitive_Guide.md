
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

### 方法

    1. GET - 通常用于请求服务器发送某个资源
    2. HEAD - 类似GET，但在响应中只返回首部，没有实体部分。用于检查：资源情况、对象是否存在、资源是否被个性等
    3. PUT - 用于在服务器上写入文档
    4. POST - 向服务器输入数据
    5. TRACE - 查看请求通过节点时是否发生改变
    6. OPTIONS - 请求服务器告知支持哪些方法
    7. DELETE  - 删除指定资源

  扩展方法： HTTP是字段可扩展的，扩展方法指没有在HTTP/1.1规范中定义的方法。

### 状态码

    100～199 信息性状态码
      100 Continue - 用于优化以下情况：客户端要向服务端发送一个实体的主体部分，但希望在发送之前查看下服务器是否接受此实体。
    200～299 成功状态码
    300～399 重定向状态码
      304 Not Modified 重定向为使用本地副本
    400～499 客户端错误状态码
      404 Not Found 客户端请求资源不存在或错误
    500～599 服务器错误状态码

  
## 第4章 连接管理

### TCP连接

  TCP为HTTP提供了一条可靠（按序、无差错）的比特传输管道。

  TCP流是分段的、由IP分组传送。TCP通过端口号保持所有连接的正确性。
  

## 其它
    1. boundary 上传文件
    POST URL HTTP/1.1
    Content-Type:multipart/form-data;boundary=----------------------------7db372eb000e2
    Content-Length: n
    ----------------------------7db372eb000e2
    Content-Disposition: form-data; name="file"; filename="kn.jpg"
    Content-Type: image/jpeg
    (此处省略jpeg文件二进制数据...）
    -------------------------------7db372eb000e2--
    Form每个部分用分隔符分割，分隔符之前必须加上"--"着两个字符(即--{boundary})才能被http协议认为是Form的分隔符，表示结束的话用在正确的分隔符后面添加"--"表示结束。

## 网上资料
[上传文件报文](http://www.cnblogs.com/liangbin/articles/2117288.html "上传文件报文")