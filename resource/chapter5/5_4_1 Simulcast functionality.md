### [5.4.1 联播功能](http://w3c.github.io/webrtc-pc/#simulcast-functionality)

通过`RTCPeerConnection`对象的`addTransceiver`方法和`RTCRtpSender`对象的`setParameters`方法提供联播功能。
`addTransceiver`方法建立联播信封，其中包括可以发送的最大联播流数量，以及编码的顺序。虽然可以使用`setParameters`方法修改单个联播流的特征，但不能更改联播信封。此模型的一个含义是`addTrack`方法无法提供联播功能，因为它不将`sendEncodings`作为参数，因此无法配置`RTCRtpTransceiver`来发送联播。
虽然`setParameters`无法修改联播信封，但仍可以控制发送的流的数量和这些流的特征。使用`setParameters`，可以通过将`active`属性设置为`false`来使联播流处于非活动状态，或者可以通过将`active`属性设置为`true`来重新激活联播流。使用`setParameters`，可以通过修改`maxBitrate`和`maxFramerate`等属性来更改流特性。

此规范未定义如何配置`createOffer`以接收多个 RTP 编码。但是，当使用能够发送[JSEP]中定义的多个 RTP 编码的相应远程描述调用`setRemoteDescription`时，`RTCRtpReceiver`可以接收多个 RTP 编码，并且通过收发器的`receiver.getParameters（）`检索的参数将反映协商的编码。
>NOTE
>
>在选择性转发单元（SFU）在从用户代理接收的联播流之间切换的情况下，`RTCRtpReceiver`可以接收多个RTP流。如果 SFU 不重写 RTP 报头以便在转发之前将切换流安排到单个 RTP 流中，则 RTCRtpReceiver 将接收来自不同 RTP 流的分组，每个 RTP 流具有其自己的 SSRC 和序列号空间。虽然 SFU 可能仅在任何给定时间转发单个 RTP 流，但是由于重新排序，来自多个 RTP 流的分组可能在接收器处混合。因此，配备用于接收多个 RTP 流的 RTCRtpReceiver 将需要能够正确地对接收的分组进行排序，识别潜在的丢失事件并对它们作出反应。在这种情况下的正确操作是非常重要的，因此对于本规范的实现是可选的。
