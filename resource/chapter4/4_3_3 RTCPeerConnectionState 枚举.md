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
		zh:RTCPeerConnection对象的[[IsClosed]]值为true。
		</td>
	</tr>
	<tr>
		<td>
		failed
		</td>
		<td>
		zh:之前的状态不适用，任何RTCIceTransports或RTCDtlsTransports都处于“failed”状态。
		</td>
	</tr>
	<tr>
		<td>
		disconnected
		</td>
		<td>
		zh:之前的状态不适用，任何RTCIceTransports或RTCDtlsTransports都处于“disconnected”状态。
		</td>
	</tr>
	<tr>
		<td>
		new	
		</td>
		<td>
		None of the previous states apply and all RTCIceTransports and RTCDtlsTransports are in the "new" or "closed" state, or there are no transports.
		zh：以前的状态都不适用，并且所有RTCIceTransports或RTCDtlsTransport都处于“new”或“closed”状态，或者当前没有传输。
		</td>
	</tr>
	<tr>
		<td>
		connecting	
		</td>
		<td>
		None of the previous states apply and all RTCIceTransports or RTCDtlsTransports are in the "new", "connecting" or "checking" state.
		zh：以前的状态都不适用，并且所有RTCIceTransports或RTCDtlsTransport都处于“new”，“connecting”或”checking”状态。
		</td>
	</tr>
	<tr>
		<td>
		connected
		</td>
		<td>
		None of the previous states apply and all RTCIceTransports and RTCDtlsTransports are in the "connected", "completed" or "closed" state.
		zh：以前的状态均不适用，并且所有RTCIceTransports和RTCDtlsTransports都处于“connected”，“completed”或“closed”状态。
		</td>
	</tr>
</table>
