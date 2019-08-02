#### [4.8.1.4 RTCIceCandidateType枚举](http://w3c.github.io/webrtc-pc/#rtcicecandidatetype-enum)

RTCIceCandidateType表示ICE候选的类型，如[ICE]第15.1节中所定义。

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
		枚举描述
		</td>
	</tr>
	<tr>
		<td>
		host
		</td>
		<td>
		表示一个主持人候选人, 详细描述参考 4.1.1.1 节 [ICE].
		</td>
	</tr>
	<tr>
		<td>
		srflx
		</td>
		<td>
		表示一个服务端反身候选人,  详细描述参考 4.1.1.2 节 [ICE].
		</td>
	</tr>
	<tr>
		<td>
		prflx
		</td>
		<td>
		表示一个对端反身候选人，详细描述参考 4.1.1.2 节 [ICE].
		</td>
	</tr>
	<tr>
		<td>
		relay
		</td>
		<td>
		表示一个中继候选人, 详细描述参考 7.1.3.2.1 节 [ICE].
		</td>
	</tr>
</table>
