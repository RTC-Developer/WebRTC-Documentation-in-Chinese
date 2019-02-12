### [5.2.6 RTCRtpEncodingParameters Dictionary](http://w3c.github.io/webrtc-pc/#rtcrtpencodingparameters)

```
dictionary RTCRtpEncodingParameters : RTCRtpCodingParameters {
             octet               codecPayloadType;
             RTCDtxStatus        dtx;
             boolean             active = true;
             unsigned long       ptime;
             unsigned long       maxBitrate;
             double              maxFramerate;
             double              scaleResolutionDownBy;
};
```

**Dictionary RTCRtpEncodingParameters Members**

*codecPayloadType* of type octet:
zh:octet类型的codecPayloadType

References a payload type from the codecs member of RTCRtpParameters. Read-only parameter.

zh:从RTCRtpParameters的编解码器成员引用有效内容类型。只读参数。

*dtx* of type RTCDtxStatus:
zh:RTCDtxStatus类型的dtx

This member is only used if the sender's kind is "audio". It indicates whether discontinuous transmission will be used. Setting it to disabled causes discontinuous transmission to be turned off. Setting it to enabled causes discontinuous transmission to be turned on if it was negotiated (either via a codec-specific parameter or via negotiation of the CN codec); if it was not negotiated (such as when setting voiceActivityDetection to false), then discontinuous operation will be turned off regardless of the value of dtx, and media will be sent even when silence is detected.

zh:仅当发件人的类型为“音频”时才使用此成员。它表示是否使用不连续传输。将其设置为禁用会导致关闭不连续传输。将其设置为启用会导致在协商时（通过特定于编解码器的参数或通过协商CN编解码器）打开不连续传输;如果没有协商（例如将voiceActivityDetection设置为false），则无论dtx的值如何，都将关闭不连续操作，即使检测到静音也会发送媒体。

*active* of type boolean, defaulting to true:
zh:boolean类型的活动，默认为true

Indicates that this encoding is actively being sent. Setting it to false causes this encoding to no longer be sent. Setting it to true causes this encoding to be sent. 

zh:表示正在积极发送此编码。将其设置为false会导致不再发送此编码。将其设置为true会导致发送此编码。

*ptime* of type unsigned long:
zh:类型为unsigned long的ptime

When present, indicates the preferred duration of media represented by a packet in milliseconds for this encoding. Typically, this is only relevant for audio encoding. The user agent MUST use this duration if possible, and otherwise use the closest available duration. This value MUST take precedence over any "ptime" attribute in the remote description, whose processing is described in [JSEP] (section 5.10.). Note that the user agent MUST still respect the limit imposed by any "maxptime" attribute, as defined in [RFC4566], Section 6.

zh:如果存在，则表示此编码的数据包所代表的媒体的首选持续时间（以毫秒为单位）。通常，这仅与音频编码有关。如果可能，用户代理必须使用此持续时间，否则使用最接近的可用持续时间。该值必须优先于远程描述中的任何“ptime”属性，其处理在[JSEP]（第5.10节）中描述。请注意，用户代理必须仍然遵守任何“maxptime”属性所施加的限制，如[RFC4566]第6节中所定义。

*maxBitrate* of type unsigned long:
zh:maxBitrate类型为unsigned long

When present, indicates the maximum bitrate that can be used to send this encoding. The encoding may also be further constrained by other limits (such as maxFramerate or per-transport or per-session bandwidth limits) below the maximum specified here. maxBitrate is computed the same way as the Transport Independent Application Specific Maximum (TIAS) bandwidth defined in [RFC3890] Section 6.2.2, which is the maximum bandwidth needed without counting IP or other transport layers like TCP or UDP.

zh:存在时，表示可用于发送此编码的最大比特率。编码还可能受到低于此处指定的最大值的其他限制（例如maxFramerate或每传输或每会话带宽限制）的限制。 maxBitrate的计算方法与[RFC3890]第6.2.2节中定义的传输独立应用程序特定最大值（TIAS）带宽相同，后者是不计算IP或TCP或UDP等其他传输层所需的最大带宽。

*maxFramerate* of type double:
zh:double类型的maxFramerate

When present, indicates the maximum framerate that can be used to send this encoding, in frames per second.

zh:存在时，表示可用于发送此编码的最大帧速率，以每秒帧数为单位。

 If changed with setParameters, the new framerate takes effect after the current picture is completed; setting the max framerate to zero thus has the effect of freezing the video on the next frame. 

zh: 如果使用setParameters更改，则新帧速率在当前图片完成后生效;将最大帧速率设置为零因此具有在下一帧上冻结视频的效果。

*scaleResolutionDownBy* of type double:
zh:scaleResolutionDown类型为double

This member is only present if the sender's kind is "video". The video's resolution will be scaled down in each dimension by the given value before sending. For example, if the value is 2.0, the video will be scaled down by a factor of 2 in each dimension, resulting in sending a video of one quarter the size. If the value is 1.0, the video will not be affected. The value must be greater than or equal to 1.0. By default, the sender will not apply any scaling, (i.e., scaleResolutionDownBy will be 1.0).

zh:此会员仅在发件人的类型为“视频”时才会出现。在发送之前，视频的分辨率将按给定值按比例缩小。例如，如果值为2.0，则视频将在每个维度中按比例缩小2倍，从而发送大小为四分之一的视频。如果值为1.0，则视频不会受到影响。该值必须大于或等于1.0。默认情况下，发件人不会应用任何缩放（即scaleResolutionDownBy将为1.0）。
