## [5.6 RTCIceTransport Interface](http://w3c.github.io/webrtc-pc/#rtcicetransport)

The RTCIceTransport interface allows an application access to information about the ICE transport over which packets are sent and received. In particular, ICE manages peer-to-peer connections which involve state which the application may want to access. RTCIceTransport objects are constructed as a result of calls to setLocalDescription() and setRemoteDescription(). The underlying ICE state is managed by the ICE agent; as such, the state of an RTCIceTransport changes when the ICE Agent provides indications to the user agent as described below. Each RTCIceTransport object represents the ICE transport layer for the RTP or RTCP component of a specific RTCRtpTransceiver, or a group of RTCRtpTransceivers if such a group has been negotiated via [BUNDLE].

zh:RTCIceTransport接口允许应用程序访问有关发送和接收数据包的ICE传输的信息。特别地，ICE管理对等连接，其涉及应用可能想要访问的状态。由于调用setLocalDescription（）和setRemoteDescription（），RTCIceTransport对象被构造。底层ICE状态由ICE代理管理;因此，当ICE代理向用户代理提供指示时，RTCIceTransport的状态改变，如下所述。每个RTCIceTransport对象表示特定RTCRtpTransceiver的RTP或RTCP组件的ICE传输层，或者一组RTCRtpTransceivers（如果已通过[BUNDLE]协商这样的组）。

>NOTE
>
>An ICE restart for an existing RTCRtpTransceiver will be represented by an existing RTCIceTransport object, whose state will be updated accordingly, as opposed to being represented by a new object.

>zh:现有RTCRtpTransceiver的ICE重新启动将由现有的RTCIceTransport对象表示，其状态将相应更新，而不是由新对象表示。

When the ICE Agent indicates that it began gathering a generation of candidates for an RTCIceTransport, the user agent MUST queue a task that runs the following steps:

zh:当ICE代理指示它开始为RTCIceTransport收集一代候选者时，用户代理必须排队运行以下步骤的任务：

1.  Let connection be the RTCPeerConnection object associated with this ICE Agent. 
zh: 让connection成为与此ICE代理关联的RTCPeerConnection对象。

2.  If connection's [[IsClosed]] slot is true, abort these steps. 
zh: 如果connection的[[IsClosed]]插槽为true，则中止这些步骤。

3.  Let transport be the RTCIceTransport for which candidate gathering began. 
zh: 让transport成为开始候选人聚会的RTCIceTransport。

4.  Set transport's [[IceGathererState]] slot to gathering. 
zh: 将transport的[[IceGathererState]]槽设置为收集。

5.  Fire an event named gatheringstatechange at transport. 
zh: 在运输中发起一个名为gatherstatechange的事件。

6.  Update the ICE gathering state of connection. 
zh: 更新ICE收集连接状态。

When the ICE Agent indicates that it finished gathering a generation of candidates for an RTCIceTransport, the user agent MUST queue a task that runs the following steps:

zh:当ICE代理指示它已完成为RTCIceTransport收集一代候选项时，用户代理必须对运行以下步骤的任务进行排队：

1.  Let connection be the RTCPeerConnection object associated with this ICE Agent. 
zh: 让connection成为与此ICE代理关联的RTCPeerConnection对象。

2.  If connection's [[IsClosed]] slot is true, abort these steps. 
zh: 如果connection的[[IsClosed]]插槽为true，则中止这些步骤。

3.  Let transport be the RTCIceTransport for which candidate gathering finished. 
zh: 让transport成为候选聚会完成的RTCIceTransport。

4.  Create an RTCIceCandidate instance newCandidate, with sdpMid and sdpMLineIndex set to the values associated with this RTCIceTransport, with usernameFragment set to the username fragment of the generation of candidates for which gathering finished, with candidate set to an empty string, and with all other nullable members set to null. 
zh: 创建一个RTCIceCandidate实例newCandidate，将sdpMid和sdpMLineIndex设置为与此RTCIceTransport关联的值，将usernameFragment设置为收集完成的候选生成的用户名片段，候选设置为空字符串，以及所有其他可空成员设为null。

5.  Fire an event named icecandidate using the RTCPeerConnectionIceEvent interface with the candidate attribute set to newCandidate at connection. 
zh: 使用RTCPeerConnectionIceEvent接口触发名为icecandidate的事件，其候选属性在连接时设置为newCandidate。

6.  If another generation of candidates is still being gathered, abort these steps.  
zh: 如果还在收集另一代候选人，请中止这些步骤。

	>Note
	> This may occur if an ICE restart is initiated while the ICE agent is still gathering the previous generation of candidates. 
	>zh: 注意如果在ICE代理仍在收集上一代候选项时启动ICE重新启动，则可能会发生这种情况。


7.  Set transport's [[IceGathererState]] slot to complete. 
zh: 设置传输的[[IceGathererState]]插槽即可完成。

8.  Fire an event named gatheringstatechange at transport. 
zh: 在运输中发起一个名为gatherstatechange的事件。

9.  Update the ICE gathering state of connection. 
zh: 更新ICE收集连接状态。


When the ICE Agent indicates that a new ICE candidate is available for an RTCIceTransport, either by taking one from the ICE candidate pool or gathering it from scratch, the user agent MUST queue a task that runs the following steps:

zh:当ICE代理指示新的ICE候选者可用于RTCIceTransport时，通过从ICE候选池中取一个或从头开始收集它，用户代理必须排队运行以下步骤的任务：

1.  Let connection be the RTCPeerConnection object associated with this ICE Agent. 
zh: 让connection成为与此ICE代理关联的RTCPeerConnection对象。

2.  If connection's [[IsClosed]] slot is true, abort these steps. 
zh: 如果connection的[[IsClosed]]插槽为true，则中止这些步骤。

3.  Let transport be the RTCIceTransport for which this candidate is being made available. 
zh: 让transport成为可供该候选人使用的RTCIceTransport。

4.  If connection.[[PendingLocalDescription]] is not null, and represents the ICE generation for which candidate was gathered, add candidate to the connection.[[PendingLocalDescription]].sdp. 
zh: 如果connection。[[PendingLocalDescription]]不为null，并且表示为其收集候选者的ICE生成，则将候选添加到连接。[[PendingLocalDescription]]。sdp。

5.  If connection.[[CurrentLocalDescription]] is not null, and represents the ICE generation for which candidate was gathered, add candidate to the connection.[[CurrentLocalDescription]].sdp. 
zh: 如果连接。[[CurrentLocalDescription]]不为null，并且表示为其收集候选者的ICE生成，则将候选添加到连接。[[CurrentLocalDescription]]。sdp。

6.  Create an RTCIceCandidate instance to represent the candidate. Let newCandidate be that object. 
zh: 创建一个RTCIceCandidate实例来表示候选者。让newCandidate成为那个对象。

7.  Add newCandidate to transport's set of local candidates. 
zh: 将newCandidate添加到transport的本地候选者集。

8.  Fire an event named icecandidate using the RTCPeerConnectionIceEvent interface with the candidate attribute set to newCandidate at connection. 
zh: 使用RTCPeerConnectionIceEvent接口触发名为icecandidate的事件，其候选属性在连接时设置为newCandidate。

When the ICE Agent indicates that the RTCIceTransportState for an RTCIceTransport has changed, the user agent MUST queue a task that runs the following steps:

zh:当ICE代理指示RTCIceTransport的RTCIceTransportState已更改时，用户代理必须对运行以下步骤的任务进行排队：

1.  Let connection be the RTCPeerConnection object associated with this ICE Agent. 
zh: 让connection成为与此ICE代理关联的RTCPeerConnection对象。

2.  If connection's [[IsClosed]] slot is true, abort these steps. 
zh: 如果connection的[[IsClosed]]插槽为true，则中止这些步骤。

3.  Let transport be the RTCIceTransport whose state is changing. 
zh: 让transport成为状态正在发生变化的RTCIceTransport。

4.  Let newState be the new indicated RTCIceTransportState. 
zh: 让newState成为新指示的RTCIceTransportState。

5.  Set transport's [[IceTransportState]] slot to newState. 
zh: 将transport的[[IceTransportState]]槽设置为newState。

6.  Fire an event named statechange at transport. 
zh: 在运输中发起名为statechange的事件。

7.  Update the ICE connection state of connection.  
zh: 更新ICE连接状态。

8.  Update the connection state of connection. 
zh: 更新连接的连接状态。

When the ICE Agent indicates that the selected candidate pair for an RTCIceTransport has changed, the user agent MUST queue a task that runs the following steps:

zh:当ICE代理指示RTCIceTransport的所选候选对已更改时，用户代理必须对运行以下步骤的任务进行排队：

1.  Let connection be the RTCPeerConnection object associated with this ICE Agent. 
zh: 让connection成为与此ICE代理关联的RTCPeerConnection对象。

2.  If connection's [[IsClosed]] slot is true, abort these steps. 
zh: 如果connection的[[IsClosed]]插槽为true，则中止这些步骤。

3.  Let transport be the RTCIceTransport whose selected candidate pair is changing. 
zh: 让transport成为所选候选对正在变化的RTCIceTransport。

4.  Let newCandidatePair be a newly created RTCIceCandidatePair representing the indicated pair if one is selected, and null otherwise. 
zh: 让newCandidatePair成为新创建的RTCIceCandidatePair，如果选择了一个，则表示指示的对，否则为null。

5.  Set transport's [[SelectedCandidatePair]] slot to newCandidatePair. 
zh: 将transport的[[SelectedCandidatePair]]槽设置为newCandidatePair。

6.  Fire an event named selectedcandidatepairchange at transport. 
zh: 在传输时触发名为selectedcandidatepairchange的事件。


An RTCIceTransport object has the following internal slots:

zh:RTCIceTransport对象具有以下内部插槽：

* [[IceTransportState]] initialized to  new
zh:[[IceTransportState]]初始化为新的
* [[IceGathererState]] initialized to  new
zh:[[IceGathererState]]初始化为新的
* [[SelectedCandidatePair]] initialized to null
zh:[[SelectedCandidatePair]]初始化为null

```
[Exposed=Window] interface RTCIceTransport : EventTarget {
    readonly        attribute RTCIceRole           role;
    readonly        attribute RTCIceComponent      component;
    readonly        attribute RTCIceTransportState state;
    readonly        attribute RTCIceGathererState gatheringState;
    sequence<RTCIceCandidate> getLocalCandidates ();
    sequence<RTCIceCandidate> getRemoteCandidates ();
    RTCIceCandidatePair?      getSelectedCandidatePair ();
    RTCIceParameters?         getLocalParameters ();
    RTCIceParameters?         getRemoteParameters ();
                    attribute EventHandler         onstatechange;
                    attribute EventHandler         ongatheringstatechange;
                    attribute EventHandler         onselectedcandidatepairchange;
};
```

**Attributes**

*role* of type RTCIceRole, readonly:
zh:RTCIceRole类型的作用，readonly

The role attribute MUST return the ICE role of the transport.

zh:role属性必须返回传输的ICE角色。

*component* of type RTCIceComponent, readonly:
zh:RTCIceComponent类型的组件，只读

The component attribute MUST return the ICE component of the transport. When RTCP mux is used, a single RTCIceTransport transports both RTP and RTCP and component is set to "RTP".

zh:组件属性必须返回传输的ICE组件。使用RTCP mux时，单个RTCIceTransport传输RTP和RTCP，组件设置为“RTP”。

*state* of type RTCIceTransportState, readonly:
zh:RTCIceTransportState类型的状态，只读

The state attribute MUST, on getting, return the value of the [[IceTransportState]] slot.

zh:获取时，状态属性必须返回[[IceTransportState]]槽的值。

*gatheringState* of type RTCIceGathererState, readonly:
zh:只读取RTCIceGathererState类型的状态，只读

The gathering state attribute MUST, on getting, return the value of the [[IceGathererState]] slot.

zh:收集状态属性必须在获取时返回[[IceGathererState]]槽的值。

*onstatechange* of type EventHandler:
zh:eventHandler类型的onstatechange

This event handler, of event handler event type statechange, MUST be fired any time the RTCIceTransport state changes. 
zh: 事件处理程序事件类型statechange的事件处理程序必须在RTCIceTransport状态更改时触发。

*ongatheringstatechange* of type EventHandler:
zh:hoststate交换EventHandler类型

This event handler, of event handler event type gatheringstatechange, MUST be fired any time the RTCIceTransportgathering state changes. 
zh: 事件处理程序事件类型gatherstatechange的事件处理程序必须在RTCIceTransportgathering状态更改时触发。

*onselectedcandidatepairchange* of type EventHandler:
zh:onselectedcandidatepairchange或类型EventHandler

This event handler, of event handler event type selectedcandidatepairchange, MUST be fired any time the RTCIceTransport's selected candidate pair changes.
zh:事件处理程序事件类型selectedcandidatepairchange的事件处理程序必须在RTCIceTransport的所选候选对更改时触发。

**Methods**

`getLocalCandidates`

Returns a sequence describing the local ICE candidates gathered for this RTCIceTransport and sent in onicecandidate 
zh: 返回一个序列，描述为此RTCIceTransport收集并在onicecandidate中发送的本地ICE候选项

`getRemoteCandidates`

Returns a sequence describing the remote ICE candidates received by this RTCIceTransport via addIceCandidate() 
zh: 返回描述此RTCIceTransport通过addIceCandidate（）接收的远程ICE候选的序列

`getSelectedCandidatePair`

Returns the selected candidate pair on which packets are sent. This method MUST return the value of the [[SelectedCandidatePair]] slot. 
zh: 返回发送数据包的选定候选对。此方法必须返回[[SelectedCandidatePair]]槽的值。

`getLocalParameters`

Returns the local ICE parameters received by this RTCIceTransport via setLocalDescription, or null if the parameters have not yet been received. 
zh: 返回此RTCIceTransport通过setLocalDescription接收的本地ICE参数，如果尚未接收参数，则返回null。

`getRemoteParameters`

Returns the remote ICE parameters received by this RTCIceTransport via setRemoteDescription or null if the parameters have not yet been received. 
zh: 返回此RTCIceTransport通过setRemoteDescription接收的远程ICE参数，如果尚未接收参数，则返回null。