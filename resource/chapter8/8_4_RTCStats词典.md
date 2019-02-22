

## [8.4 RTCStats Dictionary zh:8.4 RTCStats字典](http://w3c.github.io/webrtc-pc/#rtcstats-dictionary)

An RTCStats dictionary represents the stats object constructed by inspecting a specific monitored object. The RTCStats dictionary is a base type that specifies as set of default attributes, such as timestamp and type. Specific stats are added by extending the RTCStats dictionary.

zh:RTCStats字典表示通过检查特定受监视对象构造的stats对象。 RTCStats字典是一种基本类型，它指定一组默认属性，例如时间戳和类型。通过扩展RTCStats字典添加特定的统计信息。

Note that while stats names are standardized, any given implementation may be using experimental values or values not yet known to the Web application. Thus, applications MUST be prepared to deal with unknown stats.

zh:请注意，虽然统计信息名称是标准化的，但任何给定的实现都可能使用Web应用程序尚不知道的实验值或值。因此，应用程序必须准备好处理未知的统计数据。

Statistics need to be synchronized with each other in order to yield reasonable values in computation; for instance, if "bytesSent" and "packetsSent" are both reported, they both need to be reported over the same interval, so that "average packet size" can be computed as "bytes / packets" - if the intervals are different, this will yield errors. Thus implementations MUST return synchronized values for all stats in an RTCStats-derived dictionary.

zh:统计需要彼此同步才能产生合理的计算值;例如，如果同时报告“bytesSent”和“packetsSent”，则需要在相同的时间间隔内报告它们，以便“平均数据包大小”可以计算为“字节/数据包” - 如果间隔不同，则会产生错误。因此，实现必须返回RTCStats派生字典中所有统计信息的同步值。

```
dictionary RTCStats {
             required DOMHighResTimeStamp timestamp;
             required RTCStatsType        type;
             required DOMString           id;
};
```

**Dictionary RTCStats Members**

*timestamp* of type DOMHighResTimeStamp:
zh:DOMHighResTimeStamp类型的时间戳

The timestamp, of type DOMHighResTimeStamp [HIGHRES-TIME], associated with this object. The time is relative to the UNIX epoch (Jan 1, 1970, UTC). For statistics that came from a remote source (e.g., from received RTCP packets), timestamp represents the time at which the information arrived at the local endpoint. The remote timestamp can be found in an additional field in an RTCStats-derived dictionary, if applicable.

zh:与此对象关联的DOMHighResTimeStamp [HIGHRES-TIME]类型的时间戳。时间相对于UNIX纪元（1970年1月1日，UTC）。对于来自远程源（例如，来自接收的RTCP分组）的统计，时间戳表示信息到达本地端点的时间。如果适用，可以在RTCStats派生的字典中的附加字段中找到远程时间戳。

*type* of type RTCStatsType:
zh:RTCStatsType类型的类型

The type of this object.

zh:这个对象的类型。

The type attribute MUST be initialized to the name of the most specific type this RTCStats dictionary represents.

zh:type属性必须初始化为此RTCStats字典所代表的最具体类型的名称。

*id* of type DOMString:
zh:DOMString类型的id

A unique id that is associated with the object that was inspected to produce this RTCStats object. Two RTCStats objects, extracted from two different RTCStatsReport objects, MUST have the same id if they were produced by inspecting the same underlying object. User agents are free to pick any format for the id as long as it meets the requirements above.

zh:与检查生成此RTCStats对象的对象关联的唯一ID。从两个不同的RTCStatsReport对象中提取的两个RTCStats对象，如果它们是通过检查相同的底层对象生成的，则必须具有相同的id。用户代理可以自由选择id的任何格式，只要它符合上述要求即可。

The set of valid values for RTCStatsType, and the dictionaries derived from RTCStats that they indicate, are documented in [WEBRTC-STATS].

zh:RTBRStatsType的有效值集以及它们指示的RTCStats派生的字典记录在[WEBRTC-STATS]中。

