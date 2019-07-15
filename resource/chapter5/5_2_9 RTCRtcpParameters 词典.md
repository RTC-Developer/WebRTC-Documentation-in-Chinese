### 5.2.9 `RTCRtpParameters`字典

```java
dictionary RTCRtcpParameters {
             DOMString cname;
             boolean   reducedSize;
};
```

**字典`RTCRtcpParameters`成员**

DOMString类型的`cname`:

RTCP使用的规范名称(CNAME) (例如，在SDES消息中)。只读参数。

boolean类型的`reducedSize`:

是否已配置缩小的RTCP[RFC5506] (如果为true)或[RFC3550]中指定的复合RTCP(如果为false)。只读参数。
