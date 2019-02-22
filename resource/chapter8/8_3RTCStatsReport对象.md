## [8.3 RTCStatsReport Object zh:8.3 RTCStatsReport对象](http://w3c.github.io/webrtc-pc/#rtcstatsreport-object)

The getStats() method delivers a successful result in the form of an RTCStatsReport object. An RTCStatsReport object is a map between strings that identify the inspected objects (id attribute in RTCStats instances), and their corresponding RTCStats-derived dictionaries.

zh:getStats（）方法以RTCStatsReport对象的形式提供成功的结果。 RTCStatsReport对象是标识被检查对象（RTCStats实例中的id属性）的字符串之间的映射，以及它们对应的RTCStats派生的字典。

An RTCStatsReport may be composed of several RTCStats-derived dictionaries, each reporting stats for one underlying object that the implementation thinks is relevant for the selector. One achieves the total for the selector by summing over all the stats of a certain type; for instance, if an RTCRtpSender uses multiple SSRCs to carry its track over the network, the RTCStatsReport may contain one RTCStats-derived dictionary per SSRC (which can be distinguished by the value of the "ssrc" stats attribute).

zh:RTCStatsReport可以由几个RTCStats派生的字典组成，每个字典报告实现认为与选择器相关的一个底层对象的统计信息。通过对某种类型的所有统计量求和，可以实现选择器的总和;例如，如果RTCRtpSender使用多个SSRC通过网络传输其跟踪，则RTCStatsReport可以包含每个SSRC一个RTCStats派生的字典（可以通过“ssrc”stats属性的值来区分）。

```
[Exposed=Window] interface RTCStatsReport {
    readonly maplike<DOMString, object>;
};
```


This interface has "entries", "forEach", "get", "has", "keys", "values", @@iterator methods and a "size" getter brought by readonly maplike.

zh:这个接口有“entries”，“forEach”，“get”，“has”，“keys”，“values”，@@ iterator方法和readonly maplike带来的“size”getter。

Use these to retrieve the various dictionaries descended from RTCStats that this stats report is composed of. The set of supported property names [WEBIDL-1] is defined as the ids of all the RTCStats-derived dictionaries that have been generated for this stats report.

zh:使用这些来检索此统计报告由RTCStats组成的各种词典。支持的属性名称[WEBIDL-1]的集合被定义为为此统计信息报告生成的所有RTCStats派生词典的ID。