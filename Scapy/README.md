# 从0到1学习Scapy之路

## 专业术语对照表
English | 中文 | 含义
----|----|----
TTL | 生存时间值（time to live）|该字段指定IP包被路由器丢弃之前允许通过的最大网段数量
network segment|网段|一般指一个计算机网络中使用同一物理层设备（传输介质，中继器，集线器等）能够直接通讯的那一部分

## tutorial
### [Stacking Layers](http://scapy.readthedocs.io/en/latest/usage.html#stacking-layers)
The `/` operator has been used as a composition operator between two layers. When doing so, the lower layer can **have one or more of its defaults fields overloaded according to the upper layer**. (You still can give the value you want). A string can be used as a raw layer.


