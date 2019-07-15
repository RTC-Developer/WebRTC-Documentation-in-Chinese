### 5.2.1 `RTCRtpParameters`字典

```java
dictionary RTCRtpParameters {
             required sequence<RTCRtpHeaderExtensionParameters> headerExtensions;
             required RTCRtcpParameters                         rtcp;
             required sequence<RTCRtpCodecParameters>           codecs;
};
```

**字典`RTCRtpParameters`成员**

序列<RTCRtpHeaderExtensionParameters>类型的headerExtensions:

包含RTP标头扩展参数的序列。只读参数。

`RTCRtcpParameters`类型的`rtcp`:

用于RTCP的参数。只读参数。

序列`<RTCRtpCodeParameters>`类型的`codecs`:

包含`RTCRtpSender`将选择的媒体编码器序列，以及RTX，RED和FEC机制的条目。对应于通过RTX进行重新传输的每个媒体编解码器，在`codecs[]`中将有一个条目，其中`mimeType`属性表示通过"audio/rtx"或"video/rtx"重新传输，以及`sdpFmtpLine`属性(提供"apt"和"rtx-time"参数)。只读参数。

