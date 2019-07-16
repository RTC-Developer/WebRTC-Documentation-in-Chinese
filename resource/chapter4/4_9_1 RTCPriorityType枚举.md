### [4.9.1 RTCPriorityType枚举类型](http://w3c.github.io/webrtc-pc/#rtcprioritytype-enum)

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
		枚举类型描述
		</td>
	</tr>
	<tr>
		<td>
		very-low	
		</td>
		<td>
		参看[RTCWEB-TRANSPORT], 第4.1和4.2小节. 等同于定义在[RTCWEB-DATA]中的"below normal".
		</td>
	</tr>
	<tr>
		<td>
		low	
		</td>
		<td>
		参看[RTCWEB-TRANSPORT], 第4.1和4.2小节. 等同于定义在[RTCWEB-DATA]中的"normal".
		</td>
	</tr>
	<tr>
		<td>
		medium
		</td>
		<td>
		参看[RTCWEB-TRANSPORT], 第4.1和4.2小节. 等同于定义在[RTCWEB-DATA]中的"high".
		</td>
	</tr>
	<tr>
		<td>
		high
		</td>
		<td>
		参看[RTCWEB-TRANSPORT], 第4.1和4.2小节. 等同于定义在[RTCWEB-DATA]中的"extra high".
		</td>
	</tr>
</table>

当在应用程序中使用该API时，开发者需要意识到更好的整体用户体验通常来自于主动降低某些不重要媒体流的优先级而不是一味地去提高某些重要媒体流的优先级。
