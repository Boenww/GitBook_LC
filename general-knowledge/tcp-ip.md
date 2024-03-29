# Network

### 访问Web URL，发生了什么？

1. 域名解析：通过域名查找IP
2. TCP handshake + TLS handshake if required (非对称加密交换密钥+对称加密交换数据)
3. 发送HTTP请求
4. 服务器处理请求并返回结果
5. 断开连接

**域名解析**：浏览器缓存->系统缓存->路由器缓存（客户端DNS缓存结束）->本地DNS服务器（网络接入服务商提供，e.g. 电信移动）->根域名服务器->顶级域名服务器（e.g. .com域服务器）->主域名服务器

<figure><img src="../.gitbook/assets/dns.jpeg" alt=""><figcaption></figcaption></figure>

### TCP handshake

<figure><img src="../.gitbook/assets/tcp-3.png" alt=""><figcaption></figcaption></figure>

### why need 3-way handshake for TCP?

为了防止server端收到已经失效的连接请求报文段而建立连接后一直等待，浪费资源。

### 4-way bye

<figure><img src="../.gitbook/assets/tcp-4.png" alt=""><figcaption></figcaption></figure>

TIME\_WAIT

* 确保最后一个确认报文段能够到达。如果B没收到A发送来的ACK，就会重新发送FIN。
* 为了让本连接持续时间内所产生的所有报文段从网络中消失，使下一个连接不会出现旧的报文段。





ARP协议查询2层MAC地址

<figure><img src="../.gitbook/assets/ARP.png" alt=""><figcaption></figcaption></figure>

网卡驱动控制网卡将网络包复制到网卡缓存区内并封装后，转为电信号通过网线发送出去。电信号到达网线接口后，交换机里的模块进行接受，将其从电信号转回数字信号。再转发到路由器，然后路由表查询转发目标，把以太网包发给下一个路由器，最后跳到相应端口的路由器。



<figure><img src="../.gitbook/assets/网络报文封装.png" alt=""><figcaption><p>网络报文封装</p></figcaption></figure>

### HTTPS

<figure><img src="../.gitbook/assets/How-HTTPS-Works2.png" alt=""><figcaption></figcaption></figure>

##

## RPC vs REST

|      | RPC                                                                                   | RESTful                                                                    |
| ---- | ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| 优点   | <p>- 高性能和效率</p><p>- 丰富的数据类型支持</p><p>- 明确的接口定义</p><p>- 强调服务调用</p><p>- 支持多种协议和传输方式</p>  | <p>- 简单和易于理解</p><p>- 基于标准的HTTP协议</p><p>- 松散耦合的架构</p><p>- 可缓存和可伸缩</p>       |
| 缺点   | <p>- 需要事先定义接口和数据结构</p><p>- 对编程语言和平台有依赖</p><p>- 较为复杂的部署和维护</p><p>- 不适用于浏览器和Web应用程序</p> | <p>- 缺乏标准化的接口定义</p><p>- 传输开销较大</p><p>- 不支持丰富的数据类型</p><p>- 不适合强调服务调用的场景</p> |
| 适用场景 | <p>- 分布式系统间的高性能通信</p><p>- 服务间的远程调用</p><p>- 复杂的业务逻辑和数据处理</p>                           | <p>- Web应用程序的前后端通信</p><p>- 资源的增删改查操作</p><p>- 轻量级和简单的交互</p>                 |

### cookie & session

web应用程序中用来跟踪用户状态和存储用户数据的机制。

