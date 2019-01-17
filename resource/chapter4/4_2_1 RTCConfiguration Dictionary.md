## 4.2配置
### [4.2.1 RTCConfiguration字典](http://w3c.github.io/webrtc-pc/#rtcconfiguration-dictionary)

The RTCConfiguration defines a set of parameters to configure how the peer-to-peer communication established via RTCPeerConnection is established or re-established.

zh:RTCConfiguration定义了一组参数，用于配置如何建立或重新建立通过RTCPeerConnection建立的对等通信。

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

	 An array of objects describing servers available to be used by ICE, such as STUN and TURN servers. 
	zh: 描述可供ICE使用的服务器的对象数组，例如STUN和TURN服务器。

An array of objects describing servers available to be used by ICE, such as STUN and TURN servers.

zh:描述可供ICE使用的服务器的对象数组，例如STUN和TURN服务器。

iceTransportPolicy of type RTCIceTransportPolicy, defaulting to "all":
zh:RTCIceTransportPolicy类型的iceTransportPolicy，默认为“all”

	 Indicates which candidates the ICE Agent is allowed to use. 
	zh: 指示允许ICE代理使用哪些候选者。

Indicates which candidates the ICE Agent is allowed to use.

zh:指示允许ICE代理使用哪些候选者。

bundlePolicy of type RTCBundlePolicy, defaulting to "balanced":
zh:类型为RTCBundlePolicy的bundlePolicy，默认为“平衡”

	 Indicates which media-bundling policy to use when gathering ICE candidates. 
	zh: 指示在收集ICE候选项时要使用的媒体捆绑策略。

Indicates which media-bundling policy to use when gathering ICE candidates.

zh:指示在收集ICE候选项时要使用的媒体捆绑策略。

rtcpMuxPolicy of type RTCRtcpMuxPolicy, defaulting to "require":
zh:RTCPtcpMuxPolicy类型的rtcpMuxPolicy，默认为“require”

	 Indicates which rtcp-mux policy to use when gathering ICE candidates. 
	zh: 指示收集ICE候选项时要使用的rtcp-mux策略。

Indicates which rtcp-mux policy to use when gathering ICE candidates.

zh:指示收集ICE候选项时要使用的rtcp-mux策略。

peerIdentity of type DOMString:
zh:DOMString类型的peerIdentity

	 Sets the target peer identity for the RTCPeerConnection. The RTCPeerConnection will not establish a connection to a remote peer unless it can be successfully authenticated with the provided name. 
	zh: 设置RTCPeerConnection的目标对等标识。 RTCPeerConnection不会与远程对等方建立连接，除非可以使用提供的名称成功进行身份验证。

Sets the target peer identity for the RTCPeerConnection. The RTCPeerConnection will not establish a connection to a remote peer unless it can be successfully authenticated with the provided name.

zh:设置RTCPeerConnection的目标对等标识。 RTCPeerConnection不会建立与远程对等方的连接，除非可以使用提供的名称成功进行身份验证。

certificates of type sequence<RTCCertificate>:
zh:序列号<RTCCertificate>的证书

	 A set of certificates that the RTCPeerConnection uses to authenticate. Valid values for this parameter are created through calls to the generateCertificate function. Although any given DTLS connection will use only one certificate, this attribute allows the caller to provide multiple certificates that support different algorithms. The final certificate will be selected based on the DTLS handshake, which establishes which certificates are allowed. The RTCPeerConnection implementation selects which of the certificates is used for a given connection; how certificates are selected is outside the scope of this specification. If this value is absent, then a default set of certificates is generated for each RTCPeerConnection instance. This option allows applications to establish key continuity. An RTCCertificate can be persisted in [INDEXEDDB] and reused. Persistence and reuse also avoids the cost of key generation. The value for this configuration option cannot change after its value is initially selected. 
	zh: RTCPeerConnection用于进行身份验证的一组证书。通过调用generateCertificate函数创建此参数的有效值。虽然任何给定的DTLS连接仅使用一个证书，但此属性允许调用者提供支持不同算法的多个证书。将根据DTLS握手选择最终证书，该握手确定允许哪些证书。 RTCPeerConnection实现选择将哪个证书用于给定连接;如何选择证书超出了本规范的范围。如果此值不存在，则为每个RTCPeerConnection实例生成一组默认证书。此选项允许应用程序建立密钥连续性。 RTCCertificate可以保存在[INDEXEDDB]中并重复使用。持久性和重用也避免了密钥生成的成本。最初选择此值后，此配置选项的值不能更改。

A set of certificates that the RTCPeerConnection uses to authenticate.

zh:RTCPeerConnection用于进行身份验证的一组证书。

Valid values for this parameter are created through calls to the generateCertificate function.

zh:通过调用generateCertificate函数创建此参数的有效值。

Although any given DTLS connection will use only one certificate, this attribute allows the caller to provide multiple certificates that support different algorithms. The final certificate will be selected based on the DTLS handshake, which establishes which certificates are allowed. The RTCPeerConnection implementation selects which of the certificates is used for a given connection; how certificates are selected is outside the scope of this specification.

zh:虽然任何给定的DTLS连接仅使用一个证书，但此属性允许调用者提供支持不同算法的多个证书。将根据DTLS握手选择最终证书，该握手确定允许哪些证书。 RTCPeerConnection实现选择将哪个证书用于给定连接;如何选择证书超出了本规范的范围。

If this value is absent, then a default set of certificates is generated for each RTCPeerConnection instance.

zh:如果此值不存在，则为每个RTCPeerConnection实例生成一组默认证书。

This option allows applications to establish key continuity. An RTCCertificate can be persisted in [INDEXEDDB] and reused. Persistence and reuse also avoids the cost of key generation.

zh:此选项允许应用程序建立密钥连续性。 RTCCertificate可以保存在[INDEXEDDB]中并重复使用。持久性和重用也避免了密钥生成的成本。

The value for this configuration option cannot change after its value is initially selected.

zh:最初选择此值后，此配置选项的值不能更改。

iceCandidatePoolSize of type octet, defaulting to 0:
zh:octet类型的iceCandidatePoolSize，默认为0

	 Size of the prefetched ICE pool as defined in [JSEP] (section 3.5.4. and section 4.1.1.). 
	zh: [JSEP]（第3.5.4节和第4.1.1节）中定义的预取ICE池的大小。

Size of the prefetched ICE pool as defined in [JSEP] (section 3.5.4. and section 4.1.1.).

zh:[JSEP]（第3.5.4节和第4.1.1节）中定义的预取ICE池的大小。
