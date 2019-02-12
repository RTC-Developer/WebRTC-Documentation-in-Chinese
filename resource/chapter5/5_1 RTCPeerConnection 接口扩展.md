## [5.1 RTCPeerConnection Interface Extensions](http://w3c.github.io/webrtc-pc/#rtcpeerconnection-interface-extensions)

The RTP media API extends the RTCPeerConnection interface as described below.

zh:RTP媒体API扩展了RTCPeerConnection接口，如下所述。

```
partial interface RTCPeerConnection {
    sequence<RTCRtpSender>      getSenders ();
    sequence<RTCRtpReceiver>    getReceivers ();
    sequence<RTCRtpTransceiver> getTransceivers ();
    RTCRtpSender                addTrack (MediaStreamTrack track, MediaStream... streams);
    void                        removeTrack (RTCRtpSender sender);
    RTCRtpTransceiver           addTransceiver ((MediaStreamTrack or DOMString) trackOrKind, optional RTCRtpTransceiverInit init);
                    attribute EventHandler ontrack;
};
```

**Attributes**

*ontrack* of type EventHandler:
zh:eventHandler类型的ontrack

The event type of this event handler is track.

zh:此事件处理程序的事件类型是track。

**Methods**

`getSenders`
zh:getSenders

Returns a sequence of RTCRtpSender objects representing the RTP senders that belong to non-stopped RTCRtpTransceiver objects currently attached to this RTCPeerConnection object.

zh:返回一系列RTCRtpSender对象，这些对象表示属于当前附加到此RTCPeerConnection对象的未停止的RTCRtpTransceiver对象的RTP发件人。

When the getSenders method is invoked, the user agent MUST return the result of executing the CollectSenders algorithm.

zh:当调用getSenders方法时，用户代理必须返回执行CollectSenders算法的结果。

We define the CollectSenders algorithm as follows:

zh:我们定义CollectSenders算法如下：

1. Let transceivers be the result of executing the CollectTransceivers algorithm.
zh:让收发器成为执行CollectTransceivers算法的结果。
2. Let senders be a new empty sequence.
zh:让发件人成为一个新的空序列。
3. For each transceiver in transceivers,   
zh:对于收发器中的每个收发器，
	1. If transceiver.[[Stopped]] is false add transceiver.[[Sender]] to senders.
	zh:如果收发器。[[已停止]]为假，则将收发器。[[发件人]]添加到发件人。
4. Return senders.
zh:返回发件人。

`getReceivers`
zh:getReceivers

Returns a sequence of RTCRtpReceiver objects representing the RTP receivers that belong to non-stopped RTCRtpTransceiver objects currently attached to this RTCPeerConnection object.

zh:返回一个RTCRtpReceiver对象序列，表示属于当前连接到此RTCPeerConnection对象的非停止RTCRtpTransceiver对象的RTP接收器。

When the getReceivers method is invoked, the user agent MUST run the following steps:

zh:当调用getReceivers方法时，用户代理必须运行以下步骤：

1. Let transceivers be the result of executing the CollectTransceivers algorithm.
zh:让收发器成为执行CollectTransceivers算法的结果。
2. Let receivers be a new empty sequence.
zh:让接收器成为新的空序列。
3. For each transceiver in transceivers,  
zh:对于收发器中的每个收发器，
	1. If transceiver.[[Stopped]] is false add transceiver.[[Receiver]] to receivers.
	zh:如果收发器。[[Stopped]]为false，则将收发器[[Receiver]]添加到接收器。
4. Return receivers.
zh:返回接收器。

`getTransceivers`
zh:getTransceivers

Returns a sequence of RTCRtpTransceiver objects representing the RTP transceivers that are currently attached to this RTCPeerConnection object.

zh:返回表示当前连接到此RTCPeerConnection对象的RTP收发器的RTCRtpTransceiver对象序列。

The getTransceivers method MUST return the result of executing the CollectTransceivers algorithm.

zh:getTransceivers方法必须返回执行CollectTransceivers算法的结果。


We define the CollectTransceivers algorithm as follows:

zh:我们定义CollectTransceivers算法如下：

1. Let transceivers be a new sequence consisting of all RTCRtpTransceiver objects in this RTCPeerConnection object's set of transceivers, in insertion order. 
zh:让收发器成为一个新的序列，由该RTCPeerConnection对象的收发器集中的所有RTCRtpTransceiver对象组成，按插入顺序排列。
2. Return transceivers.
zh:返回收发器。

`addTrack`
zh:addTrack

Adds a new track to the RTCPeerConnection, and indicates that it is contained in the specified MediaStreams.

zh:向RTCPeerConnection添加新轨道，并指示它包含在指定的MediaStream中。

When the addTrack method is invoked, the user agent MUST run the following steps:

zh:当调用addTrack方法时，用户代理必须运行以下步骤：

1.  Let connection be the RTCPeerConnection object on which this method was invoked. 
zh: 让connection成为调用此方法的RTCPeerConnection对象。

2.  Let track be the MediaStreamTrack object indicated by the method's first argument. 
zh: 让track成为方法第一个参数指示的MediaStreamTrack对象。

3.  Let kind be track.kind. 
zh: 让我们成为track.kind。

4.  Let streams be a list of MediaStream objects constructed from the method's remaining arguments, or an empty list if the method was called with a single argument. 
zh: 让stream成为从方法的剩余参数构造的MediaStream对象列表，如果使用单个参数调用该方法，则为空列表。

5.  If connection's [[IsClosed]] slot is true, throw an InvalidStateError. 
zh: 如果connection的[[IsClosed]]槽为true，则抛出InvalidStateError。

6.  Let senders be the result of executing the CollectSenders algorithm. If an RTCRtpSender for track already exists in senders, throw an InvalidAccessError. 
zh: 让发件人成为执行CollectSenders算法的结果。如果发件人中已存在用于轨道的RTCRtpSender，则抛出InvalidAccessError。

7. The steps below describe how to determine if an existing sender can be reused. Doing so will cause future calls to createOffer and createAnswer to mark the corresponding media description as sendrecv or sendonly and add the MSID of the sender's streams, as defined in [JSEP] (section 5.2.2. and section 5.3.2.).
zh:以下步骤描述了如何确定是否可以重用现有发件人。这样做将导致将来调用createOffer和createAnswer将相应的媒体描述标记为sendrecv或sendonly，并添加发送者流的MSID，如[JSEP]（第5.2.2节和第5.3.2节）中所定义。

	If any RTCRtpSender object in senders matches all the following criteria, let sender be that object, or null otherwise:
zh:如果发件人中的任何RTCRtpSender对象符合以下所有条件，则让sender为该对象，否则为null：

	*  The sender's track is null. 
zh: 发件人的跟踪为空。

	*  The transceiver kind of the RTCRtpTransceiver, associated with the sender, matches kind. 
zh: 与发送方相关联的RTCRtpTransceiver的收发器类型匹配类型。

	*  The transceiver is not stopped. More precisely, the [[Stopped]] slot of the RTCRtpTransceiver associated with the sender is false. 
zh: 收发器没有停止。更确切地说，与发送者关联的RTCRtpTransceiver的[[Stopped]]插槽为false。

	*  The sender has never been used to send. More precisely, the [[CurrentDirection]] slot of the RTCRtpTransceiver associated with the sender has never had a value of sendrecv or sendonly. 
zh: 发件人从未被用来发送。更确切地说，与发送者关联的RTCRtpTransceiver的[[CurrentDirection]]槽从未具有sendrecv或sendonly的值。

8. If sender is not null, run the following steps to use that sender:
zh:如果sender不为null，请运行以下步骤以使用该发件人：

	1.  Set sender's [[SenderTrack]] to track. 
zh: 设置发件人的[[SenderTrack]]进行跟踪。

	2.  Set sender's [[AssociatedMediaStreamIds]] to an empty set.  
zh: 将发件人的[[AssociatedMediaStreamIds]]设置为空集。

	3.  For each stream in streams, add stream.id to [[AssociatedMediaStreamIds]] if it's not already there.  
zh: 对于流中的每个流，将stream.id添加到[[AssociatedMediaStreamIds]]（如果它尚未存在）。

	4.  Let transceiver be the RTCRtpTransceiver associated with sender. 
zh: 让收发器成为与发送者关联的RTCRtpTransceiver。

	5.  If transceiver's [[Direction]] slot is recvonly, set transceiver's [[Direction]] slot to sendrecv. 
zh: 如果收发器的[[Direction]]插槽是recvonly，请将收发器的[[Direction]]插槽设置为sendrecv。

	6.  If transceiver's [[Direction]] slot is inactive, set transceiver's [[Direction]] slot to sendonly. 
zh: 如果收发器的[[Direction]]插槽无效，请将收发器的[[Direction]]插槽设置为sendonly。

9. If sender is null, run the following steps:
zh:如果sender为null，请运行以下步骤：

	1.  Create an RTCRtpSender with track, kind and streams, and let sender be the result. 
zh: 创建一个包含轨道，种类和流的RTCRtpSender，并让发送者成为结果。

	2.  Create an RTCRtpReceiver with kind, and let receiver be the result. 
zh: 用kind创建一个RTCRtpReceiver，让接收器成为结果。

	3.  Create an RTCRtpTransceiver with sender, receiver and an RTCRtpTransceiverDirection value of sendrecv, and let transceiver be the result. 
zh: 创建一个RTCRtpTransceiver，其发送方，接收方和sendCR的RTCRtpTransceiverDirection值，并让收发器成为结果。

	4.  Add transceiver to connection's set of transceivers 
zh: 将收发器添加到连接的收发器集

10.  A track could have contents that are inaccessible to the application. This can be due to being marked with a peerIdentity option or anything that would make a track  CORS cross-origin. These tracks can be supplied to the addTrack method, and have an RTCRtpSender created for them, but content MUST NOT be transmitted, unless they are also marked with peerIdentity and they meet the requirements for sending (see isolated stream).  All other tracks that are not accessible to the application MUST NOT be sent to the peer, with silence (audio), black frames (video) or equivalently absent content being sent in place of track content. Note that this property can change over time. 
zh: 轨道可能包含应用程序无法访问的内容。这可能是由于标记了peerIdentity选项或任何会使跟踪CORS交叉起源的选项。这些轨道可以提供给addTrack方法，并为它们创建一个RTCRtpSender，但内容绝不能传输，除非它们也标记为peerIdentity并且它们符合发送要求（参见隔离流）。应用程序无法访问的所有其他轨道不得发送给对等体，静音（音频），黑帧（视频）或等效的内容不会被发送以代替轨道内容。请注意，此属性可能会随时间而变化。

	All other tracks that are not accessible to the application MUST NOT be sent to the peer, with silence (audio), black frames (video) or equivalently absent content being sent in place of track content.
	zh:应用程序无法访问的所有其他轨道不得发送给对等体，静音（音频），黑帧（视频）或等效的内容不会被发送以代替轨道内容。

	Note that this property can change over time.
	zh:请注意，此属性可能会随时间而变化。

11.  Update the negotiation-needed flag for connection. 
zh: 更新连接所需的协商标志。

12.  Return sender. 
zh: 退货发送。

Return sender.

zh:退货发送。

`removeTrack`
zh:removeTrack

Stops sending media from sender. The RTCRtpSender will still appear in getSenders. Doing so will cause future calls to createOffer to mark the media description for the corresponding transceiver as recvonly or inactive, as defined in  [JSEP] (section 5.2.2.). 

zh:停止从发件人发送媒体。 RTCRtpSender仍将出现在getSenders中。这样做将导致将来调用createOffer将相应收发器的介质描述标记为recvonly或inactive，如[JSEP]（第5.2.2节）中所定义。

When the other peer stops sending a track in this manner, the track is removed from any remote MediaStreams that were initially revealed in the track event, and if the MediaStreamTrack is not already muted, a muted event is fired at the track.

zh:当另一个对等体停止以这种方式发送轨道时，轨道将从最初在轨道事件中显示的任何远程MediaStream中移除，并且如果MediaStreamTrack尚未静音，则在轨道处触发静音事件。

When the removeTrack method is invoked, the user agent MUST run the following steps:

zh:当调用removeTrack方法时，用户代理必须运行以下步骤：

1.  Let sender be the argument to removeTrack. 
zh: 让sender成为removeTrack的参数。

2.  Let connection be the RTCPeerConnection object on which the method was invoked. 
zh: 让connection成为调用方法的RTCPeerConnection对象。

3.  If connection's [[IsClosed]] slot is true, throw an InvalidStateError. 
zh: 如果connection的[[IsClosed]]槽为true，则抛出InvalidStateError。

4.  If sender was not created by connection, throw an InvalidAccessError. 
zh: 如果发件人不是通过连接创建的，则抛出InvalidAccessError。

5.  Let senders be the result of executing the CollectSenders algorithm. 
zh: 让发件人成为执行CollectSenders算法的结果。

6.  If sender is not in senders (which indicates that it was removed due to setting an RTCSessionDescription of type "rollback"), then abort these steps. 
zh: 如果发件人不在发件人中（表示由于设置了“回滚”类型的RTCSessionDescription而将其删除），则中止这些步骤。

7.  If sender's [[SenderTrack]] is null, abort these steps. 
zh: 如果发件人的[[SenderTrack]]为空，则中止这些步骤。

8.  Set sender's [[SenderTrack]] to null. 
zh: 将发件人的[[SenderTrack]]设置为null。

9.  Let transceiver be the RTCRtpTransceiver object corresponding to sender. 
zh: 让收发器成为与发送者对应的RTCRtpTransceiver对象。

10.  If transceiver's [[Direction]] slot is sendrecv, set transceiver's [[Direction]] slot to recvonly. 
zh: 如果收发器的[[Direction]]插槽是sendrecv，请将收发器的[[Direction]]插槽设置为recvonly。

11.  If transceiver's [[Direction]] slot is sendonly, set transceiver's [[Direction]] slot to inactive. 
zh: 如果收发器的[[Direction]]插槽是sendonly，则将收发器的[[Direction]]插槽设置为无效。

12.  Update the negotiation-needed flag for connection. 
zh: 更新连接所需的协商标志。


`addTransceiver`
zh:addTransceiver

Create a new RTCRtpTransceiver and add it to the set of transceivers.

zh:创建一个新的RTCRtpTransceiver并将其添加到收发器集。

Adding a transceiver will cause future calls to createOffer to add a media description for the corresponding transceiver, as defined in [JSEP] (section 5.2.2.).

zh:添加收发器将导致将来调用createOffer为相应的收发器添加媒体描述，如[JSEP]（第5.2.2节）中所定义。

The initial value of mid is null. Setting a new RTCSessionDescription may change it to a non-null value, as defined in [JSEP] (section 5.5. and section 5.6.).

zh:mid的初始值为null。设置新的RTCSessionDescription可能会将其更改为非空值，如[JSEP]（第5.5节和第5.6节）中所定义。

The sendEncodings argument can be used to specify the number of offered simulcast encodings, and optionally their RIDs and encoding parameters.

zh:sendEncodings参数可用于指定提供的联播编码的数量，以及可选的RID和编码参数。

When this method is invoked, the user agent MUST run the following steps:

zh:调用此方法时，用户代理必须执行以下步骤：

1.  Let init be the second argument. 
zh: 让init成为第二个参数。

2.  Let streams be init's streams member. 
zh: 让stream成为init的stream成员。

3.  Let sendEncodings be init's sendEncodings member. 
zh: 让sendEncodings成为init的sendEncodings成员。

4.  Let direction be init's direction member. 
zh: 让方向成为init的方向成员。

5. If the first argument is a string, let it be kind and run the following steps:
zh:如果第一个参数是一个字符串，那就让它好，然后运行以下步骤：

	1.  If kind is not a legal MediaStreamTrack kind, throw a TypeError. 
zh: 如果kind不是合法的MediaStreamTrack类型，则抛出TypeError。

	2.  Let track be null. 
	zh: 让跟踪为空。

6.  If the first argument is a MediaStreamTrack, let it be track and let kind be track.kind. 
zh: 如果第一个参数是MediaStreamTrack，那么让它跟踪并让kind为track.kind。

7.  If connection's [[IsClosed]] slot is true, throw an InvalidStateError. 
zh: 如果connection的[[IsClosed]]槽为true，则抛出InvalidStateError。

8. Validate sendEncodings by running the following steps: 
zh:通过运行以下步骤验证sendEncodings：
	
	1.  Verify that each rid value in sendEncodings is composed only of alphanumeric characters (a-z, A-Z, 0-9) up to a maximum of 16 characters. If one of the RIDs does not meet these requirements, throw a TypeError. 
zh: 验证sendEncodings中的每个rid值仅由字母数字字符（a-z，A-Z，0-9）组成，最多16个字符。如果其中一个RID不满足这些要求，则抛出TypeError。

	2.  If any RTCRtpEncodingParameters dictionary in sendEncodings contains a read-only parameter other than rid, throw an InvalidAccessError. 
zh: 如果sendEncodings中的任何RTCRtpEncodingParameters字典包含除rid之外的只读参数，则抛出InvalidAccessError。

	3.  Verify that each scaleResolutionDownBy value in sendEncodings is greater than or equal to 1.0. If one of the scaleResolutionDownBy values does not meet this requirement, throw a RangeError. 
zh: 验证sendEncodings中的每个scaleResolutionDownBy值是否大于或等于1.0。如果scaleResolutionDownBy值之一不满足此要求，则抛出RangeError。

	4.  Verify that each maxFramerate value in sendEncodings is greater than or equal to 0.0. If one of the maxFramerate values does not meet this requirement, throw a RangeError. 
zh: 验证sendEncodings中的每个maxFramerate值是否大于或等于0.0。如果其中一个maxFramerate值不满足此要求，则抛出RangeError。

	5.  Let maxN be the maximum number of total simultaneous encodings the user agent may support for this kind, at minimum 1.This should be an optimistic number since the codec to be used is not known yet. 
zh: 令maxN为用户代理可以支持的最大同时编码的最大数量，至少为1.这应该是一个乐观的数字，因为要使用的编解码器还不知道。

	6.  If the number of RTCRtpEncodingParameters stored in sendEncodings exceeds maxN, then trim sendEncodings from the tail until its length is maxN. 
zh: 如果存储在sendEncodings中的RTCRtpEncodingParameters的数量超过maxN，则从尾部修剪sendEncodings直到其长度为maxN。

	7.  If the number of RTCRtpEncodingParameters now stored in sendEncodings is 1, then remove any rid member from the lone entry. 
zh: 如果现在存储在sendEncodings中的RTCRtpEncodingParameters的数量为1，则从单个条目中删除任何rid成员。

	Note
	Providing a single, default RTCRtpEncodingParameters in sendEncodings allows the application to subsequently set encoding parameters using setParameters, even when simulcast isn't used. 
	zh:注意在sendEncodings中提供单个默认RTCRtpEncodingParameters允许应用程序随后使用setParameters设置编码参数，即使未使用联播也是如此。

9. Create an RTCRtpSender with track, kind, streams and sendEncodings and let sender be the result.
zh:创建一个包含track，kind，streams和sendEncodings的RTCRtpSender，让发送者成为结果。

	If sendEncodings is set, then subsequent calls to createOffer will be configured to send multiple RTP encodings as defined in [JSEP] (section 5.2.2. and section 5.2.1.). When setRemoteDescription is called with a corresponding remote description that is able to receive multiple RTP encodings as defined in [JSEP] (section 3.7.), the RTCRtpSender may send multiple RTP encodings and the parameters retrieved via the transceiver's sender.getParameters() will reflect the encodings negotiated.

	zh:如果设置了sendEncodings，则后续对createOffer的调用将被配置为发送[JSEP]中定义的多个RTP编码（第5.2.2节和第5.2.1节）。当使用能够接收[JSEP]（第3.7节）中定义的多个RTP编码的相应远程描述调用setRemoteDescription时，RTCRtpSender可以发送多个RTP编码，并且通过收发器的sender.getParameters（）检索的参数将反映出来谈判的编码。

10.  Create an RTCRtpReceiver with kind and let receiver be the result. 
zh: 创建一个带有kind的RTCRtpReceiver，让接收器成为结果。

11.  Create an RTCRtpTransceiver with sender, receiver and direction, and let transceiver be the result. 
zh: 创建一个带发送器，接收器和方向的RTCRtpTransceiver，然后让收发器成为结果。

12.  Add transceiver to connection's set of transceivers 
zh: 将收发器添加到连接的收发器集

13.  Update the negotiation-needed flag for connection. 
zh: 更新连接所需的协商标志。

14.  Return transceiver. 
zh: 返回收发器。


```
dictionary RTCRtpTransceiverInit {
             RTCRtpTransceiverDirection         direction = "sendrecv";
             sequence<MediaStream>              streams = [];
             sequence<RTCRtpEncodingParameters> sendEncodings = [];
};
```

**Dictionary `RTCRtpTransceiverInit` Members**

*direction* of type RTCRtpTransceiverDirection, defaulting to "sendrecv":
zh:RTCRtpTransceiverDirection类型的方向，默认为“sendrecv”

The direction of the RTCRtpTransceiver.
zh:RTCRtpTransceiver的方向。

*streams* of type sequence<MediaStream>:
zh:类型序列<MediaStream>的流

When the remote PeerConnection's track event fires corresponding to the RTCRtpReceiver being added, these are the streams that will be put in the event. 
zh: 当远程PeerConnection的跟踪事件触发与正在添加的RTCRtpReceiver相对应时，这些是将放入事件中的流。


*sendEncodings* of type sequence<RTCRtpEncodingParameters>:
zh:sendEncodings类型为序列<RTCRtpEncodingParameters>

A sequence containing parameters for sending RTP encodings of media.

zh:包含用于发送媒体的RTP编码的参数的序列。

```
enum RTCRtpTransceiverDirection {
    "sendrecv",
    "sendonly",
    "recvonly",
    "inactive"
};
```
<table>
	<tr>
		<td colspan="2">
		RTCRtpTransceiverDirection Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		sendrecv
		</td>
		<td>
		The RTCRtpTransceiver's RTCRtpSender sender will offer to send RTP, and will send RTP if the remote peer accepts and sender.getParameters().encodings[i].active is true for any value of i. The RTCRtpTransceiver's RTCRtpReceiver will offer to receive RTP, and will receive RTP if the remote peer accepts.
		zh：RTCRtpTransceiver的RTCRtpSender发送方将提供发送RTP，并且如果远程对等方接受并且sender.getParameters（）。encodings [i] .active对于任何i的值为true，则将发送RTP。 RTCRtpTransceiver的RTCRtpReceiver将提供接收RTP，并在远程对等方接受时接收RTP。
		</td>
	</tr>
	<tr>
		<td>
		sendonly
		</td>
		<td>
		The RTCRtpTransceiver's RTCRtpSender sender will offer to send RTP, and will send RTP if the remote peer accepts and sender.getParameters().encodings[i].active is true for any value of i. The RTCRtpTransceiver's RTCRtpReceiver will not offer to receive RTP, and will not receive RTP.
		zh：RTCRtpTransceiver的RTCRtpSender发送方将提供发送RTP，并且如果远程对等方接受并且sender.getParameters（）。encodings [i] .active对于任何i的值为true，则将发送RTP。 RTCRtpTransceiver的RTCRtpReceiver不会提供接收RTP，也不会接收RTP。
		</td>
	</tr>
	<tr>
		<td>
		recvonly
		</td>
		<td>
		The RTCRtpTransceiver's RTCRtpSender will not offer to send RTP, and will not send RTP. The RTCRtpTransceiver's RTCRtpReceiver will offer to receive RTP, and will receive RTP if the remote peer accepts.
		zh：RTCRtpTransceiver的RTCRtpSender不会提供发送RTP，也不会发送RTP。 RTCRtpTransceiver的RTCRtpReceiver将提供接收RTP，并在远程对等方接受时接收RTP。
		</td>
	</tr>
	<tr>
		<td>
		inactive
		</td>
		<td>
		The RTCRtpTransceiver's RTCRtpSender will not offer to send RTP, and will not send RTP. The RTCRtpTransceiver's RTCRtpReceiver will not offer to receive RTP, and will not receive RTP.
		zh：RTCRtpTransceiver的RTCRtpSender不会提供发送RTP，也不会发送RTP。 RTCRtpTransceiver的RTCRtpReceiver不会提供接收RTP，也不会接收RTP。
		</td>
	</tr>
</table>
	
