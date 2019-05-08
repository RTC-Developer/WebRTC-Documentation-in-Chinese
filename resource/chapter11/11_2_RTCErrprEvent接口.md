## 11.2 `RTCErrprEvent`接口

`RTCErrorEvent`接口是针对将`RTCError`作为事件引发的情况定义的:

```java
[
    Exposed=Window,
    Constructor (DOMString type, RTCErrorEventInit eventInitDict)
] interface RTCErrorEvent : Event {
    [SameObject] readonly attribute RTCError error;
};
```



### 11.2.1 构造函数

`RTCErrorEvent`:[测试：1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/idlharness.https.window.js)

构造一个新的`RTCErrorEvent`。

### 11.2.2 属性

`RTCError`类型的error，只读，可以为null：

描述触发事件的错误的`RTCError`。
