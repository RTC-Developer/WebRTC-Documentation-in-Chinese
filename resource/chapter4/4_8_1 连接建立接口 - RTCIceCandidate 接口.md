## [4.8 连接建立接口](http://w3c.github.io/webrtc-pc/#interfaces-for-connectivity-establishment)
### 4.8.1 RTCIceCandidate接口

该接口描述了ICE候选人，在[ICE]第2节中描述。除了`candidate`，`sdpMid`，`sdpMLineIndex`和`usernameFragment`之外，其余属性解析来自于`candidateInitDict`中的`candidate`成员，如果它是格式良好的。

```
[Constructor(optional RTCIceCandidateInit candidateInitDict),
 Exposed=Window]
interface RTCIceCandidate {
    readonly attribute DOMString               candidate;
    readonly attribute DOMString?              sdpMid;
    readonly attribute unsigned short?         sdpMLineIndex;
    readonly attribute DOMString?              foundation;
    readonly attribute RTCIceComponent?        component;
    readonly attribute unsigned long?          priority;
    readonly attribute DOMString?              address;
    readonly attribute RTCIceProtocol?         protocol;
    readonly attribute unsigned short?         port;
    readonly attribute RTCIceCandidateType?    type;
    readonly attribute RTCIceTcpCandidateType? tcpType;
    readonly attribute DOMString?              relatedAddress;
    readonly attribute unsigned short?         relatedPort;
    readonly attribute DOMString?              usernameFragment;
    RTCIceCandidateInit toJSON();
};
```

**构造函数**

`RTCIceCandidate`接口

RTCIceCandidate() 构造函数接受一个字典参数candidateInitDict，该参数用于初始化新的RTCIceCandidate对象。

调用时，请执行以下步骤：

1. 如果 `candidateInitDict` 中的 `sdpMid` 和 `sdpMLineIndex` 字典成员都为 `null`，则抛出 TypeError 。

2. 让 `iceCandidate` 成为新创建的`RTCIceCandidate` 对象。

3. 将 `iceCandidate` 的以下属性初始化为`null`: `foundation`, `component`, `priority`, `address`, `protocol`, `port`, `type`, `tcpType`, `relatedAddress和relatedPort`。

4. Set the candidate, sdpMid, sdpMLineIndex, usernameFragment attributes of iceCandidate with the corresponding dictionary member values of candidateInitDict.
zh:使用candidateInitDict的相应字典成员值设置iceCandidate的候选者，sdpMid，sdpMLineIndex，usernameFragment属性。

5. 将候选人设置为 `candidateInitDict`的`candidate`成员。如果设置的候选者不是空字符串，请运行以下步骤：

	1. 使用候选属性语法解析候选者。

	2. 如果候选属性语法解析失败，则中止这些步骤。

	3. 如果解析结果中的任何字段表示iceCandidate中相应属性的无效值，则中止这些步骤。

	4. 将 `iceCandidate` 中的相应属性设置为已解析结果的字段值。

6. 返回`iceCandidate`。


NOTE：`RTCIceCandidate`的构造函数仅对 `candidateInitDict` 中的字典成员进行基本解析和类型检查。在将RTCIceCandidate对象传递给 addIceCandidate() 时，会完成 `candidate`, `sdpMid`, `sdpMLineIndex`, `usernameFragment` 以及相应会话描述的良构性的详细验证。

属性

以下大多数属性在[ICE]的第15.1节中定义。

`candidate` 的类型为 `DOMString` 只读项

	`candidate-attribute`在[ICE]第15.1节中有详细说明。如果此`RTCIceCandidate表示候选者结束指示，则候选者是空字符串。

`sdpMid` 的类型为 `DOMString` 只读项，可为空

	如果不为`null`，则其包含[RFC5888]中定义的媒体流“标识标签”，用于与该候选者相关联的媒体组件。

`sdpMLineIndex` 的类型为 `unsigned short` 只读项，可为空

	 如果不为空，则这指示该候选与之关联的SDP中的媒体描述的索引（从零开始）。

`foundation` 的类型为 `DOMString` 只读项，可为空
zh:DOMString类型的基础，只读，可空

	一个唯一标识符，允许ICE关联出现在多个 RTCIceTransports 上的候选项。

`component`的类型为 `RTCIceComponent` 只读，可为空

	候选人指定的网络组件（rtp或rtcp）。这对应于 `candidate-attribute` 中的 `component-id` 字段，解码为 `RTCIceComponent` 中定义的字符串表示。

`priority`的类型为 `unsigned long` 只读，可为空

	候选人指定的优先顺序。

`address`的类型为 `DOMString` 只读，可为空

候选的地址，允许IPv4地址，IPv6地址和完全限定的域名（FQDN）。这对应于候选属性中的连接地址字段。

>NOTE：通过ICE收集并在RTCIceCandidate实例中对应用程序进行访问的候选者中公开的地址可以揭示有关设备和用户的更多信息（例如，位置，本地网络拓扑），而不是用户在非WebRTC启用的浏览器中可能预期的信息。
>
> 这些地址始终暴露给应用程序，并且可能暴露给通信方，并且可以在没有任何特定用户同意的情况下暴露（例如，用于与数据信道一起使用的对等连接，或仅用于接收媒体）。
>
>
>这些地址也可以用作临时或持久的跨源状态，因此有助于设备的指纹表面。
>
>
>应用程序可以通过强制ICE代理仅通过RTCConfiguration的iceTransportPolicy成员报告中继候选者来避免暂时或永久地向通信方公开地址。
>

>
>为了限制暴露给应用程序本身的地址，浏览器可以为其用户提供有关共享本地地址的不同策略，如[RTCWEB-IP-HANDLING]中所定义。

`protocol` 的类型为 `RTCIceProtocol`，只读项，可为空

	候选协议可以为udp和tcp。对应于候选属性中的传输字段。

`port`的类型为 `unsigned short`，只读项，可为空

	候选人的端口。

`type`的类型为 `RTCIceCandidateType`，只读项，可为空

	候选人的类型。对应于候选属性中的传输字段。

`tcpType`的类型为 `RTCIceTcpCandidateType` ，只读项，可为空

	如果 protocol 是 tcp ，则 tcpType 表示 TCP 候选的类型。否则，tcpType为null。这对应于candidate-attribute中的tcp-type字段。

`relatedAddress` 的类型为`DOMString`，只读项，可为空

	对于从另一个派生的候选者（例如中继或自反候选者），relatedAddress是从其派生的候选者的IP地址。对于主机候选者，relatedAddress为空。这对应于 candidate-attribute 中的 rel-address 字段。

`relatedPort`的类型为`unsigned short`，只读项，可为空

	对于从另一个派生的候选者（例如中继或反身候选者），`relatedPort` 是从其派生的候选者的端口。对于候选主机， `relatedPort` 为空。这对应于candidate-attribute中的rel-port字段。

`usernameFragment` 的类型为`DOMString`，只读项，可为空
	详细描述参照[ICE]第15.4节中定义的ufrag。
	
**方法**

`toJSON()`
toJSON()



1. 把json成为一个新的RTCIceCandidateInit字典。

2. 要调用RTCIceCandidate接口的toJSON()操作，请运行以下步骤：让json成为新的RTCIceCandidateInit字典。对于«“候选者”，“sdpMid”，“sdpMLineIndex”，“usernameFragment”中的每个属性标识符attr»:

	1. 在给定此RTCIceCandidate对象的情况下，将value设置为获取由attr标识的属性的基础值的结果。

	2. 将json [attr]设置为value。

3. 返回json。

```
dictionary RTCIceCandidateInit {
    DOMString       candidate = "";
    DOMString?      sdpMid = null;
    unsigned short? sdpMLineIndex = null;
    DOMString       usernameFragment;
};
```

**字典RTCIceCandidateInit成员**

`candidate` of type DOMString, defaulting to "":
	详细描述参照[ICE]第15.1节中定义的候选属性。如果这表示`candidate`结束指示，则`candidate`是空字符串。

`sdpMid` 的类型为 `DOMString`, 可为空，默认为null
	如果不为空，则其包含[RFC5888]中定义的媒体流“标识标签”，用于与该`candidate`相关联的媒体组件。

`sdpMLineIndex` 的类型为 `unsigned short`, 可为空，默认为空
	如果不为空，则这指示该候选与之关联的SDP中的媒体描述的索引（从零开始）。

`usernameFragment` 的类型为 `DOMString` 只读，可为空
	详细描述参照[ICE]第15.4节中有`ufrag`的定义。
	
