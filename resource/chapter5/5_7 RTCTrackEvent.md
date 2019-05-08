## 5.7 `RTCTrackEvent`

`track`事件使用`RTCTrackEvent`接口。

```java
        [ Constructor (DOMString type, RTCTrackEventInit eventInitDict), Exposed=Window]
interface RTCTrackEvent : Event {
    readonly        attribute RTCRtpReceiver           receiver;
    readonly        attribute MediaStreamTrack         track;
    [SameObject]
    readonly        attribute FrozenArray<MediaStream> streams;
    readonly        attribute RTCRtpTransceiver        transceiver;
};
```

**构造函数**

`RTCTrackEvent`(https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCTrackEvent-constructor.html)

**属性**

`RTCRtpReceiver`类型的`receiver`，只读：`receiver`属性表示与事件关联的`RTCRtpReceiver`对象。

`MediaStreamTrack`类型的track，只读：`track`属性表示与`RTCRtpReceiver`关联的由`receiver`验证的`MediaStreamTrack`对象。

`FrozenArray<MediaStream>`类型的streams,只读：`streams`属性返回`MediaStream`对象的数组，表示此事件的track是`MediaStreams`的一部分。

`RTCRtpTransceiver`类型的`transceiver`，只读：`transceiver`属性表示与此事件关联的`RTCRtpTransceiver`对象。

```java
dictionary RTCTrackEventInit : EventInit {
    required RTCRtpReceiver        receiver;
    required MediaStreamTrack      track;
             sequence<MediaStream> streams = [];
    required RTCRtpTransceiver     transceiver;
};
```

**字典`RTCTrackEventInit`成员**

`RTCRtpReceiver`类型的`receiver`

`MediaStreamTrack`类型的`track`

`sequence<MediaStream>`类型的`streams`

`RTCRtpTransceiver`类型的`transceiver`
