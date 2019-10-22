### [4.3.4 RTCIceConnectionState 枚举](http://w3c.github.io/webrtc-pc/#rtciceconnectionstate-enum)

```
enum RTCIceConnectionState {
  "closed",
  "failed",
  "disconnected",
  "new",
  "checking",
  "completed",
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
		RTCPeerConnection对象的[[IsClosed]]值为true。
		</td>
	</tr>
	<tr>
		<td>
		failed
		</td>
		<td>
		之前的状态不适用，并且任何RTCIceTransport都处于“failed”状态。
		</td>
	</tr>
	<tr>
		<td>
		disconnected
		</td>
		<td>
		以前的状态都不适用，并且任何RTCIceTransport都处于“disconnected”状态。
		</td>
	</tr>
	<tr>
		<td>
		new	
		</td>
		<td>
		以前的状态都不适用，并且所有RTCIceTransport都处于“new”或“closed”状态，或者没有传输。
		</td>
	</tr>
	<tr>
		<td>
		checking
		</td>
		<td>
		以前的状态都不适用，并且任何RTCIceTransport都处于new”或“checking”状态。
		</td>
	</tr>
	<tr>
		<td>
		completed
		</td>
		<td>
		以前的状态均不适用，并且所有RTCIceTransport都处于“completed”或“closed”状态。
		</td>
	</tr>
	<tr>
		<td>
		connected
		</td>
		<td>
		以前的状态均不适用，并且所有RTCIceTransport都处于“connected”，“completed”或“closed”状态。
		</td>
	</tr>
</table>

注意，如果由于信令（例如，RTCP多路复用或捆绑）而丢弃RTCIceTransport，或者由于信令（例如，添加新媒体描述）而创建RTCIceTransport，则状态可以直接从一个状态前进到另一个状态。


		
