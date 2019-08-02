### [4.6.2 RTCSessionDescription 类](http://w3c.github.io/webrtc-pc/#rtcsessiondescription-class)

RTCPeerConnection通过RTCSessionDescription类来公开本地和远程会话描述。

```
[Constructor(RTCSessionDescriptionInit descriptionInitDict),
 Exposed=Window]
interface RTCSessionDescription {
    readonly attribute RTCSdpType type;
    readonly attribute DOMString  sdp;
    [Default] object toJSON();
};

```
**构造函数**

`RTCSessionDescription 类`

RTCSessionDescription() 构造函数接受一个字典参数`descriptionInitDict`，用于初始化新的`RTCSessionDescription`对象。这个构造函数已废弃，不推荐使用此构造函数;它的存在仅用于历史兼容。
	
**属性**

`type`类型为`RTCSdpType`，只读项

	这个RTCSessionDescription的类型。

`sdp`类型为`DOMString`，只读项

  SDP [SDP]的字符串表示形式。
	
**方法**

`toJSON()`

调用时，运行[WEBIDL]的默认`toJSON`操作。
	
```
dictionary RTCSessionDescriptionInit {
    required RTCSdpType type;
             DOMString  sdp = "";
};
```
字典RTCSessionDescriptionInit成员

`type`类型为RTCSdpType，必需项
	DOMString sdp
`sdp`类型为`DOMString`
  SDP [SDP]的字符串表示形式。如果`type`为`rollback`，则该成员未使用。