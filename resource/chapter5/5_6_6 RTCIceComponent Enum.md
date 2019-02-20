### [5.6.6 RTCIceComponent Enum](http://w3c.github.io/webrtc-pc/#rtcicecomponent)

```
enum RTCIceComponent {
    "rtp",
    "rtcp"
};

```

<table>
	<tr>
		<td colspan="2">
		RTCIceComponent Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		rtp
		</td>
		<td>
		The ICE Transport is used for RTP (or RTCP multiplexing), as defined in [ICE], Section 4.1.1.1. Protocols multiplexed with RTP (e.g. data channel) share its component ID. This represents the component-id value 1 when encoded in candidate-attribute.
		</td>
	</tr>
	<tr>
		<td>
		rtcp
		</td>
		<td>
		The ICE Transport is used for RTCP as defined by [ICE], Section 4.1.1.1. This represents the component-id value 2 when encoded in candidate-attribute.
		</td>
	</tr>
</table>