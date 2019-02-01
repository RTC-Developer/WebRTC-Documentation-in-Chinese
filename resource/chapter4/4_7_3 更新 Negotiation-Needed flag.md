### [4.7.3 Updating the Negotiation-Needed flag zh:4.7.3更新Negotiation-Needed标志](http://w3c.github.io/webrtc-pc/#updating-the-negotiation-needed-flag)

The process below occurs where referenced elsewhere in this document. It also may occur as a result of internal changes within the implementation that affect negotiation. If such changes occur, the user agent MUST queue a task to update the negotiation-needed flag.

zh:以下过程在本文档的其他地方引用。它也可能由于实施中影响谈判的内部变化而发生。如果发生此类更改，则用户代理必须对任务进行排队以更新需要协商的标志。

To update the negotiation-needed flag for connection, run the following steps:

zh:要更新连接所需的协商标志，请运行以下步骤：

1. If connection's [[IsClosed]] slot is true, abort these steps. 
zh: 如果connection的[[IsClosed]]插槽为true，则中止这些步骤。
2. If connection's signaling state is not "stable", abort these steps. 
zh: 如果连接的信令状态不“稳定”，则中止这些步骤。

	NOTE:The negotiation-needed flag will be updated once the state transitions to "stable", as part of the steps for setting an RTCSessionDescription. 
zh:一旦状态转换为“稳定”，将更新需要协商的标志，作为设置RTCSessionDescription的步骤的一部分。

4. If the result of  checking if negotiation is needed is false, clear the negotiation-needed flag by setting connection's [[NegotiationNeeded]] slot to false, and abort these steps. 
zh: 如果检查是否需要协商的结果为false，则通过将connection的[[NegotiationNeeded]]槽设置为false来清除需要协商的标志，并中止这些步骤。

5. If connection's [[NegotiationNeeded]] slot is already true, abort these steps. 
zh: 如果连接的[[NegotiationNeeded]]插槽已经为真，则中止这些步骤。

6. Set connection's [[NegotiationNeeded]] slot to true. 
zh: 将连接的[[NegotiationNeeded]]插槽设置为true。

7. Queue a task that runs the following steps: 
zh: 对运行以下步骤的任务进行排队：
	1. If connection's [[IsClosed]] slot is true, abort these steps. 
zh: 如果connection的[[IsClosed]]插槽为true，则中止这些步骤。
	2.  If connection's [[NegotiationNeeded]] slot is false, abort these steps. 
zh: 如果连接的[[NegotiationNeeded]]插槽为false，则中止这些步骤。
	3.  Fire an event named negotiationneeded at connection. 
zh: 在连接时触发名为negotiationneeded的事件。

		NOTE:his queueing prevents negotiationneeded from firing prematurely, in the common situation where multiple modifications to connection are being made at once.
		zh：这种排队可防止在一次性对连接进行多次修改的常见情况下过早触发协商。
		
To check if negotiation is needed for connection, perform the following checks:

zh:要检查连接是否需要协商，请执行以下检查：

1.  If any implementation-specific negotiation is required, as described at the start of this section, return true.  
zh: 如果需要任何特定于实现的协商，如本节开头所述，则返回true。

2.  Let description be connection.[[CurrentLocalDescription]]. 
zh: 让描述成为连接。[[CurrentLocalDescription]]。

3.  If connection has created any RTCDataChannels, and no m= section in description has been negotiated yet for data, return true. 
zh: 如果连接已创建任何RTCDataChannel，并且尚未为数据协商描述中的m =部分，则返回true。

4.  For each transceiver in connection's set of transceivers, perform the following checks: 
zh: 对于连接的一组收发器中的每个收发器，执行以下检查：

	1. If transceiver isn't  stopped and isn't yet associated with an m= section in description, return true. 
zh: 如果收发器未停止且尚未与描述中的m =部分关联，则返回true。
	
	2. If transceiver isn't  stopped and is associated with an m= section in description then perform the following checks:  	
zh: 如果收发器没有停止并且与描述中的m =部分相关联，则执行以下检查：	
		1.  If transceiver.[[Direction]] is "sendrecv" or "sendonly", and the associated m= section in description either doesn't contain a single "a=msid" line, or the number of MSIDs from the "a=msid" lines in this m= section, or the MSID values themselves, differ from what is in transceiver.sender.[[AssociatedMediaStreamIds]], return true.  
zh: 如果收发器。[[Direction]]是“sendrecv”或“sendonly”，并且描述中关联的m =部分不包含单个“a = msid”行，或者来自“a = msid”的MSID数量“此m =节中的行或MSID值本身与transceiver.sender中的行不同。[[AssociatedMediaStreamIds]]，返回true。
		
		2.  If description is of type "offer", and the direction of the associated m= section in neither connection.[[CurrentLocalDescription]] nor connection.[[CurrentRemoteDescription]] matches transceiver.[[Direction]], return true. 
zh: 如果描述是“offer”类型，并且关联m = section的方向在两个连接中都没有。[[CurrentLocalDescription]]也没有连接。[[CurrentRemoteDescription]]匹配收发器。[[Direction]]，返回true。

		3.  If description is of type "answer", and the direction of the associated m= section in the description does not match transceiver.[[Direction]] intersected with the offered direction (as described in [JSEP] (section 5.3.1.)), return true. 
zh: 如果描述的类型为“answer”，并且描述中关联的m =部分的方向与收发器不匹配。[[Direction]]与提供的方向相交（如[JSEP]（第5.3.1节）中所述） ），返回true。

	3.  If transceiver is  stopped and is associated with an m= section, but the associated m= section is not yet rejected in connection.[[CurrentLocalDescription]] or connection.[[CurrentRemoteDescription]], return true. 
zh: 如果收发器已停止且与m =部分相关联，但关联的m =部分尚未在连接中被拒绝[[CurrentLocalDescription]]或连接。[[CurrentRemoteDescription]]，则返回true。

5. If all the preceding checks were performed and true was not returned, nothing remains to be negotiated; return false. 
zh: 如果执行了所有前面的检查并且未返回true，则无需进行任何协商;返回false。
