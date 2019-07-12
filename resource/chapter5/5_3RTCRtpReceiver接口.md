## [5.3 RTCRtpReceiver 接口](http://w3c.github.io/webrtc-pc/#rtcrtpreceiver-interface)

`RTCRtpReceiver`接口允许应用程序检查`MediaStreamTrack`的接收。

要使用字符串`kind`来创建`RTCRtpReceiver`，请运行以下步骤：

1. 让接收器成为新的`RTCRtpReceiver`对象。
2. 让`track`成为一个新的MediaStreamTrack对象[GETUSERMEDIA]。轨道源是接收器提供的远程源。请注意，`track.id`由用户代理生成，不会映射到远程端的任何轨道ID。
3. 将`track.kind`初始化为`kind`。
4. 将`track.label`初始化为将字符串“remote”与`kind`连接的结果。
5. 将`track.readyState`初始化为`live`。
6. 将`track.muted`初始化为`true`。请参阅`MediaStreamTrack`部分，了解在`MediaStreamTrack`接收媒体数据或者没有接收的情况下，静音属性如何反映。
7. 让接收器将[[ReceiverTrack]]内部插槽初始化为`track`。
8. 让接收器将[[ReceiverTransport]]内部插槽初始化为`null`。
9. 让接收器将[[ReceiverRtcpTransport]]内部插槽初始化为`null`。
10. 让接收器具有[[AssociatedRemoteMediaStreams]]内部槽，表示与该接收器的`MediaStreamTrack`对象相关联的`MediaStream`对象的列表，并初始化为空列表。
11. 让接收器有一个[[ReceiveCodecs]]内部插槽，表示`RTCRtpCodecParameters`字典列表，并初始化为空列表。
12. 返回接收器。

```
[Exposed=Window] interface RTCRtpReceiver {
    readonly        attribute MediaStreamTrack  track;
    readonly        attribute RTCDtlsTransport? transport;
    readonly        attribute RTCDtlsTransport? rtcpTransport;
    static RTCRtpCapabilities?         getCapabilities (DOMString kind);
    RTCRtpReceiveParameters            getParameters ();
    sequence<RTCRtpContributingSource>    getContributingSources ();
    sequence<RTCRtpSynchronizationSource> getSynchronizationSources ();
    Promise<RTCStatsReport>   getStats();
};
```

**属性**
*track* 类型`MediaStreamTrack`，只读
`track`属性是与此`RTCRtpReceiver`对象接收器关联的轨道。

请注意，`track.stop（）`是最终的，尽管克隆不受影响。由于`receiver.track.stop（）`不会隐式停止接收器，因此继续发送`Receiver Reports`。获取时，属性必须返回[[ReceiverTrack]]槽的值。

*transport* `RTCDtlsTransport`类型的传输，只读，可空

传输属性是以RTP分组的形式接收接收者的轨道的媒体的传输。在构造`RTCDtlsTransport`对象之前，transport属性将为null。使用捆绑时，多个`RTCRtpReceiver`对象将共享一个传输，并将通过同一传输接收 RTP 和 RTCP。

获取时，属性必须返回[[ReceiverTransport]]槽的值。

`rtcpTransport`类型为`RTCDtlsTransport`，只读，可空

`rtcpTransport`属性是发送和接收 RTCP 的传输。在构造`RTCDtlsTransport`对象之前，`rtcpTransport`属性将为`null`。当使用 RTCP mux（或捆绑，强制执行 RTCP mux）时，`rtcpTransport`将为`null`，并且 RTP 和 RTCP 流量都将通过传输流动。

获取时，属性必须返回[[ReceiverRtcpTransport]]槽的值。

**方法**
`getCapabilities`，静态
`getCapabilities（）`方法返回系统功能的最乐观视图，用于接收给定类型的媒体。它不保留任何资源，端口或其他状态，但旨在提供一种方法来发现浏览器的功能类型，包括可能支持的编解码器。用户代理必须支持“音频”和“视频”的类型值。如果系统没有与`kind`参数的值相对应的功能，则`getCapabilities`返回`null`。

这些功能通常在设备上提供持久的跨源信息，从而增加了应用程序的指纹表面。在隐私敏感的上下文中，浏览器可以考虑缓解，例如仅报告功能的公共子集。

`getParameters`
`getParameters（）`方法返回`RTCRtpReceiver`对象的当前参数，用于解码轨道的方式。
调用`getParameters`时，`RTCRtpReceiveParameters`字典构造如下：
根据当前远程描述中存在的 RID 填充编码。

*  `headerExtensions`序列基于接收器当前准备接收的头扩展来填充。
*  编解码器序列基于接收器当前准备接收的编解码器来填充。
   注意本地和远程描述可能会影响此编解码器列表。例如，如果提供了三个编解码器，接收器将准备好接收它们中的每一个，并将从`getParameters`返回它们。但是如果远程端点只回答两个，则`getParameters`将不再返回缺少的编解码器，因为接收器不再需要准备接收它。
*  如果接收器当前准备接收缩小的RTCP数据包，则`rtcp.reducedSize`设置为true，否则设置为`false`。 `rtcp.cname`被省略了。

`getContributingSources`
返回此RTCRtpReceiver在过去10秒内收到的每个唯一CSRC标识符的RTCRtpContributingSource。

`getSynchronizationSources`
返回此`RTCRtpReceiver`在过去10秒内收到的每个唯一 SSRC 标识符的`RTCRtpContributingSource`

`getStats`
仅收集此接收器的统计信息并异步报告结果。
当调用`getStats（）`方法时，用户代理必须运行以下步骤：

1. 让`selector`成为调用该方法的`RTCRtpReceiver`对象。

2. 让`p`成为新的承诺，并行执行以下步骤：
	1.  根据统计选择算法收集选择器指示的统计数据。
	2.  使用生成的RTCStatsReport对象解析p，其中包含收集的统计信息。
3. 返回p。

`RTCRtpContributingSource`和`RTCRtpSynchronizationSource`字典分别包含有关给定贡献源（CSRC）或同步源（SSRC）的信息，包括源所贡献的数据包的最近时间。浏览器必须保留前 10 秒内收到的 RTP 数据包的信息。当包含在 RTP 数据包中的第一个音频或视频帧被传送到`RTCRtpReceiver`的`MediaStreamTrack`进行播出时，用户代理必须排队任务，以根据数据包的内容更新`RTCRtpContributingSource`和`RTCRtpSynchronizationSource`字典的相关信息。每次更新与 SSRC 标识符对应的`RTCRtpSynchronizationSource`字典相关的信息，并且如果 RTP 分组包含 CSRC 标识符，则还更新与那些 CSRC 标识符对应的`RTCRtpContributingSource`字典相关的信息。

NOTE
如一致性部分所述，只要最终结果是等效的，可以以任何方式实现作为算法的要求。因此，实现不需要为每个数据包逐字排队任务，只要最终结果是在单个事件循环任务执行中，所有返回的特定`RTCRtpReceiver`的`RTCRtpSynchronizationSource`和`RTCRtpContributingSource`字典都包含来自 RTP 流中单个点的信息。

```
dictionary RTCRtpContributingSource {
    required DOMHighResTimeStamp timestamp;
    required unsigned long       source;
             double              audioLevel;
};
```

#### 字典 RTCRtpContributingSource 成员

*timestamp* 类型为DOMHighResTimeStamp， 必需
DOMHighResTimeStamp [HIGHRES-TIME]类型的时间戳，指示到达源自此源的RTP数据包的媒体播放的最近时间。时间戳在播出时定义为`performance.timeOrigin + performance.now（）`。

*source* 类型为unsigned，必需
贡献或同步源的 CSRC 或 SSRC 标识符。

*audioLevel* 类型为double
仅适用于音频接收器。这是 0..1（线性）之间的值，其中 1.0 表示 0 dBov，0 表示静音，0.5 表示声压级从 0 dBov变化约 6 dBSPL。
对于 CSRC，如果存在 RFC 6465 标头扩展，则必须从[RFC6465]中定义的级别值转换，否则该成员必须不存在。
对于 SSRC，如果存在 RFC 6464 标头扩展，则必须从[RFC6464]中定义的级别值转换，否则用户代理必须从音频数据计算值（音频接收器不得缺少该成员）。
两个 RFC 将级别定义为 0 到 127 的整数值，表示相对于系统可能编码的最大信号的负分贝的音频电平。因此，0 代表系统可能编码的最响亮信号，127 代表静音。
要将这些值转换为线性 0..1 范围，将值 127 转换为 0，并使用以下公式转换所有其他值：`10 ^（ -  rfc_level / 20）`。

```
dictionary RTCRtpSynchronizationSource : RTCRtpContributingSource {
    boolean voiceActivityFlag;
};
```

**字典 RTCRtpSynchronizationSource 成员**

*voiceActivityFlag* boolean类型
仅适用于音频接收器。从该源播放的最后一个RTP数据包是否包含语音活动（true）或不包含语音活动（false）。如果 RFC 6464 扩展头不存在，或者对等体通过将“vad”扩展属性设置为“off”来表示它没有使用 V bit，如[RFC6464]第 4 节中所述，则`voiceActivityFlag`将是缺席。
