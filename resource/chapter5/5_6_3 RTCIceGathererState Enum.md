### [5.6.3 RTCIceGathererState Enum](http://w3c.github.io/webrtc-pc/#rtcicegathererstate)

```
enum RTCIceGathererState {
    "new",
    "gathering",
    "complete"
};
```
<table>
	<tr>
		<td colspan="2">
		RTCIceGathererState Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		new
		</td>
		<td>
		The RTCIceTransport was just created, and has not started gathering candidates yet.
		</td>
	</tr>
	<tr>
		<td>
		gathering
		</td>
		<td>
		The RTCIceTransport is in the process of gathering candidates.
		</td>
	</tr>
	<tr>
		<td>
		complete	
		</td>
		<td>
		The RTCIceTransport has completed gathering and the end-of-candidates indication for this transport has been sent. It will not gather candidates again until an ICE restart causes it to restart.
		</td>
	</tr>
</table>