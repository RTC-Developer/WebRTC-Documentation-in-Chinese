## [4.3 状态定义](http://w3c.github.io/webrtc-pc/#state-definitions)

### [4.3.1 RTCSignalingState 枚举](http://w3c.github.io/webrtc-pc/#rtcsignalingstate-enum)

```
enum RTCSignalingState {
  "stable",
  "have-local-offer",
  "have-remote-offer",
  "have-local-pranswer",
  "have-remote-pranswer",
  "closed"
};
```

<table>
	<tr>
		<td colspan="2">
		Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		stable
		</td>
		<td>
		
		没有 offer/answer 交换正在进行。这也是初始状态，在这种情况下，本地和远程描述为空。
		</td>
	</tr>
	<tr>
		<td>
		have-local-offer	
		</td>
		<td>
		成功使用“offer”类型的本地描述。
		</td>
	</tr>
	<tr>
		<td>
		have-remote-offer	
		</td>
		<td>
		成功使用“offer”类型的远程描述。
		</td>
	</tr>
	<tr>
		<td>
		have-local-pranswer	
		</td>
		<td>
		zh：已成功应用“offer”类型的远程描述，并已成功应用“pranswer”类型的本地描述。
		</td>
	</tr>
	<tr>
		<td>
		have-remote-pranswer	
		</td>
		<td>
		已成功应用“offer”类型的本地描述，并且已成功应用“pranswer”类型的远程描述。
		</td>
	</tr>
	<tr>
		<td>
		closed	
		</td>
		<td>
		`RTCPeerConnection`已关闭;它的[[IsClosed]]值是 true 的。
		</td>
	</tr>
</table>

![](/image/peerstates.png)
*Figure 1 Non-normative signalling state transitions diagram. Method calls abbreviated.*

An example set of transitions might be:

一组状态转换示例：

呼叫者状态转换：

- new RTCPeerConnection(): stable
- setLocalDescription(offer): have-local-offer
- setRemoteDescription(pranswer): have-remote-pranswer
- setRemoteDescription(answer): stable



被呼叫者状态转换：

- new RTCPeerConnection(): stable
- setRemoteDescription(offer): have-remote-offer
- setLocalDescription(pranswer): have-local-pranswer
- setLocalDescription(answer): stable


