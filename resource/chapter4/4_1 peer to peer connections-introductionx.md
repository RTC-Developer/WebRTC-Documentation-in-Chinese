# 4.点对点连接

## [4.1简介](http://w3c.github.io/webrtc-pc/#peer-to-peer-connections)

RTCPeerConnection实例允许应用程序与另一个浏览器中的另一个RTCPeerConnection实例或另一个实现了所需协议的端点建立对等通信。通过信令信道交换控制消息（称为信令协议）来协调通信，信令信道没有指定的实现方法，通常由页面中的脚本连接服务器提供。例如，使用XMLHttpRequest [XMLHttpRequest]或WebSockets[WEBSOCKETS-API]。
