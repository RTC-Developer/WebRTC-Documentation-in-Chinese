## 5.2 `RTCRtpSender` Interface

`RTCRtpSender`接口允许应用程序控制给定`MediaStreamTrack`的编码方式并将其传输到远程对等方。在`RTCRtpSender`对象上调用`setParameters`时，编码会相应更改。

要使用`MediaStreamTrack`**创建RTCRtpSender**,跟踪，字符串，种类，`MediaStream`对象列表，流以及可选的`RTCRtpEncodingParameters`对象列表，**sendEncodings**,请运行以下步骤：

1. 让sender成为新的`RTCRtpSender`对象。
2. 让sender具有初始化为track的**[[SenderTrack]]**内部插槽。
3. 让sender具有初始化为null的**[[SenderTransport]]**内部插槽。
4. 让sender具有初始化为null的**[[Dtmf]]**内部插槽。
5. 如果种类是`“audio”`，则创建一个`RTCDTMFSender` **dtmf**并将[[Dtmf]]内部插槽设置为**dtmf**。
6. 让sender具有初始化为null的**[[SenderRtcpTransport]]**内部插槽。
7. 让sender具有一个**[[AssociatedMediaStreamsIds]]**内部插槽，表示此发件人要关联的`MediaStream`对象的Id列表。如[JSEP] (第5.2.1节)中所述，当发送方在SDP中表示时，使用`[[AssociatedMediaStreamIds]]`槽。
8. 设置sender的`[[AssociatedMediaStreamIds]]`为空集合。
9. 对于stream中的所有流，如果不存在则向`[[AssociatedMediaStreamIds]]`添加stream.id。
10. 让sender具有**[[SendEncodings]]**内部插槽，表示`RTCRtpEncodingParameters`字典列表。
11. 如果sendEncodings作为算法输入，并且非空，设置[[SendEncodings]]插槽为sendEncodings。否则，设置它为一个列表，包含单一`RTCRtpEncodingParameters`，并且`active`设置为`true`。
12. 让sender具有**[[SendCodecs]]**内部插槽，表示`RTCRtpCodecParameters`字典列表，并且初始化为空列表。
13. 让sender具有**[[LastReturnedParameters]]**内部插槽，它被用来匹配`getParameters`和`setParameters`操作。
14. 返回sender。

```java
[Exposed=Window] interface RTCRtpSender {
    readonly        attribute MediaStreamTrack? track;
    readonly        attribute RTCDtlsTransport?  transport;
    readonly        attribute RTCDtlsTransport? rtcpTransport;
    static RTCRtpCapabilities? getCapabilities (DOMString kind);
    Promise<void>             setParameters (RTCRtpSendParameters parameters);
    RTCRtpSendParameters          getParameters ();
    Promise<void>             replaceTrack (MediaStreamTrack? withTrack);
    void                            setStreams(MediaStream... streams);
    Promise<RTCStatsReport>   getStats();
};


```

**属性**

MediaStreamTrack类型的``track``，只读，可以为null：

`track`属性是与此`RTCRtpSender`对象关联的轨道。如果`track`结束，或者输出被禁用，即track被禁用和/或静音，则`RTCRtpSender`必须发送静音(音频)，黑帧(视频)，或零信息内容等效物。在视频的情况下，`RTCRtpSender`应该每秒发送一个黑帧。如果`track`为null，则`RTCRtpSender`不发送。获取时，属性必须返回[[SenderTrack]]插槽的值。

`RTCDtlsTransport`类型的`transport`，只读，可以为null：

`transport`属性是一个传输，在此之上来自`track`的媒体通过RTP数据包的形式被发送。在`RTCDtlsTransport`对象构造之前，`transport`属性将会为null。当使用了绑定，多个`RTCRtpSender`对象共享一个`transport`并且都会在相同的传输上发送RTP和RTCP。

获取时，属性必须返回[[SenderTransport]]插槽的值。

`RTCDtlsTransport`类型的`rtcpTransport`，只读，可以为null:

`rtcpTransport`属性是一个传输，在此之上RTCP被发送和接收。在`RTCDtlsTransport`对象构造之前，`rtcpTransport`属性将会是null。当多路RTCP复用时，`rtcpTransport`将会为null，并且RTP和RTCP流都会进入`transport`描述的传输。

获取时，属性必须返回[[SenderRtcpTransport]]插槽的值。

**方法**

`getCapabilities`, static

`getCapabilities()`方法返回用于发送指定媒体的系统功能的最优化视图。它不会保存任何资源，端口，或者其它状态，但旨在提供一种方法来发现浏览器的功能类型，包括可能支持的编解码器。用户代理必须支持`"audio"`和`"video"`的类型值。如果系统没有与此类型参数值对应的功能，`getCapabilities`返回`null`。

这些功能通常在设备上提供持久的跨源信息，从而增加了应用程序的指纹表面。在隐私敏感的上下文中，浏览器可能考虑缓解，例如仅报告功能的公共子集。

`setParameters`

`setParameters`方法更新`track`如何编码并传输到远程对等端。

当调用`setParameters`方法时，用户代理必须运行以下步骤：

1. 让parameters成为方法的第一个参数。
2. 让sender成为调用`setParameters`的`RTCRtpSender`对象。
3. 让transceiver成为与sender关联的`RTCRtpTransceiver`对象、
4. 如果transceiver的[[Stopped]]插槽为`true`，返回一个promise，reject为一个新创建的`InvalidStateError`。
5. 如果sender的[[LastReturnedParameters]]内部插槽为`null`，返回一个promise，reject为新创建的`InvalidStateError`。
6. 通过以下步骤验证parameter：
   1. 让encodings为`parameters.encodings`。
   2. 让codecs为`parameters.codecs`。
   3. 让N为存储在sender的内部插槽[[SendEncodings]]中的`RTCRtpEncodingParameters`数量。
   4. 如果符合以下条件任意之一，返回一个promise，reject为新创建的`InvalidModificationError`:
      1. `encodings.length`与N不同。
      2. encodings已经被重新排序。
      3. parameters中的任何参数被标记为只读参数(例如RID)，并且具有与相应sender的[[LastReturnedParameters]]内部插槽不同的值。注意这对transactionId同样有效。
   5. 验证encodings中的每个`scaleResolutionDownBy`值大于等于1.0。如果任意一个值不满足条件，返回一个promise，reject为新创建的`RangeError`。
   6. 验证encodings中的每个`maxFramerate`值大于等于0.0。如果其中一个值不满足条件，返回一个承诺，reject为新创建的`RangeError`。
7. 让p成为一个新的promise。
8. 同时，配置媒体栈来使用parameters传输sender的[[SenderTrack]]。
   1. 如果使用parameters成功配置了媒体栈，对任务进行排序，允许下列步骤：
      1. 让sender的内部[[LastReturnedParameters]]插槽为null。
      2. 让sender的内部[[SendEncodings]]插槽为`parameters.encodings`。
      3. 解析p为undefined。
   2. 如果配置媒体栈的时候出现了error，排序任务运行以下步骤：
      1. 如果由于硬件资源不可用引发error，reject p为新创建的`RTCError`,它的`errorDetail`被设置为"硬件编码器不可用"，并且中断这些步骤。
      2. 如果由于硬件编码器不支持parameters引发error，reject p为新创建的`RTCError`,它的`errorDetail`被设置为"硬件编码器错误"并且中断这些步骤。
      3. 其它错误，reject p为新创建的`OperationError`。
9. 返回p。

`setParameters`不会导致SDP重新协商，只能被用于更改媒体栈在由Offer/Answer协商的信封中发送或接收的内容。`RTCRtpSendParameters`字典中的属性旨在不启用此属性，因此像`cname`之类无法更改的属性是只读的。另外，像比特率，由`maxBitrate`之类的界限控制，此处用户代理需要确保没有超出`maxBitrate`指定的最大比特率，同时确保它满足其它例如SDP的地方指定的对比特率的限制。

`getParameters`

`getParameters()`方法返回`RTCRtpSender`对象当前参数，此参数表示`track`是如何编码并传输到远程`RTCRtpReceiver`。

当调用`getParameters`时，`RTCRtpSendParameters`字典构造如下：

- `transactionId`被设置为新的独特Id,被用来将此次`getParameters`调用与将来可能会出现的`setParameters`调用匹配。
- `encodings`被设置为[[SendEncodings]]内部插槽的值。
- `headerExtensions`序列根据已协商发送的标头扩展名进行填充。
- `codecs`被设置为[[SendCodecs]]内部插槽的值。
- `rtcp.cname`被设置为关联`RTCPeerConnection`的CNAME。`rtcp.reducedSize`被设置为`true`，如果reduced-size RTCP已经被协商发送，否则为`false`。
- `degradationPreference`被设置为传入`setParameters`的最后一个值，如果`setParameters`还未调用，则设置为默认值"balanced"。

返回的`RTCRtpSendParameters`字典必须存入`RTCRtpSender`对象的[[LastReturnedParameters]]内部插槽。

getParameters可能与setParameters并用，更改参数：

```java
async function updateParameters() {
  try {
    const params = sender.getParameters();
    // ... make changes to parameters
    params.encodings[0].active = false;
    await sender.setParameters(params);
  } catch (err) {
    console.error(err);
  }
}
```

在对`setParameters`的完全调用后，后续对`getParameters`调用将会返回修改后的参数集合。

`replaceTrack`

试图将`RTCRtpSender`当前的`track`替换为指定的track，而不需要重新协商。

当`replaceTrack`方法被调用时，用户代理必须运行以下步骤：

1. 让sender成为`RTCRtpSender`对象，并在此对象上调用`replaceTrack`。
2. 让transceiver成为与sender关联的`RTCRtpTransceiver`对象。
3. 让connection成为与sender关联的`RTCPeerConnection`对象。
4. 让withTrack成为方法参数。
5. 如果`withTrack`不为null，并且`withTrack.kind`与transceiver的transceiver类别不同，返回一个promise，reject为新创建的`TypeError`.
6. 返回将下列步骤加入connection的运行队列之后的结果：
   1. 如果transceiver的[[Stopped]]插槽为true，返回一个promise，reject为新创建的`InvalidStateError`。
   2. 让p成为新的promise。
   3. 让sending为`true`，如果transceiver的[[CurrentDirection]]是`"sendrecv"`或`"sendonly"`，否则为`false`。
   4. 并行运行以下步骤：
      1. 如果sending为`true`，并且withTrack为`null`，使sender停止发送。
      2. 如果sending为`true`，withTrack不为`null`，确定withTrack是否可以由发送方立即发送而不违反发送方协商好的信封，如果不能，则reject p为新创建的`InvalidModificationError`，并中断这些步骤。
      3. 如果sending为`true`，withTrack不为`null`，让发送方无缝切换到传输withTrack，而不是sender现存的track。
      4. 对任务进行排序，运行以下步骤：
         1. 如果connection的[[IsClosed]]插槽为`true`，中断下列步骤。
         2. 设置sender的`track`属性为withTrack。
         3. 用`undefined`解析p。
   5. 返回p。

> NOTE:改变尺寸和/或帧率可能不需要协商。可能需要协商的情形包括:
>
> 1. 将分辨率改为超出协商好的imageattr边界的值，如[RFC6236]中所述。
> 2. 将帧率改为导致编码器block rate超出的值。
> 3. 视频轨道与原始格式和预编码格式不同。
> 4. 音轨具有不同数量的通道数。
> 5. 同样编码的源(通常是硬件编码器)可能无法生成协商的编解码器；类似的，软件源可能不会实现为编码源协商的编解码器。

`setStreams`

设置`MediaStreams`与sender的track相关联。

当`setStreams`方法被调用后，用户代理必须运行以下步骤：

1. 让sender成为调用方法的`RTCRtpSender`对象。
2. 让connection成为调用方法的`RTCPeerConnection`对象。
3. 如果connection的[[IsClosed]]插槽为`true`，抛出`InvalidStateError`。
4. 让streams成为通过方法参数构建的MediaStream对象列表，如果方法没有传入参数被调用，则设置为空列表。
5. 设置sender的[[AssociatedMediaStreamIds]]为空集合。
6. 对于streams中的流，如果未存在则向[[AssocaitedMediaStreamIds]]中添加stream.id。
7. 更新连接的negotiation-needed 标记。

`getStats`

仅收集发送方的统计信息，并异步报告结果。

当调用`getStats()`后，用户代理必须运行以下步骤：

1. 让selector成为调用方法的`RTCRtpSender`对象。
2. 让p成为新的promise，并行运行以下步骤：
   1. 根据统计选择算法收集selector指定的统计信息。
   2. 使用`RTCStatsReport`对象解析p，包含收集到的统计信息。
3. 返回p。



