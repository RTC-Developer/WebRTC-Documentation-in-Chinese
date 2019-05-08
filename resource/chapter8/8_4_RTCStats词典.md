# 8.4 `RTCStats`字典

`RTCStats`字典表示通过检查特定受监视对象构造的stats对象。 `RTCStats`字典是一种基本类型，它指定一组默认属性，例如时间戳和类型。通过扩展`RTCStats`字典添加特定的统计信息。

请注意，虽然统计信息名称是标准化的，但任何给定的实现都可能使用Web应用程序尚不知道的值或实验值。因此，应用程序必须准备好处理未知的统计数据。

统计需要彼此同步才能产生合理的计算值;例如，如果同时报告“bytesSent”和“packetsSent”，则需要在相同的时间间隔内报告它们，这样“平均数据包大小”可以计算为“字节/数据包” - 如果间隔不同，则会产生错误。因此，实现必须返回`RTCStats`派生字典中所有统计信息的同步值。

```java
dictionary RTCStats {
             required DOMHighResTimeStamp timestamp;
             required RTCStatsType        type;
             required DOMString           id;
};
```

**字典`RTCStats`成员**

DOMHighResTimeStamp类型的`timestamp`:与此对象关联的DOMHighResTimeStamp [HIGHRES-TIME]类型的时间戳。时间相对于UNIX纪元（1970年1月1日，UTC）。对于来自远程源（例如，来自接收的RTCP数据包）的统计，时间戳表示信息到达本地端点的时间。如果适用，可以在`RTCStats`派生的字典中的附加字段中找到远程时间戳。

RTCStatsType类型的`type`:

此对象的类型。

`type`属性必须初始化为此`RTCStats`字典所代表的最具体类型的名称。

DOMString类型的`id`:与检查生成此`RTCStats`对象的对象关联的唯一ID。从两个不同的`RTCStatsReport`对象中提取的两个`RTCStats`对象，如果它们是通过检查相同的底层对象生成的，则必须具有相同的id。用户代理可以自由选择id的任何格式，只要它符合上述要求即可。

RTBRStatsType的有效值集以及它们指示的RTCStats派生的字典记录在[WEBRTC-STATS]中。
