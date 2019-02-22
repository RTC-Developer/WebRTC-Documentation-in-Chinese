## [9.3 MediaStreamTrack](http://w3c.github.io/webrtc-pc/#mediastreamtrack)

A MediaStreamTrack object's reference to its MediaStream in the non-local media source case (an RTP source, as is the case for each MediaStreamTrack associated with an RTCRtpReceiver) is always strong.

zh:MediaStreamTrack对象在非本地媒体源案例中对其MediaStream的引用（RTP源，与每个与RTCRtpReceiver关联的MediaStreamTrack的情况）总是很强。

Whenever an RTCRtpReceiver receives data on an RTP source whose corresponding MediaStreamTrack is muted, and the [[Receptive]] slot of the RTCRtpTransceiver object the RTCRtpReceiver is a member of is true, it MUST queue a task to set the muted state of the corresponding MediaStreamTrack to false. 

zh:每当RTCRtpReceiver在相应的MediaStreamTrack被静音的RTP源上接收数据，并且RTCRtpTraceceiver对象的[[Receptive]]时隙RTCRtpReceiver是其成员时，它必须排队任务以设置相应MediaStreamTrack的静音状态为假。

When one of the SSRCs for RTP source media streams received by an RTCRtpReceiver is removed either due to reception of a BYE or via timeout, it MUST queue a task to set the muted state of the corresponding MediaStreamTrack to true. Note that setRemoteDescription can also lead to  the setting of the muted state of the track to the value true.

zh:当RTCRtpReceiver接收到的RTP源媒体流的SSRC之一由于接收到BYE或超时而被删除时，它必须排队任务以将相应MediaStreamTrack的静音状态设置为真。请注意，setRemoteDescription还可以将轨道的静音状态设置为值true。

The procedures add a track, remove a track and set a track's muted state are specified in [GETUSERMEDIA].

zh:在[GETUSERMEDIA]中指定了添加曲目，删除曲目和设置曲目静音状态的步骤。

When a MediaStreamTrack track produced by an RTCRtpReceiver receiver has ended [GETUSERMEDIA] (such as via a call to receiver.track.stop), the user agent MAY choose to free resources allocated for the incoming stream, by for instance turning off the decoder of receiver.

zh:当RTCRtpReceiver接收器生成的MediaStreamTrack轨道已经结束[GETUSERMEDIA]时（例如通过调用receiver.track.stop），用户代理可以选择释放为传入流分配的资源，例如关闭解码器接收器。
