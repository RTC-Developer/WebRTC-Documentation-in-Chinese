### [4.3.3 RTCPeerConnectionState 枚举](http://w3c.github.io/webrtc-pc/#rtcpeerconnectionstate-enum)

```
enum RTCPeerConnectionState {
  "closed",
  "failed",
  "disconnected",
  "new",
  "connecting",
  "connected"
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
		closed
		</td>
		<td>
		The RTCPeerConnection object's [[IsClosed]] slot is true.
		zh:RTCPeerConnection对象的[[IsClosed]]插槽为true。
		</td>
	</tr>
	<tr>
		<td>
		failed
		</td>
		<td>
		The previous state doesn't apply and any RTCIceTransports or RTCDtlsTransports are in the "failed" state.
		zh:之前的状态不适用，任何RTCIceTransports或RTCDtlsTransports都处于“失败”状态。
		</td>
	</tr>
	<tr>
		<td>
		disconnected
		</td>
		<td>
		None of the previous states apply and any RTCIceTransports or RTCDtlsTransports are in the "disconnected" state.
		</td>
	</tr>
	<tr>
		<td>
		new	
		</td>
		<td>
		None of the previous states apply and all RTCIceTransports and RTCDtlsTransports are in the "new" or "closed" state, or there are no transports.
		zh:以前的状态均不适用，并且任何RTCIceTransports或RTCDtlsTransports都处于“断开连接”状态。
		</td>
	</tr>
	<tr>
		<td>
		connecting	
		</td>
		<td>
		None of the previous states apply and all RTCIceTransports or RTCDtlsTransports are in the "new", "connecting" or "checking" state.
		zh：以前的状态都不适用，并且所有RTCIceTransports或RTCDtlsTransport都处于“新”，“连接”或“检查”状态。
		
		</td>
	</tr>
	<tr>
		<td>
		connected
		</td>
		<td>
		None of the previous states apply and all RTCIceTransports and RTCDtlsTransports are in the "connected", "completed" or "closed" state.
		zh：以前的状态均不适用，并且所有RTCIceTransports和RTCDtlsTransports都处于“已连接”，“已完成”或“已关闭”状态。
		</td>
	</tr>
</table>
