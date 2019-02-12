### [5.2.2 RTCRtpSendParameters 词典](http://w3c.github.io/webrtc-pc/#rtcsendrtpparameters)

```
dictionary RTCRtpSendParameters : RTCRtpParameters {
             required DOMString             transactionId;
             required sequence<RTCRtpEncodingParameters>  encodings;
             RTCDegradationPreference       degradationPreference = "balanced";
             RTCPriorityType                priority = "low";
};
```

##### Dictionary RTCRtpSendParameters Members

*transactionId* of type DOMString, required:
zh:必需的DOMItring类型的transactionId

An unique identifier for the last set of parameters applied. Ensures that setParameters can only be called based on a previous getParameters, and that there are no intervening changes. Read-only parameter.

zh:应用的最后一组参数的唯一标识符。确保只能基于先前的getParameters调用setParameters，并且没有干预更改。只读参数。

*encodings* of type sequence<RTCRtpEncodingParameters>, required:
zh:类型序列<RTCRtpEncodingParameters>的编码，必需

A sequence containing parameters for RTP encodings of media.

zh:包含媒体RTP编码参数的序列。

*degradationPreference* of type RTCDegradationPreference, defaulting to "balanced":
zh:降级RTCDegradation类型的偏差，默认为“平衡”

When bandwidth is constrained and the RtpSender needs to choose between degrading resolution or degrading framerate, degradationPreference indicates which is preferred.

zh:当带宽受限并且RtpSender需要在降级分辨率或降低帧速率之间进行选择时，degraprepreference指示哪个是首选。

*priority* of type RTCPriorityType, defaulting to "low":
zh:RTCPriorityType类型的优先级，默认为“低”



Indicates the priority of this encoding. It is specified in [RTCWEB-TRANSPORT], Section 4.

zh:表示此编码的优先级。它在[RTCWEB-TRANSPORT]第4节中规定。
