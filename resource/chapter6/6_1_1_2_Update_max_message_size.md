
#### 6.1.1.2 更新最大信息容量

为了更新`RTCSCTPTransport`的数据最大信息容量，运行下列步骤：

1.让transport成为用来更新的`RTCSCTPTransport`对象。

2.让`remoeteMaxMessageSize`成为从远程描述中获取的"max-message-size"SDP属性的值，如[SCTP-SDP]中所述，或65536如果属性缺失。

3.让`canSendSize`成为客户端可发送的字节数(本地发送buffer的大小)，如果可以处理任意大小的信息，则设置为0。

4.如果`remoteMaxMessageSize`和`canSendSize`都为0，设置[MaxMessageSize]为正无穷。

5.否则，如果`remoteMaxMessageSize`与`canSendSize`有一个为0，设置[MaxMessageSize]为两者较大值。

6.否则，设置[MaxMessageSize]为两者较小值。
