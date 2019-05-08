## 7.4`RTCDTMFToneChangeEvent`

`tonechange`事件使用`RTCDTMFToneChangeEvent`接口。

```java
       [ Constructor (DOMString type, RTCDTMFToneChangeEventInit eventInitDict), Exposed=Window]
interface RTCDTMFToneChangeEvent : Event {
    readonly        attribute DOMString tone;
};
```

**构造函数**

`RTCDTMFToneChangeEvent`

**属性**

DOMString类型的`tone`，只读：:`tone`属性包含刚刚开始播放的音调（包括“，”）的字符（参见`insertDTMF`）。如果该值为空字符串，则表示[[ToneBuffer]]插槽为空字符串，并且前一个音调已完成播放。

```java
dictionary RTCDTMFToneChangeEventInit : EventInit {
             required DOMString tone;
};
```

**字典`RTCDTMFToneChangeEventInit`成员**

DOMString类型的`tone`:`tone`属性包含刚刚开始播放的音调（包括“，”）的字符（参见`insertDTMF`）。如果该值为空字符串，则表示[[ToneBuffer]]插槽为空字符串，并且前一个音调已完成播放。
