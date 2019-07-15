### 5.2.6 `RTCRtpEncodingParameters`字典

```java
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

**字典`RTCRtpEncodingParamters`成员**

octet类型的`codecPayloadType`:

从`RTCRtpParameters`的编解码器成员引用有效内容类型。只读参数。

`RTCDtxStatus`类型的`dtx`:

仅当发送方类型为"audio"时才使用此成员。它表示是否使用不连续传输。将它设置为禁用会导致关闭不连续传输。将它设置为启用会导致在协商完成情况下打开不连续传输(通过制定编码器参数或通过CN编码器协商)。如果没有协商(例如当设置`voiceActivityDetection`为`false`时)，则无论`dtx`的值为多少，都会关闭不连续操作,当侦测到silence后，媒体将会被发送。

boolean类型的`active`，默认为`true`：

表明此编码正在被发送。设置它为`false`导致编码不再被发送。设置为`true`导致它被发送。由于设置值为`false`不会导致SSRC被移除，所以不会发送RTCP BYE。

unsigned long 类型的`ptime`:

如果存在，则表示此编码的数据包所代表的媒体的首选持续时间(以毫秒为单位)。通常，这仅与音频编码有关。用户代理必须使用此持续时间，否则使用最接近的可用持续时间。该值必须优先于远程描述的任何"ptime"属性，其处理在[JSEP] (第5.10节)中描述。请注意，用户代理仍必须遵守任何"maxptime"属性所施加的限制，如[RFC4566]第六节中所定义。

unsigned long类型的`maxBitrate`:

存在时，表示可用于发送此编码的最大比特率。只要不超过`maxBitrate`值，用户代理就可以在编码之间自由分配带宽。编码还可能受到低于此处指定的最大值的其它限制(例如maxFramerate或每传输每会话带宽限制)。maxBitrate的计算方法与[RFC3890]第6.2.2节中定义的传输独立应用程序特定最大值(TIAS)带宽的计算方式相同，它是不计数IP或其它传输层例如TCP或UDP时所需的最大带宽。

double类型的`maxFrameate`:

存在时，表示可用于发送此编码的最大帧率，以每秒帧数为单位。只要不超过`maxFramerate`值，用户代理就可以在编码之间自由分配带宽。

如果使用`setParameters`更改，新的帧率在当前图片完成后生效。设置最大帧率为零，则会具有在下一帧冻结视频的效果。

double类型的`scaleResolutionDownBy` :

此会员仅在发件人的类型为"`video`"时才会出现。在发送之前，视频的分辨率将按给定值按比例缩小。例如，如果值为2.0，则视频将在每个维度中按比例缩小2倍，从而发送大小为四分之一的视频。如果值为1.0，则视频不会受到影响。该值必须大于等于1.0，默认情况下，发件人不会应用任何缩放(即`scaleResolutionDownBy`将为1.0)。



