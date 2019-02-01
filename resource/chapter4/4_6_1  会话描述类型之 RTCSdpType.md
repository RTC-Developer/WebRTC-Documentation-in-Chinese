## [4.6 会话描述类型](http://w3c.github.io/webrtc-pc/#session-description-model)

### 4.6.1 RTCSdpType

The RTCSdpType enum describes the type of an RTCSessionDescriptionInit or RTCSessionDescription instance.

zh:RTCSdpType枚举描述了RTCSessionDescriptionInit或RTCSessionDescription实例的类型。

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
		Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		offer
		</td>
		<td>
		An RTCSdpType of offer indicates that a description MUST be treated as an [SDP] offer.
		zh:商品的RTCSdpType表示必须将描述视为[SDP]商品。
		</td>
	</tr>
	<tr>
		<td>
		pranswer	
		</td>
		<td>
		An RTCSdpType of pranswer indicates that a description MUST be treated as an [SDP] answer, but not a final answer. A description used as an SDP pranswer may be applied as a response to an SDP offer, or an update to a previously sent SDP pranswer.
		zh:pranswer的RTCSdpType表示描述必须被视为[SDP]答案，但不是最终答案。用作SDP pranswer的描述可以用作对SDP提议的响应，或者对先前发送的SDP pranswer的更新。
		</td>
	</tr>
	<tr>
		<td>
		answer	
		</td>
		<td>
		An RTCSdpType of answer indicates that a description MUST be treated as an [SDP] final answer, and the offer-answer exchange MUST be considered complete. A description used as an SDP answer may be applied as a response to an SDP offer or as an update to a previously sent SDP pranswer.
		zh:答案的RTCSdpType表示必须将描述视为[SDP]最终答案，并且必须认为提议 - 答案交换完成。用作SDP答案的描述可以应用为对SDP提议的响应或者作为对先前发送的SDP pranswer的更新。
		</td>
	</tr>
	<tr>
		<td>
		rollback	
		</td>
		<td>
		An RTCSdpType of rollback indicates that a description MUST be treated as canceling the current SDP negotiation and moving the SDP [SDP] offer and answer back to what it was in the previous stable state. Note the local or remote SDP descriptions in the previous stable state could be null if there has not yet been a successful offer-answer negotiation.
		zh:回滚的RTCSdpType指示必须将描述视为取消当前SDP协商并移动SDP [SDP]提议并回答其在先前稳定状态下的状态。请注意，如果尚未成功进行商品 - 答案协商，则先前稳定状态中的本地或远程SDP描述可能为空。
		</td>
	</tr>
</table>


