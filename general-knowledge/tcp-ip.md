# Network

访问Web URL，发生了什么？

1. 域名解析：通过域名查找IP
2. TCP handshake + TLS handshake if required (非对称加密交换密钥+对称加密交换数据)
3. 发送HTTP请求
4. 服务器处理请求并返回结果
5. 断开连接



why need 3-way handshake for TCP?

为了防止server端收到已经失效的连接请求报文段而建立连接后一直等待，浪费资源。



ARP协议查询2层MAC地址

<figure><img src="../.gitbook/assets/ARP.png" alt=""><figcaption></figcaption></figure>

网卡驱动控制网卡将网络包复制到网卡缓存区内并封装后，转为电信号通过网线发送出去。电信号到达网线接口后，交换机里的模块进行接受，将其从电信号转回数字信号。再转发到路由器，然后路由表查询转发目标，把以太网包发给下一个路由器，最后跳到相应端口的路由器。



<figure><img src="../.gitbook/assets/网络报文封装.png" alt=""><figcaption><p>网络报文封装</p></figcaption></figure>

