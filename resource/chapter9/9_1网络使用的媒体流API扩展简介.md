# 9 网络用途的媒体流API扩展

## 9.1 简介

`MediaStreamTrack`接口（如[GETUSERMEDIA]规范中所定义）通常表示音频或视频的数据流。可以在`MediaStream`中收集一个或多个`MediaStreamTracks`（严格来说，[GETUSERMEDIA]中定义的`MediaStream`可能包含零个或多个`MediaStreamTrack`对象）。

可以扩展`MediaStreamTrack`以表示来自或被发送到远程对等体（例如，不仅仅是本地相机）的媒体流。此部分将介绍在`MediaStreamTrack`对象上启用此功能所需的扩展。在[RTCWEB-RTP]，[RTCWEB-AUDIO]和[RTCWEB-TRANSPORT]中描述了如何将媒体传输到对等体。

发送给另一个对等方的`MediaStreamTrack`将作为一个且唯一一个MediaStreamTrack向收件人显示。对等体被定义为支持该规范的用户代理。此外，发送方应用程序可以指示`MediaStreamTrack`所属的`MediaStream`对象。接收端相应的`MediaStream`对象将会被创建(如果不是已经存在)并且对应补充。

正如本文档之前所述，应用程序可以使用对象`RTCRtpSender`和`RTCRtpReceiver`来对`MediaStreamTracks`的传输和接收进行更细粒度的控制。

通道是`MediaStream`规范中考虑的最小单位。信道旨在被编码在一起以便传输，例如，RTP有效载荷类型。编解码器需要联合编码的所有通道必须位于同一个`MediaStreamTrack`中，编解码器应该能够编码或丢弃轨道中的所有通道。

对于给定`MediaStreamTrack`的输入和输出的概念也适用于通过网络传输的`MediaStreamTrack`对象。由`RTCPeerConnection`对象创建的MediaStreamTrack（如本文档前面所述）将把从远程对等方接收的数据作为输入。类似地，来自本地源的`MediaStreamTrack`（例如通过[GETUSERMEDIA]的摄像机）将具有输出，如果该对象与RTCPeerConnection对象一起使用,该输出表示传输到远程对等端的内容。

[GETUSERMEDIA]中描述的复制`MediaStream`和`MediaStreamTrack`对象的概念也适用于此处。例如，该功能可用于视频会议场景中，以便在本地监视器中显示来自用户摄像头和麦克风的本地视频，同时仅将音频发送到远程对等端（例如，响应用户使用“视频静音“功能”。在某些情况下，将不同的`MediaStreamTrack`对象组合到新的`MediaStream`对象中非常有用。

> NOTE:在本文档中，我们仅指定与`RTCPeerConnection`一起使用时相关的以下对象的各个方面。有关使用`MediaStream`和`MediaStreamTrack`的一般信息，请参阅[GETUSERMEDIA]文档中对象的原始定义。

