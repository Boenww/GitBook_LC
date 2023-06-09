# Network

访问Web URL，发生了什么？

1. 域名解析：通过域名查找IP
2. TCP handshake
3. 发送HTTP请求
4. 服务器处理请求并返回结果
5. 断开连接



why need 3-way handshake for TCP?

为了防止server端收到已经失效的连接请求报文段而建立连接后一直等待，浪费资源。



