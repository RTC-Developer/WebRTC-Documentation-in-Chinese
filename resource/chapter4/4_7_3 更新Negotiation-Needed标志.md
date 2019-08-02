### [4.7.3 更新Negotiation-Needed标志](http://w3c.github.io/webrtc-pc/#updating-the-negotiation-needed-flag)

以下的过程在本文档的其他地方引用。它也可能由于实施中影响谈判的内部变化而发生。如果发生此类更改，则用户代理必须对任务进行排队以更新协商需要的标志。

要更新连接协商需要的标志，请运行以下步骤：

1. 如果connection的[[IsClosed]]插槽为true，则中止这些步骤。
2. 如果连接的信令状态不是“stable”，则中止这些步骤。

	NOTE：一旦状态转换为“稳定”，将更新协商需要的标志，作为设置RTCSessionDescription的步骤的一部分。

3. 如果检查是否需要协商的结果为false，则通过将connection的[[NegotiationNeeded]]槽设置为false来清除需要协商的标志，并中止这些步骤。

4. 如果连接的[[NegotiationNeeded]]插槽已经为真，则中止这些步骤。

5. 将连接的[[NegotiationNeeded]]插槽设置为true。

6. 对运行以下步骤的任务进行排队：
	1. 如果connection的[[IsClosed]]插槽为true，则中止这些步骤。
	2. 如果连接的[[NegotiationNeeded]]插槽为false，则中止这些步骤。
	3. 在连接时触发名为`negotiationneeded`的事件。

		NOTE：这种排队可防止在一次性对连接进行多次修改的常见情况下过早触发协商。
		
要检查连接是否需要协商，请执行以下检查：

1.  如果需要任何特定于实现的协商，如本节开头所述，则应返回true。

2.  让描述成为连接。[[CurrentLocalDescription]]。

3.   如果连接已创建任何RTCDataChannel，并且尚未为数据协商描述中的`m= section`，则返回true。

4.  对于连接的一组收发器中的每个收发器，执行以下检查：

	1. 如果收发器未停止且尚未与描述中的`m= section`关联，则返回true。
	
	2. 如果收发器没有停止并且与描述中的`m= section`相关联，则执行以下检查：	
		1.  如果收发器。[[Direction]]是“sendrecv”或“sendonly”，并且描述中关联的m =部分不包含单个“a = msid”行，或者来自“a = msid”的MSID数量“此m =节中的行或MSID值本身与transceiver.sender中的行不同。[[AssociatedMediaStreamIds]]，返回true。
		
		2.  如果描述的类型为`offer`，并且关联`m= section`的方向在两个连接中都没有。[[CurrentLocalDescription]]也没有连接。[[CurrentRemoteDescription]]匹配收发器。[[Direction]]，返回true。

		3.  如果描述的类型为`answer`，并且描述中关联的`m= section`的方向与收发器不匹配。[[Direction]]与提供的方向相交（如[JSEP]（第5.3.1节）中所述） ），返回true。

	3.  如果收发器已停止且与`m= section`相关联，但关联的`m= section`尚未在连接中被拒绝[[CurrentLocalDescription]]或连接。[[CurrentRemoteDescription]]，则返回true。

5. 如果执行了所有前面的检查并且未返回true，则无需进行任何协商;则返回false。
