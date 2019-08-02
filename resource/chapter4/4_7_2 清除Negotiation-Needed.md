### [4.7.2 清除Negotiation-Needed](http://w3c.github.io/webrtc-pc/#clearing-negotiation-needed)

本节不具有规范性。

当应用类型为“answer”的RTCSessionDescription时，将清除`negotiation-needed`的标志，并且提供的描述与RTCPeerConnection上当前存在的RTCRtpTransceivers和RTCDataChannel的状态相匹配。具体而言，所有未停止的收发器在本地描述中具有匹配属性的相关部分，并且，如果已经创建了任何数据信道，则本地描述中存在数据部分。

NOTE：更新Negotiation-Needed的标志的明确过程如下所示。
