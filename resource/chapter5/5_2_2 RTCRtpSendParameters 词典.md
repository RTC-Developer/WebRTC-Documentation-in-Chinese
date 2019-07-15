### 5.2.2 `RTCRtpSendParameters`字典

```java
dictionary RTCRtpSendParameters : RTCRtpParameters {
             required DOMString             transactionId;
             required sequence<RTCRtpEncodingParameters>  encodings;
             RTCDegradationPreference       degradationPreference = "balanced";
             RTCPriorityType                priority = "low";
};
```

**字典`RTCRtpSendParameters`成员**

DOMString类型的`transactionId`：

应用的最后一组参数的唯一标识符。确保只能基于先前的getParameters调用setParameters，并且没有干预更改。只读参数。

序列<RTCRtpEncodingParameters>类型的`encodings`：

包含媒体RTP编码参数的序列。

`RTCDegradationPreference`类型的`degradationPreference`,默认为`"balanced":`

当带宽受到限制，`RTCRtpSender`需要在降低分辨率和降低帧率之间做出选择，`degradationPreference`指定倾向的选择。

`RTCPriorityType`类型的`priority`，默认为`"low"`:

表示`RTCRtpSender`的优先级，它影响`RTCRtpSender`对象之间的带宽分配。它在[RTCWEB-TRANSPORT]第四节中指定。用户代理可以在`RTCRtpSender`的编码之间自由地分配带宽。



