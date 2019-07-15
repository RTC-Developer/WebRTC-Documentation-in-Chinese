### 5.2.10 `RTCRtpHeaderExtensionParameters`字典

```java
dictionary RTCRtpHeaderExtensionParameters {
             required DOMString      uri;
             required unsigned short id;
             boolean                 encrypted = false;
};
```

**字典`RTCRtpHeaderExtensionParameters`成员**

DOMString类型的`uri`：

RTP标头扩展的URI，[RFC5285]中定义。只读参数。

unsigned short类型的`id`:

放入RTP数据包用于验证标头扩展的值。只读参数。

Boolean类型的`encrypted`:

标头是否加密。只读参数。

> NOTE
>
> `RTCRtpHeaderExtensionParameters`字典启用应用程序来确定是否配置了标头扩展以在`RTCRtpSender`或`RTCRtpReceiver`中使用。对于一个`RTCRtpTransceiver`收发器，应用程序可以在不解析SDP的情况下确定标头扩展的"direction"参数([RFC5285]第五章定义)，如下：
>
> 1. sendonly:标头扩展只能包含在transceiver.sender.getParameters().headerExtensions中。
> 2. recvonly:标头扩展只能包含在transceiver.receiver.getParameters().headerExtensions中。
> 3. sendrecv:标头扩展可以包含在transceiver.sender.getParameters().headerExtensions和transceiver.receiver.getParameters().headerExtensions中。
> 4. inactive:标头扩展既不包含在transceiver.sender.getParameters().headerExtensions中也不包含在transceiver.receiver.getParameters().headerExtensions中。





