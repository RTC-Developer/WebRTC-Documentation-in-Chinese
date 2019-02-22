
#### [6.1.1.2 Update max message size](http://w3c.github.io/webrtc-pc/#update-max-message-size)

To update the data max message size of an  RTCSctpTransport run the following steps:

zh:要更新RTCSctpTransport的数据最大邮件大小，请运行以下步骤：

1.  Let transport be the RTCSctpTransport  object to be updated. 
zh: 让transport成为要更新的RTCSctpTransport对象。

2.  Let remoteMaxMessageSize be the value of the "max-message-size" SDP attribute read from the remote description, as described in [SCTP-SDP] (section 6), or 65536 if the attribute is missing. 
zh: 令remoteMaxMessageSize为从远程描述中读取的“max-message-size”SDP属性的值，如[SCTP-SDP]（第6节）中所述，如果缺少该属性，则为65536。

3.  Let canSendSize be the number of bytes that this client can send (i.e. the size of the local send buffer) or 0 if the implementation can handle messages of any size. 
zh: 令canSendSize是此客户端可以发送的字节数（即本地发送缓冲区的大小），如果实现可以处理任何大小的消息，则为0。

4.  If both remoteMaxMessageSize and canSendSize are 0, set [[MaxMessageSize]] to the positive Infinity value. 
zh: 如果remoteMaxMessageSize和canSendSize都为0，则将[[MaxMessageSize]]设置为正无穷大值。

5.  Else, if either remoteMaxMessageSize or canSendSize is 0, set [[MaxMessageSize]] to the larger of the two. 
zh: 否则，如果remoteMaxMessageSize或canSendSize为0，则将[[MaxMessageSize]]设置为两者中较大的一个。

6.  Else, set [[MaxMessageSize]] to the smaller of remoteMaxMessageSize or canSendSize. 
zh: 否则，将[[MaxMessageSize]]设置为remoteMaxMessageSize或canSendSize中较小的一个。