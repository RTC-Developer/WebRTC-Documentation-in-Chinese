## 8.3 `RTCStatsReport`对象

getStats（）方法以`RTCStatsReport`对象的形式传达成功的结果。 `RTCStatsReport`对象是标识被检查对象（`RTCStats`实例中的`id`属性）的字符串之间的映射，以及它们对应的`RTCStats`派生的字典。

`RTCStatsReport`可以由几个`RTCStats`派生的字典组成，每个字典报告实现认为与选择器相关的一个底层对象的统计信息。通过对某种类型的所有统计量求和，可以实现选择器的总和;例如，如果`RTCRtpSender`使用多个SSRC通过网络传输其轨迹，则每个SSRC中`RTCStatsReport`可以包含一个`RTCStats`派生的字典（可以通过“ssrc” stats属性的值来区分）。

```java
[Exposed=Window] interface RTCStatsReport {
    readonly maplike<DOMString, object>;
};
```

这个接口有“entries”，“forEach”，“get”，“has”，“keys”，“values”，@@ iterator方法和`readonly maplike`带来的“size”getter。

使用这些来检索此统计报告由`RTCStats`组成的各种词典。支持的属性名称[WEBIDL-1]的集合被定义为为此统计信息报告生成的所有`RTCStats`派生词典的ID。

