## [5.2 RTCRtpSender 接口](http://w3c.github.io/webrtc-pc/#rtcrtpsender-interface)

The RTCRtpSender interface allows an application to control how a given MediaStreamTrack is encoded and transmitted to a remote peer. When setParameters is called on an RTCRtpSender object, the encoding is changed appropriately.

zh:RTCRtpSender接口允许应用程序控制给定MediaStreamTrack的编码方式并将其传输到远程对等方。在RTCRtpSender对象上调用setParameters时，编码会相应更改。

To create an RTCRtpSender with a MediaStreamTrack, track, a string, kind, a list of MediaStream objects, streams, and optionally a list of RTCRtpEncodingParameters objects, sendEncodings, run the following steps:

zh:要使用MediaStreamTrack创建RTCRtpSender，跟踪，字符串，种类，MediaStream对象列表，流以及可选的RTCRtpEncodingParameters对象列表sendEncodings，请运行以下步骤：

1.  Let sender be a new RTCRtpSender object. 
zh: 让发件人成为新的RTCRtpSender对象。

2.  Let sender have a [[SenderTrack]] internal slot initialized to track. 
zh: 让发件人初始化[[SenderTrack]]内部插槽进行跟踪。

3.  Let sender have a [[SenderTransport]] internal slot initialized to null. 
zh: 让发件人将[[SenderTransport]]内部插槽初始化为null。

4.  Let sender have a [[Dtmf]] internal slot initialized to null. 
zh: 让发送方将[[Dtmf]]内部槽初始化为null。

5.  If kind is "audio" then create an RTCDTMFSender dtmf and set the [[Dtmf]] internal slot to dtmf. 
zh: 如果kind是“audio”，则创建一个RTCDTMFSender dtmf并将[[Dtmf]]内部插槽设置为dtmf。

6.  Let sender have a [[SenderRtcpTransport]] internal slot initialized to null. 
zh: 让发件人将[[SenderRtcpTransport]]内部插槽初始化为null。

7.  Let sender have an [[AssociatedMediaStreamIds]] internal slot, representing a list of Ids of MediaStream objects that this sender is to be associated with. The [[AssociatedMediaStreamIds]] slot is used when sender is represented in SDP as described in [JSEP] (section 5.2.1.). 
zh: 让发件人有一个[[AssociatedMediaStreamIds]]内部插槽，表示该发件人要与之关联的MediaStream对象的ID列表。如[JSEP]（第5.2.1节）中所述，当发送方在SDP中表示时，使用[[AssociatedMediaStreamIds]]槽。

8.  Set sender's [[AssociatedMediaStreamIds]] to an empty set. 
zh: 将发件人的[[AssociatedMediaStreamIds]]设置为空集。

9.  For each stream in streams, add stream.id to [[AssociatedMediaStreamIds]] if it's not already there.  
zh: 对于流中的每个流，将stream.id添加到[[AssociatedMediaStreamIds]]（如果它尚未存在）。

10.  Let sender have a [[SendEncodings]] internal slot, representing a list of RTCRtpEncodingParameters dictionaries. 
zh: 让发件人有一个[[SendEncodings]]内部插槽，表示RTCRtpEncodingParameters字典列表。

11.  If sendEncodings is given as input to this algorithm, and is non-empty, set the [[SendEncodings]] slot to sendEncodings. Otherwise, set it to a list containing a single RTCRtpEncodingParameters with active set to true. 
zh: 如果sendEncodings作为此算法的输入，并且非空，则将[[SendEncodings]]插槽设置为sendEncodings。否则，将其设置为包含单个RTCRtpEncodingParameters且活动设置为true的列表。

12.  Let sender have a [[LastReturnedParameters]] internal slot, which will be used to match getParameters and setParameters transactions. 
zh: 让发件人有一个[[LastReturnedParameters]]内部插槽，用于匹配getParameters和setParameters事务。

13.  Return sender. 
zh: 退货发送。


```
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

**Attributes**

*track* of type MediaStreamTrack, readonly, nullable:
zh:MediaStreamTrack类型的跟踪，只读，可空


The track attribute is the track that is associated with this RTCRtpSender object. If track is ended, or if the track's output is disabled, i.e. the track is disabled and/or muted, the  RTCRtpSender MUST send silence (audio), black frames (video) or a zero-information-content equivalent. In the case of video, the RTCRtpSender SHOULD send one black frame per second. If track is null then the RTCRtpSender does not send. On getting, the attribute MUST return the value of the [[SenderTrack]] slot.

zh:track属性是与此RTCRtpSender对象关联的轨道。如果音轨结束，或者音轨的输出被禁用，即音轨被禁用和/或静音，则RTCRtpSender必须发送静音（音频），黑帧（视频）或零信息内容等效物。在视频的情况下，RTCRtpSender应该每秒发送一个黑帧。如果track为null，则RTCRtpSender不发送。获取时，属性必须返回[[SenderTrack]]槽的值。

*transport* of type RTCDtlsTransport, readonly, nullable:
zh:RTCDtlsTransport类型的传输，只读，可空

The transport attribute is the transport over which media from track is sent in the form of RTP packets. Prior to construction of the RTCDtlsTransport object, the transport attribute will be null. When bundling is used, multiple RTCRtpSender objects will share one transport and will all send RTP and RTCP over the same transport.

zh:传输属性是来自轨道的媒体以RTP分组的形式发送的传输。在构造RTCDtlsTransport对象之前，transport属性将为null。使用捆绑时，多个RTCRtpSender对象将共享一个传输，并将通过同一传输发送RTP和RTCP。

On getting, the attribute MUST return the value of the [[SenderTransport]] slot.

zh:获取时，属性必须返回[[SenderTransport]]槽的值。

*rtcpTransport* of type RTCDtlsTransport, readonly, nullable:
zh:rtcpTransport类型为RTCDtlsTransport，readonly，nullable

The rtcpTransport attribute is the transport over which RTCP is sent and received. Prior to construction of the RTCDtlsTransport object, the rtcpTransport attribute will be null. When RTCP mux is used (or bundling, which mandates RTCP mux), rtcpTransport will be null, and both RTP and RTCP traffic will flow over the transport described by transport.

zh:rtcpTransport属性是发送和接收RTCP的传输。在构造RTCDtlsTransport对象之前，rtcpTransport属性将为null。当使用RTCP mux（或捆绑，强制执行RTCP mux）时，rtcpTransport将为空，并且RTP和RTCP流量都将通过传输描述的传输流动。

On getting, the attribute MUST return the value of the [[SenderRtcpTransport]] slot.

zh:获取时，属性必须返回[[SenderRtcpTransport]]槽的值。

**Methods**

`getCapabilities, static`
zh:getCapabilities，静态

The getCapabilities() method returns the most optimistic view of the capabilities of the system for sending media of the given kind. It does not reserve any resources, ports, or other state but is meant to provide a way to discover the types of capabilities of the browser including which codecs may be supported. User agents MUST support kind values of "audio" and "video". If the system has no capabilities corresponding to the value of the kind argument, getCapabilities returns null.

zh:getCapabilities（）方法返回系统功能的最乐观视图，用于发送给定类型的媒体。它不保留任何资源，端口或其他状态，但旨在提供一种方法来发现浏览器的功能类型，包括可能支持的编解码器。用户代理必须支持“音频”和“视频”的类型值。如果系统没有与kind参数的值相对应的功能，则getCapabilities返回null。

These capabilities provide generally persistent cross-origin information on the device and thus increases the fingerprinting surface of the application. In privacy-sensitive contexts, browsers can consider mitigations such as reporting only a common subset of the capabilities.

zh:这些功能通常在设备上提供持久的跨源信息，从而增加了应用程序的指纹表面。在隐私敏感的上下文中，浏览器可以考虑缓解，例如仅报告功能的公共子集。

`setParameters`
zh:setParameters

The setParameters method updates how track is encoded and transmitted to a remote peer.

zh:setParameters方法更新如何编码轨道并将其传输到远程对等方。

When the setParameters method is called, the user agent MUST run the following steps:

zh:调用setParameters方法时，用户代理必须执行以下步骤：

1. Let parameters be the method's first argument. 
zh:让参数成为方法的第一个参数。
2. Let sender be the RTCRtpSender object on which setParameters is invoked.
zh:让sender成为调用setParameters的RTCRtpSender对象。
3. Let transceiver be the RTCRtpTransceiver object associated with sender (i.e. sender is transceiver's [[Sender]]).
zh:让收发器成为与发送器关联的RTCRtpTransceiver对象（即发送者是收发器的[[发件人]]）。
4. If transceiver's [[Stopped]] slot is true, return a promise rejected with a newly created InvalidStateError.
zh:如果收发器的[[Stopped]]插槽为true，则返回使用新创建的InvalidStateError拒绝的promise。
5. If sender's [[LastReturnedParameters]] internal slot is null, return a promise rejected with a newly created InvalidStateError.
zh:如果sender的[[LastReturnedParameters]]内部插槽为null，则返回使用新创建的InvalidStateError拒绝的promise。
6. Validate parameters by running the following steps:  
zh:通过运行以下步骤验证参数：
	1.  Let encodings be parameters.encodings. 
zh: 让编码成为参数。编码。
	2.  Let codecs be parameters.codecs. 
zh: 让编解码器为parameters.codecs。
	3.  Let N be the number of RTCRtpEncodingParameters stored in sender's internal [[SendEncodings]] slot. 
zh: 设N是存储在发送方内部[[SendEncodings]]槽中的RTCRtpEncodingParameters的数量。
	4.  If any of the following conditions are met, return a promise rejected with a newly created InvalidModificationError:    
zh: 如果满足以下任一条件，则返回使用新创建的InvalidModificationError拒绝的承诺：
		1.  encodings.length is different from N. 
zh: encodings.length与N不同。
		2.  encodings has been re-ordered. 
zh: 编码已被重新订购。
		3.  Any parameter in parameters is marked as a Read-only parameter (such as RID) and has a value that is different from the corresponding parameter value in sender's [[LastReturnedParameters]] internal slot. Note that this also applies to transactionId. 
zh: 参数中的任何参数都标记为只读参数（例如RID），并且其值与发送方[[LastReturnedParameters]]内部插槽中的相应参数值不同。请注意，这也适用于transactionId。

	5.  Verify that each scaleResolutionDownBy value in encodings is greater than or equal to 1.0. If one of the scaleResolutionDownBy values does not meet this requirement, return a promise rejected with a newly created RangeError. 
zh: 验证编码中的每个scaleResolutionDownBy值是否大于或等于1.0。如果scaleResolutionDownBy值之一不满足此要求，则返回使用新创建的RangeError拒绝的承诺。

	6.  Verify that each maxFramerate value in encodings is greater than or equal to 0.0. If one of the maxFramerate values does not meet this requirement, return a promise rejected with a newly created RangeError. 
zh: 验证编码中的每个maxFramerate值是否大于或等于0.0。如果其中一个maxFramerate值不符合此要求，则返回使用新创建的RangeError拒绝的promise。

7. Let p be a new promise.
zh:让p成为新的承诺。
8. In parallel, configure the media stack to use parameters to transmit sender's [[SenderTrack]].  If the media stack is successfully configured with parameters, queue a task to run the following steps:    
zh:并行配置媒体堆栈以使用参数来传输发送方[[SenderTrack]]。如果使用参数成功配置了媒体堆栈，请对任务进行排队以执行以下步骤：
	1. If the media stack is successfully configured with parameters, queue a task to run the following steps:  Set sender's internal [[LastReturnedParameters]] slot to null. Set sender's internal [[SendEncodings]] slot to  parameters.encodings. Resolve p with undefined.  
zh:如果使用参数成功配置了媒体堆栈，请对任务进行排队以执行以下步骤：将发件人的内部[[LastReturnedParameters]]插槽设置为null。将发件人的内部[[SendEncodings]]插槽设置为parameters.encodings。使用undefined解析p。
		1. Set sender's internal [[LastReturnedParameters]] slot to null.
zh:将发件人的内部[[LastReturnedParameters]]插槽设置为null。
		2. Set sender's internal [[SendEncodings]] slot to  parameters.encodings.
zh:将发件人的内部[[SendEncodings]]插槽设置为parameters.encodings。
		3. Resolve p with undefined. 
zh:使用undefined解析p。
	2. If any error occurred while configuring the media stack, queue a task to run the following steps:  
zh:如果在配置介质堆栈时发生任何错误，请对任务进行排队以执行以下步骤：
		1. If an error occurred due to hardware resources not being available, reject p with a newly created RTCError whose errorDetail is set to "hardware-encoder-not-available" and abort these steps.
zh:如果由于硬件资源不可用而发生错误，请使用新创建的RTCError拒绝p，其errorDetail设置为“hardware-encoder-not-available”并中止这些步骤。
		2. If an error occurred due to a hardware encoder not supporting parameters, reject p with a newly created  RTCError whose errorDetail is set to "hardware-encoder-error" and abort these steps.
zh:如果由于硬件编码器不支持参数而发生错误，请使用新创建的RTCError拒绝p，其errorDetail设置为“hardware-encoder-error”并中止这些步骤。
		3. For all other errors, reject p with a newly created OperationError.
zh:对于所有其他错误，请使用新创建的OperationError拒绝p。

9. Return p.
zh:返回p。

`setParameters` does not cause SDP renegotiation and can only be used to change what the media stack is sending or receiving within the envelope negotiated by Offer/Answer. The attributes in the RTCRtpSendParameters dictionary are designed to not enable this, so attributes like cname that cannot be changed are read-only. Other things, like bitrate, are controlled using limits such as maxBitrate, where the user agent needs to ensure it does not exceed the maximum bitrate specified by maxBitrate, while at the same time making sure it satisfies constraints on bitrate specified in other places such as the SDP.

zh:setParameters不会导致SDP重新协商，只能用于更改媒体堆栈在由Offer / Answer协商的信封内发送或接收的内容。 RTCRtpSendParameters字典中的属性旨在不启用此属性，因此无法更改的cname等属性是只读的。其他事项，如比特率，使用maxBitrate等限制进行控制，其中用户代理需要确保它不超过maxBitrate指定的最大比特率，同时确保它满足其他地方指定的比特率限制，例如SDP。

`getParameters`
zh:getParameters

The getParameters() method returns the RTCRtpSender object's current parameters for how track is encoded and transmitted to a remote RTCRtpReceiver.

zh:getParameters（）方法返回RTCRtpSender对象的当前参数，用于跟踪如何编码并传输到远程RTCRtpReceiver。

When getParameters is called, the RTCRtpSendParameters dictionary is constructed as follows:

zh:调用getParameters时，RTCRtpSendParameters字典构造如下：

*  transactionId is set to a new unique identifier, used to match this getParameters call to a setParameters call that may occur later. 
zh: transactionId设置为新的唯一标识符，用于将此getParameters调用与稍后可能发生的setParameters调用进行匹配。

*  encodings is set to the value of the [[SendEncodings]] internal slot. 
zh: 编码设置为[[SendEncodings]]内部插槽的值。

*  The headerExtensions sequence is populated based on the header extensions that have been negotiated for sending. 
zh: headerExtensions序列根据已协商发送的标头扩展名进行填充。

*  The codecs sequence is populated based on the codecs that have been negotiated for sending, and which the user agent is currently capable of sending. Prior to the completion of negotiation, the codecs sequence is empty. 
zh: 编解码器序列基于已协商用于发送的编解码器以及用户代理当前能够发送的编解码器来填充。在协商完成之前，编解码器序列为空。

*  rtcp.cname is set to the CNAME of the associated RTCPeerConnection. rtcp.reducedSize is set to true if reduced-size RTCP has been negotiated for sending, and false otherwise. 
zh: rtcp.cname设置为关联的RTCPeerConnection的CNAME。如果已协商缩小大小的RTCP以进行发送，则rtcp.reducedSize设置为true，否则设置为false。

*  degradationPreference is set to the last value passed into setParameters, or the default value of "balanced" if setParameters hasn't been called. 
zh: degradationPreference设置为传递给setParameters的最后一个值，如果尚未调用setParameters，则设置为“balanced”的默认值。

The returned RTCRtpSendParameters dictionary MUST be stored in the RTCRtpSender object's [[LastReturnedParameters]] internal slot.

zh:返回的RTCRtpSendParameters字典必须存储在RTCRtpSender对象的[[LastReturnedParameters]]内部插槽中。

getParameters may be used with setParameters to change the parameters in the following way:

zh:getParameters可以与setParameters一起使用，以下列方式更改参数：

```
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


After a completed call to setParameters, subsequent calls to getParameters will return the modified set of parameters.

zh:完成对setParameters的调用后，对getParameters的后续调用将返回修改后的参数集。

`replaceTrack`
zh:replaceTrack

Attempts to replace the RTCRtpSender's current track with another track provided (or with a null track), without renegotiation.

zh:尝试将RTCRtpSender的当前曲目替换为提供的另一曲目（或使用空曲目），而无需重新协商。

When the replaceTrack method is invoked, the user agent MUST run the following steps:
zh:当调用replaceTrack方法时，用户代理必须运行以下步骤：

1.  Let sender be the RTCRtpSender object on which replaceTrack is invoked. 
zh: 让sender成为调用replaceTrack的RTCRtpSender对象。

2.  Let transceiver be the RTCRtpTransceiver object associated with sender. 
zh: 让收发器成为与发送者关联的RTCRtpTransceiver对象。

3.  Let connection be the RTCPeerConnection object associated with sender. 
zh: 让connection成为与sender有关的RTCPeerConnection对象。

4.  Let withTrack be the argument to this method. 
zh: 让withTrack成为这种方法的参数。

5.  If withTrack is non-null and withTrack.kind differs from the transceiver kind of transceiver, return a promise rejected with a newly created TypeError. 
zh: 如果withTrack为非null且withTrack.kind与收发器类型的收发器不同，则返回使用新创建的TypeError拒绝的promise。

6.  Return the result of enqueuing the following steps to connection's operation queue:   
zh: 将以下步骤的结果返回到连接的操作队列：

	1.  If transceiver's [[Stopped]] slot is true, return a promise rejected with a newly  created InvalidStateError. 
zh: 如果收发器的[[Stopped]]插槽为true，则返回使用新创建的InvalidStateError拒绝的promise。

	2.  Let p be a new promise. 
zh: 让p成为新的承诺。

	3.  Let sending be true if the transceiver's [[CurrentDirection]] is "sendrecv" or "sendonly", and false otherwise. 
zh: 如果收发器的[[CurrentDirection]]是“sendrecv”或“sendonly”，则发送为true，否则为false。

	4.  Run the following steps in parallel:     
zh: 并行运行以下步骤：

		1.  If sending is true, and withTrack is null, have the sender stop sending. 
zh: 如果发送为真，并且withTrack为空，则让发件人停止发送。

		2.  If sending is true, and withTrack is not null, determine if withTrack can be sent immediately by the sender without violating the sender's already-negotiated envelope, and if it cannot, then reject p with a newly created InvalidModificationError, and abort these steps. 
zh: 如果发送为真，并且withTrack不为空，则确定发件人是否可以立即发送withTrack而不违反发件人已经协商的信封，如果不能，则拒绝p与新创建的InvalidModificationError，并中止这些步骤。

		3.  If sending is true, and withTrack is not null, have the sender switch seamlessly to transmitting withTrack instead of the sender's existing track. 
zh: 如果发送为真，并且withTrack不为空，则让发送方无缝切换到传输withTrack而不是发送方的现有磁道。

		4. Queue a task that runs the following steps:
zh:对运行以下步骤的任务进行排队：

			1.  If transceiver's [[Stopped]] slot is true, abort these steps. 
zh: 如果收发器的[[已停止]]插槽为真，则中止这些步骤。

			2.  Set sender's track attribute to withTrack. 
zh: 将发件人的track属性设置为withTrack。

			3.  Resolve p with undefined. 
zh: 使用undefined解析p。

	5.  Return p. 
zh: 返回p。

NOTE
Changing dimensions and/or frame rates might not require negotiation. Cases that may require negotiation include:

zh:更改尺寸和/或帧速率可能不需要协商。可能需要谈判的案例包括：

1. Changing a resolution to a value outside of the negotiated imageattr bounds, as described in [RFC6236].
zh:将分辨率更改为协商的imageattr边界之外的值，如[RFC6236]中所述。
2. Changing a frame rate to a value that causes the block rate for the codec to be exceeded.
zh:将帧速率更改为导致编解码器的块速率超出的值。
3. A video track differing in raw vs. pre-encoded format.
zh:视频轨道与原始格式和预编码格式不同。
4. An audio track having a different number of channels.
zh:具有不同通道数的音轨。
5. Sources that also encode (typically hardware encoders) might be unable to produce the negotiated codec; similarly, software sources might not implement the codec that was negotiated for an encoding source.
zh:同样编码的源（通常是硬件编码器）可能无法生成协商的编解码器;同样，软件源可能不会实现为编码源协商的编解码器。

`setStreams`
zh:setStreams

Sets the `MediaStreams` to be associated with this sender's track.

zh:将MediaStream设置为与此发件人的轨道关联。

When the setStreams method is invoked, the user agent MUST run the following steps:

zh:当调用setStreams方法时，用户代理必须运行以下步骤：

1.  Let sender be the RTCRtpSender object on which this method was invoked. 
zh: 让sender为调用此方法的RTCRtpSender对象。

2.  Let connection be the RTCPeerConnection object on which this method was invoked. 
zh: 让connection成为调用此方法的RTCPeerConnection对象。

3.  If connection's [[IsClosed]] slot is true, throw an InvalidStateError. 
zh: 如果connection的[[IsClosed]]槽为true，则抛出InvalidStateError。

4.  Let streams be a list of MediaStream objects constructed from the method's arguments, or an empty list if the method was called without arguments. 
zh: 让stream成为从方法参数构造的MediaStream对象列表，如果方法是在没有参数的情况下调用的话，则为空列表。

5.  Set sender's [[AssociatedMediaStreamIds]] to an empty set.  
zh: 将发件人的[[AssociatedMediaStreamIds]]设置为空集。

6.  For each stream in streams, add stream.id to [[AssociatedMediaStreamIds]] if it's not already there.  
zh: 对于流中的每个流，将stream.id添加到[[AssociatedMediaStreamIds]]（如果它尚未存在）。

7.  Update the negotiation-needed flag for connection. 
zh: 更新连接所需的协商标志。

`getStats`
zh:getStats

Gathers stats for this sender only and reports the result asynchronously.

zh:仅收集此发件人的统计信息，并异步报告结果。

When the  getStats() method is invoked, the user agent MUST run the following steps:

zh:当调用getStats（）方法时，用户代理必须运行以下步骤：

1.  Let selector be the RTCRtpSender object on which the method was invoked. 
zh: 让selector成为调用该方法的RTCRtpSender对象。

2.  Let p be a new promise, and run the following steps in parallel:    
zh: 设p为新的承诺，并行执行以下步骤：

	1.  Gather the stats indicated by selector according to the stats selection algorithm. 
zh: 根据统计选择算法收集选择器指示的统计数据。

	2.  Resolve p with the resulting RTCStatsReport object, containing the gathered stats. 
zh: 使用生成的RTCStatsReport对象解析p，其中包含收集的统计信息。


3.  Return p. 
zh: 返回p。
