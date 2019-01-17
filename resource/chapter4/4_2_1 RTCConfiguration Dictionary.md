## 4.2配置
### 4.2.1 RTCConfiguration字典

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
