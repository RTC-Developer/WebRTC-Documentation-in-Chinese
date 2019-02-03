### [4.9.1 RTCPriorityType Enum zh:4.9.1 RTCPriorityType枚举](http://w3c.github.io/webrtc-pc/#rtcprioritytype-enum)

```
enum RTCPriorityType {
    "very-low",
    "low",
    "medium",
    "high"
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
		very-low	
		</td>
		<td>
		See [RTCWEB-TRANSPORT], Sections 4.1 and 4.2. Corresponds to "below normal" as defined in [RTCWEB-DATA].
		</td>
	</tr>
	<tr>
		<td>
		low	
		</td>
		<td>
		See [RTCWEB-TRANSPORT], Sections 4.1 and 4.2. Corresponds to "normal" as defined in [RTCWEB-DATA].
		</td>
	</tr>
	<tr>
		<td>
		medium
		</td>
		<td>
		See [RTCWEB-TRANSPORT], Sections 4.1 and 4.2. Corresponds to "high" as defined in [RTCWEB-DATA].
		</td>
	</tr>
	<tr>
		<td>
		high
		</td>
		<td>
		See [RTCWEB-TRANSPORT], Sections 4.1 and 4.2. Corresponds to "extra high" as defined in [RTCWEB-DATA].
		</td>
	</tr>
</table>

Applications that use this API should be aware that often better overall user experience is obtained by lowering the priority of things that are not as important rather than raising the priority of the things that are.

zh:使用此API的应用程序应该意识到，通过降低不重要的事物的优先级而不是提高事物的优先级，通常可以获得更好的整体用户体验。
