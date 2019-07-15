### 5.2.11 `RTCRtpCodecParameters`字典

```java
dictionary RTCRtpCodecParameters {
             required octet          payloadType;
             required DOMString      mimeType;
             required unsigned long  clockRate;
             unsigned short channels;
             DOMString      sdpFmtpLine;
};
```

**字典`RTCRtpCodecParameters`成员**

**octet**类型的`payloadType`:

用于验证编解码器的RTP负载类型。只读参数。

**DOMString**类型的mimeType：

编解码器MIME媒体类型/子类型。有效的媒体类型和子类型都在[IANA-RTP-2]中列出。只读参数。

**unsigned long**类型的`clockRate`:

编解码器的时钟速率，以赫兹为单位。只读参数。

**unsigned short**类型的`channels`：

存在时，表示通道数量(mono=1, stereo=2)。只读参数。

**DOMString**类型的`sdpFmtpLine`:

SDP中对应于编解码器的"a=fmtp"行中的"格式特定参数"字段(如果存在)，如[JSEP]所定义(第5.8节)。对于`RTCRtpSender`,这些参数来自远程描述，对于`RTCRtpReceiver`,它们来自本地描述。只读参数。

