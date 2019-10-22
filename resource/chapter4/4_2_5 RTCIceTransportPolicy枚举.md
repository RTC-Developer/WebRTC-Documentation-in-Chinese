### [4.2.5 RTCIceTransportPolicy 枚举](http://w3c.github.io/webrtc-pc/#rtcicetransportpolicy-enum)



如[JSEP]（第4.1.1节）中所述，如果指定了RTCConfiguration的iceTransportPolicy成员，则它定义了浏览器获取ICE候选地址的策略[JSEP]（第3.5.3节）;只有这些候选地址才会用于连接性检查。

```
enum RTCIceTransportPolicy {
  "relay",
  "all"
};
```

<table>
	<tr>
		<td colspan="2">
		Enumeration description (non-normative)
		</td>
	</tr>
	<tr>
		<td>
		relay
		</td>
		<td>
		ICE代理仅使用媒体中继候选地址，例如通过TURN服务器的候选地址。
		NOTE：这可以用于防止远端了解到用户的IP地址，这可能用于一些特定的情况下。例如，在基于“呼叫”的应用程序中，应用程序可能不希望未知呼叫者知道被呼叫者的IP地址，直到被呼叫者以某种方式同意为止。
		</td>
	</tr>
	<tr>
		<td>
		all	
		</td>
		<td>
		指定此值时，ICE代理可以使用任何类型的候选地址。
		该实现仍然可以使用其自己的候选过滤策略，以限制暴露IP地址给应用程序，如RTCIceCandidate.address的描述中所述。
		</td>
	</tr>
</table>
