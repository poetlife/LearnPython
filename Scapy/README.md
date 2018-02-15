# 从0到1学习Scapy之路

## 常识
1. HTTP HEADER 约定以 \r\n\r\n 结尾
## 专业术语对照表
English | 中文 | 含义
----|----|----
TTL | 生存时间值（time to live）|该字段指定IP包被路由器丢弃之前允许通过的最大网段数量
network segment|网段|一般指一个计算机网络中使用同一物理层设备（传输介质，中继器，集线器等）能够直接通讯的那一部分

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

