### [4.8.3 RTCPeerConnectionIceErrorEvent zh:4.8.3 RTCPeerConnectionIceErrorEvent](http://w3c.github.io/webrtc-pc/#rtcpeerconnectioniceerrorevent)

The icecandidateerror event of the RTCPeerConnection uses the RTCPeerConnectionIceErrorEvent interface.

zh:RTCPeerConnection的icecandidateerror事件使用RTCPeerConnectionIceErrorEvent接口。

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
##### Constructors zh:构造函数

`RTCPeerConnectionIceErrorEvent`

##### Attributes zh:属性

hostCandidate of type DOMString, readonly:
zh:DOMString类型的hostCandidate，readonly

The hostCandidate attribute is the local IP address and port used to communicate with the STUN or TURN server.

zh:hostCandidate属性是用于与STUN或TURN服务器通信的本地IP地址和端口。

On a multihomed system, multiple interfaces may be used to contact the server, and this attribute allows the application to figure out on which one the failure occurred.

zh:在多宿主系统上，可以使用多个接口来联系服务器，该属性允许应用程序确定故障发生在哪一个上。

If use of multiple interfaces has been prohibited for privacy reasons, this attribute will be set to 0.0.0.0:0 or [::]:0, as appropriate.

zh:如果出于隐私原因禁止使用多个接口，则此属性将根据需要设置为0.0.0.0:0或[::]：0。

url of type DOMString, readonly:
zh:DOMString类型的url，readonly

The url attribute is the STUN or TURN URL that identifies the STUN or TURN server for which the failure occurred.

zh:url属性是STUN或TURN URL，用于标识发生故障的STUN或TURN服务器。

errorCode of type unsigned short, readonly:
zh:errorCode类型unsigned short，readonly

The errorCode attribute is the numeric STUN error code returned by the STUN or TURN server [STUN-PARAMETERS].

zh:errorCode属性是STUN或TURN服务器[STUN-PARAMETERS]返回的数字STUN错误代码。

If no host candidate can reach the server, errorCode will be set to the value 701 which is outside the STUN error code range. This error is only fired once per server URL while in the RTCIceGatheringState of "gathering".

zh:如果没有主机候选者可以到达服务器，则errorCode将被设置为超出STUN错误代码范围的值701。在“收集”的RTCIceGatheringState中，每个服务器URL仅触发一次此错误。

errorText of type USVString, readonly:
zh:USVString类型的errorText，只读

The errorText attribute is the STUN reason text returned by the STUN or TURN server [STUN-PARAMETERS].

zh:errorText属性是STUN或TURN服务器[STUN-PARAMETERS]返回的STUN原因文本。

If the server could not be reached, errorText will be set to an implementation-specific value providing details about the error.

zh:如果无法访问服务器，则errorText将设置为特定于实现的值，提供有关错误的详细信息。

```
dictionary RTCPeerConnectionIceErrorEventInit : EventInit {
             DOMString      hostCandidate;
             DOMString      url;
    required unsigned short errorCode;
             USVString      statusText;
};
```
##### Dictionary RTCPeerConnectionIceErrorEventInit Members zh:字典RTCPeerConnectionIceErrorEventInit成员

hostCandidate of type DOMString:
zh:DOMString类型的hostCandidate

The local address and port used to communicate with the STUN or TURN server.

zh:用于与STUN或TURN服务器通信的本地地址和端口。

url of type DOMString:
zh:DOMString类型的url

The STUN or TURN URL that identifies the STUN or TURN server for which the failure occurred.

zh:STUN或TURN URL，用于标识发生故障的STUN或TURN服务器。

errorCode of type unsigned short, required:
zh:errorCode类型为unsigned short，必需

The numeric STUN error code returned by the STUN or TURN server.

zh:STUN或TURN服务器返回的数字STUN错误代码。

statusText of type USVString:
zh:USVString类型的statusText

The STUN reason text returned by the STUN or TURN server.

zh:STUN或TURN服务器返回的STUN原因文本。


