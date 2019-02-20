
## [5.7 RTCTrackEvent](http://w3c.github.io/webrtc-pc/#rtctrackevent)

The track event uses the RTCTrackEvent interface.

zh:track事件使用RTCTrackEvent接口。

```
        [ Constructor (DOMString type, RTCTrackEventInit eventInitDict), Exposed=Window]
interface RTCTrackEvent : Event {
    readonly        attribute RTCRtpReceiver           receiver;
    readonly        attribute MediaStreamTrack         track;
    [SameObject]
    readonly        attribute FrozenArray<MediaStream> streams;
    readonly        attribute RTCRtpTransceiver        transceiver;
};
```

**Constructors**

`RTCTrackEvent`
	 

**Attributes**

*receiver* of type `RTCRtpReceiver`, readonly:
zh:RTCRtpReceiver类型的接收器，只读

The receiver attribute represents the RTCRtpReceiver object associated with the event.

zh:receiver属性表示与事件关联的RTCRtpReceiver对象。

*track* of type MediaStreamTrack, readonly:
zh:追踪类型MediaStreamTrack，readonly

The track attribute represents the MediaStreamTrack object that is associated with the RTCRtpReceiver identified by receiver.

zh:track属性表示与接收方标识的RTCRtpReceiver关联的MediaStreamTrack对象。

*streams* of type FrozenArray<MediaStream>, readonly:
zh:FrozenArray <MediaStream>类型的流，只读

The streams attribute returns an array of MediaStream objects representing the MediaStreams that this event's track is a part of.

zh:streams属性返回一个MediaStream对象数组，表示此事件的轨道所属的MediaStream。

*transceiver* of type RTCRtpTransceiver, readonly:
zh:RTCRtpTransceiver类型的收发器，只读

The transceiver attribute represents the RTCRtpTransceiver object associated with the event.

zh:transceiver属性表示与事件关联的RTCRtpTransceiver对象。

```
dictionary RTCTrackEventInit : EventInit {
    required RTCRtpReceiver        receiver;
    required MediaStreamTrack      track;
             sequence<MediaStream> streams = [];
    required RTCRtpTransceiver     transceiver;
};
```

**Dictionary RTCTrackEventInit Members**

*receiver* of type RTCRtpReceiver, required:
zh:RTCRtpReceiver类型的接收器，必需

The receiver attribute represents the RTCRtpReceiver object associated with the event.

zh:receiver属性表示与事件关联的RTCRtpReceiver对象。

*track* of type MediaStreamTrack, required:
zh:需要跟踪MediaStreamTrack类型

The track attribute represents the MediaStreamTrack object that is associated with the RTCRtpReceiver identified by receiver.

zh:track属性表示与接收方标识的RTCRtpReceiver关联的MediaStreamTrack对象。

*streams* of type sequence<MediaStream>, defaulting to []:
zh:类型序列<MediaStream>的流，默认为[]

The streams attribute returns an array of MediaStream objects representing the MediaStreams that this event's track is a part of.

zh:streams属性返回一个MediaStream对象数组，表示此事件的轨道所属的MediaStream。

*transceiver* of type RTCRtpTransceiver, required:
zh:需要RTCRtpTransceiver类型的收发器

The transceiver attribute represents the RTCRtpTransceiver object associated with the event.

zh:transceiver属性表示与事件关联的RTCRtpTransceiver对象。

