### [5.1.1 处理远程 MediaStreamTracks](http://w3c.github.io/webrtc-pc/#processing-remote-mediastreamtracks)

应用程序可以通过调用RTCRtpTransceiver.stop()停止收发direction来拒绝传入的媒体描述，或者将收发器的direction设置为“sendonly”以仅拒绝对端接入。

要在给定RTCRtpTransceiver收发器和trackEventInits的情况下为传入媒体描述[JSEP]（第5.10节）添加remote track，用户代理必须执行以下步骤：

1.  让receiver成为收发器的[[receiver]]。

2.  让track成为receiver的[[ReceiverTrack]]。

3.  让streams成为receiver的[[AssociatedRemoteMediaStreams]]。

4.  创建一个新的RTCTrackEventInit字典，其中包含receiver，track，streams和收发器作为成员，并将其添加到trackEventInits。


要在给定RTCRtpTransceiver收发器和muteTracks的情况下处理传入媒体描述[JSEP]（第5.10节）的remote track，用户代理必须执行以下步骤：

1.  让receiver成为收发器的[[Receiver]]。

2.  让track成为receiver的[[ReceiverTrack]]。

3.  如果track.muted为false，则将track添加到muteTracks。

要在给定RTCRtpReceiver类型的receiver，msids，addList和removeList的情况下设置关联的remote streams，用户代理必须执行以下步骤：

1.  让connection成为与receiver关联的RTCPeerConnection对象。

2.  对于msids中的每个MSID都创建MediaStream对象，除非先前已使用该连接的id创建了MediaStream对象。

3.  让stream成为上一步创建的MediaStream对象的列表。

4.  让track成为receiver的[[ReceiverTrack]]。

5.  对于streams中不存在于receiver的[[AssociatedRemoteMediaStreams]]中的每个stream，将其和track作为一对添加到removeList中。

6.  对于streams中不存在于receiver的[[AssociatedRemoteMediaStreams]]中的每个stream，将其和track作为一对添加到addList。

7.  将receiver的[[AssociatedRemoteMediaStreams]]值设置为streams。
