### [5.2.3 RTCRtpReceiveParameters 词典](http://w3c.github.io/webrtc-pc/#rtcreceivertpparameters)

```
dictionary RTCRtpReceiveParameters : RTCRtpParameters {
             required sequence<RTCRtpDecodingParameters>  encodings;
};
```

**Dictionary RTCRtpReceiveParameters Members**

*encodings* of type sequence<RTCRtpDecodingParameters>, required:
zh:类型序列<RTCRtpDecodingParameters>的编码，必需

A sequence containing information about incoming RTP encodings of media.

zh:包含有关媒体的传入RTP编码的信息的序列。

>(FEATURE AT RISK) ISSUE 2
>
>Support for the encodings attribute of RTCRtpReceiveParameters is marked as a feature at risk, since there is no clear commitment from implementers.
>
>zh:对RTCRtpReceiveParameters的编码属性的支持被标记为风险特征，因为实施者没有明确的承诺。
