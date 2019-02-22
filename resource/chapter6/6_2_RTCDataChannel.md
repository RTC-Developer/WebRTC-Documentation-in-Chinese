## [6.2 RTCDataChannel](http://w3c.github.io/webrtc-pc/#rtcdatachannel)

The RTCDataChannel interface represents a bi-directional data channel between two peers. An RTCDataChannel is created via a factory method on an RTCPeerConnection object. The messages sent between the browsers are described in [RTCWEB-DATA] and [RTCWEB-DATA-PROTOCOL].

zh:RTCDataChannel接口表示两个对等体之间的双向数据信道。 RTCDataChannel是通过RTCPeerConnection对象上的工厂方法创建的。浏览器之间发送的消息在[RTCWEB-DATA]和[RTCWEB-DATA-PROTOCOL]中描述。

There are two ways to establish a connection with RTCDataChannel. The first way is to simply create an RTCDataChannel at one of the peers with the negotiated RTCDataChannelInit dictionary member unset or set to its default value false. This will announce the new channel in-band and trigger an RTCDataChannelEvent with the corresponding RTCDataChannel object at the other peer. The second way is to let the application negotiate the RTCDataChannel. To do this, create an RTCDataChannel object with the negotiated RTCDataChannelInit dictionary member set to true, and signal out-of-band (e.g. via a web server) to the other side that it SHOULD create a corresponding RTCDataChannel with the negotiated RTCDataChannelInit dictionary member set to true and the same id. This will connect the two separately created RTCDataChannel objects. The second way makes it possible to create channels with asymmetric properties and to create channels in a declarative way by specifying matching ids.

zh:有两种方法可以与RTCDataChannel建立连接。第一种方法是在其中一个对等体上创建一个RTCDataChannel，并且协商的RTCDataChannelInit字典成员未设置或设置为其默认值false。这将在带内公布新通道，并在另一个对等体上触发带有相应RTCDataChannel对象的RTCDataChannelEvent。第二种方法是让应用程序协商RTCDataChannel。为此，创建一个RTCDataChannel对象，将协商的RTCDataChannelInit字典成员设置为true，并通过带外信号（例如通过Web服务器）向另一方发出信号，它应该创建一个带有协商的RTCDataChannelInit字典成员集的相应RTCDataChannel。真实和相同的身份。这将连接两个单独创建的RTCDataChannel对象。第二种方法可以创建具有非对称属性的通道，并通过指定匹配的ID以声明方式创建通道。

Each RTCDataChannel has an associated underlying data transport that is used to transport actual data to the other peer. In the case of SCTP data channels utilizing an RTCSctpTransport (which represents the state of the SCTP association), the underlying data transport is the SCTP stream pair. The transport properties of the underlying data transport, such as in order delivery settings and reliability mode, are configured by the peer as the channel is created. The properties of a channel cannot change after the channel has been created. The actual wire protocol between the peers is specified by the WebRTC DataChannel Protocol specification [RTCWEB-DATA].

zh:每个RTCDataChannel都有一个关联的底层数据传输，用于将实际数据传输到另一个对等端。在SCTP数据信道利用RTCSctpTransport（表示SCTP关联的状态）的情况下，底层数据传输是SCTP流对。底层数据传输的传输属性（例如订单传递设置和可靠性模式）由对等方在创建通道时配置。创建通道后，通道的属性不会更改。对等体之间的实际有线协议由WebRTC DataChannel协议规范[RTCWEB-DATA]指定。

An RTCDataChannel can be configured to operate in different reliability modes. A reliable channel ensures that the data is delivered at the other peer through retransmissions. An unreliable channel is configured to either limit the number of retransmissions ( maxRetransmits ) or set a time during which transmissions (including retransmissions) are allowed ( maxPacketLifeTime ). These properties can not be used simultaneously and an attempt to do so will result in an error. Not setting any of these properties results in a reliable channel.

zh:可以将RTCDataChannel配置为在不同的可靠性模式下操作。可靠的信道确保通过重传在另一个对等体上传送数据。不可靠信道被配置为限制重传次数（maxRetransmits）或设置允许传输（包括重传）的时间（maxPacketLifeTime）。这些属性不能同时使用，尝试这样做会导致错误。不设置任何这些属性会产生可靠的通道。

An RTCDataChannel, created with createDataChannel or dispatched via an RTCDataChannelEvent, MUST initially be in the connecting state. When the RTCDataChannel object's underlying data transport is ready, the user agent MUST announce the RTCDataChannel as open.

zh:使用createDataChannel创建或通过RTCDataChannelEvent调度的RTCDataChannel必须最初处于连接状态。当RTCDataChannel对象的底层数据传输准备就绪时，用户代理必须宣布RTCDataChannel为open。

To create an RTCDataChannel, run the following steps:

zh:要创建RTCDataChannel，请运行以下步骤：

1.  Let channel be a newly created  RTCDataChannel object. 
zh: 让channel成为新创建的RTCDataChannel对象。

2.  Let channel have a [[ReadyState]] internal slot initialized to "connecting". 
zh: 让通道将[[ReadyState]]内部插槽初始化为“连接”。

3.  Let channel have a [[BufferedAmount]] internal slot initialized to 0. 
zh: 让通道将[[BufferedAmount]]内部插槽初始化为0。

4.  Let channel have internal slots named [[DataChannelLabel]], [[Ordered]], [[MaxPacketLifeTime]], [[MaxRetransmits]], [[DataChannelProtocol]], [[Negotiated]], [[DataChannelId]], and [[DataChannelPriority]]. 
zh: 让通道有内部插槽，名为[[DataChannelLabel]]，[[Ordered]]，[[MaxPacketLifeTime]]，[[MaxRetransmits]]，[[DataChannelProtocol]]，[[Negotiated]]，[[DataChannelId]]和[ [DataChannelPriority]。

5.  Return channel. 
zh: 退货渠道。

When the user agent is to announce an RTCDataChannel as open, the user agent MUST queue a task to run the following steps:

zh:当用户代理宣布RTCDataChannel为open时，用户代理必须对任务进行排队以运行以下步骤：

1.  If the associated RTCPeerConnection object's [[IsClosed]] slot is true, abort these steps. 
zh: 如果关联的RTCPeerConnection对象的[[IsClosed]]插槽为true，则中止这些步骤。

2.  Let channel be the RTCDataChannel object to be announced. 
zh: 让channel成为要宣布的RTCDataChannel对象。

3.  If channel's [[ReadyState]] is closing or closed, abort these steps. 
zh: 如果通道的[[ReadyState]]正在关闭或关闭，请中止这些步骤。

4.  Set channel's [[ReadyState]] slot to open. 
zh: 将通道的[[ReadyState]]插槽设置为打开。

5.  Fire an event named open at channel. 
zh: 在通道上触发一个名为open的事件。

When an underlying data transport is to be announced (the other peer created a channel with negotiated unset or set to false), the user agent of the peer that did not initiate the creation process MUST queue a task to run the following steps:

zh:当要宣布基础数据传输时（另一个对等方创建一个协商未设置或设置为false的通道），未启动创建过程的对等方的用户代理必须排队任务以运行以下步骤：

1.  If the associated RTCPeerConnection object's [[IsClosed]] slot is true, abort these steps. 
zh: 如果关联的RTCPeerConnection对象的[[IsClosed]]插槽为true，则中止这些步骤。

2.  Create an RTCDataChannel, channel. 
zh: 创建一个RTCDataChannel，频道。

3.  Let configuration be an information bundle received from the other peer as a part of the process to establish the underlying data transport described by the WebRTC DataChannel Protocol specification [RTCWEB-DATA-PROTOCOL]. 
zh: 让配置成为从另一个对等体接收的信息包，作为建立WebRTC数据通道协议规范[RTCWEB-DATA-PROTOCOL]描述的基础数据传输的过程的一部分。

4.  Initialize channel's [[DataChannelLabel]], [[Ordered]], [[MaxPacketLifeTime]], [[MaxRetransmits]], [[DataChannelProtocol]], and [[DataChannelId]] internal slots to the corresponding values in configuration. 
zh: 将通道的[[DataChannelLabel]]，[[Ordered]]，[[MaxPacketLifeTime]]，[[MaxRetransmits]]，[[DataChannelProtocol]]和[[DataChannelId]]内部插槽初始化为配置中的相应值。

5.  Initialize channel's [[Negotiated]] internal slot to false. 
zh: 将通道的[[Negotiated]]内部插槽初始化为false。

6.  Initialize channel's [[DataChannelPriority]] internal slot based on the integer priority value in configuration, according to the following mapping:    
zh: 根据配置中的整数优先级值初始化通道的[[DataChannelPriority]]内部插槽，根据以下映射：
	<table>
		<tr>
			<td>
			configuration priority value	
			</td>
			<td>
			RTCPriorityType value
			</td>
		</tr>
		<tr>
			<td>
			0 to 128	
			</td>
			<td>
			very-low
			</td>
		</tr>
		<tr>
			<td>
			129 to 256	
			</td>
			<td>
			low
			</td>
		</tr>
		<tr>
			<td>
			257 to 512	
			</td>
			<td>
			medium>
			</td>
		</tr>
		<tr>
			<td>
			513 and greater	
			</td>
			<td>
			high
			</td>
		</tr>
	</table>


7.  Set channel's [[ReadyState]] to open (but do not fire the open event, yet). 
zh: 将通道的[[ReadyState]]设置为打开（但不要触发打开的事件）。

	>Note
	>
	>This allows to start sending messages inside of the datachannel event handler prior to the open event being fired. 
	>zh:注意这允许在触发打开事件之前开始在datachannel事件处理程序内发送消息。

8.  Fire an event named datachannel using the RTCDataChannelEvent interface with the channel attribute set to channel at the RTCPeerConnection object. 
zh: 使用RTCDataChannelEvent接口触发名为datachannel的事件，并将channel属性设置为RTCPeerConnection对象的channel。

9.  Announce the data channel as open. 
zh: 宣布数据通道处于打开状态。

An RTCDataChannel object's underlying data transport may be torn down in a non-abrupt manner by running the closing procedure. When that happens the user agent MUST queue a task to run the following steps:

zh:通过运行关闭过程，可以以非突然的方式拆除RTCDataChannel对象的底层数据传输。当发生这种情况时，用户代理必须排队任务以运行以下步骤：

1.  Let channel be the RTCDataChannel object whose transport was closed. 
zh: 让channel成为其传输已关闭的RTCDataChannel对象。

2.  Unless the procedure was initiated by the channel's close method, set channel's [[ReadyState]] slot to closing. 
zh: 除非通过通道的关闭方法启动该过程，否则将通道的[[ReadyState]]插槽设置为关闭。

3.  Run the following steps in parallel:
zh:并行运行以下步骤：

	1.  Finish sending all currently pending messages of the channel. 
	zh: 完成发送频道的所有当前待处理消息。

	2.  Follow the closing procedure defined for the channel's underlying transport:     
	zh: 遵循为通道的基础传输定义的结束过程：
		1.  In the case of an SCTP-based  transport, follow [RTCWEB-DATA], section 6.7. 
zh: 如果是基于SCTP的传输，请按照[RTCWEB-DATA]的6.7节进行操作。


	3.  Render the channel's data transport closed by following the associated procedure. 
	zh: 按照相关步骤渲染通道的数据传输。

When an RTCDataChannel object's underlying data transport has been closed, the user agent MUST queue a task to run the following steps:

zh:当RTCDataChannel对象的基础数据传输已关闭时，用户代理必须对任务进行排队以运行以下步骤：

1.  Let channel be the RTCDataChannel object whose transport was closed. 
zh: 让channel成为其传输已关闭的RTCDataChannel对象。

2.  Set channel's [[ReadyState]] slot to closed. 
zh: 将通道的[[ReadyState]]插槽设置为关闭。

3.  If the transport was closed with an error, fire an event named error using the RTCErrorEvent interface with its errorDetail attribute set to "sctp-failure" at channel. 
zh: 如果传输因错误而关闭，则使用RTCErrorEvent接口触发名为error的事件，并在通道中将其errorDetail属性设置为“sctp-failure”。

4.  Fire an event named close at channel. 
zh: 在通道上发射一个名为close的事件。

In some cases, the user agent may be unable to create an RTCDataChannel 's underlying data transport. For example, the data channel's id may be outside the range negotiated by the [RTCWEB-DATA] implementations in the SCTP handshake. When the user agent determines that an RTCDataChannel's underlying data transport cannot be created, the user agent MUST queue a task to run the following steps:

zh:在某些情况下，用户代理可能无法创建RTCDataChannel的基础数据传输。例如，数据通道的id可能超出SCTP握手中[RTCWEB-DATA]实现协商的范围。当用户代理确定无法创建RTCDataChannel的基础数据传输时，用户代理必须排队任务以运行以下步骤：

1.  Let channel be the RTCDataChannel object for which the user agent could not create an underlying data transport. 
zh: 令channel为RTCDataChannel对象，用户代理无法为其创建基础数据传输。

2.  Set channel's [[ReadyState]] slot to closed. 
zh: 将通道的[[ReadyState]]插槽设置为关闭。

3.  Fire an event named error using the RTCErrorEvent interface with the errorDetail attribute set to "data-channel-failure" at channel. 
zh: 使用RTCErrorEvent接口触发名为error的事件，并在通道中将errorDetail属性设置为“data-channel-failure”。

4.  Fire an event named close at channel. 
zh: 在通道上发射一个名为close的事件。

When an  RTCDataChannel message has been received via the underlying data transport with type type and data rawData, the user agent MUST queue a task to run the following steps:

zh:当通过类型类型和数据rawData的基础数据传输接收到RTCDataChannel消息时，用户代理必须排队任务以运行以下步骤：

1.  Let channel be the RTCDataChannel object for which the user agent has received a message. 
zh: 令channel为用户代理已收到消息的RTCDataChannel对象。

2.  If channel's [[ReadyState]] slot is not open, abort these steps and discard rawData.  
zh: 如果通道的[[ReadyState]]插槽未打开，则中止这些步骤并丢弃rawData。

3. Execute the sub step by switching on type and the channel's binaryType:
zh:通过打开类型和通道的binaryType来执行子步骤：

	* If type indicates that rawData is a string:
	zh:如果type表示rawData是一个字符串：

		Let data be a DOMString that represents the result of decoding rawData as UTF-8.

		zh:令数据为DOMString，表示将rawData解码为UTF-8的结果。
	
	*  If type indicates that rawData is binary and binaryType is "blob":

		zh:如果type表示rawData是二进制而binaryType是“blob”：

		Let data be a new Blob object containing rawData as its raw data source.

		zh:让data成为包含rawData作为其原始数据源的新Blob对象。

	*  If type indicates that rawData is binary and binaryType is "arraybuffer":

	zh:如果type表示rawData是二进制，而binaryType是“arraybuffer”：

		Let data be a new ArrayBuffer object containing rawData as its raw data source.

		zh:让data成为一个新的ArrayBuffer对象，包含rawData作为其原始数据源。
		
1.  Fire an event named message using the MessageEvent interface with its origin attribute initialized to the origin of the document that created the channel's associated RTCPeerConnection, and the data attribute initialized to data at channel. 
zh: 使用MessageEvent接口触发名为message的事件，其origin属性初始化为创建通道关联的RTCPeerConnection的文档的原点，并且数据属性初始化为通道上的数据。


```
[Exposed=Window] interface RTCDataChannel : EventTarget {
    readonly        attribute USVString           label;
    readonly        attribute boolean             ordered;
    readonly        attribute unsigned short?     maxPacketLifeTime;
    readonly        attribute unsigned short?     maxRetransmits;
    readonly        attribute USVString           protocol;
    readonly        attribute boolean             negotiated;
    readonly        attribute unsigned short?     id;
    readonly        attribute RTCPriorityType     priority;
    readonly        attribute RTCDataChannelState readyState;
    readonly        attribute unsigned long       bufferedAmount;
                    [EnforceRange]
                    attribute unsigned long       bufferedAmountLowThreshold;
                    attribute EventHandler        onopen;
                    attribute EventHandler        onbufferedamountlow;
                    attribute EventHandler        onerror;
                    attribute EventHandler        onclose;
    void close ();
                    attribute EventHandler        onmessage;
                    attribute DOMString           binaryType;
    void send (USVString data);
    void send (Blob data);
    void send (ArrayBuffer data);
    void send (ArrayBufferView data);
};
```

**Attributes**

*label* of type USVString, readonly:
zh:USVString类型的标签，readonly

The label attribute represents a label that can be used to distinguish this RTCDataChannel object from other RTCDataChannel objects. Scripts are allowed to create multiple RTCDataChannel objects with the same label. On getting, the attribute MUST return the value of the [[DataChannelLabel]] slot.

zh:label属性表示可用于将此RTCDataChannel对象与其他RTCDataChannel对象区分开的标签。允许脚本使用相同的标签创建多个RTCDataChannel对象。获取时，属性必须返回[[DataChannelLabel]]槽的值。

*ordered* of type boolean, readonly:
zh:有序的boolean类型，readonly

The ordered attribute returns true if the RTCDataChannel is ordered, and false if other of order delivery is allowed. On getting, the attribute MUST return the value of the [[Ordered]] slot.

zh:如果订购了RTCDataChannel，则ordered属性返回true，如果允许其他订单传递，则返回false。获取时，属性必须返回[[Ordered]]槽的值。

*maxPacketLifeTime* of type unsigned short, readonly, nullable:
zh:maxPacketLifeTime类型为unsigned short，readonly，nullable

The maxPacketLifeTime attribute returns the length of the time window (in milliseconds) during which transmissions and retransmissions may occur in unreliable mode. On getting, the attribute MUST return the value of the [[MaxPacketLifeTime]] slot.

zh:maxPacketLifeTime属性返回在不可靠模式下可能发生传输和重传的时间窗口的长度（以毫秒为单位）。获取时，属性必须返回[[MaxPacketLifeTime]]槽的值。

*maxRetransmits* of type unsigned short, readonly, nullable:
zh:maxRetransmits类型unsigned short，readonly，nullable

The maxRetransmits attribute returns the maximum number of retransmissions that are attempted in unreliable mode. On getting, the attribute MUST return the value of the [[MaxRetransmits]] slot.

zh:maxRetransmits属性返回在不可靠模式下尝试的最大重新传输次数。获取时，属性必须返回[[MaxRetransmits]]槽的值。

*protocol* of type USVString, readonly:
zh:USVString类型的协议，readonly

The protocol attribute returns the name of the sub-protocol used with this RTCDataChannel. On getting, the attribute MUST return the value of the [[DataChannelProtocol]] slot.

zh:protocol属性返回与此RTCDataChannel一起使用的子协议的名称。获取时，属性必须返回[[DataChannelProtocol]]槽的值。

*negotiated* of type boolean, readonly:
zh:协商类型boolean，readonly

The negotiated attribute returns true if this RTCDataChannel was negotiated by the application, or false otherwise. On getting, the attribute MUST return the value of the [[Negotiated]] slot.

zh:如果此RTCDataChannel由应用程序协商，则negotiated属性返回true，否则返回false。获取时，属性必须返回[[Negotiated]]插槽的值。

*id* of type unsigned short, readonly, nullable:
zh:id uns类型unsigned short，readonly，nullable

The id attribute returns the ID for this RTCDataChannel. The value is initally null, which is what will be returned if the ID was not provided at channel creation time, and the DTLS role of the SCTP transport has not yet been negotiated. Otherwise, it will return the ID that was either selected by the script or generated by the user agent according to [RTCWEB-DATA-PROTOCOL]. After the ID is set to a non-null value, it will not change. On getting, the attribute MUST return the value of the [[DataChannelId]] slot.

zh:id属性返回此RTCDataChannel的ID。该值初始为null，如果在创建通道时未提供ID，则返回该值，并且尚未协商SCTP传输的DTLS角色。否则，它将返回由脚本选择的ID或由用户代理根据[RTCWEB-DATA-PROTOCOL]生成的ID。将ID设置为非空值后，它不会更改。获取时，属性必须返回[[DataChannelId]]槽的值。

*priority* of type RTCPriorityType, readonly:
zh:RTCPriorityType类型的优先级，只读

The priority attribute returns the priority for this RTCDataChannel. The priority is assigned by the user agent at channel creation time. On getting, the attribute MUST return the value of the [[DataChannelPriority]] slot.

zh:priority属性返回此RTCDataChannel的优先级。优先级由用户代理在通道创建时分配。获取时，属性必须返回[[DataChannelPriority]]槽的值。

*readyState* of type RTCDataChannelState, readonly:
zh:ready字节类型为RTCDataChannelState，readonly

The readyState attribute represents the state of the RTCDataChannel object. On getting, the attribute MUST return the value of the [[ReadyState]] slot.

zh:readyState属性表示RTCDataChannel对象的状态。获取时，属性必须返回[[ReadyState]]槽的值。

*bufferedAmount* of type unsigned long, readonly:
zh:bufferedAmount类型unsigned long，readonly

The bufferedAmount attribute MUST, on getting, return the value of the [[BufferedAmount]] slot. The attribute exposes the number of bytes of application data (UTF-8 text and binary data) that have been queued using send(). Even though the data transmission can occur in parallel, the returned value MUST NOT be decreased before the current task yielded back to the event loop to prevent race conditions. The value does not include framing overhead incurred by the protocol, or buffering done by the operating system or network hardware. The value of the [[BufferedAmount]] slot will only increase with each call to the send() method as long as the  [[ReadyState]] slot is open; however, the slot does not reset to zero once the channel closes. When the underlying data transport sends data from its queue, the user agent MUST queue a task that reduces [[BufferedAmount]] with the number of bytes that was sent.

zh:获取时，bufferedAmount属性必须返回[[BufferedAmount]]槽的值。该属性公开使用send（）排队的应用程序数据（UTF-8文本和二进制数据）的字节数。即使数据传输可以并行发生，在当前任务返回事件循环以防止竞争条件之前，不得减小返回值。该值不包括协议产生的帧开销，或操作系统或网络硬件完成的缓冲。只要[[ReadyState]]插槽打开，[[BufferedAmount]]插槽的值只会随着每次调用send（）方法而增加;但是，一旦通道关闭，插槽不会重置为零。当底层数据传输从其队列发送数据时，用户代理必须排队一个任务，该任务使用发送的字节数减少[[BufferedAmount]]。

*bufferedAmountLowThreshold* of type unsigned long:
zh:bufferedAmountLowThreshold类型为unsigned long

The bufferedAmountLowThreshold attribute sets the threshold at which the bufferedAmount is considered to be low. When the bufferedAmount decreases from above this threshold to equal or below it, the bufferedamountlow event fires. The bufferedAmountLowThreshold is initially zero on each new RTCDataChannel, but the application may change its value at any time.

zh:bufferedAmountLowThreshold属性设置bufferedAmount被视为低的阈值。当bufferedAmount从此阈值以上减小到等于或低于此阈值时，将触发bufferedamountlow事件。 bufferedAmountLowThreshold在每个新的RTCDataChannel上最初为零，但应用程序可能随时更改其值。

*onopen* of type EventHandler:
zh:onOn类型EventHandler

The event type of this event handler is open.
zh:此事件处理程序的事件类型已打开。

*onbufferedamountlow* of type EventHandler:
zh:eventHandler类型的onbufferedamountlow

The event type of this event handler is bufferedamountlow.
zh:此事件处理程序的事件类型为bufferedamountlow。

*onerror* of type EventHandler:
zh:eventHandler类型的错误

The event type of this event handler is RTCErrorEvent. errorDetail contains "sctp-failure", sctpCauseCode contains the SCTP Cause Code value, and message contains the SCTP Cause-Specific-Information, possibly with additional text.

zh:此事件处理程序的事件类型是RTCErrorEvent。 errorDetail包含“sctp-failure”，sctpCauseCode包含SCTP Cause Code值，并且消息包含SCTP Cause-Specific-Information，可能包含其他文本。

*onclose* of type EventHandler:
zh:onHose类型为EventHandler

The event type of this event handler is close.

zh:此事件处理程序的事件类型已关闭。

*onmessage* of type EventHandler:
zh:eventHandler类型的onmessage

The event type of this event handler is message.

zh:此事件处理程序的事件类型是message。

*binaryType* of type DOMString:
zh:DOMString类型的binaryType

The binaryType attribute MUST, on getting, return the value to which it was last set. On setting, if the new value is either the string "blob" or the string "arraybuffer", then set the IDL attribute to this new value. Otherwise, throw a SyntaxError. When an RTCDataChannel object is created, the binaryType attribute MUST be initialized to the string "blob".

zh:获取时，binaryType属性必须返回上次设置的值。在设置时，如果新值是字符串“blob”或字符串“arraybuffer”，则将IDL属性设置为此新值。否则，抛出一个SyntaxError。创建RTCDataChannel对象时，必须将binaryType属性初始化为字符串“blob”。

This attribute controls how binary data is exposed to scripts. See the [WEBSOCKETS-API] for more information.

zh:此属性控制二进制数据如何向脚本公开。有关更多信息，请参阅[WEBSOCKETS-API]。

**Methods**

`close`

Closes the RTCDataChannel. It may be called regardless of whether the RTCDataChannel object was created by this peer or the remote peer.

zh:关闭RTCDataChannel。无论RTCDataChannel对象是由对等方还是远程对等方创建，都可以调用它。

When the close method is called, the user agent MUST run the following steps:

zh:调用close方法时，用户代理必须执行以下步骤：

1.  Let channel be the RTCDataChannel object which is about to be closed. 
zh: 让channel成为即将关闭的RTCDataChannel对象。

2.  If channel's [[ReadyState]] slot is closing or closed, then abort these steps. 
zh: 如果通道的[[ReadyState]]插槽正在关闭或关闭，则中止这些步骤。

3.  Set channel's [[ReadyState]] slot to closing. 
zh: 将通道的[[ReadyState]]插槽设置为关闭。

4.  If the closing procedure has not started yet, start it. 
zh: 如果关闭程序尚未开始，请启动它。

`send`

Run the steps described by the send() algorithm with argument type string object.

zh:使用参数类型字符串对象运行send（）算法描述的步骤。

`send`

Run the steps described by the send() algorithm with argument type Blob object.

zh:使用参数类型Blob对象运行send（）算法描述的步骤。

`send`

Run the steps described by the send() algorithm with argument type ArrayBuffer object.

zh:使用参数类型ArrayBuffer对象运行send（）算法描述的步骤。


```
dictionary RTCDataChannelInit {
             boolean         ordered = true;
             [EnforceRange]
             unsigned short  maxPacketLifeTime;
             [EnforceRange]
             unsigned short  maxRetransmits;
             USVString       protocol = "";
             boolean         negotiated = false;
             [EnforceRange]
             unsigned short  id;
             RTCPriorityType priority = "low";
};
```

**Dictionary RTCDataChannelInit Members**

*ordered* of type boolean, defaulting to true:
zh:有序的boolean类型，默认为true

If set to false, data is allowed to be delivered out of order. The default value of true, guarantees that data will be delivered in order.

zh:如果设置为false，则允许数据不按顺序传送。默认值为true，保证数据按顺序传递。

*maxPacketLifeTime* of type unsigned short:
zh:maxPacketLifeTime类型为unsigned short

Limits the time (in milliseconds) during which the channel will transmit or retransmit data if not acknowledged. This value may be clamped if it exceeds the maximum value supported by the user agent.

zh:限制通道在未确认的情况下传输或重新传输数据的时间（以毫秒为单位）。如果该值超过用户代理支持的最大值，则可以限制该值。

*maxRetransmits* of type unsigned short:
zh:maxRetransmits类型为unsigned short

Limits the number of times a channel will retransmit data if not successfully delivered. This value may be clamped if it exceeds the maximum value supported by the user agent.

zh:如果未成功传递，则限制通道重新传输数据的次数。如果该值超过用户代理支持的最大值，则可以限制该值。

*protocol* of type USVString, defaulting to "":
zh:USVString类型的协议，默认为“”

Subprotocol name used for this channel.

zh:用于此渠道的子协议名称。

*negotiated* of type boolean, defaulting to false:
zh:协商类型boolean，默认为false

	 The default value of false tells the user agent to announce the channel in-band and instruct the other peer to dispatch a corresponding RTCDataChannel object. If set to true, it is up to the application to negotiate the channel and create an RTCDataChannel object with the same id at the other peer.  
	zh: 默认值false指示用户代理在带内通告通道并指示另一个对等方分派相应的RTCDataChannel对象。如果设置为true，则由应用程序协商通道并在另一个对等方创建具有相同ID的RTCDataChannel对象。


>Note
>
>If set to true, the application must also take care to not send a message until the other peer has created a data channel to receive it. Receiving a message on an SCTP stream with no associated data channel is undefined behavior, and it may be silently dropped. This will not be possible as long as both endpoints create their data channel before the first offer/answer exchange is complete.
>zh:注意如果设置为true，则应用程序还必须注意不要发送消息，直到另一个对等方创建了一个数据通道来接收它。在没有关联数据通道的SCTP流上接收消息是未定义的行为，可能会以静默方式丢弃。只要两个端点在第一个提议/应答交换完成之前创建其数据通道，就不可能实现这一点。

*id* of type unsigned short:
zh:id为unsigned short的类型

Overrides the default selection of ID for this channel.

zh:覆盖此通道的默认ID选择。

*priority* of type RTCPriorityType, defaulting to low:
zh:RTCPriorityType类型的优先级，默认为低

Priority of this channel.

zh:此频道的优先级。

The send() method is overloaded to handle different data argument types. When any version of the method is called, the user agent MUST run the following steps:

zh:send（）方法被重载以处理不同的数据参数类型。当调用任何版本的方法时，用户代理必须运行以下步骤：

1.  Let channel be the RTCDataChannel object on which data is to be sent. 
zh: 让channel成为要在其上发送数据的RTCDataChannel对象。

2.  If channel's [[ReadyState]] slot is not open, throw an InvalidStateError. 
zh: 如果通道的[[ReadyState]]插槽未打开，则抛出InvalidStateError。

3. Execute the sub step that corresponds to the type of the methods argument:
zh:执行与methods参数类型对应的子步骤：

	*  string object:
		zh:字符串对象：

		Let data be a byte buffer that represents the result of encoding the 	method's argument as UTF-8.
	zh:令数据为字节缓冲区，表示将方法的参数编码为UTF-8的结果。

	*  Blob object:
zh:Blob对象：

		Let data be the raw data represented by the Blob object.

	zh:令数据为Blob对象表示的原始数据。
	
	*  ArrayBuffer object:
zh:ArrayBuffer对象：

		Let data be the data stored in the buffer described by the ArrayBuffer object.
zh:设数据是存储在ArrayBuffer对象描述的缓冲区中的数据。

	*  ArrayBufferView object:
zh:ArrayBufferView对象：

		Let data be the data stored in the section of the buffer described by the ArrayBuffer object that the ArrayBufferView object references.
zh:设数据是存储在ArrayBufferView对象引用的ArrayBuffer对象描述的缓冲区部分中的数据。

	>NOTE
	>
	>Any data argument type this method has not been overloaded with will result in a TypeError. This includes null and undefined.
	>zh:此方法尚未重载的任何数据参数类型都将导致TypeError。这包括null和undefined。

4.  If the byte size of data exceeds the value of  maxMessageSize on channel's associated RTCSctpTransport, throw a TypeError. 
zh: 如果数据的字节大小超过通道关联的RTCSctpTransport上的maxMessageSize值，则抛出TypeError。

5.  Queue data for transmission on channel's underlying data transport. If queuing data is not possible because not enough buffer space is available, throw an OperationError.
zh: 队列数据，用于在通道的底层数据传输上传输。如果由于没有足够的缓冲区空间而无法排队数据，则抛出OperationError。
	
	 >Note
	 >
	 >The actual transmission of data occurs in parallel. If sending data leads to an SCTP-level error, the application will be notified asynchronously through onerror. 
	 >zh:注意实际的数据传输是并行发生的。如果发送数据导致SCTP级错误，将通过错误异步通知应用程序。

6.  Increase the value of the [[BufferedAmount]] slot by the byte size of data. 
zh: 通过数据的字节大小增加[[BufferedAmount]]插槽的值。

```
enum RTCDataChannelState {
    "connecting",
    "open",
    "closing",
    "closed"
};

```

<table>
	<tr>
		<td colspan="2">
		RTCDataChannelState Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		connecting
		</td>
		<td>
		The user agent is attempting to establish the underlying data transport. This is the initial state of an RTCDataChannel object, whether created with createDataChannel, or dispatched as a part of an RTCDataChannelEvent.
		zh:用户代理正在尝试建立基础数据传输。这是RTCDataChannel对象的初始状态，无论是使用createDataChannel创建，还是作为RTCDataChannelEvent的一部分调度。
		</td>
	</tr>
	<tr>
		<td>
		open
		</td>
		<td>
		The underlying data transport is established and communication is possible.
		zh:建立基础数据传输并且可以进行通信。
		</td>
	</tr>
	<tr>
		<td>
		closing
		</td>
		<td>
		The procedure to close down the underlying data transport has started.
		zh:关闭基础数据传输的过程已经开始。
		</td>
	</tr>
	<tr>
		<td>
		closed
		</td>
		<td>
		The underlying data transport has been closed or could not be established.
		zh:基础数据传输已关闭或无法建立。
		</td>
	</tr>
</table>