### [5.2.13 RTCRtpCodecCapability Dictionary](http://w3c.github.io/webrtc-pc/#rtcrtpcodeccapability)

```
dictionary RTCRtpCodecCapability {
             required DOMString mimeType;
             required unsigned long  clockRate;
             unsigned short channels;
             DOMString      sdpFmtpLine;
};
```

**Dictionary RTCRtpCodecCapability Members **

The RTCRtpCodecCapability dictionary provides information about codec capabilities. Only capability combinations that would utilize distinct payload types in a generated SDP offer are provided. For example:

zh:RTCRtpCodecCapability字典提供有关编解码器功能的信息。仅提供将在生成的SDP提供中利用不同有效载荷类型的能力组合。例如：

1. Two H.264/AVC codecs, one for each of two supported packetization-mode values.
zh:两个H.264 / AVC编解码器，分别用于两个支持的分组模式值。
2. Two CN codecs with different clock rates.
zh:两个具有不同时钟速率的CN编解码器。

*mimeType* of type DOMString, required:
zh:需要DOMString类型的mimeType

The codec MIME media type/subtype. Valid media types and subtypes are listed in [IANA-RTP-2].

zh:编解码器MIME媒体类型/子类型。 [IANA-RTP-2]中列出了有效的媒体类型和子类型。

*clockRate* of type unsigned long, required:
zh:clockRate类型为unsigned long，必需

The codec clock rate expressed in Hertz.

zh:编解码器时钟速率以赫兹表示。

*channels* of type unsigned short:
zh:无符号短型通道

If present, indicates the maximum number of channels (mono=1, stereo=2).

zh:如果存在，则表示最大通道数（mono = 1，stereo = 2）。

*sdpFmtpLine* of type DOMString:
zh:DOMString类型的sdpFmtpLine

The "format specific parameters" field from the "a=fmtp" line in the SDP corresponding to the codec, if one exists.

zh:SDP中对应于编解码器的“a = fmtp”行中的“格式特定参数”字段（如果存在）。
