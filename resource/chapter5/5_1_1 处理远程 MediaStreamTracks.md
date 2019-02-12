### [5.1.1 Processing Remote MediaStreamTracks](http://w3c.github.io/webrtc-pc/#processing-remote-mediastreamtracks)

An application can reject incoming media descriptions by calling RTCRtpTransceiver.stop() to stop both directions, or set the transceiver's direction to "sendonly" to reject only the incoming side.

zh:应用程序可以通过调用RTCRtpTransceiver.stop（）来停止两个方向来拒绝传入的媒体描述，或者将收发器的方向设置为“sendonly”以仅拒绝传入的一方。

To  process the addition of a remote track for an incoming media description [JSEP] (section 5.10.) given RTCRtpTransceiver transceiver and trackEventInits, the user agent MUST run the following steps:

zh:要在给定RTCRtpTransceiver收发器和trackEventInits的情况下为传入媒体描述[JSEP]（第5.10节）添加远程轨道，用户代理必须运行以下步骤：

1.  Let receiver be transceiver's [[Receiver]].  
zh: 让接收器成为收发器的[[接收器]]。

2.  Let track be receiver's [[ReceiverTrack]].  
zh: 让跟踪成为接收者的[[ReceiverTrack]]。

3.  Let streams be receiver's [[AssociatedRemoteMediaStreams]] slot.  
zh: 让流成为接收者的[[AssociatedRemoteMediaStreams]]时隙。

4.  Create a new RTCTrackEventInit dictionary with receiver, track, streams and transceiver as members and add it to trackEventInits. 
zh: 创建一个新的RTCTrackEventInit字典，其中包含接收器，轨道，流和收发器作为成员，并将其添加到trackEventInits。


To  process the removal of a remote track for an incoming media description [JSEP] (section 5.10.) given RTCRtpTransceiver transceiver and muteTracks, the user agent MUST run the following steps:

zh:要在给定RTCRtpTransceiver收发器和muteTracks的情况下处理传入媒体描述[JSEP]（第5.10节）的远程轨道，用户代理必须执行以下步骤：

1.  Let receiver be transceiver's [[Receiver]].  
zh: 让接收器成为收发器的[[接收器]]。

2.  Let track be receiver's [[ReceiverTrack]].  
zh: 让跟踪成为接收者的[[ReceiverTrack]]。

3.  If track.muted is false, add track to muteTracks. 
zh: 如果track.muted为false，则将轨道添加到muteTracks。

To set the associated remote streams given RTCRtpReceiver receiver, msids, addList, and removeList, the user agent MUST run the following steps:

zh:要在给定RTCRtpReceiver接收器，msids，addList和removeList的情况下设置关联的远程流，用户代理必须运行以下步骤：

1.  Let connection be the RTCPeerConnection object associated with receiver. 
zh: 让连接成为与接收者关联的RTCPeerConnection对象。

2.  For each MSID in msids, unless a MediaStream object has previously been created with that id for this connection, create a MediaStream object with that id. 
zh: 对于msids中的每个MSID，除非先前已使用该连接的id创建了MediaStream对象，否则请使用该id创建MediaStream对象。

3.  Let streams be a list of the MediaStream objects created for this connection with the ids corresponding to msids. 
zh: 令stream为使用与msids对应的id为此连接创建的MediaStream对象的列表。

4.  Let track be receiver's [[ReceiverTrack]].  
zh: 让跟踪成为接收者的[[ReceiverTrack]]。

5.  For each stream in receiver's [[AssociatedRemoteMediaStreams]] that is not present in streams, add stream and track as a pair to removeList.  
zh: 对于流中不存在的接收者[[AssociatedRemoteMediaStreams]]中的每个流，将stream和track作为一对添加到removeList中。

6.  For each stream in streams that is not present in receiver's [[AssociatedRemoteMediaStreams]], add stream and track as a pair to addList. 
zh: 对于接收者[[AssociatedRemoteMediaStreams]]中不存在的流中的每个流，将流和跟踪作为一对添加到addList。

7.  Set receiver's [[AssociatedRemoteMediaStreams]] slot to streams.  
zh: 将接收者的[[AssociatedRemoteMediaStreams]]时隙设置为流。
