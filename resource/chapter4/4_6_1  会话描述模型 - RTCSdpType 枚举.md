## [4.6 会话描述模型](http://w3c.github.io/webrtc-pc/#session-description-model)

### 4.6.1 `RTCSdpType` 枚举

RTCSdpType 枚举描述了RTCSessionDescriptionInit或RTCSessionDescription实例的类型。

```
enum RTCSdpType {
    "offer",
    "pranswer",
    "answer",
    "rollback"
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
		offer
		</td>
		<td>
		一个RTCSdpType的`offer`表示必须将一个描述视为一个[SDP]提供。
		</td>
	</tr>
	<tr>
		<td>
		pranswer	
		</td>
		<td>
		一个RTCSdpType的`pranswer`表示必须将一个描述视为[SDP]应答，但不是最终应答。一个描述可以作为一个 SDP offer 的应答响应，或对先前发送的 SDP pranswer 的更新。
		</td>
	</tr>
	<tr>
		<td>
		answer	
		</td>
		<td>
		一个RTCSdpType的`answer`表示必须将一个描述视为[SDP]的最终应答，并且必须认为 offer-answer 交换完成。一个描述可以用于响应 SDP offer 的最终应答或者可作为对先前发送的SDP pranswer的更新。
		</td>
	</tr>
	<tr>
		<td>
		rollback	
		</td>
		<td>
		一个RTCSdpType的`rollback`表示必须将一个描述视为取消当前SDP协商并回退SDP [SDP]提供和最终应答到它先前的稳定状态下。请注意，如果还没有成功进行 offer - answer 协商，则先前稳定状态的本地或远程SDP的描述可能为空。
		</td>
	</tr>
</table>


