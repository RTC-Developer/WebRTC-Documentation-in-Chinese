#### [4.8.1.2 RTCIceProtocol Enum zh:4.8.1.2 RTCIceProtocol枚举](http://w3c.github.io/webrtc-pc/#rtciceprotocol-enum)

The RTCIceProtocol represents the protocol of the ICE candidate.

zh:RTCIceProtocol表示ICE候选者的协议。

```
enum RTCIceProtocol {
    "udp",
    "tcp"
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
		udp
		</td>
		<td>
		A UDP candidate, as described in [ICE].
		</td>
	</tr>
	<tr>
		<td>
		tcp
		</td>
		<td>
		A TCP candidate, as described in [RFC6544].
		</td>
	</tr>
</table>
