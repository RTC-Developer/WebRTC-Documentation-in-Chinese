## [5.6 `RTCIceTransport`接口](http://w3c.github.io/webrtc-pc/#rtcicetransport)

`RTCIceTransport`接口允许应用程序获取有关用来发送接收数据包的ICE传输的信息。特别的，ICE管理对等连接，它牵涉到应用程序可能获取的状态。由于需要调用`setLocalDescription()`和`setRemoteDescription()`,`RTCIceTransport`对象被创建。底层ICE状态由ICE代理管理，所以当ICE代理向用户代理提供指示时，`RTCIceTransport`的状态就会改变。每个`RTCIceTransport`对象代表一个特定`RTCRtpTransceiver`的RTP或RTCP组件的ICE传输层，或者是一组已经通过[BUNDLE]协商的`RTCRtpTransceiver`。

> NOTE:现存`RTCRtpTranceiver`的ICE重启将会由现存`RTCIceTransport`对象表示，它的状态将会被对应更新，而不是由新对象表示。

当ICE代理表示它将为一个`RTCIceTransport`收集一系列的候选者时，用户代理必须对运行以下步骤的任务进行排序:

1. 让connection成为与这个ICE代理关联的`RTCPeerConnection`对象。
2. 如果connection的[[IsClosed]]插槽为`true`，中断这些步骤。
3. 让transport成为RTCIceTransport。
4. 设置transport的[[IceGathererState]]插槽为`gathering`。
5. 在transport发起一个名为`gatheringstatechange`的事件。
6. 更新connection的ICE收集状态。

当ICE代理表示它已经成功收集了一个`RTCIceTransport`的一系列候选者时，用户代理必须对运行以下步骤的任务进行排序：

1. 让connection成为与ICE代理关联的`RTCPeerConnection`对象。

2. 如果connection的[[IsClosed]]插槽为`true`，中断这些步骤。

3. 让transport成为`RTCIceTransport`。

4. 让`newCandidate`成为创建一个RTCIceCandidate的结果，伴随一个新字典，它的`sdpMid`和`sdpMLineIndex`都被设置为与此`RTCIceTransport`相关联的值，`usernameFrangment`被设置为收集完成的candidates的用户名片段，`candidate`被设置为空字符串。

5. 使用`RTCPeerConnectionIceEvent`接口发起一个名为`icecandidate`的事件，并且candidate属性在connection被设置为`newCandidate`。

6. 如果另一代candidates还在被收集，中断这些步骤。

   > NOTE:这可能会出现，如果在ICE代理还在收集上一代的candidates时，开始ICE重启，可能会发生这种情况。

7. 设置transport的[[IceGathererState]]插槽为complete。

8. 在transport发起一个名为`gatheringstatechange`的事件。

9. 更新connection的ICE收集状态。

当用户代理表示新的ICE candidate可用于`RTCIceTransport`，或者从ICE候选者池中选择一个，或者从头开始收集它，用户代理必须对运行以下步骤的任务进行排序：

1. 让`candidate`成为可用的ICE候选者。
2. 让connection成为与这个ICE代理相关联的`RTCPeerConnection`对象。
3. 如果connection的[[IsClosed]]插槽为`true`，中断这些步骤。
4. 让transport成为可供候选者使用的`RTCIceTransport`。
5. 如果connection.[[PendingLocalDescription]]不是`null`，并且表示收集候选者的ICE generation，向connection.[[PendingLocalDesciption]].sdp中添加候选者。
6. 如果connection.[[CurrentLocalDescription]]不是`null`，并且表示收集候选者的ICE generation，向connection.[[CurrentLocalDescription]].sdp中添加候选者。
7. 让`newCandidate`成为创建一个RTCIceCandidate的结果，伴随一个新字典，它的`sdpMid`和`sdpMLineIndex`都被设置为与此`RTCIceTransport`相关联的值，`usernameFrangment`被设置为候选者的用户名片段，并且`candidate`被设置为使用`candidate-attribute`语法编码的字符串来代表`candidate`。
8. 将`newCandidate`添加到transport的本地候选者集合中。
9. 使用`RTCPeerConnectionIceEvent`接口发起一个名为`icecandidate`的事件，并且候选者属性在`connection`被设置为`newCandidate`。

当ICE代理表示`RTCIceTransport`的`RTCIceTransportState`已经改变时，用户代理必须对运行以下步骤的任务进行排序:

1. 让`connection`成为与这个ICE代理相关联的`RTCPeerConnection`对象。
2. 如果`connection`的[[IsClosed]]插槽为`true`，中断这些步骤。
3. 让`transport`成为状态正在改变的`RTCIceTransport`。
4. 让`newState`成为新的被指示的`RTCIceTransportState`。
5. 设置`transport`的[[IceTransportState]]插槽为`newState`。
6. 在`transport`发起一个名为`statechange`的事件。
7. 更新`connection`的ICE连接状态。
8. 更新`connection`的连接状态。

当ICE代理表示选定的一对`RTCIceTransport`候选者已经改变时，用户代理必须对运行以下步骤的任务进行排序：

1. 让`connection`成为与这个ICE代理相关联的`RTCPeerConnection`对象。
2. 如果`connection`的[[IsClosed]]插槽为`true`，中断这些步骤。
3. 让`transport`成为选定候选者对正在改变的`RTCIceTransport`。
4. 让`newCandidatePair`成为新常见的`RTCIceCandidatePair`，如果选定了一个，表示选择正确，否则为null。
5. 设置`transport`的[[SelectedCandidatePair]]插槽为`newCandidatePair`。
6. 在`transport`发起一个名为`selectedcandidatepairchange`的事件。

一个`RTCIceTransport`对象具有下列内部插槽：

- [[IceTransportState]]初始化为`new`
- [[IceGathererState]]初始化为`new`
- [[SelectedCandidatePair]]初始化为`null`

```java
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



**属性**

`RTCIceRole`类型的`role`，只读：`role`属性必须返回transport的ICE role。

`RTCIceComponent`类型的`component`，只读：`component`属性必须返回`transport`的ICE组件。当RTCP mux被使用时，单一的`RTCIceTransport`同时传输RTP和RTCP，并且`component`被设置为`RTP`。

`RTCIceTransportState`类型的`state`，只读：当需要获得`state`属性时，它必须返回[[IceTransportState]]插槽的值。

`RTCIceGathererState`类型的`gatheringState`，只读：当获取`gathering state`属性时，它必须返回[[IceGathererState]]插槽的值。

`EventHandler`类型的`onstatechange`:此event handler，当`RTCIceTransportstate`类型改变时，必须启动。

`EventHandler`类型的`ongatheringstatechange`：此event handler，当`RTCIceTransportgatheringstate`改变时，必须启动。

`EventHandler`类型的`onselectedcandidatepairchange`：此event handler，当`RTCIceTransport`选定的候选者对改变时，必须启动。

**方法**

`getLocalCandidates`:返回一个序列，描述为`RTCIceTransport`收集并在`onicecandidate`中发送的本地候选者。

`getRemoteCandidates`:返回一个序列，描述通过`addIceCandidate()`，由`RTCIceTransport`接收的ICE候选者。

> NOTE:`getRemoteCandidates`不会暴露peer reflexive candidates，因为它们不是通过`addIceCandidate()`接收的。

`getSelectedCandidatePair`:返回用来发送数据包的选定候选者对。此方法必须返回[[SelectedCandidatePair]]插槽的值。

`getLocalParameters`:返回通过`setLocalDescription`由`RTCIceTransport`接收的本地ICE参数，如果参数未被接收，则为`null`。

`getRemoteParameters`:返回通过`setRemoteDescription`，由`RTCIceTransport`接收的ICE远程参数，如果参数未被接收，则为`null`。
