### [5.6.4 RTCIceTransportState Enum](http://w3c.github.io/webrtc-pc/#rtcicetransportstate)

```
enum RTCIceTransportState {
    "new",
    "checking",
    "connected",
    "completed",
    "disconnected",
    "failed",
    "closed"
};
```

<table>
	<tr>
		<td colspan="2">
		RTCIceTransportState Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		new
		</td>
		<td>
		The RTCIceTransport is gathering candidates and/or waiting for remote candidates to be supplied, and has not yet started checking.
		</td>
	</tr>
	<tr>
		<td>
		checking
		</td>
		<td>
		The RTCIceTransport has received at least one remote candidate and is checking candidate pairs and has either not yet found a connection or consent checks [RFC7675] have failed on all previously successful candidate pairs. In addition to checking, it may also still be gathering.
		</td>
	</tr>
	<tr>
		<td>
		connected
		</td>
		<td>
		The RTCIceTransport has found a usable connection, but is still checking other candidate pairs to see if there is a better connection. It may also still be gathering and/or waiting for additional remote candidates. If consent checks [RFC7675] fail on the connection in use, and there are no other successful candidate pairs available, then the state transitions to "checking" (if there are candidate pairs remaining to be checked) or "disconnected" (if there are no candidate pairs to check, but the peer is still gathering and/or waiting for additional remote candidates).
		</td>
	</tr>
	<tr>
		<td>
		completed
		</td>
		<td>
		The RTCIceTransport has finished gathering, received an indication that there are no more remote candidates, finished checking all candidate pairs and found a connection. If consent checks [RFC7675] subsequently fail on all successful candidate pairs, the state transitions to "failed".
		</td>
	</tr>
	<tr>
		<td>
		disconnected
		</td>
		<td>
		The ICE Agent has determined that connectivity is currently lost for this RTCIceTransport. This is a transient state that may trigger intermittently (and resolve itself without action) on a flaky network. The way this state is determined is implementation dependent. Examples include:
	<br>
	- Losing the network interface for the connection in use.
	<br>
	- Repeatedly failing to receive a response to STUN requests.
	<br>
Alternatively, the RTCIceTransport has finished checking all existing candidates pairs and not found a connection (or consent checks [RFC7675] once successful, have now failed), but it is still gathering and/or waiting for additional remote candidates.
		</td>
	</tr>
	<tr>
		<td>
		failed
		</td>
		<td>
		The RTCIceTransport has finished gathering, received an indication that there are no more remote candidates, finished checking all candidate pairs, and all pairs have either failed connectivity checks or have lost consent. This is a terminal state.
		</td>
	</tr>
	<tr>
		<td>
		closed
		</td>
		<td>
		The RTCIceTransport has shut down and is no longer responding to STUN requests.
		</td>
	</tr>
</table>

An ICE restart causes candidate gathering and connectity checks to begin anew, causing a transition to connected if begun in the completed state. If begun in the transient disconnected state, it causes a transition to checking, effectively forgetting that connectivity was previously lost.

zh:ICE重启导致候选收集和连接检查重新开始，如果在完成状态下开始则导致转换到连接。如果在瞬态断开状态下开始，则会导致转换到检查，从而有效地忘记先前已丢失连接。

The failed and completed states require an indication that there are no additional remote candidates. This can be indicated by calling addIceCandidate with a candidate value whose candidate property is set to an empty string or by canTrickleIceCandidates being set to false.

zh:失败和完成状态需要指示没有其他远程候选者。这可以通过调用addIceCandidate来指示候选属性设置为空字符串或canTrickleIceCandidates设置为false的候选值来指示。

Some example state transitions are:

zh:一些示例状态转换是：

* (RTCIceTransport first created, as a result of setLocalDescription or setRemoteDescription): new
zh:（由于setLocalDescription或setRemoteDescription，RTCIceTransport首次创建）：new
* (new, remote candidates received): checking
zh:（收到新的，偏远的候选人）：检查
* (checking, found usable connection): connected
zh:（检查，发现可用连接）：已连接
* (checking, checks fail but gathering still in progress): disconnected
zh:（检查，检查失败但仍在进行中）：断开连接
* (checking, gave up): failed
zh:（检查，放弃）：失败
* (disconnected, new local candidates): checking
zh:（断开连接，新的本地候选人）：检查
* (connected, finished all checks): completed
zh:（连接，完成所有检查）：完成
* (completed, lost connectivity): disconnected
zh:（已完成，丢失连接）：已断开连接
* (disconnected or failed, ICE restart occurs): checking
zh:（断开连接或失败，ICE重启）：检查
* (completed, ICE restart occurs): connected
zh:（已完成，ICE重启）：已连接
* RTCPeerConnection.close(): closed
zh:RTCPeerConnection.close（）：已关闭

![](./image/5_6_4 pic.png)
