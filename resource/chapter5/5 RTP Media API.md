# [5. RTP Media API](http://w3c.github.io/webrtc-pc/#rtp-media-api)

The RTP media API lets a web application send and receive MediaStreamTracks over a peer-to-peer connection. Tracks, when added to an RTCPeerConnection, result in signaling; when this signaling is forwarded to a remote peer, it causes corresponding tracks to be created on the remote side.

zh:RTP媒体API允许Web应用程序通过对等连接发送和接收MediaStreamTracks。跟踪添加到RTCPeerConnection时会产生信令;当该信令被转发到远程对等体时，它导致在远程侧创建相应的信道。

*NOTE
There is not an exact 1:1 correspondence between tracks sent by one RTCPeerConnection and received by the other. For one, IDs of tracks sent have no mapping to the IDs of tracks received. Also, replaceTrack changes the track sent by an RTCRtpSender without creating a new track on the receiver side; the corresponding RTCRtpReceiver will only have a single track, potentially representing multiple sources of media stitched together. Both addTransceiver and replaceTrack can be used to cause the same track to be sent multiple times, which will be observed on the receiver side as multiple receivers each with its own separate track. Thus it's more accurate to think of a 1:1 relationship between an RTCRtpSender on one side and an RTCRtpReceiver's track on the other side, matching senders and receivers using the RTCRtpTransceiver's mid if necessary.*

zh:一个RTCPeerConnection发送的轨道与另一个RTCPeerConnection接收的轨道之间没有确切的1：1对应关系。例如，发送的曲目的ID没有映射到接收的曲目的ID。此外，replaceTrack更改RTCRtpSender发送的曲目，而不在接收方创建新曲目;相应的RTCRtpReceiver只有一个轨道，可能代表缝合在一起的多个媒体源。 addTransceiver和replaceTrack都可以用于使相同的轨道被多次发送，这将在接收器侧被观察为多个接收器，每个接收器具有其自己的单独轨道。因此，考虑一侧的RTCRtpSender与另一侧的RTCRtpReceiver的轨道之间的1：1关系更为准确，如果需要，使用RTCRtpTransceiver的mid匹配发送者和接收者。

When sending media, the sender may need to rescale or resample the media to meet various requirements including the envelope negotiated by SDP.

zh:发送媒体时，发送方可能需要重新调整或重新采样媒体，以满足各种要求，包括SDP协商的信封。

Following the rules in [JSEP] (section 3.6.), the video MAY be downscaled in order to fit the SDP constraints. The media MUST NOT be upscaled to create fake data that did not occur in the input source, the media MUST NOT be cropped except as needed to satisfy constraints on pixel counts, and the aspect ratio MUST NOT be changed.

zh:遵循[JSEP]（第3.6节）中的规则，可以缩小视频尺寸以适应SDP约束。媒体不得升级以创建未在输入源中出现的伪数据，除非满足像素计数约束，否则不得裁剪媒体，并且不得更改宽高比。

*NOTE
The WebRTC Working Group is seeking implementation feedback on the need and timeline for a more complex handling of this situation. Some possible designs have been discussed in GitHub issue 1283.*

zh:WebRTC工作组正在寻求关于需求和时间表的实施反馈，以便更复杂地处理这种情况。 GitHub issue 1283中讨论了一些可能的设计。

When video is rescaled, for example for certain combinations of width or height and scaleResolutionDownBy values, situations when the resulting width or height is not an integer may occur. In such situations the user agent MUST use the integer part of the result. What to transmit if the integer part of the scaled width or height is zero is implementation-specific.

zh:当视频被重新缩放时，例如对于宽度或高度的某些组合以及scaleResolutionDownBy值，可能出现所得宽度或高度不是整数的情况。在这种情况下，用户代理必须使用结果的整数部分。如果缩放宽度或高度的整数部分为零，则传输什么是特定于实现的。

The actual encoding and transmission of MediaStreamTracks is managed through objects called RTCRtpSenders. Similarly, the reception and decoding of MediaStreamTracks is managed through objects called RTCRtpReceivers. Each RTCRtpSender is associated with at most one track, and each track to be received is associated with exactly one RTCRtpReceiver.

zh:MediaStreamTracks的实际编码和传输是通过名为RTCRtpSenders的对象来管理的。同样，MediaStreamTracks的接收和解码通过称为RTCRtpReceivers的对象进行管理。每个RTCRtpSender与至多一个轨道相关联，并且要接收的每个轨道仅与一个RTCRtpReceiver相关联。

The encoding and transmission of each MediaStreamTrack SHOULD be made such that its characteristics (width, height and frameRate for video tracks; volume, sampleSize, sampleRate and channelCount for audio tracks) are to a reasonable degree retained by the track created on the remote side. There are situations when this does not apply, there may for example be resource constraints at either endpoint or in the network or there may be RTCRtpSender settings applied that instruct the implementation to act differently.

zh:应该对每个MediaStreamTrack进行编码和传输，使其特性（视频轨道的宽度，高度和frameRate;音频轨道的volume，sampleSize，sampleRate和channelCount）在远程端创建的轨道保持合理的程度。在某些情况下，如果不适用，可能会在端点或网络中出现资源限制，或者可能会应用RTCRtpSender设置来指示实施采取不同的行动。

An RTCPeerConnection object contains a set of RTCRtpTransceivers, representing the paired senders and receivers with some shared state. This set is initialized to the empty set when the RTCPeerConnection object is created. RTCRtpSenders and RTCRtpReceivers are always created at the same time as an RTCRtpTransceiver, which they will remain attached to for their lifetime. RTCRtpTransceivers are created implicitly when the application attaches a MediaStreamTrack to an RTCPeerConnection via the addTrack method, or explicitly when the application uses the addTransceiver method. They are also created when a remote description is applied that includes a new media description. Additionally, when a remote description is applied that indicates the remote endpoint has media to send, the relevant MediaStreamTrack and RTCRtpReceiver are surfaced to the application via the track event.

zh: RTCPeerConnection对象包含一组RTCRtpTransceivers，表示配对的发送者和接收者具有某种共享状态。创建RTCPeerConnection对象时，此集初始化为空集。 RTCRtpSenders和RTCRtpReceivers始终与RTCRtpTransceiver同时创建，它们将在其生命周期内保持连接状态。当应用程序通过addTrack方法将MediaStreamTrack附加到RTCPeerConnection时，或者在应用程序使用addTransceiver方法时显式地创建RTCRtpTransceivers。当应用包含新媒体描述的远程描述时，也会创建它们。此外，当应用指示远程端点具有要发送的媒体的远程描述时，相关的MediaStreamTrack和RTCRtpReceiver通过跟踪事件浮现到应用程序。
