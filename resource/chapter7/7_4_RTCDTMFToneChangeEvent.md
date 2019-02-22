## [7.4 RTCDTMFToneChangeEvent zh:7.4 RTCDTMFToneChangeEvent](http://w3c.github.io/webrtc-pc/#rtcdtmftonechangeevent)

The tonechange event uses the RTCDTMFToneChangeEvent interface.

zh:tonechange事件使用RTCDTMFToneChangeEvent接口。

```
        [ Constructor (DOMString type, RTCDTMFToneChangeEventInit eventInitDict), Exposed=Window]
interface RTCDTMFToneChangeEvent : Event {
    readonly        attribute DOMString tone;
};

```

**Constructors zh:构造函数**

`RTCDTMFToneChangeEvent`
 
**Attributes zh:属性**

*tone* of type DOMString, readonly:
zh:DOMString类型的语气，readonly

The tone attribute contains the character for the tone (including ",") that has just begun playout (see insertDTMF ). If the value is the empty string, it indicates that the [[ToneBuffer]] slot is an empty string and that the previous tones have completed playback.

zh:tone属性包含刚刚开始播放的音调（包括“，”）的字符（参见insertDTMF）。如果该值为空字符串，则表示[[ToneBuffer]]插槽为空字符串，并且前一个音调已完成播放。

```
dictionary RTCDTMFToneChangeEventInit : EventInit {
             required DOMString tone;
};
```

**Dictionary RTCDTMFToneChangeEventInit Members **

*tone* of type DOMString:
zh:DOMString类型的基调

The tone attribute contains the character for the tone (including ",") that has just begun playout (see insertDTMF ). If the value is the empty string, it indicates that the [[ToneBuffer]] slot is an empty string and that the previous tones have completed playback.

zh:tone属性包含刚刚开始播放的音调（包括“，”）的字符（参见insertDTMF）。如果该值为空字符串，则表示[[ToneBuffer]]插槽为空字符串，并且前一个音调已完成播放。