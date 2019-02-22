## [6.3 RTCDataChannelEvent](http://w3c.github.io/webrtc-pc/#rtcdatachannelevent)

The datachannel event uses the RTCDataChannelEvent interface.

zh:datachannel事件使用RTCDataChannelEvent接口。

```
        [ Constructor (DOMString type, RTCDataChannelEventInit eventInitDict), Exposed=Window]
interface RTCDataChannelEvent : Event {
    readonly        attribute RTCDataChannel channel;
};
```

**Constructors**

`RTCDataChannelEvent`
 
**Attributes**

*channel* of type RTCDataChannel, readonly:
zh:RTCDataChannel类型的通道，只读

The channel attribute represents the RTCDataChannel object associated with the event.

zh:channel属性表示与事件关联的RTCDataChannel对象。

```
dictionary RTCDataChannelEventInit : EventInit {
             required RTCDataChannel channel;
};
```

**Dictionary RTCDataChannelEventInit Members**

channel of type RTCDataChannel, required:
zh:必需的RTCDataChannel类型的通道

The RTCDataChannel object to be announced by the event.

zh:事件要宣布的RTCDataChannel对象。
