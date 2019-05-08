## 6.1 RTCPeerConnection 接口扩展

对等数据API对RTCPeerConnection接口的扩展如下。

```java
partial interface RTCPeerConnection {
    readonly        attribute RTCSctpTransport? sctp;
    RTCDataChannel createDataChannel (USVString label, optional RTCDataChannelInit dataChannelDict);
                    attribute EventHandler      ondatachannel;
};
```

**属性**

`RTCSctpTransport`类型的`sctp`，只读，可以为null,[测试](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCIceTransport.html)：SCTP数据通过SCTP传输发送和接收。如果SCTP还未经过协商，值为null。此属性必须返回存储在[SctpTransport]内部插槽的`RTCSctpTransport`对象。

`EventHandler`类型的`ondatachannel`,[测试](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCPeerConnection-ondatachannel.html)：此event handler的事件类型是`datachannel`。



**方法**

`createDataChannel`

以给定标签创建一个新的`RTCDataChannel`对象。`RTCDataChannelInit`字典可以被用来配置底层通道属性，例如数据可靠性。

当`createDataChannel`方法被调用时，用户代理必须运行下列步骤。

1.让`connection`成为用来调用方法的`RTCPeerConnection`对象。

2.如果`connection`的[IsClosed]插槽为`true`，抛出一个`InvalidStateError`。[测试](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCPeerConnection-createDataChannel.html)

3.创建一个`RTCDataChannel`,channel。

4.初始化channel的[DataChannelLable]插槽为第一个参数的值。

5.如果[DataChannelLabel]长度大于65535bytes,抛出`TypeError`。

6.让options成为第二个参数。

7.初始化channels的[MaxPacketLifeTime]插槽为option的`maxPacketLifeTime`成员，如果存在，否则为`null`。

8.初始化channel的[MaxRetransmits]插槽为option的`maxRetransmits`成员，如果存在，否则为`null`。

9.初始化channel的[Ordered]插槽为option的`ordered`成员。

10.初始化channel的[DataChannelProtocol]插槽为option的`protocol`成员。

11.如果[DataChannelProtocol]长度大于65535bytes，抛出`TypeError`。

12.初始化channel的[Negotiated]插槽为option的`negotiated`成员。

13.初始化channel的[DataChannelId]插槽为option的`id`成员的值，如果存在并且[Negotiated]为`true`，否则为`null`。

> NOTE:这意味着如果数据通道在带内协商，id成员将会被忽略。这是有意的。数据通道带内协商应该基于DTLS角色选择ID，如[RTCWEB-DATA-PROTOCOL]中所述。

14.如果[Negotiated]为`true`，并且[DataChannelId]为`null`，抛出`TypeError`。

15.初始化channel的[DATAChannelPriority]插槽为option的`priority`成员。

16.如果[MaxPacketLifeTime]和[MaxRetransmits]属性都被设置(不为null)，抛出`TypeError`。

17.如果一个设置，或是[MaxPacketLifeTime],或是[MaxRetransmits]已经被设置用来表示不可靠模式，并且它的值超过了用户代理支持的最大值，此数值必须被设置为用户代理最大值。

18.如果[DataChannelId]等于65535，比最大允许ID65534长，但是仍然是无符号short值，抛出`TypeError`。

19.如果[DataChannelId]插槽为`null`（由于没有ID被传入`createDataChannel`，或者[Negotiated]为false)，并且SCTP传输DTLS角色已经协商，则初始化[DataChannelId]为用户代理生成的值，根据[RTCWEB-DATA-PROTOCOL]，并且跳过下列步骤。如果不能生成可用ID，或者[DataChannelId]插槽的值被现存`RTCDataChannel`使用，抛出`OperationError`异常。

> NOTE:如果在此步骤之后[DataChannelId]插槽为`null`，则在设置`RTCSessionDescription`的过程中确定DTLS角色后，将填充该插槽。

20.让transport成为connection的[SctpTransport]插槽。如果[DataChannelId]插槽为`null`，transport处于`connected`状态，并且[DataChannelId]大于等于transport的[MaxChannels]插槽，抛出`OperationError`。

21.如果channel是在connection上创建的第一个`RTCDataChannel`，更新negotiation-needed标记。

22.返回channel并且继续并行执行下列步骤。

23.创建channel的关联底层数据传输，并且根据相关channel属性配置。

