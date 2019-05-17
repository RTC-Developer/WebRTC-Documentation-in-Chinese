## 9.3 媒体流轨道

`MediaStreamTrack`对象在非本地媒体源案例中对其`MediaStream`的引用（RTP源，每个`RTCRtpReceiver`关联一个`MediaStreamTrack`的情况）总是很强。

每当`RTCRtpReceiver`在相应的MediaStreamTrack被静音的RTP源上接收数据，并且包含`RTCRtpReceiver`的`RTCRtpTraceceiver`对象的[[Receptive]]插槽为`true`时，它必须对任务排序以设置相应MediaStreamTrack的静音状态为`false`。

当RTCRtpReceiver接收到的RTP源媒体流的SSRC之一由于接收到BYE或超时而被移除时，它必须对任务排序以将相应MediaStreamTrack的静音状态设置为`true`。注意，`setRemoteDescription`还可以将`track`的静音状态设置为值`true`。

在[GETUSERMEDIA]中指定了添加track，删除track和设置track静音状态的步骤。

当`RTCRtpReceiver`接收器生成的MediaStreamTrack轨道已经结束[GETUSERMEDIA]时（例如通过调用`receiver.track.stop`），用户代理可以选择释放为输入流分配的资源，例如通过关闭接收端解码器。



