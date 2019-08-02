#### [4.8.1.3 RTCIceTcpCandidateType枚举](http://w3c.github.io/webrtc-pc/#rtcicetcpcandidatetype-enum)

`RTCIceTcpCandidateType`表示ICE TCP候选的类型，如[RFC6544]中所定义。

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
		枚举描述
		</td>
	</tr>
	<tr>
		<td>
		active
		</td>
		<td>
		表示一个`active`状态的TCP候选人，这将会尝试打开一个出站连接，但不会接收传入连接的请求。
		</td>
	</tr>
	<tr>
		<td>
		passive
		</td>
		<td>
		表示一个`passive`状态的TCP候选人，这将会接收传入连接的请求，但不会尝试打开一个出站连接。
		</td>
	</tr>
	<tr>
		<td>
		so	
		</td>
		<td>
		表示一个`so`状态的候选人，这将会尝试与对端同时打开一个连接。
		</td>
	</tr>	
</table>

NOTE：用户代理通常只收集活动的ICE TCP候选者。
