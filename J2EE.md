[TOC]

## 基本概念

**什么是web应用程序？**

Web应用程序是一种可以通过Web访问的应用程序，程序的最大好处是用户很容易访问应用程序，用户只需要有浏览器即可，不需要再安装其他软件。
> B/S架构，C/S架构

**浏览器和servlet通信使用的是什么协议？**

浏览器和Servlet通信使用的是HTTP协议。

**URL编码和URL解码**

URL只能使用英文字母、阿拉伯数字和某些标点符号，不能使用其他文字和符号，
URL编码通常也被称为百分号编码，使用%加上两位的字符“0123456789ABCDEF”代表一个字节的十六进制形式。URL编码将每一个非安全的ASCII字符都被替换为“%xx”格式。
> JS：encodeURI和decodeURI（部分编码）、encodeURIComponent和decodeURIComponent（全部编码）
> Java：URLEncoder.encode和URLEncoder.decode

**GET与POST**

GET和POST是http协议的两种方法，GET只有一个流，参数附加在url后，大小个数有严格限制且只能是字符串，安全性较低。post的参数是通过另外的流传递的，可以很大，也可以传递二进制数据，安全性较高。

**HTTPS和HTTP的区别**

https协议需要到CA申请证书，一般免费证书较少。
http是超文本传输协议，信息是明文传输，https则是SSL+HTTP协议构成的加密传输协议，更加安全。
http默认端口号80，https默认端口号443。

## API

**Servlet、Filter和Listener的区别**

Servlet职责是接受请求、处理请求、响应数据。
Filter职责是对请求或响应做一些通用的处理，所以一个Filter可以拦截多个请求。
Listener职责是监听Application、Session、Request的事件。

**什么是Servlet**

Java编写的服务器端程序，主要功能在于交互式地浏览和修改数据，生成动态Web内容。

**servlet生命周期**

init（初始化）、service（处理请求）、destroy（销毁）、垃圾回收器回收

**doGet方法和doPost方法的区别**

doGet方法和doPost方法分别处理GET和POST方法。

**forword和redirect的区别**

forword表示转发，客户端和浏览器只发出一次请求，Servlet、HTML、JSP或其它信息资源，由第二个信息资源响应该请求，在请求对象request中，保存的对象对于每个信息资源是共享的。
redirect表示重定向，实际是两次HTTP请求，服务器端在响应第一次请求的时候，让浏览器再向另外一个URL发出请求，从而达到转发的目的。

**什么是servlet链（Servlet Chaining）**

责任链模式

**什么是JSP**

JSP全名为Java Server Pages（Java服务器页面），它在传统的HTML中插入Java代码，其根本是一个简化的Servlet设计。

**JSP九大隐式对象和四大作用域**

request、response、out、session、application、config、pageContext、page、exception
page、request、session、application

**什么是cookie? session和cookie的区别**

Cookie是Web服务器发送给浏览器的一块信息。浏览器会在本地文件中给每一个Web服务器存储cookie。以后浏览器在给特定的Web服务器发请求的时候，同时会发送所有为该服务器存储的cookie。
Cookie通过在客户端记录信息确定用户身份，Session通过在服务器端记录信息确定用户身份。

**Session失效有哪几种方法,session的过期时间默认是多少？在哪里配置？**

服务器关闭（如果是正常关闭，应用服务器会做持久化）、Session过期、Session.removeAttribute()
默认30分钟
```xml
<web-app>
    <session-config>
        <session-timeout>15</session-timeout>
    </session-config>
</web-app>
```

**Request和Session的区别**

Request表示客户端的一次请求，携带客户端的传入的数据，可以看作局部变量。
Session表示客户端的生命周期，携带客户端的数据，可以看作全局变量。

## 解决方案

**常用的防止页面重复提交的方式**

禁用提交按钮：当用户提交表单之后，使用JS隐藏或禁用提交按钮。
session令牌：每次访问页面为表单分配唯一的随机标识号，同时在用户的Session中保存这个标识号。当提交表单时，服务器比较客户端的标识号。

**服务端获取客户端的ip地址**

```java
public static String getIp(HttpServletRequest request) {
           String ip = request.getHeader("X-Forwarded-For");
           if(StringUtils.isNotEmpty(ip) && !"unKnown".equalsIgnoreCase(ip)){
               //多次反向代理后会有多个ip值，第一个ip才是真实ip
               int index = ip.indexOf(",");
               if(index != -1){
                   return ip.substring(0,index);
               }else{
                   return ip;
               }
           }
           ip = request.getHeader("X-Real-IP");
           if(StringUtils.isNotEmpty(ip) && !"unKnown".equalsIgnoreCase(ip)){
               return ip;
           }
           return request.getRemoteAddr();
       }
```