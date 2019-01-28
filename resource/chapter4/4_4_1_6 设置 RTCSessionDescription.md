#### [4.4.1.6 设置 RTCSessionDescription](http://w3c.github.io/webrtc-pc/#set-the-rtcsessiondescription)

To set an RTCSessionDescription description on an RTCPeerConnection object connection, enqueue the following steps to connection's operation queue:

zh:要在RTCPeerConnection对象连接上设置RTCSessionDescription描述，请将以下步骤排入连接的操作队列：

1. Let p be a new promise. 
zh: 让p成为新的承诺。

2. In parallel, start the process to apply description as described in [JSEP] (section 5.5. and section 5.6.).
zh:同时，按照[JSEP]（第5.5节和第5.6节）中的描述启动流程以应用描述。

	1. If the process to apply description fails for any reason, then user agent MUST queue a task that runs the following steps:
	zh:如果应用描述的过程因任何原因失败，则用户代理必须对运行以下步骤的任务进行排队：

		1. If connection's [[IsClosed]] slot is true, then abort these steps. 
		zh: 如果connection的[[IsClosed]] slot为true，则中止这些步骤。
		
		2. If the description's type is invalid for the current signaling state of connection as described in [JSEP] (section 5.5. and section 5.6.), then reject p with a newly created InvalidStateError and abort these steps. 
		zh: 如果描述的类型对于当前信令连接状态无效，如[JSEP]（第5.5节和第5.6节）中所述，则使用新创建的InvalidStateError拒绝p并中止这些步骤。

		3. If description is set as a local description, if description.type is offer and description.sdp is not equal to connection's [[LastOffer]] slot, then reject p with a newly created InvalidModificationError and abort these steps. 
		zh: 如果description被设置为本地描述，如果提供description.type并且description.sdp不等于connection的[[LastOffer]]槽，则使用新创建的InvalidModificationError拒绝p并中止这些步骤。

		4. If description is set as a local description, if description.type is "rollback" and signaling state is "stable" then reject p with a newly created InvalidStateError and abort these steps. 
		zh: 如果将description设置为本地描述，如果description.type为“rollback”且信令状态为“stable”，则使用新创建的InvalidStateError拒绝p并中止这些步骤。

		5. If description is set as a local description, if description.type is "answer" or "pranswer" and description.sdp is not equal to connection's [[LastAnswer]] slot, then reject p with a newly created InvalidModificationError and abort these steps. 
		zh: 如果description被设置为本地描述，如果description.type是“answer”或“pranswer”并且description.sdp不等于connection的[[LastAnswer]]槽，则使用新创建的InvalidModificationError拒绝p并中止这些步骤。

		6. If the content of description is not valid SDP syntax, then reject p with an RTCError (with errorDetail set to "sdp-syntax-error" and the sdpLineNumber attribute set to the line number in the SDP where the syntax error was detected) and abort these steps. 
		zh: 如果描述内容不是有效的SDP语法，则使用RTCError拒绝p（将errorDetail设置为“sdp-syntax-error”并将sdpLineNumber属性设置为检测到语法错误的SDP中的行号）并中止这些步骤。

		7. If description is set as a remote description, the connection's RTCRtcpMuxPolicy is require and the remote description does not use RTCP mux, then reject p with a newly created InvalidAccessError and abort these steps. 
		zh: 如果将description设置为远程描述，则连接的RTCRtcpMuxPolicy是必需的，远程描述不使用RTCP mux，然后使用新创建的InvalidAccessError拒绝p并中止这些步骤。

		8. If the content of description is invalid, then reject p with a newly created InvalidAccessError and abort these steps. 
		zh: 如果描述内容无效，则使用新创建的InvalidAccessError拒绝p并中止这些步骤。

		9. For all other errors, reject p with a newly created OperationError. 
		zh: 对于所有其他错误，请使用新创建的OperationError拒绝p。

	2. If description is applied successfully, the user agent MUST queue a task that runs the following steps:
zh:如果成功应用说明，则用户代理必须对运行以下步骤的任务进行排队：

		1. If connection's [[IsClosed]] slot is true, then abort these steps. 
zh: 如果connection的[[IsClosed]] slot为true，则中止这些步骤。

		2. If description is set as a local description, then run one of the following steps:
zh:如果将description设置为本地描述，则运行以下步骤之一：

			- If description is of type "offer", set connection.[[PendingLocalDescription]] to a new RTCSessionDescription object constructed from description, and set signaling state to "have-local-offer". 
zh: 如果description是“offer”类型，则将connection。[[PendingLocalDescription]]设置为从description构造的新RTCSessionDescription对象，并将信令状态设置为“have-local-offer”。

			- If description is of type "answer", then this completes an offer answer negotiation. Set connection.[[CurrentLocalDescription]] to a new RTCSessionDescription object constructed from description, and set connection.[[CurrentRemoteDescription]] to connection.[[PendingRemoteDescription]]. Set both connection.[[PendingRemoteDescription]] and connection.[[PendingLocalDescription]] to null. Finally set connection's signaling state to "stable". 
zh: 如果描述的类型为“answer”，那么这就完成了要约回答协商。将[[CurrentLocalDescription]]连接到从描述构造的新RTCSessionDescription对象，并设置连接。[[CurrentRemoteDescription]]到连接。[[PendingRemoteDescription]]。将[。[PendingRemoteDescription]]和connection。[[PendingLocalDescription]]设置为null。最后将连接的信令状态设置为“稳定”。

			- If description is of type "rollback", then this is a rollback. Set connection.[[PendingLocalDescription]] to null, and set signaling state to "stable". 
zh: 如果description是“rollback”类型，那么这是一个回滚。将连接。[[PendingLocalDescription]]设置为null，并将信令状态设置为“stable”。

			- If description is of type "pranswer", then set connection.[[PendingLocalDescription]] to a new RTCSessionDescription object constructed from description, and set signaling state to "have-local-pranswer". 
zh: 如果description是“pranswer”类型，则将connection [[PendingLocalDescription]]设置为从描述构造的新RTCSessionDescription对象，并将信令状态设置为“have-local-pranswer”。

		3. Otherwise, if description is set as a remote description, then run one of the following steps:
zh:否则，如果将description设置为远程描述，则运行以下步骤之一： 

			- If description is set as a remote description, if description.type is "rollback" and signaling state is "stable" then reject p with a newly created InvalidStateError and abort these steps. 
zh: 如果将description设置为远程描述，如果description.type为“rollback”且信令状态为“stable”，则使用新创建的InvalidStateError拒绝p并中止这些步骤。

			- If description is of type "offer", set connection.[[PendingRemoteDescription]] attribute to a new RTCSessionDescription object constructed from description, and set signaling state to "have-remote-offer". 
zh: 如果description是“offer”类型，则将connection。[[PendingRemoteDescription]]属性设置为从description构造的新RTCSessionDescription对象，并将信令状态设置为“have-remote-offer”。

			- If description is of type "answer", then this completes an offer answer negotiation. Set connection.[[CurrentRemoteDescription]] to a new RTCSessionDescription object constructed from description, and set connection.[[CurrentLocalDescription]] to connection.[[PendingLocalDescription]]. Set both connection.[[PendingRemoteDescription]] and connection.[[PendingLocalDescription]] to null. Finally set connection's signaling state to "stable". 
zh: 如果描述的类型为“answer”，那么这就完成了要约回答协商。将[[CurrentRemoteDescription]]连接到从描述构造的新RTCSessionDescription对象，并设置连接。[[CurrentLocalDescription]]到连接。[[PendingLocalDescription]]。将[。[PendingRemoteDescription]]和connection。[[PendingLocalDescription]]设置为null。最后将连接的信令状态设置为“稳定”。

			- If description is of type "rollback", then this is a rollback. Set connection.[[PendingRemoteDescription]] to null, and set signaling state to "stable". 
zh: 如果description是“rollback”类型，那么这是一个回滚。将连接。[[PendingRemoteDescription]]设置为null，并将信令状态设置为“stable”。

			- If description is of type "pranswer", then set connection.[[PendingRemoteDescription]] to a new RTCSessionDescription object constructed from description and signaling state to "have-remote-pranswer". 
zh: 如果description是“pranswer”类型，则将connection [。[PendingRemoteDescription]]设置为从描述和信令状态构造为“have-remote-pranswer”的新RTCSessionDescription对象。

		4. If description is of type "answer", and it initiates the closure of an existing SCTP association, as defined in [SCTP-SDP], Sections 10.3 and 10.4, set the value of connection's [[SctpTransport]] internal slot to null. 
zh: 如果description是“answer”类型，并且它启动现有SCTP关联的关闭，如[SCTP-SDP]第10.3和10.4节中所定义，则将connection的[[SctpTransport]]内部槽的值设置为null。

		5. If description is of type "answer" or "pranswer", then run the following steps:
zh:如果描述的类型为“answer”或“pranswer”，则执行以下步骤：

			1. If description initiates the establishment of a new SCTP association, as defined in [SCTP-SDP], Sections 10.3 and 10.4, create an RTCSctpTransport with an initial state of "connecting" and assign the result to the [[SctpTransport]] slot. 
zh: 如果描述启动了新SCTP关联的建立，如[SCTP-SDP]第10.3和10.4节中所定义，则创建一个初始状态为“连接”的RTCSctpTransport，并将结果分配给[[SctpTransport]]插槽。

			2. Otherwise, if an SCTP association is established, but the "max-message-size" SDP attribute is updated, update the data max message size of connection's [[SctpTransport]]. 
zh: 否则，如果建立了SCTP关联，但更新了“max-message-size”SDP属性，则更新连接的[[SctpTransport]]的数据最大消息大小。

			3. If description negotiates the DTLS role of the SCTP transport, and there is an RTCDataChannel with a null id, then generate an ID according to [RTCWEB-DATA-PROTOCOL]. If no available ID could be generated, then run the following steps:
zh:如果描述协商SCTP传输的DTLS角色，并且存在具有空id的RTCDataChannel，则根据[RTCWEB-DATA-PROTOCOL]生成ID。如果无法生成可用的ID，请运行以下步骤：

				1. Let channel be the RTCDataChannel object for which an ID could not be generated. 
zh: 设channel为无法生成ID的RTCDataChannel对象。

				2. Set channel's [[ReadyState]] slot to "closed". 
zh: 将通道的[[ReadyState]]插槽设置为“关闭”。

				3. Fire an event named error using the RTCErrorEvent interface with the errorDetail attribute set to "data-channel-failure" at channel. 
zh: 使用RTCErrorEvent接口触发名为error的事件，并在通道中将errorDetail属性设置为“data-channel-failure”。

				4. Fire an event named close at channel. 
zh: 在通道上发射一个名为close的事件。

		6. Let trackEventInits, muteTracks, addList, and removeList be empty lists. 
zh: 让trackEventInits，muteTracks，addList和removeList为空列表。

		7. If description is set as a local description, then run the following steps:
zh:如果将description设置为本地描述，则运行以下步骤：

			1. Run the following steps for each media description in description:
zh:对描述中的每个媒体描述运行以下步骤：
				1. If the media description is not yet associated with an RTCRtpTransceiver object then run the following steps:
zh:如果媒体描述尚未与RTCRtpTransceiver对象关联，请运行以下步骤：

					1. Let transceiver be the RTCRtpTransceiver used to create the media description.
					zh: 让收发器成为用于创建媒体描述的RTCRtpTransceiver。
					
					2. Set transceiver's mid value to the mid of the media description. 
zh: 将收发器的中间值设置为媒体描述的中间值。
					
					3. If transceiver's [[Stopped]] slot is true, abort these sub steps. 
zh: 如果收发器的[[Stopped]]插槽为真，则中止这些子步骤。

					4. If the media description is indicated as using an existing media transport according to [BUNDLE], let transport and rtcpTransport be the RTCDtlsTransport objects representing the RTP and RTCP components of that transport, respectively.  
zh:  如果根据[BUNDLE]将媒体描述指示为使用现有媒体传输，则让transport和rtcpTransport分别为表示该传输的RTP和RTCP组件的RTCDtlsTransport对象。

					5. Otherwise, let transport and rtcpTransport be newly created RTCDtlsTransport objects, each with a new underlying RTCIceTransport. Though if RTCP multiplexing is negotiated according to [RFC5761], or if connection's RTCRtcpMuxPolicy is require, do not create any RTCP-specific transport objects, and instead let rtcpTransport equal transport.  
zh:  否则，让transport和rtcpTransport成为新创建的RTCDtlsTransport对象，每个对象都有一个新的底层RTCIceTransport。虽然如果根据[RFC5761]协商RTCP多路复用，或者如果需要连接的RTCRtcpMuxPolicy，则不要创建任何特定于RTCP的传输对象，而是让rtcpTransport等于传输。

					6. Set transceiver.[[Sender]].[[SenderTransport]] to transport.  
zh:  设置收发器。[[Sender]]。[[SenderTransport]]进行传输。

					7. Set transceiver.[[Sender]].[[SenderRtcpTransport]] to rtcpTransport.  
zh:  将收发器。[[Sender]]。[[SenderRtcpTransport]]设置为rtcpTransport。

					8. Set transceiver.[[Receiver]].[[ReceiverTransport]] to transport.  
zh:  设置收发器。[[接收器]]。[[ReceiverTransport]]进行传输。

					9. Set transceiver.[[Receiver]].[[ReceiverRtcpTransport]] to rtcpTransport.  
zh:  将收发器。[[Receiver]]。[[ReceiverRtcpTransport]]设置为rtcpTransport。

				2. Let transceiver be the  RTCRtpTransceiver associated with the media description. 
zh: 让收发器成为与媒体描述相关联的RTCRtpTransceiver。

				3. If transceiver's [[Stopped]] slot is true, abort these sub steps. 
zh: 如果收发器的[[Stopped]]插槽为真，则中止这些子步骤。

				4. Let direction be an  RTCRtpTransceiverDirection value representing the direction from the media description. 
zh: 设方向是RTCRtpTransceiverDirection值，表示媒体描述的方向。

				5. If direction is "sendrecv" or "recvonly", set transceiver's [[Receptive]] slot to true, otherwise set it to false. 
zh: 如果direction是“sendrecv”或“recvonly”，则将收发器的[[Receptive]]插槽设置为true，否则将其设置为false。

				6. If description is of type "answer" or "pranswer", then run the following steps:
zh:如果描述的类型为“answer”或“pranswer”，则执行以下步骤：

					1. If direction is "sendonly" or "inactive", and transceiver's [[FiredDirection]] slot is either "sendrecv" or "recvonly", then run the following steps:
zh:如果direction是“sendonly”或“inactive”，并且收发器的[[FiredDirection]]插槽是“sendrecv”或“recvonly”，则执行以下步骤：

						1. Set the associated remote streams given transceiver.[[Receiver]], an empty list, another empty list, and removeList. 
zh: 给收发器设置相关的远程流。[[Receiver]]，空列表，另一个空列表和removeList。

						2. process the removal of a remote track for the media description, given transceiver and muteTracks. 
zh: 在给定收发器和静音轨道的情况下，处理媒体描述的远程轨道的移除。

					2. Set transceiver's [[CurrentDirection]] and [[FiredDirection]] slots to direction. 
zh: 将收发器的[[CurrentDirection]]和[[FiredDirection]]插槽设置为方向。

		8. If description is set as a remote description, then run the following steps:
zh:如果将description设置为远程描述，则运行以下步骤：

			1. Run the following steps for each media description in description:
zh:对描述中的每个媒体描述运行以下步骤：

				1. Let direction be an  RTCRtpTransceiverDirection value representing the direction from the media description, but with the send and receive directions reversed to represent this peer's point of view. 
zh: 设方向是RTCRtpTransceiverDirection值，表示来自媒体描述的方向，但发送方式和接收方向相反，以表示此对等方的观点。

				2. As described by [JSEP] (section 5.10.), attempt to find an existing RTCRtpTransceiver object, transceiver, to represent the media description. 
zh: 如[JSEP]（第5.10节）所述，尝试查找现有的RTCRtpTransceiver对象，收发器，以表示媒体描述。

				3. If no suitable transceiver is found (transceiver is unset), run the following steps:      
zh:  如果未找到合适的收发器（未设置收发器），请执行以下步骤：

					1. Create an RTCRtpSender, sender, from the media description. 
zh: 从媒体描述创建RTCRtpSender发件人。

					2. Create an RTCRtpReceiver, receiver, from the media description. 
zh: 从媒体描述创建RTCRtpReceiver，receiver。

					3. Create an RTCRtpTransceiver with sender, receiver and an RTCRtpTransceiverDirection value of "recvonly", and let transceiver be the result. 
zh: 创建一个RTCRtpTransceiver，其发送方，接收方和RTCRtpTransceiverDirection值为“recvonly”，并让收发器成为结果。

				4. Set transceiver's mid value to the mid of the corresponding media description. If the media description has no MID, and transceiver's mid is unset, generate a random value as described in [JSEP] (section 5.10.). 
zh: 将收发器的中间值设置为相应媒体描述的中间位置。如果媒体描述没有MID，并且未设置收发器的mid，则生成随机值，如[JSEP]（第5.10节）中所述。

				5. If direction is "sendrecv" or "recvonly", let msids be a list of the MSIDs that the media description indicates transceiver.[[Receiver]].[[ReceiverTrack]] is to be associated with. Otherwise, let msids be an empty list. 
zh: 如果direction是“sendrecv”或“recvonly”，则让msids成为媒体描述指示收发器的MSID列表。[[Receiver]]。[[ReceiverTrack]]将与之关联。否则，让msids为空列表。

				6. Set the associated remote streams given transceiver.[[Receiver]], msids, addList, and removeList. 
zh: 给定收发器[[Receiver]]，msids，addList和removeList的相关远程流。

				7. If the previous step increased the length of addList, or if transceiver's [[FiredDirection]] slot is neither "sendrecv" nor "recvonly", process the addition of a remote track for the media description, given transceiver and trackEventInits. 
zh: 如果上一步增加了addList的长度，或者收发器的[[FiredDirection]]槽既不是“sendrecv”也不是“recvonly”，则在给定收发器和trackEventInits的情况下处理媒体描述的远程轨道的添加。

				8. If direction is "sendonly" or "inactive", set transceiver's [[Receptive]] slot to false. 
zh: 如果direction是“sendonly”或“inactive”，则将收发器的[[Receptive]]插槽设置为false。

				9. If direction is "sendonly" or "inactive", and transceiver's [[FiredDirection]] slot is either "sendrecv" or "recvonly", process the removal of a remote track for the media description, given transceiver and muteTracks. 
zh: 如果direction是“sendonly”或“inactive”，并且收发器的[[FiredDirection]]插槽是“sendrecv”或“recvonly”，则在给定收发器和muteTracks的情况下处理媒体描述的远程轨道的移除。

				10. Set transceiver's [[FiredDirection]] slot to direction. 
zh: 将收发器的[[FiredDirection]]插槽设置为方向。

				11. If description is of type "answer" or "pranswer", then run the following steps:
zh:如果描述的类型为“answer”或“pranswer”，则执行以下步骤：

					1. Set transceiver's [[CurrentDirection]] and [[Direction]] slots to direction. 
zh: 将收发器的[[CurrentDirection]]和[[Direction]]插槽设置为方向。

					2. Let transport and rtcpTransport be the RTCDtlsTransport objects representing the RTP and RTCP components of the media transport used by transceiver's associated media description, according to [BUNDLE].  
zh:  根据[BUNDLE]，让transport和rtcpTransport成为RTCDtlsTransport对象，表示收发器相关媒体描述所使用的媒体传输的RTP和RTCP组件。

					3. Set transceiver.[[Sender]].[[SenderTransport]] to transport.  
zh:  设置收发器。[[Sender]]。[[SenderTransport]]进行传输。

					4. Set transceiver.[[Sender]].[[SenderRtcpTransport]] to rtcpTransport.  
zh:  将收发器。[[Sender]]。[[SenderRtcpTransport]]设置为rtcpTransport。

					5. Set transceiver.[[Receiver]].[[ReceiverTransport]] to transport.  
zh:  设置收发器。[[接收器]]。[[ReceiverTransport]]进行传输。

					6. Set transceiver.[[Receiver]].[[ReceiverRtcpTransport]] to rtcpTransport.  
zh:  将收发器。[[Receiver]]。[[ReceiverRtcpTransport]]设置为rtcpTransport。

				12. If the media description is rejected, and transceiver is not already stopped, stop the RTCRtpTransceiver transceiver. 
zh: 如果媒体描述被拒绝，并且收发器尚未停止，请停止RTCRtpTransceiver收发器。

		9. If description is of type "rollback", then run the following steps:
zh:如果description是“rollback”类型，则运行以下步骤：

			1. If the mid value of an RTCRtpTransceiver was set to a non-null value by the RTCSessionDescription that is being rolled back, set the mid value of that transceiver to null, as described by [JSEP] (section 4.1.8.2.). 
zh: 如果正在回滚的RTCSessionDescription将RTCRtpTransceiver的中间值设置为非空值，请将该收发器的中间值设置为null，如[JSEP]（第4.1.8.2节）所述。

			2. If an RTCRtpTransceiver was created by applying the RTCSessionDescription that is being rolled back, and a track has not been attached to it via addTrack, remove that transceiver from connection's set of transceivers, as described by [JSEP] (section 4.1.8.2.). 
zh: 如果通过应用正在回滚的RTCSessionDescription创建了RTCRtpTransceiver，并且没有通过addTrack将轨道连接到它，则从连接的收发器集中删除该收发器，如[JSEP]（第4.1.8.2节）所述。

			3. For the RTCRtpTransceivers remaining on connection, revert any changes to the [[CurrentDirection]] and [[Receptive]] internal slots made by the application of the RTCSessionDescription that is being rolled back. 
zh:对于保持连接的RTCRtpTransceivers，还原对正在回滚的RTCSessionDescription应用程序所做的[[CurrentDirection]]和[[Receptive]]内部插槽的任何更改。

			4. Restore the value of connection's [[SctpTransport]] internal slot to its value at the last stable signaling state. 
zh: 将连接的[[SctpTransport]]内部插槽的值恢复为上次稳定信令状态下的值。

		10. If connection's signaling state changed above, fire an event named signalingstatechange at connection. 
zh: 如果连接的信令状态发生变化，则在连接时触发名为signalingstatechange的事件。

		11. For each track in muteTracks, set the muted state of track to the value true. 
zh: 对于muteTracks中的每个轨道，将轨道的静音状态设置为值true。

		12. For each stream and track pair in removeList, remove the track track from stream. 
zh: 对于removeList中的每个流和轨道对，从流中删除轨道轨道。

		13. For each stream and track pair in addList, add the track track to stream. 
zh: 对于addList中的每个流和轨道对，将轨道轨道添加到流。

		14. For each entry entry in trackEventInits, fire an event named track using the RTCTrackEvent interface with its receiver attribute initialized to entry.receiver, its track attribute initialized to entry.track, its streams attribute initialized to entry.streams and its transceiver attribute initialized to entry.transceiver at the connection object. 
zh: 对于trackEventInits中的每个条目，使用RTCTrackEvent接口触发名为track的事件，其receiver属性初始化为entry.receiver，其track属性初始化为entry.track，其streams属性初始化为entry.streams，其receiver属性初始化为entry .transceiver在连接对象。

		15. If connection's signaling state is now "stable", update the negotiation-needed flag. If connection's [[NegotiationNeeded]] slot was true both before and after this update, queue a task that runs the following steps:
zh:如果连接的信令状态现在是“稳定的”，则更新需要协商的标志。如果此更新之前和之后连接的[[NegotiationNeeded]]插槽均为true，则对运行以下步骤的任务进行排队：

			1. If connection's [[IsClosed]] slot is true, abort these steps. 
zh: 如果connection的[[IsClosed]]插槽为true，则中止这些步骤

			2. If connection's [[NegotiationNeeded]] slot is false, abort these steps. 
zh: 如果连接的[[NegotiationNeeded]]插槽为false，则中止这些步骤。

			3. Fire an event named negotiationneeded at connection. 
zh: 在连接时触发名为negotiationneeded的事件。

		16. Resolve p with undefined. 
zh: 使用undefined解析p。

3. Return p. 
zh: 返回p。
				
