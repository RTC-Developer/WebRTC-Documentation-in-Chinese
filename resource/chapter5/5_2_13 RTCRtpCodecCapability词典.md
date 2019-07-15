### 5.2.13 `RTCRtpCodecCapability`字典

```java
dictionary RTCRtpCodecCapability {
             required DOMString mimeType;
             required unsigned long  clockRate;
             unsigned short channels;
             DOMString      sdpFmtpLine;
};
```

**字典`RTCRtpCodecCapability`成员**

`RTCRtpCodecCapability`字典提供有关编解码器功能的信息。仅提供将在生成SDP请求中利用不同有效载荷类型的capability组合。例如：

1. 两个H.264/AVC编解码器，分别用于两个支持的分组模式值。
2. 具有不同始终速率的两个CN编解码器。

**DOMString类型**的`mimeType`:

编解码器MIME媒体类型/子类型。[IANA-RTP-2]中列出了有效的媒体类型和子类型。

**unsigned long 类型**的`clockRate`:

以赫兹为单位的编解码器的时钟速率。

**unsigned short类型**的`channels`:

如果存在，表示最大通道数量(mono=1，stereo=2)。

**DOMString类型**的`sdpFmtpLine`:

来自SDP中与编解码器对应的"a=fmtp"行的"格式特定参数"字段(如果存在)。

