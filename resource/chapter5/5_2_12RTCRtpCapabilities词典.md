### [5.2.12 RTCRtpCapabilities Dictionary](http://w3c.github.io/webrtc-pc/#rtcrtpcapabilities)

```
dictionary RTCRtpCapabilities {
             required sequence<RTCRtpCodecCapability>           codecs;
             required sequence<RTCRtpHeaderExtensionCapability> headerExtensions;
};
```

**Dictionary RTCRtpCapabilities Members**

*codecs* of type sequence<RTCRtpCodecCapability>, required:
zh:类型序列<RTCRtpCodecCapability>的编解码器，必需

Supported media codecs as well as entries for RTX, RED and FEC mechanisms. There will only be a single entry in codecs[] for retransmission via RTX, with sdpFmtpLine not present.

zh:支持的媒体编解码器以及RTX，RED和FEC机制的条目。在codecs []中只有一个条目用于通过RTX进行重传，sdpFmtpLine不存在。

*headerExtensions* of type sequence<RTCRtpHeaderExtensionCapability>, required:
zh:headerExtensions类型为序列<RTCRtpHeaderExtensionCapability>，必需

Supported RTP header extensions.

zh:支持的RTP标头扩展。