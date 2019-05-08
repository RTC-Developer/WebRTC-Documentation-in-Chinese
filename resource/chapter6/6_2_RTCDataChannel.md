## 6.2 `RTCDataChannel`

`RTCDataChannel`接口表示两个对等体之间的双向数据信道。 `RTCDataChannel`是通过`RTCPeerConnection`对象上的工厂方法创建的。浏览器之间发送的消息在[RTCWEB-DATA]和[RTCWEB-DATA-PROTOCOL]中描述。

有两种方法可以与`RTCDataChannel`建立连接。第一种方法是在其中一个对等体上创建一个`RTCDataChannel`，并且协商的`RTCDataChannelInit`字典成员为未设置或被设置为默认值false。这将在带内公布新通道，并在另一个对等体上触发带有相应`RTCDataChannel`对象的`RTCDataChannelEvent`。第二种方法是让应用程序协商`RTCDataChannel`。为此，创建一个`RTCDataChannel`对象，将协商的`RTCDataChannelInit`字典成员设置为true，并通过带外信号（例如通过Web服务器）向另一方发出信号，它应该创建一个带有协商的`RTCDataChannelInit`字典成员集的相应`RTCDataChannel`，字典成员被设置为true，并且具有相同`id`。这将连接两个单独创建的`RTCDataChannel`对象。第二种方法可以创建具有非对称属性的通道，并通过指定匹配的ID以声明方式创建通道。

每个`RTCDataChannel`都有一个关联的底层数据传输，用于将实际数据传输到另一个对等端。在SCTP数据信道利用`RTCSctpTransport`（表示SCTP关联的状态）的情况下，底层数据传输是SCTP流对。底层数据传输的传输属性（例如有序发送设置和可靠性模式）由对等方在创建通道时配置。创建通道后，通道的属性不会更改。对等体之间的实际有线协议由WebRTC DataChannel协议规范[RTCWEB-DATA]指定。

可以将`RTCDataChannel`配置为在不同的依赖模式下操作。可靠的信道确保通过重新传输在另一个对等体上传达数据。不可靠信道被配置为限制重传次数（`maxRetransmits`）或设置允许传输（包括重传）的时间（`maxPacketLifeTime`）。这些属性不能同时使用，这样做会导致错误。不设置任何这些属性会得到可靠的通道。

使用`createDataChannel`创建或通过`RTCDataChannelEvent`调度的`RTCDataChannel`必须最初处于`connecing`状态。当`RTCDataChannel`对象的底层数据传输准备就绪时，用户代理必须宣布`RTCDataChannel`为open。

要创建`RTCDataChannel`，请运行以下步骤:

1. 让channel成为新创建的`RTCDataChannel`对象。
2. 让通道将[[ReadyState]]内部插槽初始化为`“connecting”`。[测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCPeerConnection-ondatachannel.html)
3. 让通道将[[BufferedAmount]]内部插槽初始化为`0`。
4. 让通道具有内部插槽，名为[[DataChannelLabel]]，[[Ordered]]，[[MaxPacketLifeTime]]，[[MaxRetransmits]]，[[DataChannelProtocol]]，[[Negotiated]]，[[DataChannelId]]和[ [DataChannelPriority]。
5. 返回通道。

当用户代理宣布`RTCDataChannel`为open时，用户代理必须对任务进行排队,运行以下步骤：

1. 如果关联的`RTCPeerConnection`对象的[[IsClosed]]插槽为true，则中止这些步骤。
2. 让channel成为要宣布的`RTCDataChannel`对象。
3. 如果通道的[[ReadyState]]为`closing`或`closed`，请中止这些步骤。
4. 将通道的[[ReadyState]]插槽设置为`open`。
5. 在通道上触发一个名为open的事件。[测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCPeerConnection-ondatachannel.html)

当要宣布底层数据传输时（另一个对等方创建一个negotiated为未设置或设置为false的通道），未启动创建过程的对等方的用户代理必须对任务排序，以运行以下步骤：

1. 如果关联的`RTCPeerConnection`对象的[[IsClosed]]插槽为true，则中止这些步骤。

2. 创建一个`RTCDataChannel`，通道。

3. 让配置成为从另一个对等体接收的信息包，作为建立由WebRTC数据通道协议规范[RTCWEB-DATA-PROTOCOL]描述的底层数据传输的过程的一部分。

4. 将通道的[[DataChannelLabel]]，[[Ordered]]，[[MaxPacketLifeTime]]，[[MaxRetransmits]]，[[DataChannelProtocol]]和[[DataChannelId]]内部插槽初始化为配置中的相应值。

5. 将通道的[[Negotiated]]内部插槽初始化为`false`。

6. 根据配置中的整数优先级值初始化通道的[[DataChannelPriority]]内部插槽，根据以下映射：

   | configuration priority value | RTCPriorityType value |
   | ---------------------------- | --------------------- |
   | 0 to 128                     | very-low              |
   | 129 to 256                   | low                   |
   | 257 to 512                   | medium                |
   | 513 and greater              | high                  |

7. 将通道的[[ReadyState]]设置为`open`（但不要触发`open`事件）。

   > NOTE:这允许在触发open事件之前开始在`datachannel`事件处理程序内发送消息。

8. 使用`RTCDataChannelEvent`接口触发名为`datachannel`的事件，并将channel属性设置为`RTCPeerConnection`对象的channel。

9. 宣布数据通道处于open状态。

通过运行关闭过程，可以以非突然的方式拆除`RTCDataChannel`对象的底层数据传输。当发生这种情况时，用户代理必须排队任务以运行以下步骤：

1. 让channel成为其传输已关闭的`RTCDataChannel`对象。
2. 除非通过通道的`close`方法启动该过程，否则将通道的[[ReadyState]]插槽设置为`closing`。
3. 并行运行以下步骤:
   1. 完成发送channel的所有当前待处理消息。
   2. 遵循为通道的底层传输定义的关闭过程：
      1. 如果是基于SCTP的传输，请按照[RTCWEB-DATA]的6.7节进行操作。
   3. 按照相关步骤渲染通道的数据传输。

当`RTCDataChannel`对象的基础数据传输已关闭时，用户代理必须对任务进行排队以运行以下步骤：

1. 让channel成为其传输已关闭的`RTCDataChannel`对象。
2. 将通道的[[ReadyState]]插槽设置为`closed`。
3. 如果传输因错误而关闭，则使用`RTCErrorEvent`接口触发名为`error`的事件，并在通道中将其`errorDetail`属性设置为`“sctp-failure”`。
4. 在通道内发起一个名为`close`的事件。

在某些情况下，用户代理可能无法创建`RTCDataChannel`的基础数据传输。例如，数据通道的`id`可能超出SCTP握手中[RTCWEB-DATA]实现协商的范围。当用户代理确定无法创建`RTCDataChannel`的基础数据传输时，用户代理必须排队任务以运行以下步骤：

1. 令channel为`RTCDataChannel`对象，用户代理无法为其创建底层数据传输。
2. 将通道的[[ReadyState]]插槽设置为`closed`。
3. 使用`RTCErrorEvent`接口触发名为`error`的事件，并在通道中将`errorDetail`属性设置为“data-channel-failure”。
4. 在通道上发起一个名为`close`的事件。

当通过类型`type`和数据`rawData`的底层数据传输接收到`RTCDataChannel`消息时，用户代理必须排队任务以运行以下步骤：

1. 令channel为用户代理已收到消息的`RTCDataChannel`对象。

2. 如果通道的[[ReadyState]]插槽不为`open`，则中止这些步骤并丢弃`rawData`。

3. 通过打开`type`和`channel`的`binaryType`来执行子步骤：

   - 如果type表示rawData是一个字符串:

     令数据为DOMString，表示将`rawData`解码为UTF-8的结果。

     [测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/datachannel-emptystring.html)

   - 如果type表示rawData是二进制而`binaryType`是`“blob”`：

     让data成为包含rawData作为其原始数据源的新`Blob`对象。

   - 如果type表示rawData是二进制，而`binaryType`是`“arraybuffer”`：

     让data成为一个新的`ArrayBuffer`对象，包含rawData作为原始数据源。

4. 使用MessageEvent接口触发名为`message`的事件，其`origin`属性初始化为创建通道关联的`RTCPeerConnection`的文档的原点，并且`data`属性初始化为通道上的数据。

```java
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

**属性**

USVString类型的`label`，只读:label属性表示可用于将此`RTCDataChannel`对象与其他`RTCDataChannel`对象区分开的标签。允许脚本使用相同的标签创建多个`RTCDataChannel`对象。获取时，属性必须返回[[DataChannelLabel]]槽的值。[测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCPeerConnection-createDataChannel.html)

boolean类型`ordered`，只读：如果`RTCDataChannel`有序，则`ordered`属性返回true，如果允许无序传递，则返回false。获取时，属性必须返回[[Ordered]]槽的值。

unsigned short类型的`maxPacketLifeTime`，只读的，可以为null：`maxPacketLifeTime`属性返回在不可靠模式下可能发生传输和重传的时间窗口的长度（以毫秒为单位）。获取时，属性必须返回[[MaxPacketLifeTime]]槽的值。

unsigned short类型的`maxRetransmits`，只读的，可以为null：`maxRetransmits`属性返回在不可靠模式下尝试的最大重新传输次数。获取时，属性必须返回[[MaxRetransmits]]槽的值。

USVString类型的`protocol`，只读的：`protocol`属性返回与此`RTCDataChannel`一起使用的子协议的名称。获取时，属性必须返回[[DataChannelProtocol]]槽的值。

boolean类型的`negotiated`，只读的：如果此`RTCDataChannel`由应用程序协商，则`negotiated`属性返回true，否则返回false。获取时，属性必须返回[[Negotiated]]插槽的值。

unsigned short类型的`id`，只读的，可以为null：`id`属性返回此`RTCDataChannel`的ID。该值初始为null，如果在创建通道时未提供ID，则返回该值，并且尚未协商SCTP传输的DTLS角色。否则，它将返回由脚本选择的ID或由用户代理根据[RTCWEB-DATA-PROTOCOL]生成的ID。将ID设置为非空值后，它不会更改。获取时，属性必须返回[[DataChannelId]]槽的值。[测试2](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCDataChannel-id.html)

RTCPriorityType类型的`priority`，只读:`priority`属性返回此`RTCDataChannel`的优先级。优先级由用户代理在通道创建时分配。获取时，属性必须返回[[DataChannelPriority]]槽的值。

`RTCDataChannelState`类型的`readyState`，只读的：`readyState`属性表示`RTCDataChannel`对象的状态。获取时，属性必须返回[[ReadyState]]槽的值。

unsigned long类型的`bufferedAmount`，只读的：获取时，`bufferedAmount`属性必须返回[[BufferedAmount]]槽的值。该属性公开使用`send（)`排队的应用程序数据（UTF-8文本和二进制数据）的字节数。即使数据传输可以并行发生，在当前任务返回事件循环以防止race condition之前，不得减小返回值。该值不包括协议产生的帧开销，或操作系统或网络硬件完成的缓冲。只要[[ReadyState]]插槽打开，[[BufferedAmount]]插槽的值只会随着每次调用send（）方法而增加;但是，一旦通道关闭，插槽不会重置为零。当底层数据传输从其队列发送数据时，用户代理必须排队一个任务，该任务随着发送的字节数减少[[BufferedAmount]]。

unsigned long类型的`bufferedAmountLowThreshold`:`bufferedAmountLowThreshold`属性设置`bufferedAmount`被视为低的阈值。当`bufferedAmount`从此阈值以上减小到等于或低于此阈值时，将触发`bufferedamountlow`事件。 `bufferedAmountLowThreshold`在每个新的`RTCDataChannel`上最初为零，但应用程序可能随时更改其值。

EventHandler类型的`onopen`:此事件处理程序的事件类型为`open`。

eventHandler类型的`onbufferedamountlow`:此事件处理程序的事件类型为`bufferedamountlow`。

eventHandler类型的`onerror`:此事件处理程序的事件类型是`RTCErrorEvent`。` errorDetail`包含“sctp-failure”，`sctpCauseCode`包含SCTP Cause Code值，并且`message`包含SCTP Cause-Specific-Information，可能包含其他文本。

EventHandler类型的`onclose`:此事件处理程序的事件类型为`close`。

eventHandler类型的`onmessage`:此事件处理程序的事件类型是`message`。

DOMString类型的`binaryType`:获取时，`binaryType`属性必须返回上次设置的值。在设置时，如果新值是字符串`“blob”`或字符串`“arraybuffer”`，则将IDL属性设置为此新值。否则，抛出一个`SyntaxError`。创建`RTCDataChannel`对象时，必须将`binaryType`属性初始化为字符串`“blob”`。

此属性控制二进制数据如何向脚本公开。有关更多信息，请参阅[WEBSOCKETS-API]。

**方法**

`close`:

关闭`RTCDataChannel`。无论`RTCDataChannel`对象是由对等方还是远程对等方创建，都可以调用它。

调用close方法时，用户代理必须执行以下步骤：

1. 让channel成为即将关闭的`RTCDataChannel`对象。
2. 如果通道的[[ReadyState]]插槽为`closing`或`closed`，则中止这些步骤。
3. 将通道的[[ReadyState]]插槽设置为`closing`。
4. 如果关闭程序尚未开始，请启动它。

`send`

使用参数类型`string`对象运行`send（）`算法描述的步骤。[测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCDataChannel-send.html)

`send`

使用参数类型`Blob`对象运行`send（）`算法描述的步骤。

`send`

使用参数类型`ArrayBuffer`对象运行`send（）`算法描述的步骤。

`send`

使用参数类型`ArrayBufferView`对象运行`send（）`算法描述的步骤。

`send()`方法被重载，用来处理不同数据参数类型。当该方法的任何版本被调用时，用户代理必须运行下列步骤：

1. 让channel成为将要发送数据的`RTCDataChannel`对象。

2. 如果channel的[ReadyState]插槽不为`open`，抛出`InvalidStateError`。

3. 执行对应方法参数类型的子步骤：

   - `string`对象:

     让data成为byte buffer，表示将方法参数编码为UTF-8的结果。

   - `Blob`对象:

     让data成为由`Blob`对象表示的原始数据。

   - `ArrayBuffer`对象:

     让data成为由`ArrayBuffer`对象描述的存在buffer中的数据。

   - `ArrayBufferView`对象：

     让data成为`ArrayBufferView`对象提到的`ArrayBuffer`对象描述的buffer中存储的数据。

   > NOTE:任何该方法没有重载的数据类型将会导致`TypeError`。这包括null和undefined。

4. 如果data的大小超过了channel的关联`RTCSctpTransport`上的`maxMessageSize`的值，抛出`TypeError`。

5. 对在channel的底层数据传输的data进行排队。

   > NOTE:实际数据传输是并行的。如果发送数据导致SCTP层级的错误，应用程序将会被通过`onerror`异步通知。

6. 增加[BufferedAmount]插槽的值，增加量为data的大小。

```java
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

**字典`RTCDataChannelInit`成员**

boolean类型的`ordered`，默认为true:如果设置为false，则允许数据不按顺序传送。默认值为true，保证数据按顺序传递。

unsigned short类型的`maxPacketLifeTime`:限制通道在未确认的情况下传输或重新传输数据的时间（以毫秒为单位）。如果该值超过用户代理支持的最大值，则可以限制该值。[测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCPeerConnection-createDataChannel.html)

unsigned short类型的`maxRetransmits`:如果未成功传递，则限制通道重新传输数据的次数。如果该值超过用户代理支持的最大值，则可以限制该值。

USVString类型的`protocol`，默认为`“”`:用于此通道的子协议名称。

boolean类型的`negotiated`，默认为`false`:默认值false指示用户代理在带内通告通道并指示另一个对等方分派相应的`RTCDataChannel`对象。如果设置为true，则由应用程序协商通道并在另一个对等方创建具有相同ID的`RTCDataChannel`对象。

> NOTE:如果设置为true，则应用程序还必须注意不要发送消息，直到另一个对等方创建了一个数据通道来接收它。在没有关联数据通道的SCTP流上接收消息是未定义的行为，可能会以静默方式丢弃。只要两个端点在第一个提议/应答交换完成之前创建其数据通道，就不可能实现这一点。

unsigned short类型的`id`:重写此通道的默认ID选择。

RTCPriorityType类型的`priority`，默认为`low`:此通道的优先级。

```java
enum RTCDataChannelState {
    "connecting",
    "open",
    "closing",
    "closed"
};
```

| RTCDataChannelState枚举描述 |                                                              |
| --------------------------- | ------------------------------------------------------------ |
| `connecting`                | 用户代理正在尝试建立底层数据传输。这是`RTCDataChannel`对象的初始状态，无论是使用`createDataChannel`创建，还是作为`RTCDataChannelEvent`的一部分调度。 |
| `open`                      | 建立基础数据传输并且可以进行通信。                           |
| `closing`                   | 关闭底层数据传输的过程已经开始。                             |
| `closed`                    | 底层数据传输已关闭或无法建立。                               |

