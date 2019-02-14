### [5.4.1 Simulcast functionality](http://w3c.github.io/webrtc-pc/#simulcast-functionality)

Simulcast functionality is provided via the addTransceiver method of the RTCPeerConnection object and the setParameters method of the RTCRtpSender object.

zh:通过RTCPeerConnection对象的addTransceiver方法和RTCRtpSender对象的setParameters方法提供Simulcast功能。

The addTransceiver method establishes the simulcast envelope which includes the maximum number of simulcast streams that can be sent, as well as the ordering of the encodings. While characteristics of individual simulcast streams can be modified using the setParameters method, the simulcast envelope cannot be changed. One of the implications of this model is that the addTrack method cannot provide simulcast functionality since it does not take sendEncodings as an argument, and therefore cannot configure an RTCRtpTransceiver to send simulcast.

zh:addTransceiver方法建立联播信封，其中包括可以发送的最大联播流数量，以及编码的顺序。虽然可以使用setParameters方法修改单个联播流的特征，但不能更改联播信封。此模型的一个含义是addTrack方法无法提供联播功能，因为它不将sendEncodings作为参数，因此无法配置RTCRtpTransceiver来发送联播。

While setParameters cannot modify the simulcast envelope, it is still possible to control the number of streams that are sent and the characteristics of those streams. Using setParameters, simulcast streams can be made inactive by setting the active attribute to false, or can be reactivated by setting the active attribute to true. Using setParameters, stream characteristics can be changed by modifying attributes such as maxBitrate and maxFramerate.

zh:虽然setParameters无法修改联播信封，但仍可以控制发送的流的数量和这些流的特征。使用setParameters，可以通过将active属性设置为false来使联播流处于非活动状态，或者可以通过将active属性设置为true来重新激活联播流。使用setParameters，可以通过修改maxBitrate和maxFramerate等属性来更改流特性。

This specification does not define how to configure createOffer to receive multiple RTP encodings. However when setRemoteDescription is called with a corresponding remote description that is able to send multiple RTP encodings as defined in [JSEP], the RTCRtpReceiver may receive multiple RTP encodings and the parameters retrieved via the transceiver's receiver.getParameters() will reflect the encodings negotiated.

zh:此规范未定义如何配置createOffer以接收多个RTP编码。但是，当使用能够发送[JSEP]中定义的多个RTP编码的相应远程描述调用setRemoteDescription时，RTCRtpReceiver可以接收多个RTP编码，并且通过收发器的receiver.getParameters（）检索的参数将反映协商的编码。
>NOTE
>
>An RTCRtpReceiver can receive multiple RTP streams in a scenario where a Selective Forwarding Unit (SFU) switches between simulcast streams it receives from user agents. If the SFU does not rewrite RTP headers so as to arrange the switched streams into a single RTP stream prior to forwarding, the RTCRtpReceiver will receive packets from distinct RTP streams, each with their own SSRC and sequence number space. While the SFU may only forward a single RTP stream at any given time, packets from multiple RTP streams can become intermingled at the receiver due to reordering. An RTCRtpReceiver equipped to receive multiple RTP streams will therefore need to be able to correctly order the received packets, recognize potential loss events and react to them. Correct operation in this scenario is non-trivial and therefore is optional for implementations of this specification.
>
>zh:在选择性转发单元（SFU）在从用户代理接收的联播流之间切换的情况下，RTCRtpReceiver可以接收多个RTP流。如果SFU不重写RTP报头以便在转发之前将切换流安排到单个RTP流中，则RTCRtpReceiver将接收来自不同RTP流的分组，每个RTP流具有其自己的SSRC和序列号空间。虽然SFU可能仅在任何给定时间转发单个RTP流，但是由于重新排序，来自多个RTP流的分组可能在接收器处混合。因此，配备用于接收多个RTP流的RTCRtpReceiver将需要能够正确地对接收的分组进行排序，识别潜在的丢失事件并对它们作出反应。在这种情况下的正确操作是非常重要的，因此对于本规范的实现是可选的。