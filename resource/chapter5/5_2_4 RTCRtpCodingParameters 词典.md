### 5.2.4 `RTCRtpCodingParameters`字典

```java
dictionary RTCRtpCodingParameters {
             DOMString           rid;
};
```

**字典RTCRtpCodingParameters成员**

DOMString类型的`rid`:

如果设置，RTP编码将与[JSEP] (第5.2.1节)定义的RID头扩展一起发送。RID不能通过`setParameters`修改。它只能在发送端的`addTransceiver`中设置或修改。只读参数。

