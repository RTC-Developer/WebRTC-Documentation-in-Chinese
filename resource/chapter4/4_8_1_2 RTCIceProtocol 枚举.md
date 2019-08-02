#### [4.8.1.2 RTCIceProtocol枚举](http://w3c.github.io/webrtc-pc/#rtciceprotocol-enum)

`RTCIceProtocol`表示ICE候选者的协议。

```
enum RTCIceProtocol {
    "udp",
    "tcp"
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
		udp
		</td>
		<td>
		表示一个基于UDP协议的候选人，详细描述参考 [ICE].
		</td>
	</tr>
	<tr>
		<td>
		tcp
		</td>
		<td>
	  表示一个基于tcp协议的候选人，详细描述参考 [RFC6544].
		</td>
	</tr>
</table>
