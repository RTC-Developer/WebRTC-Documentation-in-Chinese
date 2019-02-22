## [7.1 RTCRtpSender Interface Extensions zh:7.1 RTCRtpSender接口扩展](http://w3c.github.io/webrtc-pc/#rtcrtpsender-interface-extensions)

The Peer-to-peer DTMF API extends the RTCRtpSender interface as described below.

zh:点对点DTMF API扩展了RTCRtpSender接口，如下所述。

```
partial interface RTCRtpSender {
    readonly        attribute RTCDTMFSender? dtmf;
};

```

**Attributes** 

*dtmf* of type RTCDTMFSender, readonly, nullable:
zh:RTCDTMFSender类型的dtmf，只读，可以为空

On getting, the dtmf attribute returns the value of the [[Dtmf]]internal slot, which represents a  RTCDTMFSender which can be used to send DTMF, or null if unset. The [[Dtmf]]internal slot is set when the kind of an RTCRtpSender's [[SenderTrack]] is "audio".

zh:获取时，dtmf属性返回[[Dtmf]]内部插槽的值，表示可用于发送DTMF的RTCDTMFSender，如果未设置，则返回null。当RTCRtpSender的[[SenderTrack]]的类型为“audio”时，[[Dtmf]]内部插槽被设置。
