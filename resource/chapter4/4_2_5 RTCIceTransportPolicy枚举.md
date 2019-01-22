[4.2.5 RTCIceTransportPolicy 枚举](http://w3c.github.io/webrtc-pc/#rtcicetransportpolicy-enum)

As described in [JSEP] (section 4.1.1.), if the iceTransportPolicy member of the RTCConfiguration is specified, it defines the ICE candidate policy [JSEP] (section 3.5.3.) the browser uses to surface the permitted candidates to the application; only these candidates will be used for connectivity checks.

zh:如[JSEP]（第4.1.1节）中所述，如果指定了RTCConfiguration的iceTransportPolicy成员，则它定义了浏览器用于将允许的候选者表面化为ICE候选策略[JSEP]（第3.5.3节）。应用;只有这些候选人才会用于连接检查。

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
		The ICE Agent uses only media relay candidates such as candidates passing through a TURN server.
		zh: ICE代理仅使用媒体中继候选者，例如通过TURN服务器的候选者。
		NOTE:This can be used to prevent the remote endpoint from learning the user's IP addresses, which may be desired in certain use cases. For example, in a "call"-based application, the application may want to prevent an unknown caller from learning the callee's IP addresses until the callee has consented in some way.
		NOTE：这可以用于防止远程端点了解到用户的IP地址，这在某些用例中可能是需求。例如，在基于“呼叫”的应用程序中，应用程序可能希望阻止未知呼叫者学习被呼叫者的IP地址，直到被呼叫者以某种方式同意为止。
		</td>
	</tr>
	<tr>
		<td>
		all	
		</td>
		<td>
		The ICE Agent can use any type of candidate when this value is specified.
		zh: 指定此值时，ICE代理可以使用任何类型的候选。
		NOTE:The implementation can still use its own candidate filtering policy in order to limit the IP addresses exposed to the application, as noted in the description of RTCIceCandidate.address.
		zh:该实现仍然可以使用其自己的候选过滤策略，以限制暴露给应用程序的IP地址，如RTCIceCandidate.address的描述中所述。
		</td>
	</tr>
</table>
