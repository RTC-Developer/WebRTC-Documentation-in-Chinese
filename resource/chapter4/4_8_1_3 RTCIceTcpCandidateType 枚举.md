#### [4.8.1.3 RTCIceTcpCandidateType Enum zh:4.8.1.3 RTCIceTcpCandidateType枚举](http://w3c.github.io/webrtc-pc/#rtcicetcpcandidatetype-enum)

The RTCIceTcpCandidateType represents the type of the ICE TCP candidate, as defined in [RFC6544].

zh:RTCIceTcpCandidateType表示ICE TCP候选的类型，如[RFC6544]中所定义。

```
enum RTCIceTcpCandidateType {
    "active",
    "passive",
    "so"
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
		active
		</td>
		<td>
		An active TCP candidate is one for which the transport will attempt to open an outbound connection but will not receive incoming connection requests.
		</td>
	</tr>
	<tr>
		<td>
		passive
		</td>
		<td>
		A passive TCP candidate is one for which the transport will receive incoming connection attempts but not attempt a connection.
		</td>
	</tr>
	<tr>
		<td>
		so	
		</td>
		<td>
		An so candidate is one for which the transport will attempt to open a connection simultaneously with its peer.
		</td>
	</tr>	
</table>

NOTE
The user agent will typically only gather active ICE TCP candidates.

zh:用户代理通常只收集活动的ICE TCP候选者。
