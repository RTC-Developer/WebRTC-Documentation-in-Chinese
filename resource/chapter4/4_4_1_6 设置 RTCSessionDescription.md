#### [4.4.1.6 设置 RTCSessionDescription](http://w3c.github.io/webrtc-pc/#set-the-rtcsessiondescription)

要在 RTCPeerConnection 对象连接上设置 RTCSessionDescription 描述，请将运行以下步骤加入 connection 的操作队列：

1.  让 p 成为新的 promise。

2. 同时，按照[JSEP]（第5.5节和第5.6节）中的描述，启动应用 description 的流程。

	1. 如果应用 description 的过程因任何原因失败，则用户代理必须将运行以下步骤的任务加入队列：

		1.  如果 connection 的[[IsClosed]] 值为true，则中止这些步骤。
		
		2.  如果 description 的类型对于当前信令连接状态无效，如[JSEP]（第5.5节和第5.6节）中所述，则使用新创建的 InvalidStateError 错误，p 以拒绝的状态返回这个错误，并中止这些步骤。

		3.  如果 description 被设置为本地描述，如果 escription.type 是 offer 并且description.sdp 不等于 connection 的[[LastOffer]]，则创建新的 InvalidModificationError 错误，p 以拒绝的状态返回这个错误，并中止这些步骤。

		4.  如果将 description 设置为本地描述，如果 description.type 为“rollback”且信令状态为“stable”，则创建新的 InvalidStateError 错误，p以拒绝的状态返回这个错误，并中止这些步骤。

		5.  如果description被设置为本地描述，如果description.type是“answer”或“pranswer”并且description.sdp不等于connection的[[LastAnswer]]，则创建新的 InvalidModificationError 错误，p 以拒绝的状态返回这个错误，并中止这些步骤。

		6. zh: 如果 description 内容不是有效的SDP语法，则使用 RTCError 拒绝 p（将errorDetail设置为“sdp-syntax-error”并将 sdpLineNumber 属性设置为检测到语法错误的SDP中的行号）并中止这些步骤。

		7.  如果将 description 设置为远程描述，则连接的 RTCRtcpMuxPolicy 是必需的，远程描述不使用 RTCP mux，然后创建新的 InvalidAccessError 错误，p 以拒绝的状态返回这个错误，并中止这些步骤。

		8.  如果 description 内容无效，则创建新的 InvalidAccessError 错误，p 以拒绝的状态返回这个错误，并中止这些步骤。

		9.  对于所有其他错误，创建新的 OperationError 错误，p 以拒绝的状态返回这个错误。

	2. zh:如果成功应用 description，则用户代理必须对运行以下步骤的任务进行排队：

		1.  如果connection的[[IsClosed]] 值为true，则中止这些步骤。

		2. 如果将 description 设置为本地描述，则运行以下步骤之一：

			- 如果 description 是“offer”类型，则将connection的[[PendingLocalDescription]]设置为从 description 构造出的新 RTCSessionDescription 对象，并将信令状态设置为“have-local-offer”。

			-  如果 description 的类型为“answer”，那么这就完成了 offer/answer 协商。将[[CurrentLocalDescription]]连接到从 description 构造的新 RTCSessionDescription 对象，并设置connection的[[PendingRemoteDescription]]为connection的[[CurrentRemoteDescription]]。将connection的[[PendingRemoteDescription]]和connection的[[PendingLocalDescription]]设置为null。最后将连接的信令状态设置为“stable”。

			-  如果 description 是“rollback”类型，那么这是一个回滚。将connection的[[PendingLocalDescription]]设置为null，并将信令状态设置为“stable”。

			-  如果 description 是“pranswer”类型，则将connection的[[PendingLocalDescription]]设置为从 description 构造出的新 RTCSessionDescription 对象，并将信令状态设置为“have-local-pranswer”。

		3. 否则，如果将 description 设置为远程描述，则运行以下步骤之一： 

			-  如果将 description 设置为远程描述，如果description.type为“rollback”且信令状态为“stable”，则使用新创建的InvalidStateError拒绝p并中止这些步骤。

			-  如果 description 是“offer”类型，则将connection的[[PendingRemoteDescription]]属性设置为从 description 构造出的新 RTCSessionDescription 对象，并将信令状态设置为“have-remote-offer”。

			-  如果 description 的类型为“answer”，那么这就完成了 offer/answer 协商。将connection的[[CurrentRemoteDescription]]属性设置为从 description 构造出的新 RTCSessionDescription 对象，并设置connection的[[CurrentLocalDescription]]到connection的[[PendingLocalDescription]]。将connection的[[PendingRemoteDescription]]和connection的[[PendingLocalDescription]]设置为null。最后将连接的信令状态设置为“stable”。

			-  如果 description 是“rollback”类型，那么这是一个回滚。将connection的[[PendingRemoteDescription]]设置为 null，并将信令状态设置为“stable”。

			-  如果 description 是“pranswer”类型，则将connection的[[PendingRemoteDescription]]设置为从 description 构造出的新 RTCSessionDescription 对象。最后将连接的信令状态设置为“have-remote-pranswer”。

		4.  如果 description 是“answer”类型，并且它启动现有 SCTP 关联的关闭，如[SCTP-SDP]第10.3和10.4节中所定义，则将 connection 的[[SctpTransport]]的值设置为null。

		5. 如果 description 的类型为“answer”或“pranswer”，则执行以下步骤：

			1.  如果 description 启动了新 SCTP 关联的建立，如[SCTP-SDP]第10.3和10.4节中所定义，则创建一个初始状态为“connecting”的 RTCSctpTransport ，并将结果分配给[[SctpTransport]]。

			2.  否则，如果建立了 SCTP 关联，但更新了“max-message-size” SDP 属性，则更新connection的[[SctpTransport]]的最大消息大小。

			3. 如果 description 协商 SCTP 传输的 DTLS 角色，并且存在具有空 id 的 RTCDataChannel，则根据[RTCWEB-DATA-PROTOCOL]生成ID。如果无法生成可用的ID，请运行以下步骤：

				1.  设channel为无法生成ID的 RTCDataChannel 对象。

				2.  将channel的[[ReadyState]]设置为“closed”。

				3.  使用 RTCErrorEvent 接口触发名为 error 的事件，并在 channel 中将 errorDetail 属性设置为“data-channel-failure”。

				4.  在 channel 上触发一个名为 close 的事件。

		6.  让trackEventInits，muteTracks，addList和removeList为空列表。

		7. 如果将 description 设置为本地描述，则运行以下步骤：

			1. 对 description 中的每个媒体描述运行以下步骤：
				1. 如果媒体描述尚未与 RTCRtpTransceiver 对象关联，请运行以下步骤：

					1. 让收发器成为用于创建媒体描述的RTCRtpTransceiver。
					
					2.  将收发器的中间值设置为媒体描述的中间值。
					
					3.  如果收发器的[[Stopped]]为true，则中止这些子步骤。

					4.   如果根据[BUNDLE]将媒体描述指示为使用现有媒体传输，则让 transport 和 rtcpTransport 分别为表示该传输的 RTP 和 RTCP 组件的R TCDtlsTransport 对象。

					5.   否则，让 transport 和 rtcpTransport 成为新创建的 RTCDtlsTransport 对象，每个对象都有一个新的底层 RTCIceTransport。虽然如果根据[RFC5761]协商 RTCP 多路复用，或者如果需要 connection 的RTCRtcpMuxPolicy，则不要创建任何特定于 RTCP 的传输对象，而是让 rtcpTransport 等于传输。

					6.   设置transceiver.[[Sender]].[[SenderTransport]]进行传输。

					7.   将transceiver.[[Sender]].[[SenderRtcpTransport]]设置为 rtcpTransport。

					8.   设置transceiver.[[接收器]].[[ReceiverTransport]]进行传输。

					9.   将transceiver.[[Receiver]].[[ReceiverRtcpTransport]]设置为 rtcpTransport。

				2.  让收发器成为与媒体描述相关联的 RTCRtpTransceiver。

				3.  如果收发器的[[Stopped]]值为true，则中止这些子步骤。

				4.  设方向是 RTCRtpTransceiverDirection 值，表示媒体描述的方向。

				5.  如果 direction 是“sendrecv”或“recvonly”，则将收发器的[[Receptive]]值设置为true，否则将其设置为false。

				6.  如果 description 的类型为“answer”或“pranswer”，则执行以下步骤：

					1. 如果 direction 是“sendonly”或“inactive”，并且收发器的[[FiredDirection]]值是“sendrecv”或“recvonly”，则执行以下步骤：

						1.  给收发器设置相关的transceiver.[[Receiver]]，空列表，另一个空列表和removeList。

						2.  在给定收发器和静音轨道的情况下，处理媒体描述的远程轨道的移除。

					2.  将收发器的[[CurrentDirection]]和[[FiredDirection]]值设置为方向。

		8. 如果将 description 设置为远程描述，则运行以下步骤：

			1. 对 description 中的每个媒体描述运行以下步骤：

				1.  设方向是 RTCRtpTransceiverDirection 类型的值，表示来自媒体描述的方向，但发送方式和接收方向相反，以表示此对等方的视图。

				2.  如[JSEP]（第5.10节）所述，尝试查找现有的 RTCRtpTransceiver 对象，收发器，以表示媒体描述。

				3.   如果未找到合适的收发器（未设置收发器），请执行以下步骤：

					1.  从媒体描述创建 RTCRtpSender 对象作为 sender。

					2.  从媒体描述创建RTCRtpReceiver 对象作为 receiver。

					3.  使用 sender、 receiver 和 值为“recvonly”的 RTCRtpTransceiverDirection 创建一个 RTCRtpTransceiver，并让收发器成为结果。

				4.  将收发器的中间值设置为相应媒体描述的中间值。如果媒体描述没有 MID，并且未设置收发器的 mid，则生成随机值，如[JSEP]（第5.10节）中所述。

				5.  如果 direction 是 “sendrecv” 或 “recvonly”，则让 msids 成为媒体描述指示收发器的 MSID 列表。[[Receiver]]。[[ReceiverTrack]]将与之关联。否则，让msids为空列表。

				6.  给定 transceiver.[[Receiver]]，msids，addList 和 removeList 的相关远程流。

				7.  如果上一步增加了 addList 的长度，或者收发器的[[FiredDirection]]值既不是 “sendrecv” 也不是 “recvonly”，则在给定收发器和 trackEventInits 的情况下添加媒体描述的远程轨道。

				8.  如果direction是“sendonly”或“inactive”，则将收发器的[[Receptive]]值设置为 false。

				9.  如果direction是“sendonly”或“inactive”，并且收发器的[[FiredDirection]]值是“sendrecv”或“recvonly”，则在给定收发器和muteTracks的情况下移除媒体描述的远程轨道。

				10.  将收发器的[[FiredDirection]]值设置为方向。

				11.  如果描述的类型为 “answer” 或 “pranswer”，则执行以下步骤：

					1.  将收发器的[[CurrentDirection]]和[[Direction]]值设置为方向。

					2.  根据[BUNDLE]，让 transport 和 rtcpTransport 成为 RTCDtlsTransport 对象，表示收发器相关媒体描述所使用的媒体传输的 RTP 和 RTCP 组件。

					3.  设置收发器.[[Sender]].[[SenderTransport]]进行传输。

					4.  将收发器.[[Sender]].[[SenderRtcpTransport]]设置为 rtcpTransport。

					5.  设置收发器.[[接收器]].[[ReceiverTransport]]进行传输。

					6.  将收发器.[[Receiver]].[[ReceiverRtcpTransport]]设置为rtcpTransport。

				12.  如果媒体描述被拒绝，并且收发器尚未停止，请停止 RTCRtpTransceiver 收发器。

		9. 如果 description 是 “rollback” 类型，则运行以下步骤：

			1.  如果正在回滚的 RTCSessionDescription 将 RTCRtpTransceiver 的中间值设置为非空值，请将该收发器的中间值设置为 null，如[JSEP]（第4.1.8.2节）所述。

			2.  如果通过应用正在回滚的 RTCSessionDescription 创建了 RTCRtpTransceiver，并且没有通过addTrack将轨道连接到它，则从 connection 的收发器集中删除该收发器，如[JSEP]（第4.1.8.2节）所述。

			3. 对于保持 connection 的 RTCRtpTransceivers，对正在回滚的 RTCSessionDescription 应用程序所做的[[CurrentDirection]]和[[Receptive]]内部值的任何更改进行还原。

			4.  将 connection 的[[SctpTransport]]的值恢复为上次稳定信令状态下的值。

		10.  如果 connection 的信令状态发生变化，则在连接时触发名为 signalingstatechange 的事件。

		11.  对于 muteTracks 中的每个轨道，将轨道的静音状态设置为值true。

		12.  对于 removeList 中的每个流和轨道对，从流中删除轨道轨道。

		13.  对于 addList 中的每个流和轨道对，将轨道轨道添加到流。

		14.  对于 trackEventInits 中的每个条目，使用 RTCTrackEvent 接口触发名为track的事件，其 receiver 属性初始化为 entry.receiver，其 track 属性初始化为entry.track，其 streams 属性初始化为entry.streams，其 receiver 属性初始化为entry .transceiver 在 connection 对象。

		15. 如果 connection 的信令状态现在是“stable”，则更新需要协商的标志。如果此更新之前和之后连接的[[NegotiationNeeded]]值均为true，则对运行以下步骤的任务进行排队：

			1.  如果connection的[[IsClosed]]值为true，则中止这些步骤

			2.  如果连接的[[NegotiationNeeded]]值为false，则中止这些步骤。

			3.  在连接时触发名为 negotiationneeded 的事件。

		16.  将 p 设为值为 undefined 的 Resolve 状态。

3.  返回p。
				
