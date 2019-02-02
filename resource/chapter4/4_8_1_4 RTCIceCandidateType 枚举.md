#### [4.8.1.4 RTCIceCandidateType Enum zh:4.8.1.4 RTCIceCandidateType枚举](http://w3c.github.io/webrtc-pc/#rtcicecandidatetype-enum)

The RTCIceCandidateType represents the type of the ICE candidate, as defined in [ICE] section 15.1.

zh:RTCIceCandidateType表示ICE候选的类型，如[ICE]第15.1节中所定义。

```
enum RTCIceCandidateType {
    "host",
    "srflx",
    "prflx",
    "relay"
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
		host
		</td>
		<td>
		A host candidate, as defined in Section 4.1.1.1 of [ICE].
		</td>
	</tr>
	<tr>
		<td>
		srflx
		</td>
		<td>
		A server reflexive candidate, as defined in Section 4.1.1.2 of [ICE].
		</td>
	</tr>
	<tr>
		<td>
		prflx
		</td>
		<td>
		A peer reflexive candidate, as defined in Section 4.1.1.2 of [ICE].
		</td>
	</tr>
	<tr>
		<td>
		relay
		</td>
		<td>
		A relay candidate, as defined in Section 7.1.3.2.1 of [ICE].
		</td>
	</tr>
</table>
