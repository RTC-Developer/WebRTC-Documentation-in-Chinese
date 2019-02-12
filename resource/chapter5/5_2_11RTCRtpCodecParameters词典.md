### [5.2.11 RTCRtpCodecParameters 词典](http://w3c.github.io/webrtc-pc/#rtcrtpcodecparameters)

```
dictionary RTCRtpCodecParameters {
             required octet          payloadType;
             required DOMString      mimeType;
             required unsigned long  clockRate;
             unsigned short channels;
             DOMString      sdpFmtpLine;
};
```

**Dictionary RTCRtpCodecParameters Members**

*payloadType* of type octet:
zh:payload类型为octet的类型

The RTP payload type used to identify this codec. Read-only parameter.

zh:用于标识此编解码器的RTP有效内容类型。只读参数。

*mimeType* of type DOMString:
zh:DOMString类型的mimeType

The codec MIME media type/subtype. Valid media types and subtypes are listed in [IANA-RTP-2]. Read-only parameter.

zh:编解码器MIME媒体类型/子类型。 [IANA-RTP-2]中列出了有效的媒体类型和子类型。只读参数。

*clockRate* of type unsigned long:
zh:clockRate类型为unsigned long

The codec clock rate expressed in Hertz. Read-only parameter.

zh:编解码器时钟速率以赫兹表示。只读参数。

*channels* of type unsigned short:
zh:无符号短型通道

When present, indicates the number of channels (mono=1, stereo=2). Read-only parameter.

zh:存在时，表示通道数（mono = 1，stereo = 2）。只读参数。

*sdpFmtpLine* of type DOMString:
zh:DOMString类型的sdpFmtpLine

The "format specific parameters" field from the "a=fmtp" line in the SDP corresponding to the codec, if one exists, as defined by [JSEP] (section 5.8.). For an RTCRtpSender, these parameters come from the remote description, and for an RTCRtpReceiver, they come from the local description. Read-only parameter.

zh:SDP中对应于编解码器的“a = fmtp”行中的“格式特定参数”字段，如果存在，如[JSEP]所定义（第5.8节）。对于RTCRtpSender，这些参数来自远程描述，对于RTCRtpReceiver，它们来自本地描述。只读参数。