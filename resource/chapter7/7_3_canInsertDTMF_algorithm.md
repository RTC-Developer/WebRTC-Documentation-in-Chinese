## 7.3 canInsertDTMF算法

为了确定是否可以为RTCDTMFSender实例dtmfSender发送DTMF,用户代理必须对运行以下步骤的任务排队：

1. 让sender成为与dtmfSender关联的`RTCRtpSender`。
2. 让收发器成为与sender关联的`RTCRtpTransceiver`。
3. 让connection成为与收发器关联的`RTCPeerConnection`。
4. 如果connection的`RTCPeerConnectionState`不为`connected`，返回`false`。
5. 如果sender的[SenderTrack]为`null`，返回`false`。
6. 如果收发器的[CurrentDirection]既不是`sendrecv`也不是`sendonly`,返回`false`。
7. 如果发送者的[[SendEncodings]] `[0] .active`为`false`，则返回`false`。
8. 如果没有协商mimetype“audio / telephone-event”的编解码器与此发件人一起发送，则返回`false`。
9. 否则，返回`true`。

