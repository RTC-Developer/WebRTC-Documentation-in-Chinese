### 4.3.2 [RTCIceGatheringState 枚举](http://w3c.github.io/webrtc-pc/#rtcicegatheringstate-enum)

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
		Any of the RTCIceTransports are in the "new" gathering state and none of the transports are in the "gathering" state, or there are no transports.
		zh:任何RTCIceTransport都处于“新”聚集状态，并且没有任何传输处于“聚集”状态，或者没有传输。
		</td>
	</tr>
	<tr>
		<td>
		gathering
		</td>
		<td>
		Any of the RTCIceTransports are in the "gathering" state.
		</td>
	</tr>
	<tr>
		<td>
		complete
		</td>
		<td>
		At least one RTCIceTransport exists, and all RTCIceTransports are in the "completed" gathering state.
		zh:至少存在一个RTCIceTransport，并且所有RTCIceTransport都处于“已完成”的收集状态。
		</td>
	</tr>
</table>

