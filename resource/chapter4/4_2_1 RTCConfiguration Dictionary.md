## 4.2配置
### [4.2.1 RTCConfiguration字典](http://w3c.github.io/webrtc-pc/#rtcconfiguration-dictionary)

RTCConfiguration定义了一组参数，用于配置 RTCPeerConnection 如何建立或重新建立点对点通信。

```
dictionary RTCConfiguration {
  sequence<RTCIceServer> iceServers;
  RTCIceTransportPolicy iceTransportPolicy = "all";
  RTCBundlePolicy bundlePolicy = "balanced";
  RTCRtcpMuxPolicy rtcpMuxPolicy = "require";
  DOMString peerIdentity;
  sequence<RTCCertificate> certificates;
  [EnforceRange]
  octet iceCandidatePoolSize = 0;
};

```
字典RTCConfiguration成员

iceServers of type sequence<RTCIceServer>:
zh:<RTCIceServer>类的`iceServers`

	一组可供ICE使用的服务器的描述，例如 STUN 和 TURN 服务器。

一组可供ICE使用的服务器的描述，例如 STUN 和 TURN 服务器。

iceTransportPolicy of type RTCIceTransportPolicy, defaulting to "all":
zh:RTCIceTransportPolicy 类型的 iceTransportPolicy，默认为“all”

	指示允许ICE代理使用哪些候选者。

指示允许ICE代理使用哪些候选者。

bundlePolicy of type RTCBundlePolicy, defaulting to "balanced":
zh:类型为 RTCBundlePolicy 的 bundlePolicy ，默认为“balanced”

	指示在收集ICE候选项时要使用的媒体捆绑策略。

指示在收集ICE候选项时要使用的媒体捆绑策略。

rtcpMuxPolicy of type RTCRtcpMuxPolicy, defaulting to "require":
zh:RTCPtcpMuxPolicy类型的rtcpMuxPolicy，默认为“require”

	指示收集ICE候选项时要使用的 rtcp-mux 策略。

指示收集ICE候选项时要使用的 rtcp-mux 策略。

peerIdentity of type DOMString:
zh:DOMString类型的peerIdentity

	设置 RTCPeerConnection 目标对端的标识。 RTCPeerConnection 不会与对端建立连接，除非对端提供名称并用该名称成功验证身份。

设置 RTCPeerConnection 目标对端的标识。 RTCPeerConnection 不会与对端建立连接，除非对端提供名称并用该名称成功验证身份。

certificates of type sequence<RTCCertificate>:
序列号<RTCCertificate>的证书。

RTCPeerConnection 用于进行身份验证的一组证书。

通过调用 generateCertificate 函数创建此参数的有效值

虽然任何给定的 DTLS 连接仅使用一个证书，但此属性允许调用者提供支持不同算法的多个证书。将根据 DTLS 握手允许哪些证书，来选择最终证书。 RTCPeerConnection 实现选择将哪个证书用于给定连接;如何选择证书超出了本规范的范围。

如果此值不存在，则为每个 RTCPeerConnection 实例生成一组默认证书。

此选项允许应用程序建立密钥连续性。 RTCCertificate 可以保存在 [INDEXEDDB] 中并重复使用。持久性和重用也避免了密钥生成的成本。

最初选择此值后，此配置选项的值不能更改

octet类型的iceCandidatePoolSize，默认为0

	 Size of the prefetched ICE pool as defined in [JSEP] (section 3.5.4. and section 4.1.1.). 
	zh: [JSEP]（第3.5.4节和第4.1.1节）中定义的预取ICE池的大小。

Size of the prefetched ICE pool as defined in [JSEP] (section 3.5.4. and section 4.1.1.).

[JSEP]（第3.5.4节和第4.1.1节）中定义的预取ICE池的大小。
