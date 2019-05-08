## 7.1 RTCRtpSender接口扩展

点对点DTMF API对`RTCRtpSender`接口的扩展如下。

```java
partial interface RTCRtpSender {
    readonly        attribute RTCDTMFSender? dtmf;
};
```

**属性**

RTCDTMFSender类型的dtmf,只读的，可以为null：当获取时，dtmf属性返回[Dtmf]内部插槽的值，它代表一个可用来发送DTMF的`RTCDTMFSender`,如果未设置，则为null。当RTCRtpSender的[SenderTrack]为“audio”，[Dtmf]内部插槽被设置。
