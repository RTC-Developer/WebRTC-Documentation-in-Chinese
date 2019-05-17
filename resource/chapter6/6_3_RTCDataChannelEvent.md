## 6.3 `RTCDataChannelEvent`

使用`RTCDataChannelEvent`接口的`datachannel`事件。[测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCPeerConnection-ondatachannel.html)

```java
        [ Constructor (DOMString type, RTCDataChannelEventInit eventInitDict), Exposed=Window]
interface RTCDataChannelEvent : Event {
    readonly        attribute RTCDataChannel channel;
};
```

**构造函数**

`RTCDataChannelEvent`

[测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCDataChannelEvent-constructor.html)

**属性**

`RTCDataChannel`类型的channel，只读：channel属性表示与事件关联的`RTCDataChannel`对象。

```java
dictionary RTCDataChannelEventInit : EventInit {
             required RTCDataChannel channel;
};
```

**字典`RTCDataChannelEventInit`成员**

`RTCDataChannel`类型的channel，required：将要被事件宣布的`RTCDataChannel`对象。
