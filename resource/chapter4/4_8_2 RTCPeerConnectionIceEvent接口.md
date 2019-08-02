### [4.8.2 RTCPeerConnectionIceEvent接口](http://w3c.github.io/webrtc-pc/#rtcpeerconnectioniceevent)

`RTCPeerConnection` 的 `icecandidate` 事件使用 `RTCPeerConnectionIceEvent` 接口。

当触发包含 `RTCIceCandidate` 对象的 `RTCPeerConnectionIceEvent` 事件时，它必须包含`sdpMid`和`sdpMLineIndex`的值。如果RTCIceCandidate的类型为srflx或类型为relay，则事件的url属性必须设置为从中获取候选者的ICE服务器的URL。

NOTE

The icecandidate event is used for three different types of indications:
zh:icecandidate事件用于三种不同类型的指示：

*  A candidate has been gathered. The candidate member of the event will be populated normally. It should be signaled to the remote peer and passed into addIceCandidate. 
zh: 候选人已经聚集。该活动的候选成员将正常填充。它应该发信号通知远程对等体并传递给addIceCandidate。
*  An RTCIceTransport has finished gathering a generation of candidates, and is providing an end-of-candidates indication as defined by Section 8.2 of [TRICKLE-ICE]. This is indicated by candidate.candidate being set to an empty string. The candidate object should be signaled to the remote peer and passed into addIceCandidate like a typical ICE candidate, in order to provide the end-of-candidates indication to the remote peer. 
zh: RTCIceTransport已完成收集一代候选者，并提供[TRICKLE-ICE]第8.2节定义的候选终结指示。这由candidate.candidate设置为空字符串表示。候选对象应该被发信号通知远程对等体并像典型的ICE候选者一样被传递到addIceCandidate，以便向远程对等体提供候选终止指示。
*  All RTCIceTransports have finished gathering candidates, and the RTCPeerConnection's RTCIceGatheringState has transitioned to "complete". This is indicated by the candidate member of the event being set to null. This only exists for backwards compatibility, and this event does not need to be signaled to the remote peer. It's equivalent to an "icegatheringstatechange" event with the "complete" state. 
zh: 所有RTCIceTransports都已完成收集候选者，RTCPeerConnection的RTCIceGatheringState已转换为“完成”。这由事件的候选成员设置为null来指示。这仅用于向后兼容，并且不需要向远程对等方发信号通知此事件。它相当于具有“完整”状态的“icegatheringstatechange”事件。

```
[Constructor(DOMString type, optional RTCPeerConnectionIceEventInit eventInitDict),
 Exposed=Window]
interface RTCPeerConnectionIceEvent : Event {
    readonly attribute RTCIceCandidate? candidate;
    readonly attribute DOMString?       url;
};
```

##### Constructors zh:构造函数

`RTCPeerConnectionIceEvent`

##### Attributes zh:属性

candidate of type RTCIceCandidate, readonly, nullable:
zh:RTCIceCandidate类型的候选者，只读，可以为空

The candidate attribute is the RTCIceCandidate object with the new ICE candidate that caused the event.

zh:候选属性是RTCIceCandidate对象，其中包含导致该事件的新ICE候选对象。

This attribute is set to null when an event is generated to indicate the end of candidate gathering.

zh:生成事件以指示候选收集结束时，此属性设置为null。

NOTE
Even where there are multiple media components, only one event containing a null candidate is fired.

zh:即使存在多个媒体组件，也只会触发一个包含空候选的事件。

url of type DOMString, readonly, nullable:
zh:DOMString类型的url，只读，可以为空

The url attribute is the STUN or TURN URL that identifies the STUN or TURN server used to gather this candidate. If the candidate was not gathered from a STUN or TURN server, this parameter will be set to null.

zh:url属性是STUN或TURN URL，用于标识用于收集此候选项的STUN或TURN服务器。如果未从STUN或TURN服务器收集候选项，则此参数将设置为null。

```
dictionary RTCPeerConnectionIceEventInit : EventInit {
    RTCIceCandidate? candidate;
    DOMString?       url;
};
```

##### Dictionary RTCPeerConnectionIceEventInit Members zh:字典RTCPeerConnectionIceEventInit成员

candidate of type RTCIceCandidate, nullable:
zh:RTCIceCandidate类型的候选者，可以为空

See the candidate attribute of the RTCPeerConnectionIceEvent interface.

zh:请参阅RTCPeerConnectionIceEvent接口的候选属性。

url of type DOMString, nullable:
zh:DOMString类型的url，可以为空

The url attribute is the STUN or TURN URL that identifies the STUN or TURN server used to gather this candidate.

zh:url属性是STUN或TURN URL，用于标识用于收集此候选项的STUN或TURN服务器。

