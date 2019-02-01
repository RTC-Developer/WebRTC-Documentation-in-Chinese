### [4.6.2 RTCSessionDescription 类](http://w3c.github.io/webrtc-pc/#rtcsessiondescription-class)

The RTCSessionDescription class is used by RTCPeerConnection to expose local and remote session descriptions.

zh:RTCPeerConnection使用RTCSessionDescription类来公开本地和远程会话描述。

```
[Constructor(RTCSessionDescriptionInit descriptionInitDict),
 Exposed=Window]
interface RTCSessionDescription {
    readonly attribute RTCSdpType type;
    readonly attribute DOMString  sdp;
    [Default] object toJSON();
};

```
**Constructors zh:构造函数**

`RTCSessionDescription`

The RTCSessionDescription() constructor takes a dictionary argument, descriptionInitDict, whose content is used to initialize the new RTCSessionDescription object. This constructor is deprecated; it exists for legacy compatibility reasons only. 
	zh: RTCSessionDescription（）构造函数接受字典参数descriptionInitDict，其内容用于初始化新的RTCSessionDescription对象。不推荐使用此构造函数;它仅用于遗留兼容性原因。
	
**Attributes zh:属性**

type of type RTCSdpType, readonly:
zh:类型为RTCSdpType，只读

	The type of this RTCSessionDescription.
	zh:此RTCSessionDescription的类型。

sdp of type DOMString, readonly:
zh:DOMString类型的sdp，readonly

	The string representation of the SDP [SDP].
	zh:SDP [SDP]的字符串表示形式。
	
**Methods zh:方法**

`toJSON()`

When called, run [WEBIDL]'s default toJSON operation. 
	zh: 调用时，运行[WEBIDL]的默认为JSON操作。
	
```
dictionary RTCSessionDescriptionInit {
    required RTCSdpType type;
             DOMString  sdp = "";
};
```
Dictionary RTCSessionDescriptionInit Members zh:字典RTCSessionDescriptionInit成员

type of type RTCSdpType, required:
zh:类型为RTCSdpType，必需

	DOMString sdp
	zh:DOMString sdp

sdp of type DOMString:
zh:DOMString类型的sdp

	The string representation of the SDP [SDP]; if type is "rollback", this member is unused. 
	zh:SDP [SDP]的字符串表示;如果type为“rollback”，则此成员未使用。
