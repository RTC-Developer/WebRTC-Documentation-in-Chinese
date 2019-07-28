### [4.8.3 RTCPeerConnectionIceErrorEvent接口](http://w3c.github.io/webrtc-pc/#rtcpeerconnectioniceerrorevent)

`RTCPeerConnection` 的 `icecandidateerror` 事件使用 `RTCPeerConnectionIceErrorEvent` 接口。

```
[Constructor(DOMString type, RTCPeerConnectionIceErrorEventInit eventInitDict),
 Exposed=Window]
interface RTCPeerConnectionIceErrorEvent : Event {
    readonly attribute DOMString      hostCandidate;
    readonly attribute DOMString      url;
    readonly attribute unsigned short errorCode;
    readonly attribute USVString      errorText;
};
```
##### 构造函数

`RTCPeerConnectionIceErrorEvent`

##### 属性

`hostCandidate`的类型为`DOMString`, 只读项:

`hostCandidate`属性是用于与STUN或TURN服务器通信的本地IP地址和端口。

 在多宿主系统上，可以使用多个接口来联系服务器，该属性允许应用程序确定故障发生在哪一个上。

 如果出于隐私原因禁止使用多个接口，则此属性将根据需要设置为0.0.0.0:0或[::]：0。

`url`的类型为`DOMString`, 只读项:

`url`属性是 STUN 或 TURN URL ，用于标识发生故障的STUN或TURN服务器。

`errorCode`的类型为`unsigned short`，只读项:

`errorCode`属性是 STUN 或 TURN 服务器 [STUN-PARAMETERS] 返回的数字 STUN 错误代码。

 如果没有主机候选者可以到达服务器，则 `errorCode` 将被设置为超出 STUN 错误代码范围的值701。在“收集”的`RTCIceGatheringState`中，每个服务器 URL 仅触发一次此错误。

`errorText`的类型为`USVString`, 只读项:

`errorText`属性是 STUN 或 TURN 服务器 [STUN-PARAMETERS] 返回的 STUN 原因文本。

 如果无法访问服务器，则`errorText`将设置为特定于实现的值，提供有关错误的详细信息。

```
dictionary RTCPeerConnectionIceErrorEventInit : EventInit {
             DOMString      hostCandidate;
             DOMString      url;
    required unsigned short errorCode;
             USVString      statusText;
};
```
##### 字典RTCPeerConnectionIceErrorEventInit的成员

`hostCandidate`的类型为`DOMString`

用于与 STUN 或 TURN 服务器通信的本地地址和端口。

`url`的类型为`DOMString`:

STUN 或 TURN URL ，用于标识发生故障的STUN或TURN服务器。

`errorCode`的类型为unsigned short，必需项：

STUN 或 TURN 服务器返回的数字 STUN 错误代码。

`statusText`的类型为`USVString`:

STUN 或 TURN 服务器返回的 STUN 原因文本。


