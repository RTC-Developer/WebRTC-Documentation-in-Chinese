### [5.2.9 RTCRtcpParameters 词典](http://w3c.github.io/webrtc-pc/#rtcrtcpparameters)

```
dictionary RTCRtcpParameters {
             DOMString cname;
             boolean   reducedSize;
};
```

**Dictionary RTCRtcpParameters Members**

*cname* of type DOMString:
zh:DOMString类型的cname

The Canonical Name (CNAME) used by RTCP (e.g. in SDES messages). Read-only parameter.

zh:RTCP使用的规范名称（CNAME）（例如，在SDES消息中）。只读参数。

*reducedSize* of type boolean:
zh:reduceSize类型为boolean

Whether reduced size RTCP [RFC5506] is configured (if true) or compound RTCP as specified in [RFC3550] (if false). Read-only parameter.

zh:是否已配置缩小的RTCP [RFC5506]（如果为true）或[RFC3550]中指定的复合RTCP（如果为false）。只读参数。
