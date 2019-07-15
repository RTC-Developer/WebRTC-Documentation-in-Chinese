### 5.2.3 `RTCRtpReceiveParameters`字典

```java
dictionary RTCRtpReceiveParameters : RTCRtpParameters {
             required sequence<RTCRtpDecodingParameters>  encodings;
};
```

**字典`RTCRtpReceiveParameters`成员**

序列<RTCRtpDecodingParameters>类型的encodings：

包含入向媒体RTP编码信息的序列。

> (FEATURE AT RISK) ISSUE 3
>
> 对`RTCRtpReceiveParameters`的`encodings`属性的支持被标记为存在危险的特性，因为实现者没有明确的承诺。

