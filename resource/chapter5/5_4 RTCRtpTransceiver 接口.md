## [5.4 RTCRtpTransceiver 接口](http://w3c.github.io/webrtc-pc/#rtcrtptransceiver-interface)

`RTCRtpTransceiver`接口表示共享公共mid的`RTCRtpSender`和`RTCRtpReceiver`的组合。如[JSEP]（第3.4.1节）中所定义的，如果`RTCRtpTransceiver`的 `mid` 属性为非`null`，则称其与媒体描述相关联;否则据说是不相关的。从概念上讲，相关联的收发器是在最后应用的会话描述中表示的收发器。
`RTCRtpTransceiver`的收发器类型由关联的`RTCRtpReceiver`的`MediaStreamTrack`对象的类型定义。
要使用`RTCRtpReceiver`对象，接收方，`RTCRtpSender`对象，发送方和`RTCRtpTransceiverDirection`值，方向创建`RTCRtpTransceiver`，请运行以下步骤：
1.  让收发器成为新的`RTCRtpTransceiver`对象。
2.  让收发器有一个[[Sender]]内部插槽，初始化为发送方。
3.  让收发器有一个[[Receiver]]内部插槽，初始化为接收器。
4.  让收发器有一个[[Stopped]]内部插槽，初始化为`false`。
5.  让收发器有一个[[Direction]]内部插槽，初始化为方向。
6.  让收发器有一个[[Receptive]]内部插槽，初始化为`false`。
7.  让收发器具有[[CurrentDirection]]内部插槽，初始化为`null`。
8.  让收发器有一个[[FiredDirection]]内部插槽，初始化为`null`。
9.  让收发器具有[[PreferredCodecs]]内部插槽，初始化为空列表。
10. 返回收发器。

>NOTE
>
>创建收发器不会创建基于`RTCDtlsTransport`和`RTCIceTransport`的对象。这只会在设置`RTCSessionDescription`的过程中发生。


```
[Exposed=Window] interface RTCRtpTransceiver {
    readonly        attribute DOMString?                  mid;
    [SameObject]
    readonly        attribute RTCRtpSender                sender;
    [SameObject]
    readonly        attribute RTCRtpReceiver              receiver;
    readonly        attribute boolean                     stopped;
                    attribute RTCRtpTransceiverDirection  direction;
    readonly        attribute RTCRtpTransceiverDirection? currentDirection;
    void stop ();
    void setCodecPreferences (sequence<RTCRtpCodecCapability> codecs);
};

```

**属性**

*mid* DOMString类型，只读，可以为空
`mid`属性是中间协商的，并且存在于[JSEP]（第 5.2.1 节和第 5.3.1 节）中定义的本地和远程描述中。在协商完成之前，中间值可能为空。回滚后，该值可能会从非`null`值更改为`null`。

*sender* RTCRtpSender类型，只读
`sender`属性公开了可能以`mid = mid`发送的 RTP 媒体相对应的`RTCRtpSender`。获取时，属性必须返回[[Sender]]槽的值。

*receiver* RTCRtpReceiver类型，只读
接收器属性是对应于可以用`mid = mid`接收的RTP媒体的`RTCRtpReceiver`。获取属性时必须返回[[Receiver]]插槽的值。

*stopped* 类型boolean，只读
`stopped`属性表示此收发器的发送方将不再发送，接收方将不再接收。如果已调用`stop`或设置本地或远程描述导致`RTCRtpTransceiver`停止，则为`true`。获取时，此属性必须返回[[Stopped]]插槽的值。

*direction* RTCRtpTransceiverDirection类型
如[JSEP]（第 4.2.4 节）中所定义，`direction`属性指示此收发器的首选方向，该方向将用于调用`createOffer和createAnswer`。方向性更新不会立即生效。相反，将来调用`createOffer`和`createAnswer`会将相应的媒体描述标记为`sendSearchv`，`sendonly`，`recvonly`或`inactive`，如[JSEP]中所定义（第 5.2.2 节和第 5.3.2 节）。
获取时，此属性必须返回[[Direction]]插槽的值。
在设置时，用户代理必须执行以下步骤：
1.  让收发器成为调用设置者的`RTCRtpTransceiver`对象。
2.  让连接成为与收发器关联的`RTCPeerConnection`对象。
3.  如果连接的[[IsClosed]]槽为`true`，则抛出`InvalidStateError`。
4.  如果收发器的[[Stopped]]插槽为`true`，则抛出`InvalidStateError`。
5.  让`newDirection`成为设置者的参数。
6.  如果`newDirection`等于收发器的[[Direction]]插槽，则中止这些步骤。
7.  将收发器的[[Direction]]插槽设置为`newDirection`。
8.  更新连接所需的协商标志。

*currentDirection* 类型为RTCRtpTransceiverDirection，只读，可为空
如[JSEP]（第4.2.5节）中所定义，`currentDirection`属性指示为此收发器协商的当前方向。 `currentDirection`的值独立于`RTCRtpEncodingParameters.active`的值，因为无法从另一个推导出。如果此收发器从未在提供/应答交换中表示，或者收发器已停止，则该值为空。获取时，该属性必须返回[[CurrentDirection]]槽的值。

**方法**

`stop`
不可逆转地停止`RTCRtpTransceiver`。此收发器的发送器将不再发送，接收器将不再接收。调用`stop（）`会更新`RTCRtpTransceiver`关联的RTCPeerConnection的需要协商标志。
停止收发器将导致将来调用`createOffer`或`createAnswer`以在相应收发器的媒体描述中生成零端口，如[JSEP]（第 4.2.1 节）中所定义。

>NOTE
>
>如果在应用远程报价和创建答案之间调用此方法，并且收发器与[BUNDLE]中定义的“提供者标记”媒体描述相关联，则这将导致捆绑组中的所有其他收发器停止为好。为避免这种情况，当`signalingState`为“稳定”并执行后续的提议/应答交换时，可以只停止当前收发器。

当调用stop方法时，用户代理必须运行以下步骤：
1.  让收发器成为调用该方法的`RTCRtpTransceiver`对象。
2.  让连接成为与收发器关联的`RTCPeerConnection`对象。
3.  如果连接的[[IsClosed]]槽为`true`，则抛出`InvalidStateError`。
4.  如果收发器的[[已停止]]插槽为`true`，则中止这些步骤。
5.  停止收发器指定的`RTCRtpTransceiver`。
6.  更新连接所需的协商标志。

给定收发器的`RTCRtpTransceiver`停止算法如下：
1.  让发送者成为收发器的[[发件人]]。
2.  让接收器成为收发器的[[接收器]]。
3.  停止向发件人发送媒体。
4.  按照[RFC3550]中的规定，为发送方发送的每个 RTP 流发送 RTCP BYE。
5.  停止使用接收器接收媒体。
6.  执行接收方[[ReceiverTrack]]的结束步骤。
7.  将收发器的[[Stopped]]插槽设置为`true`。
8.  将收发器的[[Receptive]]插槽设置为`false`。
9.  将收发器的[[CurrentDirection]]插槽设置为空。

`setCodecPreferences`
`setCodecPreferences`方法会覆盖用户代理使用的默认编解码器首选项。当使用`createOffer`或`createAnswer`生成会话描述时，用户代理必须按照编解码参数中指定的顺序使用指示的编解码器，用于与此`RTCRtpTransceiver`对应的媒体部分。
此方法允许应用程序禁用特定编解码器的协商。它还允许应用程序使远程对等方优先选择列表中首先出现的编解码器。
对于包含此`RTCRtpTransceiver`的`createOffer`和`createAnswer`的所有调用，编解码器首选项仍然有效，直到再次调用此方法。将编解码器设置为空序列会将编解码器首选项重置为任何默认值。
传递给`setCodecPreferences`的编解码器序列只能包含由`RTCRtpSender.getCapabilities（kind）`或`RTCRtpReceiver.getCapabilities（kind）`返回的编解码器，其中`kind`是调用该方法的`RTCRtpTransceiver`的类型。此外，不能修改`RTCRtpCodecCapability`字典成员。如果编解码器不满足这些要求，则用户代理必须抛出`InvalidAccessError`。

>NOTE
>
>由于[SDP]中的建议，对`createAnswer`的调用应该只使用编解码器首选项的公共子集和商品中出现的编解码器。例如，如果编解码器首选项是“C，B，A”，但仅提供编解码器“A，B”，则答案应仅包含编解码器“B，A”。但是，[JSEP]（第 5.3.1 节）允许添加不在商品中的编解码器，因此实现的行为可能不同。

当调用`setCodecPreferences（）`时，用户代理必须运行以下步骤：
1.  让收发器成为调用此方法的`RTCRtpTransceiver`对象。
2.  让编解码器成为第一个参数。
3.  如果编解码器是空列表，请将收发器的[[PreferredCodecs]]插槽设置为编解码器并中止这些步骤。
4.  删除编解码器中的任何重复值。从列表的后面开始，以保持编解码器的优先级;列表中第一次出现编解码器的索引在此步骤之前和之后是相同的。
5.  让我们成为收发器的收发器类型。
6.  如果编解码器和`RTCRtpSender.getCapabilities（kind）.codecs`之间的交集或编解码器与`RTCRtpReceiver.getCapabilities（kind）.codecs`之间的交集是一个空集，则抛出`InvalidModificationError`。这确保了无论收发器方向如何，我们总能提供一些东西。
7.  让`codecCapabilities`成为`RTCRtpSender.getCapabilities（kind）.codecs`和`RTCRtpReceiver.getCapabilities（kind）.codecs`的联合。
8. 对于编解码器中的每个编解码器，
	1. 如果编解码器不在`codecCapabilities`中，则抛出`InvalidModificationError`。
9.  将收发器的[[PreferredCodecs]]插槽设置为编解码器。
