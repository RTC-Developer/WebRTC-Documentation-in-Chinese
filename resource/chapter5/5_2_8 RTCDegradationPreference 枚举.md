### [5.2.8 RTCDegradationPreference 枚举](http://w3c.github.io/webrtc-pc/#rtcdegradationpreference)

```
enum RTCDegradationPreference {
    "maintain-framerate",
    "maintain-resolution",
    "balanced"
};
```

<table>
	<tr>
		<td colspan="2">
		RTCDegradationPreference Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		maintain-framerate
		</td>
		<td>
		Degrade resolution in order to maintain framerate.
		zh:降低分辨率以保持帧率。
		</td>
	</tr>
	<tr>
		<td>
		maintain-resolution
		</td>
		<td>
		Degrade framerate in order to maintain resolution.
		zh:降低帧率以保持分辨率。
		</td>
	</tr>
	<tr>
		<td>
		balanced
		</td>
		<td>
		Degrade a balance of framerate and resolution.
		zh:降低帧率和分辨率的平衡。
		</td>
	</tr>
</table>
