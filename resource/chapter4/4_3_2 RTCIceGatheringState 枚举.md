### [4.3.2 RTCIceGatheringState 枚举](http://w3c.github.io/webrtc-pc/#rtcicegatheringstate-enum)

```
enum RTCIceGatheringState {
  "new",
  "gathering",
  "complete"
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
		new
		</td>
		<td>
		任何 RTCIceTransport 都处于“new”收集状态，并且没有任何传输处于“gathering”状态，或者没有传输。
		</td>
	</tr>
	<tr>
		<td>
		gathering
		</td>
		<td>
		任何 RTCIceTransport 都处于“gathering”收集状态。
		</td>
	</tr>
	<tr>
		<td>
		complete
		</td>
		<td>
		至少存在一个 RTCIceTransport，并且所有RTCIceTransport都处于“已完成”的收集状态。
		</td>
	</tr>
</table>

