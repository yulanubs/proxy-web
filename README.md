# proxyWebApplication
proxyWebApplication是以[snail007/goproxy](https://github.com/snail007/goproxy/)为基础服务，完成的网页可视化应用。

---
[![stable](https://img.shields.io/badge/stable-stable-green.svg)](https://github.com/snail007/goproxy/)

### 使用前须知
 - [下载](#下载)
 - [目录位置](#目录位置)
 - [依赖包](#依赖包)
 
### 手册目录
- [1. 运行](#1运行)
- [2. 参数介绍](#2参数介绍)
     - [2.1 http参数](#21http参数)
     - [2.2 tcp参数](#22tcp参数)
     - [2.3 udp参数](#23udp参数)
     - [2.4 socks参数](#24socks参数)
     - [2.5 tclient参数](#25tclient参数)
     - [2.6 tserver参数](#26tserver参数)
     - [2.7 tbridge参数](#27tbridge参数)
 
### 下载
暂时没有 
  

### 目录位置
下载[snail007/goproxy](https://github.com/snail007/goproxy/releases)  
在与proxyWebApplication平级的目录下建proxyService目录  
压缩包解压  
加密文件默认在proxyService/.cert/目录里  
也可在config里修改目录路径  

### 依赖包
[github.com/mattn/go-sqlite3](https://github.com/mattn/go-sqlite3)使用sqlite作为数据库  
[github.com/Unknwon/goconfig](https://github.com/Unknwon/goconfig)解析配置文件  

### 1.运行
然后用8080端口在浏览器进入，如localhost:8080
<img src="https://github.com/yincongcyincong/proxyWebApplication/raw/master/docs-images/preview.png?raw=true" /> 
  
### 2.参数介绍
代理协议：需要用到的协议 如http， tcp等协议。  
本次链接类型：-t参数。  
链式代理：区分此次链接类型，顶级代理不需要“上级服务器+端口”。  
代理服务器+端口：-p参数。  
上级服务器+端口：-P参数。  
父级连接类型：-T参数 选取后可能会有不同的加密方式，上传文件的加密方式会有默认文件，tcp形式默认不加密。 

#### **2.1.http参数** 
tls形式加密：-C .crt文件 和 -K参数 .key文件  
ssh形式加密：有密钥和密码两种方式，-u用户名 -A密码 -S .key文件  
kcp形式加密：-B密码  
<img src="https://github.com/yincongcyincong/proxyWebApplication/raw/master/docs-images/http1.png?raw=true" />  
`path to proxy/proxy http -t tcp -p :8081`  
<img src="https://github.com/yincongcyincong/proxyWebApplication/raw/master/docs-images/http2.png?raw=true" /> 
`path to proxy/proxy http -t tls -p :8081 -T tls -P 2.2.2.2:8081 -C path to file/proxy.crt -K path to file/proxy.key`  

#### **2.2.tcp参数** 
tls形式加密：-C .crt文件 和 -K参数 .key文件  
kcp形式加密：-B密码  
<img src="https://github.com/yincongcyincong/proxyWebApplication/raw/master/docs-images/tcp1.png?raw=true" /> 
`path to proxy/proxy tcp -t tls -p :8081 -T tls -P 2.2.2.2:8081 -C path to file/proxy.crt -K path to file/proxy.key`  

#### **2.3.udp参数** 
没有加密模式  
“本次链接类型”只有udp模式  
<img src="https://github.com/yincongcyincong/proxyWebApplication/raw/master/docs-images/tcp1.png?raw=true" /> 
`path to proxy/proxy udp -p :8081 -T tls -P 2.2.2.2:8081 -C path to file/proxy.crt -K path to file/proxy.key`

#### **2.4.socks参数** 
tls形式加密：-C .crt文件 和 -K参数 .key文件  
ssh形式加密：有密钥和密码两种方式，-u用户名 -A密码 -S .key文件  
kcp形式加密：-B密码  
<img src="https://github.com/yincongcyincong/proxyWebApplication/raw/master/docs-images/socks.png?raw=true" /> 
`path to proxy/proxy socks -t tcp -p :8081 -T kcp -P 2.2.2.2:8081 -B 1234 `

#### **2.5.tclient参数** 
只有tls形式的机密且必须加密  
tls形式加密：-C .crt文件 和 -K参数 .key文件 
<img src="https://github.com/yincongcyincong/proxyWebApplication/raw/master/docs-images/tclient.png?raw=true" /> 
`path to proxy/proxy tclient -P ":8081" -C path to file/proxy.crt -K path to file/proxy.key `  
“上级服务器+接口”填写的内容无效

#### **2.6.tserver参数** 
只有tls形式的机密且必须加密  
tls形式加密：-C .crt文件 和 -K参数 .key文件  
“代理服务器+端口”填写-r参数  
<img src="https://github.com/yincongcyincong/proxyWebApplication/raw/master/docs-images/tserver.png?raw=true" /> 
`path to proxy/proxy tserver -r "udp://:10053@:53" -P "2.2.2.2:8081" -C path to file/proxy.crt -K path to file/proxy.key`

#### **2.7.tbridge参数** 
只有tls形式的机密且必须加密  
tls形式加密：-C .crt文件 和 -K参数 .key文件  
<img src="https://github.com/yincongcyincong/proxyWebApplication/raw/master/docs-images/tbridge.png?raw=true" /> 
`path to proxy/proxy tbridge -P ":8081" -C path to file/proxy.crt -K path to file/proxy.key `  
“上级服务器+接口”填写的内容无效  

### 源码使用  
- git下载源码  
- 配置文件在config  
- 端口在server/server.go  
   
### TODO
- -L参数进程池  
- tserver -r参数分解  

### License
- under GPLv3 license  

### Contact
- QQ群：189618940