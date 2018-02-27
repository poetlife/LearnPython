# 从0到1学习Scapy之路

## 常识
1. HTTP HEADER 约定以 \r\n\r\n 结尾
## 专业术语对照表
English | 中文 | 含义
----|----|----
TTL | 生存时间值（time to live）|该字段指定IP包被路由器丢弃之前允许通过的最大网段数量
network segment|网段|一般指一个计算机网络中使用同一物理层设备（传输介质，中继器，集线器等）能够直接通讯的那一部分
EtherNet|以太网|以太网(Ethernet)指的是由Xerox公司创建并由Xerox、Intel和DEC公司联合开发的基带局域网规范，是当今现有局域网采用的最通用的通信协议标准。
ICMP | Internet Control Message Protocol |它是TCP/IP协议族的一个子协议，用于在IP主机、路由器之间传递控制消息。控制消息是指网络通不通、主机是否可达、路由是否可用等网络本身的消息。
SYN| Synchronous|SYN（synchronous）是TCP/IP建立连接时使用的握手信号。在客户机和服务器之间建立正常的TCP网络连接时，客户机首先发出一个SYN消息，服务器使用SYN+ACK应答表示接收到了这个消息，最后客户机再以ACK消息响应。
gateway| 网关|网关(Gateway)又称网间连接器、协议转换器。网关在网络层以上实现网络互连，是最复杂的网络互连设备，仅用于两个高层协议不同的网络互连。
MAC|Media Access Control介质访问控制层|它定义了数据帧怎样在介质上进行传输。在共享同一个带宽的链路中，对连接介质的访问是“先来先服务”的。
ARP| Address Resolution Protocol地址解析协议|主机发送信息时将包含目标IP地址的ARP请求广播到网络上的所有主机，并接收返回消息，以此确定目标的物理地址；收到返回消息后将该IP地址和物理地址存入本机ARP缓存中并保留一定时间，下次请求时直接查询ARP缓存以节约资源。
TLS |Transport Layer Security安全层传输协议|安全传输层协议（TLS）用于在两个通信应用程序之间提供保密性和数据完整性。该协议由两层组成： TLS 记录协议（TLS Record）和 TLS 握手协议（TLS Handshake）。较低的层为 TLS 记录协议，位于某个可靠的传输协议（例如 TCP）上面，与具体的应用无关，所以，一般把TLS协议归为传输层安全协议。 

## tutorial
### [Stacking Layers](http://scapy.readthedocs.io/en/latest/usage.html#stacking-layers)
The `/` operator has been used as a composition operator between two layers. When doing so, the lower layer can **have one or more of its defaults fields overloaded according to the upper layer**. (You still can give the value you want). A string can be used as a raw layer.
![figure](http://scapy.readthedocs.io/en/latest/_images/fieldsmanagement.png)  
Each packet can be build or **dissected** (note: in Python _ (underscore) is the latest result):
```
>>> raw(IP())
b'E\x00\x00\x14\x00\x01\x00\x00@\x00|\xe7\x7f\x00\x00\x01\x7f\x00\x00\x01'
>>> IP()
<IP  |>
>>> raw(IP()/TCP())
b'E\x00\x00(\x00\x01\x00\x00@\x06|\xcd\x7f\x00\x00\x01\x7f\x00\x00\x01\x00\x14\x00P\x00\x00\x00\x00\x00\x00\x00\x00P\x02 \x00\x91|\x00\x00'
>>> IP()/TCP()
<IP  frag=0 proto=tcp |<TCP  |>>
>>> IP(_)
<IP  version=4 ihl=5 tos=0x0 len=40 id=1 flags= frag=0 ttl=64 proto=tcp chksum=0x7ccd src=127.0.0.1 dst=127.0.0.1 options=[] |<TCP  sport=ftp_data dport=http seq=0 ack=0 dataofs=5 reserved=0 flags=S window=8192 chksum=0x917c urgptr=0 |>>
```

