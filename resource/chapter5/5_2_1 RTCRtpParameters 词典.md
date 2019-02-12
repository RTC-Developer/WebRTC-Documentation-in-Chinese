### [5.2.1 RTCRtpParameters 词典](http://w3c.github.io/webrtc-pc/#rtcrtpparameters)

```
dictionary RTCRtpParameters {
             required sequence<RTCRtpHeaderExtensionParameters> headerExtensions;
             required RTCRtcpParameters                         rtcp;
             required sequence<RTCRtpCodecParameters>           codecs;
};
```

**Dictionary RTCRtpParameters Members**

*headerExtensions* of type sequence<RTCRtpHeaderExtensionParameters>, required:
zh:headerExtensions类型为序列<RTCRtpHeaderExtensionParameters>，必需

A sequence containing parameters for RTP header extensions. Read-only parameter.

zh:包含RTP标头扩展参数的序列。只读参数。

*rtcp* of type RTCRtcpParameters, required:
zh:必需的RTCRtcpParameters类型的rtcp

Parameters used for RTCP. Read-only parameter.

zh:用于RTCP的参数。只读参数。

*codecs* of type sequence<RTCRtpCodecParameters>, required:
zh:类型序列<RTCRtpCodecParameters>的编解码器，必需

A sequence containing the media codecs that an RTCRtpSender will choose from, as well as entries for RTX, RED and FEC mechanisms. Corresponding to each media codec where retransmission via RTX is enabled, there will be an entry in codecs[] with a mimeType attribute indicating retransmission via "audio/rtx" or "video/rtx", and an sdpFmtpLine attribute (providing the "apt" and "rtx-time" parameters). Read-only parameter.

zh:包含RTCRtpSender将选择的媒体编解码器的序列，以及RTX，RED和FEC机制的条目。对应于通过RTX进行重传的每个媒体编解码器，在codecs []中将有一个条目，其中mimeType属性指示通过“audio / rtx”或“video / rtx”进行重传，以及sdpFmtpLine属性（提供“apt”）和“rtx-time”参数）。只读参数。
