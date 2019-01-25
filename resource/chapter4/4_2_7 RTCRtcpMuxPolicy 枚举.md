4.2.7 [RTCRtcpMuxPolicy 枚举](http://w3c.github.io/webrtc-pc/#rtcrtcpmuxpolicy-enum)

As described in [JSEP] (section 4.1.1.), the RtcpMuxPolicy affects what ICE candidates are gathered to support non-multiplexed RTCP.

zh:如[JSEP]（第4.1.1节）中所述，RtcpMuxPolicy会影响为收集非多路复用RTCP而收集的ICE候选项。

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
    Gather ICE candidates for both RTP and RTCP candidates. If the remote-endpoint is capable of multiplexing RTCP, multiplex RTCP on the RTP candidates. If it is not, use both the RTP and RTCP candidates separately. Note that, as stated in [JSEP] (section 4.1.1.), the user agent MAY not implement non-multiplexed RTCP, in which case it will reject attempts to construct an RTCPeerConnection with the negotiate policy.
    zh:收集RTP和RTCP候选人的ICE候选人。如果远程端点能够复用RTCP，则在RTP候选上复用RTCP。如果不是，请分别使用RTP和RTCP候选。请注意，如[JSEP]（第4.1.1节）中所述，用户代理可能无法实现非多路复用的RTCP，在这种情况下，它将拒绝使用协商策略构建RTCPeerConnection的尝试。
    </td>
  </tr>
  <tr>
    <td>
    require
    </td>
    <td>
    Gather ICE candidates only for RTP and multiplex RTCP on the RTP candidates. If the remote endpoint is not capable of rtcp-mux, session negotiation will fail.
    zh:仅针对RTP候选者上的RTP和多路RTCP收集ICE候选者。如果远程端点不支持rtcp-mux，则会话协商将失败。
    </td>
  </tr>
</table>

>FEATURE AT RISK 1
>
>Aspects of this specification supporting non-multiplexed RTP/RTCP are marked as features at risk, since there is no clear commitment from implementers. This includes:zh:支持非多路复用RTP / RTCP的本规范的各个方面被标记为存在风险的特征，因为实施者没有明确的承诺。这包括：
>
>1. The value negotiate, since there is no clear commitment from implementers for the behavior associated with this.
>2. Support for the rtcpTransport attribute within the RTCRtpSender and RTCRtpReceiver.
>1. zh:价值进行协商，因为实施者没有明确承诺与此相关的行为。
>2. zh:支持RTCRtpSender和RTCRtpReceiver中的rtcpTransport属性。
