### 5.2.12 `RTCRtpCapabilities`字典

```java
dictionary RTCRtpCapabilities {
             required sequence<RTCRtpCodecCapability>           codecs;
             required sequence<RTCRtpHeaderExtensionCapability> headerExtensions;
};
```

**字典`RTCRtpCapabilities`成员**

序列`<RTCRtpCodecCapability>`类型的`codecs`：

支持的媒体编解码器以及RTX,RED和FEC机制的条目。在`codecs[]`中只有一个条目用于通过RTX重传，并且`sdpFmtpLine`不存在。

**序列**`<RTCRtpHeaderExtensionCapability>`类型的`headerExtensions`：

支持的RTP标头扩展。

