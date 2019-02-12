### [5.2.4 RTCRtpCodingParameters Dictionary](http://w3c.github.io/webrtc-pc/#rtcrtpcodingparameters)

```
dictionary RTCRtpCodingParameters {
             DOMString           rid;
};
```

**Dictionary RTCRtpCodingParameters Members**

*rid* of type DOMString:
zh:摆脱DOMString类型

If set, this RTP encoding will be sent with the RID header extension as defined by [JSEP] (section 5.2.1.). The RID is not modifiable via setParameters. It can only be set or modified in addTransceiver on the sending side. Read-only parameter.

zh:如果设置，则此RTP编码将与[JSEP]（第5.2.1节）定义的RID头扩展一起发送。 RID不能通过setParameters修改。它只能在发送端的addTransceiver中设置或修改。只读参数。
