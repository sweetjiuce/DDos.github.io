## 第八章 拒绝服务攻击
### 8.1 拒绝服务攻击
- **要点说明**
    1. 拒绝服务攻击是通过造成IT基础设施的损害或毁坏而导致服务能力丧失的攻击。
    2. 拒绝服务（Dos）耗尽CPU、内存、带宽以及磁盘空间等系统资源，来阻止或削弱对网络、系统或应用程序的授权使用的行为。  
   
**Dos攻击对象-网络带宽**  

网络带宽与连接服务器和因特网的网络链路容量相关。用大量恶意流量发往目标服务器，当这种流量大于目标服务器的可承受量。那么目标服务器就会拒绝合理性的访问。  

**Dos攻击对象-系统资源**  

通过过度加载或者使系统网络处理程序奔溃来实现攻击。利用特殊类型的数据包耗尽服务器上有限的可用系统资源。这些系统资源主要包括接收数据包的临时缓冲区、打开连接表和类似内存的数据结构。另一种攻击方法是使用某些特殊数据包来出发系统的网络处理软件的缺陷，从而导致系统崩溃。例如*有毒数据包*、[死亡之ping](https://baike.baidu.com/item/Ping%20of%20Death/5511153?fr=aladdin)和[泪滴攻击](https://baike.baidu.com/item/%E6%B3%AA%E6%BB%B4%E6%94%BB%E5%87%BB/14204397?fr=aladdin)  

**Dos攻击对象-特定应用服务程序**  

例如web服务器一般采用一定数量的合法请求，而每个请求都会消耗掉服务器的系统资源。Cyberslam攻击就是这种类型的攻击方式。


### 8.1.2 经典的拒绝服务攻击  

**洪泛攻击**  

最简单的经典Dos攻击就是洪泛攻击。洪泛攻击的目标就是占据所有到目标机构的网络连接的容量。如果攻击者能够访问具有大容量网络连接的系统，那么这个系统可能会产生比目标连接容量大得多的通信容量。例如：攻击者可以利用大型公司的Web服务器来攻击较小容量网络连接的中型公司的Web服务器。发送大量的ping包占据中型公司的链路容量。**注意：**ICMP协议会有回包，会携带攻击者的真实ip地址，且攻击者会和被攻击者一样接收到ping包的数量，但由于拥有较高网络带宽，不至于被反ping死。  

**源地址欺骗**  

所谓源地址欺骗，就是数据包的源地址是伪造的。由于历史兼容性和继承性，很多操作系统保留着原始套接字接口（raw socket interface）使得攻击者很容易产生伪造源地址的数据包。但拥有这些权限之后，攻击者可以很轻易的制造出大量的目的地址指向目标系统的数据包，但源地址是随机选择的。例如当发送大量的ping包之后，ICMP的回包并不会回到攻击者的主机中，而是散发在网络的各地。这些包或许被丢掉，或许到达了真实的主机中。

**SYN欺骗** 

SYN欺骗攻击通过造成服务器上用于管理TCP连接的链接表溢出，从而攻击网络服务器响应TCP连接请求的能力。意味着合法用户的TCP连接请求将得不到服务器的响应。那么SYN是如何做到的呢？回顾一下三次TCP三次握手。客户端发送SYN连接给客户端，初始序号为q，服务器端在TCP连接表中记录这个连接请求，接着用SYN-ACK数据包来响应客户端，同时发送服务器端的序号，发送客户端的序号+1，代表已经收到请求。客户端收到回包之后，发送服务器端序号+1。代表已经连接。


### UDP洪泛

攻击者也可以用UDP进行攻击，UDP数据包被发送到目标系统提供服务的端口上。

## 分布式拒绝服务攻击


攻击者通过系统漏洞控制大量主机，称为僵尸机。用这些僵尸机组成僵尸网络，对网络链路发起攻击。著名的例子有TFN。
    1. **反射攻击**  
        攻击者将其想攻击的目标系统地址作为数据包的源地址，并将这些数据包发送到中间媒介的已知网络服务。大量的响应数据包会被发送给源地址锁指向的目标系统。
    2. **放大攻击**
        放大攻击是反射攻击的变种。








