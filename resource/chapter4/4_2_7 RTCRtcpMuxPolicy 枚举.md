###  [4.2.7 RTCRtcpMuxPolicy 枚举](http://w3c.github.io/webrtc-pc/#rtcrtcpmuxpolicy-enum)

如[JSEP]（第4.1.1节）中所述，RtcpMuxPolicy会影响为支持非多路复用而收集哪些ICE候选项。

```
enum RTCRtcpMuxPolicy {
  // At risk due to lack of implementers' interest.
  "negotiate",
  "require"
};
```

<table>
  <tr>
    <td colspan="2">
    Enumeration description (non-normative)
    </td>
  </tr>
  <tr>
    <td>
    negotiate	
    </td>
    <td>
    同时收集RTP和RTCP的ICE候选项。如果远程端点能够复用RTCP，则在RTP候选地址上复用RTCP。如果不是，请分开使用RTP和RTCP候选项。请注意，如[JSEP]（第4.1.1节）中所述，用户代理可能无法实现非多路复用的RTCP，在这种情况下，它将拒绝使用协商策略创建 RTCPeerConnection 实例的尝试。
    </td>
  </tr>
  <tr>
    <td>
    require
    </td>
    <td>
    只收集RTC候选地址和在RTP上复用了RTCP的候选地址。如果远程端点不支持rtcp-mux，则会话协商将失败。
    </td>
  </tr>
</table>

>FEATURE AT RISK 1
>
支持非多路复用RTP / RTCP的本规范的各个方面被标记为存在风险的特征，因为实施者没有明确的承诺。这包括：
>1. 对于negotiate值，实施者没有明确承诺与此相关的行为。
>2. 支持RTCRtpSender和RTCRtpReceiver中的rtcpTransport属性。
