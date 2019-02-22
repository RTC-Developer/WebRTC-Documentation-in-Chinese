## [7.3 canInsertDTMF algorithm zh:7.3 canInsertDTMF算法](http://w3c.github.io/webrtc-pc/#caninsertdtmf-algorithm)

To determine if DTMF can be sent for an RTCDTMFSender instance dtmfSender, the user agent MUST queue a task that runs the following steps:

zh:要确定是否可以为RTCDTMFSender实例dtmfSender发送DTMF，用户代理必须对运行以下步骤的任务进行排队：

1. Let sender be the RTCRtpSender associated with dtmfSender.
zh:让发件人成为与dtmfSender关联的RTCRtpSender。
2. Let transceiver be the RTCRtpTransceiver associated with sender.
zh:让收发器成为与发送者关联的RTCRtpTransceiver。
3. Let connection be the RTCPeerConnection associated with transceiver.
zh:让连接成为与收发器关联的RTCPeerConnection。
4. If connection's RTCPeerConnectionState is not "connected" return false.
zh:如果连接的RTCPeerConnectionState未“连接”，则返回false。
5. If sender's [[SenderTrack]] is null return false.
zh:如果sender的[[SenderTrack]]为null，则返回false。
6. If transceiver's [[CurrentDirection]] is neither "sendrecv" nor "sendonly" return false.
zh:如果收发器的[[CurrentDirection]]既不是“sendrecv”也不是“sendonly”，则返回false。
7. If sender's [[SendEncodings]][0].active is false return false.
zh:如果发送者的[[SendEncodings]] [0] .active为false，则返回false。
8. If no codec with mimetype "audio/telephone-event" has been negotiated for sending with this sender, return false.
zh:如果没有协商mimetype“audio / telephone-event”的编解码器与此发件人一起发送，则返回false。
9. Otherwise, return true.
zh:否则，返回true。