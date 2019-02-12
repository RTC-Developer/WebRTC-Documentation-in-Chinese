### [5.2.10 RTCRtpHeaderExtensionParameters 词典](http://w3c.github.io/webrtc-pc/#rtcrtpheaderextensionparameters)

```
dictionary RTCRtpHeaderExtensionParameters {
             required DOMString      uri;
             required unsigned short id;
             boolean                 encrypted = false;
};
```

**Dictionary RTCRtpHeaderExtensionParameters Members**

*uri* of type DOMString, required:
zh:uri是DOMString类型，必需

zh:RTP头扩展的URI，如[RFC5285]中所定义。只读参数。

*id* of type unsigned short, required:
zh:id为unsigned short，必需


The value put in the RTP packet to identify the header extension. Read-only parameter.

zh:放入RTP数据包中的值以标识标头扩展名。只读参数。

*encrypted* of type boolean:
zh:加密类型为boolean


Whether the header extension is encrypted or not. Read-only parameter.

zh:标头扩展是否加密。只读参数。

>NOTE
>The RTCRtpHeaderExtensionParameters dictionary enables an application to determine whether a header extension is configured for use within an RTCRtpSender or RTCRtpReceiver. For an RTCRtpTransceiver transceiver, an application can determine the "direction" parameter (defined in Section 5 of [RFC5285]) of a header extension as follows without having to parse SDP:
>
>zh:RTCRtpHeaderExtensionParameters字典使应用程序能够确定是否配置了标头扩展以在RTCRtpSender或RTCRtpReceiver中使用。对于RTCRtpTransceiver收发器，应用程序可以确定头扩展的“方向”参数（在[RFC5285]的第5节中定义），如下所示，而不必解析SDP：
> 
> 1. sendonly: The header extension is only included in transceiver.sender.getParameters().headerExtensions.
> zh:sendonly：头扩展仅包含在transceiver.sender.getParameters（）。headerExtensions中。
> 2. recvonly: The header extension is only included in transceiver.receiver.getParameters().headerExtensions.
> zh:recvonly：标头扩展仅包含在transceiver.receiver.getParameters（）。headerExtensions中。
> 3. sendrecv: The header extension is included in both transceiver.sender.getParameters().headerExtensions and transceiver.receiver.getParameters().headerExtensions.
> zh:sendrecv：头扩展包含在transceiver.sender.getParameters（）。headerExtensions和transceiver.receiver.getParameters（）。headerExtensions中。
> 4. inactive: The header extension is included in neither
> transceiver.sender.getParameters().headerExtensions nor
> transceiver.receiver.getParameters().headerExtensions.
> zh:inactive：头扩展名既不包含在transceiver.sender.getParameters（）。headerExtensions中，也不包含在transceiver.receiver.getParameters（）。headerExtensions中。
> 
