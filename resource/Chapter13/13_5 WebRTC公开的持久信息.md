## 13.5 WebRTC公开的持久信息

如上所述，WebRTC API公开的IP地址列表可以用作持久的跨源状态。

除IP地址以外，WebRTC API通过`RTCRtpSender.getCapabilities`和`RTCRtpReceiver.getCapabilities`方法公开有关底层媒体系统的信息，包括系统可以生成和使用的编解码器的详细和有序信息。该信息的一部分可能在会话协商期间生成，公开和传输的SDP会话描述中表示。该信息大多数情况下，跨时间和跨源是持久的，并且增加了给定设备的指纹表面。

如果设置，由`RTCPeerConnection`实例上的`getDefaultIceServers`公开的配置的默认ICE服务器也提供跨时间跨源信息，这增加了给定浏览器的指纹表面。

建立DTLS连接时，WebRTC API可以生成可由应用程序持久保存的证书(例如在IndexedDB中)。这些证书不是跨源共享的，当该源的持久存储被清除时，它同时被清除。

