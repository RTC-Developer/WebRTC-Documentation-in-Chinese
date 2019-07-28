### [4.7.1 设置Negotiation-Needed](http://w3c.github.io/webrtc-pc/#setting-negotiation-needed)

本节不具有规范性。

如果在需要信令的RTCPeerConnection上执行操作，则该连接将被标记为需要协商。这种操作的示例包括添加或停止RTCRtpTransceiver，或添加第一个RTCDataChannel。

实现中的内部更改还可能导致连接被标记为需要协商。

请注意，更新需要协商的标志的确切过程如下所示。
