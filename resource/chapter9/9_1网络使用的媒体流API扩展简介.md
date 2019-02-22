# [9. Media Stream API Extensions for Network Use zh:9.网络使用的媒体流API扩展](http://w3c.github.io/webrtc-pc/#media-stream-api-extensions-for-network-use)
## [9.1 Introduction zh:9.1简介](http://w3c.github.io/webrtc-pc/#introduction-1)

The MediaStreamTrack interface, as defined in the [GETUSERMEDIA] specification, typically represents a stream of data of audio or video. One or more MediaStreamTracks can be collected in a MediaStream (strictly speaking, a MediaStream as defined in [GETUSERMEDIA] may contain zero or more MediaStreamTrack objects).

zh:MediaStreamTrack接口（如[GETUSERMEDIA]规范中所定义）通常表示音频或视频的数据流。可以在MediaStream中收集一个或多个MediaStreamTracks（严格来说，[GETUSERMEDIA]中定义的MediaStream可能包含零个或多个MediaStreamTrack对象）。

A MediaStreamTrack may be extended to represent a media flow that either comes from or is sent to a remote peer (and not just the local camera, for instance). The extensions required to enable this capability on the MediaStreamTrack object will be described in this section. How the media is transmitted to the peer is described in [RTCWEB-RTP], [RTCWEB-AUDIO], and [RTCWEB-TRANSPORT].

zh:可以扩展MediaStreamTrack以表示来自或被发送到远程对等体（例如，不仅仅是本地相机）的媒体流。此部分将介绍在MediaStreamTrack对象上启用此功能所需的扩展。在[RTCWEB-RTP]，[RTCWEB-AUDIO]和[RTCWEB-TRANSPORT]中描述了如何将媒体传输到对等体。

A MediaStreamTrack sent to another peer will appear as one and only one MediaStreamTrack to the recipient. A peer is defined as a user agent that supports this specification. In addition, the sending side application can indicate what MediaStream object(s) the MediaStreamTrack is a member of. The corresponding MediaStream object(s) on the receiver side will be created (if not already present) and populated accordingly.

zh:发送给另一个对等方的MediaStreamTrack将作为一个且仅一个MediaStreamTrack显示给收件人。对等体被定义为支持该规范的用户代理。此外，发送方应用程序可以指示MediaStreamTrack所属的MediaStream对象。将创建接收方侧的相应MediaStream对象（如果尚未存在）并相应地填充。

As also described earlier in this document, the objects RTCRtpSender and RTCRtpReceiver can be used by the application to get more fine grained control over the transmission and reception of MediaStreamTracks.

zh:正如本文档前面所述，应用程序可以使用对象RTCRtpSender和RTCRtpReceiver来对MediaStreamTracks的传输和接收进行更细粒度的控制。

Channels are the smallest unit considered in the MediaStream specification. Channels are intended to be encoded together for transmission as, for instance, an RTP payload type. All of the channels that a codec needs to encode jointly MUST be in the same MediaStreamTrack and the codecs SHOULD be able to encode, or discard, all the channels in the track.

zh:通道是MediaStream规范中考虑的最小单位。信道旨在被编码在一起以便传输，例如，RTP有效载荷类型。编解码器需要联合编码的所有通道必须位于同一个MediaStreamTrack中，编解码器应该能够编码或丢弃轨道中的所有通道。

The concepts of an input and output to a given MediaStreamTrack apply in the case of MediaStreamTrack objects transmitted over the network as well. A MediaStreamTrack created by an RTCPeerConnection object (as described previously in this document) will take as input the data received from a remote peer. Similarly, a MediaStreamTrack from a local source, for instance a camera via [GETUSERMEDIA], will have an output that represents what is transmitted to a remote peer if the object is used with an RTCPeerConnection object.

zh:对于给定MediaStreamTrack的输入和输出的概念也适用于通过网络传输的MediaStreamTrack对象。由RTCPeerConnection对象创建的MediaStreamTrack（如本文档前面所述）将从远程对等方接收数据作为输入。类似地，来自本地源的MediaStreamTrack（例如通过[GETUSERMEDIA]的摄像机）将具有输出，该输出表示如果该对象与RTCPeerConnection对象一起使用则传输到远程对等端的内容。

The concept of duplicating MediaStream and MediaStreamTrack objects as described in [GETUSERMEDIA] is also applicable here. This feature can be used, for instance, in a video-conferencing scenario to display the local video from the user's camera and microphone in a local monitor, while only transmitting the audio to the remote peer (e.g. in response to the user using a "video mute" feature). Combining different MediaStreamTrack objects into new MediaStream objects is useful in certain situations.

zh:[GETUSERMEDIA]中描述的复制MediaStream和MediaStreamTrack对象的概念也适用于此处。例如，该功能可用于视频会议场景中，以便在本地监视器中显示来自用户摄像头和麦克风的本地视频，同时仅将音频发送到远程对等端（例如，响应用户使用“视频静音“功能”。在某些情况下，将不同的MediaStreamTrack对象组合到新的MediaStream对象中非常有用。

>NOTE
>
>In this document, we only specify aspects of the following objects that are relevant when used along with an RTCPeerConnection. Please refer to the original definitions of the objects in the [GETUSERMEDIA] document for general information on using MediaStream and MediaStreamTrack.
>
>zh:在本文档中，我们仅指定与RTCPeerConnection一起使用时相关的以下对象的各个方面。有关使用MediaStream和MediaStreamTrack的一般信息，请参阅[GETUSERMEDIA]文档中对象的原始定义。
