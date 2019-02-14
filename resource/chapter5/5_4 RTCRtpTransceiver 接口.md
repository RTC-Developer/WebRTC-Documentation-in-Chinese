## [5.4 RTCRtpTransceiver 接口](http://w3c.github.io/webrtc-pc/#rtcrtptransceiver-interface)

The RTCRtpTransceiver interface represents a combination of an RTCRtpSender and an RTCRtpReceiver that share a common mid. As defined in [JSEP] (section 3.4.1.), an RTCRtpTransceiver is said to be associated with a media description if its mid property is non-null; otherwise it is said to be disassociated. Conceptually, an associated transceiver is one that's represented in the last applied session description.

zh:RTCRtpTransceiver接口表示共享公共mid的RTCRtpSender和RTCRtpReceiver的组合。如[JSEP]（第3.4.1节）中所定义的，如果RTCRtpTransceiver的mid属性为非null，则称其与媒体描述相关联;否则据说是不相关的。从概念上讲，相关联的收发器是在最后应用的会话描述中表示的收发器。

The transceiver kind of an RTCRtpTransceiver is defined by the kind of the associated RTCRtpReceiver's MediaStreamTrack object.

zh:RTCRtpTransceiver的收发器类型由关联的RTCRtpReceiver的MediaStreamTrack对象的类型定义。

To create an RTCRtpTransceiver with an RTCRtpReceiver object, receiver, RTCRtpSender object, sender, and an RTCRtpTransceiverDirection value, direction, run the following steps:

zh:要使用RTCRtpReceiver对象，接收方，RTCRtpSender对象，发送方和RTCRtpTransceiverDirection值，方向创建RTCRtpTransceiver，请运行以下步骤：

1.  Let transceiver be a new RTCRtpTransceiver object. 
zh: 让收发器成为新的RTCRtpTransceiver对象。

2.  Let transceiver have a [[Sender]] internal slot, initialized to sender. 
zh: 让收发器有一个[[Sender]]内部插槽，初始化为发送方。

3.  Let transceiver have a [[Receiver]] internal slot, initialized to receiver. 
zh: 让收发器有一个[[Receiver]]内部插槽，初始化为接收器。

4.  Let transceiver have a [[Stopped]] internal slot, initialized to false. 
zh: 让收发器有一个[[Stopped]]内部插槽，初始化为false。

5.  Let transceiver have a [[Direction]] internal slot, initialized to direction. 
zh: 让收发器有一个[[Direction]]内部插槽，初始化为方向。

6.  Let transceiver have a [[Receptive]] internal slot, initialized to false. 
zh: 让收发器有一个[[Receptive]]内部插槽，初始化为false。

7.  Let transceiver have a [[CurrentDirection]] internal slot, initialized to null. 
zh: 让收发器具有[[CurrentDirection]]内部插槽，初始化为null。

8.  Let transceiver have a [[FiredDirection]] internal slot, initialized to null. 
zh: 让收发器有一个[[FiredDirection]]内部插槽，初始化为null。

9.  Let transceiver have a [[PreferredCodecs]] internal slot, initialized to an empty list. 
zh: 让收发器具有[[PreferredCodecs]]内部插槽，初始化为空列表。

10.  Return transceiver. 
zh: 返回收发器。

>NOTE
>
>Creating a transceiver does not create the underlying RTCDtlsTransport and RTCIceTransport objects. This will only occur as part of the process of setting an RTCSessionDescription.
>
>zh:创建收发器不会创建基于RTCDtlsTransport和RTCIceTransport的对象。这只会在设置RTCSessionDescription的过程中发生。


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

**Attributes**

*mid* of type DOMString, readonly, nullable:
zh:DOMString类型的中间，只读，可以为空

The mid attribute is the mid negotatiated and present in the local and remote descriptions as defined in [JSEP] (section 5.2.1. and section 5.3.1.). Before negotiation is complete, the mid value may be null. After rollbacks, the value may change from a non-null value to null.

zh:mid属性是中间协商的，并且存在于[JSEP]（第5.2.1节和第5.3.1节）中定义的本地和远程描述中。在协商完成之前，中间值可能为空。回滚后，该值可能会从非null值更改为null。

*sender* of type RTCRtpSender, readonly:
zh:RTCRtpSender类型的发件人，只读

The sender attribute exposes the RTCRtpSender corresponding to the RTP media that may be sent with mid = mid. On getting, the attribute MUST return the value of the [[Sender]] slot.

zh:sender属性公开与可能以mid = mid发送的RTP媒体相对应的RTCRtpSender。获取时，属性必须返回[[Sender]]槽的值。

*receiver* of type RTCRtpReceiver, readonly:
zh:RTCRtpReceiver类型的接收器，只读

The receiver attribute is the RTCRtpReceiver corresponding to the RTP media that may be received with mid = mid. On getting the attribute MUST return the value of the [[Receiver]] slot.

zh:接收器属性是对应于可以用mid = mid接收的RTP媒体的RTCRtpReceiver。获取属性时必须返回[[Receiver]]插槽的值。

*stopped* of type boolean, readonly:
zh:停止类型boolean，readonly

The stopped attribute indicates that the sender of this transceiver will no longer send, and that the receiver will no longer receive. It is true if either stop has been called or if setting the local or remote description has caused the RTCRtpTransceiver to be stopped. On getting, this attribute MUST return the value of the [[Stopped]] slot.

zh:stopped属性表示此收发器的发送方将不再发送，接收方将不再接收。如果已调用stop或设置本地或远程描述导致RTCRtpTransceiver停止，则为true。获取时，此属性必须返回[[Stopped]]插槽的值。

*direction* of type RTCRtpTransceiverDirection:
zh:RTCRtpTransceiverDirection类型的方向

As defined in [JSEP] (section 4.2.4.), the direction attribute indicates the preferred direction of this transceiver, which will be used in calls to createOffer and createAnswer. An update of directionality does not take effect immediately. Instead, future calls to createOffer and createAnswer mark the corresponding media description as sendrecv, sendonly, recvonly or inactive as defined in [JSEP] (section 5.2.2. and section 5.3.2.)

zh:如[JSEP]（第4.2.4节）中所定义，direction属性指示此收发器的首选方向，该方向将用于调用createOffer和createAnswer。方向性更新不会立即生效。相反，将来调用createOffer和createAnswer会将相应的媒体描述标记为sendSearchv，sendonly，recvonly或inactive，如[JSEP]中所定义（第5.2.2节和第5.3.2节）。

On getting, this attribute MUST return the value of the [[Direction]] slot.

zh:获取时，此属性必须返回[[Direction]]插槽的值。

On setting, the user agent MUST run the following steps:

zh:在设置时，用户代理必须执行以下步骤：

1.  Let transceiver be the RTCRtpTransceiver object on which the setter is invoked. 
zh: 让收发器成为调用setter的RTCRtpTransceiver对象。

2.  Let connection be the RTCPeerConnection object associated with transceiver. 
zh: 让连接成为与收发器关联的RTCPeerConnection对象。

3.  If connection's [[IsClosed]] slot is true, throw an InvalidStateError. 
zh: 如果connection的[[IsClosed]]槽为true，则抛出InvalidStateError。

4.  If transceiver's [[Stopped]] slot is true, throw an InvalidStateError. 
zh: 如果收发器的[[Stopped]]插槽为true，则抛出InvalidStateError。

5.  Let newDirection be the argument to the setter. 
zh: 让newDirection成为setter的参数。

6.  If newDirection is equal to transceiver's [[Direction]] slot, abort these steps. 
zh: 如果newDirection等于收发器的[[Direction]]插槽，则中止这些步骤。

7.  Set transceiver's [[Direction]] slot to newDirection. 
zh: 将收发器的[[Direction]]插槽设置为newDirection。

8.  Update the negotiation-needed flag for connection. 
zh: 更新连接所需的协商标志。


*currentDirection* of type RTCRtpTransceiverDirection, readonly, nullable:
zh:currentDirection类型RTCRtpTransceiverDirection，readonly，nullable

As defined in [JSEP] (section 4.2.5.), the currentDirection attribute indicates the current direction negotiated for this transceiver. The value of currentDirection is independent of the value of RTCRtpEncodingParameters.active since one cannot be deduced from the other. If this transceiver has never been represented in an offer/answer exchange, or if the transceiver is stopped, the value is null. On getting, this attribute MUST return the value of the [[CurrentDirection]] slot.

zh:如[JSEP]（第4.2.5节）中所定义，currentDirection属性指示为此收发器协商的当前方向。 currentDirection的值独立于RTCRtpEncodingParameters.active的值，因为无法从另一个推导出。如果此收发器从未在提供/应答交换中表示，或者收发器已停止，则该值为空。获取时，该属性必须返回[[CurrentDirection]]槽的值。

**Methods**

`stop`
zh:停

Irreversibly stops the RTCRtpTransceiver. The sender of this transceiver will no longer send, the receiver will no longer receive. Calling stop() updates the negotiation-needed flag for the RTCRtpTransceiver's associated RTCPeerConnection.

zh:不可逆转地停止RTCRtpTransceiver。此收发器的发送器将不再发送，接收器将不再接收。调用stop（）会更新RTCRtpTransceiver关联的RTCPeerConnection的需要协商标志。

Stopping a transceiver will cause future calls to createOffer or createAnswer to generate a zero port in the media description for the corresponding transceiver, as defined in  [JSEP] (section 4.2.1.).

zh:停止收发器将导致将来调用createOffer或createAnswer以在相应收发器的媒体描述中生成零端口，如[JSEP]（第4.2.1节）中所定义。

>NOTE
>
>If this method is called in between applying a remote offer and creating an answer, and the transceiver is associated with the "offerer tagged" media description as defined in [BUNDLE], this will cause all other transceivers in the bundle group to be stopped as well. To avoid this, one could instead stop the transceiver when signalingState is "stable" and perform a subsequent offer/answer exchange. 
>
>zh:如果在应用远程报价和创建答案之间调用此方法，并且收发器与[BUNDLE]中定义的“提供者标记”媒体描述相关联，则这将导致捆绑组中的所有其他收发器停止为好。为避免这种情况，当signalingState为“稳定”并执行后续的提议/应答交换时，可以改为停止收发器。

When the stop method is invoked, the user agent MUST run the following steps:

zh:当调用stop方法时，用户代理必须运行以下步骤：

1.  Let transceiver be the RTCRtpTransceiver object on which the method is invoked. 
zh: 让收发器成为调用该方法的RTCRtpTransceiver对象。

2.  Let connection be the RTCPeerConnection object associated with transceiver. 
zh: 让连接成为与收发器关联的RTCPeerConnection对象。

3.  If connection's [[IsClosed]] slot is true, throw an InvalidStateError. 
zh: 如果connection的[[IsClosed]]槽为true，则抛出InvalidStateError。

4.  If transceiver's [[Stopped]] slot is true, abort these steps. 
zh: 如果收发器的[[已停止]]插槽为真，则中止这些步骤。

5.   Stop the RTCRtpTransceiver specified by transceiver. 
zh:  停止收发器指定的RTCRtpTransceiver。

6.  Update the negotiation-needed flag for connection. 
zh: 更新连接所需的协商标志。

The stop the RTCRtpTransceiver algorithm given a transceiver is as follows:

zh:给定收发器的RTCRtpTransceiver算法停止如下：

1.  Let sender be transceiver's [[Sender]]. 
zh: 让发送者成为收发器的[[发件人]]。

2.  Let receiver be transceiver's [[Receiver]]. 
zh: 让接收器成为收发器的[[接收器]]。

3.  Stop sending media with sender. 
zh: 停止向发件人发送媒体。

4.  Send an RTCP BYE for each RTP stream that was being sent by sender, as specified in [RFC3550]. 
zh: 按照[RFC3550]中的规定，为发送方发送的每个RTP流发送RTCP BYE。

5.  Stop receiving media with receiver. 
zh: 停止使用接收器接收媒体。

6.  Execute the steps for receiver's [[ReceiverTrack]] to be ended. 
zh: 执行接收方[[ReceiverTrack]]的步骤结束。

7.  Set transceiver's [[Stopped]] slot to true. 
zh: 将收发器的[[Stopped]]插槽设置为true。

8.  Set transceiver's [[Receptive]] slot to false. 
zh: 将收发器的[[Receptive]]插槽设置为false。

9.  Set transceiver's [[CurrentDirection]] slot to null. 
zh: 将收发器的[[CurrentDirection]]插槽设置为空。

`setCodecPreferences`
zh:setCodecPreferences

The setCodecPreferences method overrides the default codec preferences used by the user agent. When generating a session description using either createOffer or createAnswer, the user agent MUST use the indicated codecs, in the order specified in the codecs argument, for the media section corresponding to this RTCRtpTransceiver. 

zh:setCodecPreferences方法会覆盖用户代理使用的默认编解码器首选项。当使用createOffer或createAnswer生成会话描述时，用户代理必须按照codecs参数中指定的顺序使用指示的编解码器，用于与此RTCRtpTransceiver对应的媒体部分。

This method allows applications to disable the negotiation of specific codecs. It also allows an application to cause a remote peer to prefer the codec that appears first in the list for sending.

zh:此方法允许应用程序禁用特定编解码器的协商。它还允许应用程序使远程对等方更喜欢列表中首先出现的编解码器。

Codec preferences remain in effect for all calls to createOffer and createAnswer that include this RTCRtpTransceiver until this method is called again. Setting codecs to an empty sequence resets codec preferences to any default value.

zh:对于包含此RTCRtpTransceiver的createOffer和createAnswer的所有调用，编解码器首选项仍然有效，直到再次调用此方法。将编解码器设置为空序列会将编解码器首选项重置为任何默认值。

The codecs sequence passed into setCodecPreferences can only contain codecs that are returned by RTCRtpSender.getCapabilities(kind) or RTCRtpReceiver.getCapabilities(kind), where kind is the kind of the RTCRtpTransceiver on which the method is called. Additionally, the RTCRtpCodecCapability dictionary members cannot be modified. If codecs does not fulfill these requirements, the user agent MUST throw an InvalidAccessError.

zh:传递给setCodecPreferences的编解码器序列只能包含由RTCRtpSender.getCapabilities（kind）或RTCRtpReceiver.getCapabilities（kind）返回的编解码器，其中kind是调用该方法的RTCRtpTransceiver的类型。此外，无法修改RTCRtpCodecCapability字典成员。如果编解码器不满足这些要求，则用户代理必须抛出InvalidAccessError。

>NOTE
>
>Due to a recommendation in [SDP], calls to createAnswer SHOULD use only the common subset of the codec preferences and the codecs that appear in the offer. For example, if codec preferences are "C, B, A", but only codecs "A, B" were offered, the answer should only contain codecs "B, A". However, [JSEP] (section 5.3.1.) allows adding codecs that were not in the offer, so implementations can behave differently.
>
>zh: 由于[SDP]中的建议，对createAnswer的调用应该只使用编解码器首选项的公共子集和商品中出现的编解码器。例如，如果编解码器首选项是“C，B，A”，但仅提供编解码器“A，B”，则答案应仅包含编解码器“B，A”。但是，[JSEP]（第5.3.1节）允许添加不在商品中的编解码器，因此实现的行为可能不同。

When setCodecPreferences() in invoked, the user agent MUST run the following steps:

zh:当调用setCodecPreferences（）时，用户代理必须运行以下步骤：

1.  Let transceiver be the RTCRtpTransceiver object this method was invoked on. 
zh: 让收发器成为调用此方法的RTCRtpTransceiver对象。

2.  Let codecs be the first argument. 
zh: 让编解码器成为第一个参数。

3.  If codecs is an empty list, set transceiver's [[PreferredCodecs]] slot to codecs and abort these steps. 
zh: 如果编解码器是空列表，请将收发器的[[PreferredCodecs]]插槽设置为编解码器并中止这些步骤。

4.  Remove any duplicate values in codecs. Start at the back of the list such that the priority of the codecs is maintained; the index of the first occurrence of a codec within the list is the same before and after this step. 
zh: 删除编解码器中的任何重复值。从列表的后面开始，以保持编解码器的优先级;列表中第一次出现编解码器的索引在此步骤之前和之后是相同的。

5.  Let kind be the transceiver's transceiver kind. 
zh: 让我们成为收发器的收发器类型。

6.  If the intersection between codecs and RTCRtpSender.getCapabilities(kind).codecs or the intersection between codecs and RTCRtpReceiver.getCapabilities(kind).codecs is an empty set, throw InvalidModificationError. This ensures that we always have something to offer, regardless of transceiverdirection. 
zh: 如果编解码器和RTCRtpSender.getCapabilities（kind）.codecs之间的交集或编解码器与RTCRtpReceiver.getCapabilities（kind）.codecs之间的交集是一个空集，则抛出InvalidModificationError。这确保了无论收发器方向如何，我们总能提供一些东西。

7.  Let codecCapabilities be the union of RTCRtpSender.getCapabilities(kind).codecs and RTCRtpReceiver.getCapabilities(kind).codecs. 
zh: 让codecCapabilities成为RTCRtpSender.getCapabilities（kind）.codecs和RTCRtpReceiver.getCapabilities（kind）.codecs的联合。

8.  For each codec in codecs,
zh:对于编解码器中的每个编解码器，

	1. If codec is not in codecCapabilities, throw InvalidModificationError.
	zh:如果编解码器不在codecCapabilities中，则抛出InvalidModificationError。

9.  Set transceiver's [[PreferredCodecs]] slot to codecs. 
zh: 将收发器的[[PreferredCodecs]]插槽设置为编解码器。
