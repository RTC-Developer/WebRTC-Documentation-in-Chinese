## [4.8 Interfaces for Connectivity Establishment zh:4.8连接建立接口](http://w3c.github.io/webrtc-pc/#interfaces-for-connectivity-establishment)
### 4.8.1 RTCIceCandidate Interface zh:4.8.1 RTCIceCandidate接口

This interface describes an ICE candidate, described in [ICE] Section 2. Other than candidate, sdpMid, sdpMLineIndex, and usernameFragment, the remaining attributes are derived from parsing the candidate member in candidateInitDict, if it is well formed.

zh:该接口描述了ICE候选者，在[ICE]第2节中描述。除了候选者，sdpMid，sdpMLineIndex和usernameFragment之外，其余属性来自于候选成员在candidateInitDict中的解析，如果它是格式良好的。

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

**Constructor zh:构造函数**

`RTCIceCandidate`
zh:RTCIceCandidate

The RTCIceCandidate() constructor takes a dictionary argument, candidateInitDict, whose content is used to initialize the new RTCIceCandidate object.

zh:RTCIceCandidate（）构造函数接受一个字典参数candidateInitDict，其内容用于初始化新的RTCIceCandidate对象。

When invoked, run the following steps:

zh:调用时，请运行以下步骤：

1. If both the  sdpMid and  sdpMLineIndex  dictionary members in candidateInitDict are null, throw a TypeError.
zh:如果candidateInitDict中的sdpMid和sdpMLineIndex字典成员都为null，则抛出TypeError。

2. Let iceCandidate be a newly created RTCIceCandidate object.
zh:让iceCandidate成为新创建的RTCIceCandidate对象。

3. Initialize the following attributes of iceCandidate to null: foundation, component, priority, address, protocol, port, type, tcpType, relatedAddress, and relatedPort.
zh:将iceCandidate的以下属性初始化为null：foundation，component，priority，address，protocol，port，type，tcpType，relatedAddress和relatedPort。

4. Set the candidate, sdpMid, sdpMLineIndex, usernameFragment attributes of iceCandidate with the corresponding dictionary member values of candidateInitDict.
zh:使用candidateInitDict的相应字典成员值设置iceCandidate的候选者，sdpMid，sdpMLineIndex，usernameFragment属性。

5. Let candidate be the  candidate dictionary member of candidateInitDict. If candidate is not an empty string, run the following steps:
zh:让候选者成为candidateInitDict的候选词典成员。如果候选者不是空字符串，请运行以下步骤：

	1. Parse candidate using the candidate-attribute  grammar.
zh:使用候选属性语法解析候选者。

	2. If parsing of candidate-attribute has failed, abort these steps.
zh:如果候选属性的解析失败，则中止这些步骤。

	3. If any field in the parse result represents an invalid value for the corresponding attribute in iceCandidate, abort these steps.
zh:如果解析结果中的任何字段表示iceCandidate中相应属性的无效值，则中止这些步骤。

	4. Set the corresponding attributes in iceCandidate to the field values of the parsed result.
zh:将iceCandidate中的相应属性设置为已解析结果的字段值。

6. Return iceCandidate.
zh:返回iceCandidate。


NOTE:The constructor for RTCIceCandidate only does basic parsing and type checking for the dictionary members in candidateInitDict. Detailed validation on the well-formedness of candidate, sdpMid, sdpMLineIndex, usernameFragment with the corresponding session description is done when passing the RTCIceCandidate object to addIceCandidate().

zh:RTCIceCandidate的构造函数仅对candidateInitDict中的字典成员进行基本解析和类型检查。在将RTCIceCandidate对象传递给addIceCandidate（）时，会完成对候选，sdpMid，sdpMLineIndex，usernameFragment以及相应会话描述的良构性的详细验证。

Attributes zh:属性

Most attributes below are defined in section 15.1 of [ICE].

zh:以下大多数属性在[ICE]的第15.1节中定义。

`candidate` of type DOMString, readonly:
zh:DOMString类型的候选者，readonly

	This carries the candidate-attribute as defined in section 15.1 of [ICE]. If this RTCIceCandidate represents an end-of-candidates indication, candidate is an empty string.
	zh:它携带[ICE]第15.1节中定义的候选属性。如果此RTCIceCandidate表示候选者结束指示，则候选者是空字符串。

`sdpMid` of type DOMString, readonly, nullable:
zh:DOMString类型的sdpMid，readonly，nullable

	If not null, this contains the media stream "identification-tag" defined in [RFC5888] for the media component this candidate is associated with.
	zh:如果不为空，则其包含[RFC5888]中定义的媒体流“标识标签”，用于与该候选者相关联的媒体组件。

`sdpMLineIndex `of type unsigned short, readonly, nullable:
zh:sdpMLineIndex类型unsigned short，readonly，nullable

	 If not null, this indicates the index (starting at zero) of the media description in the SDP this candidate is associated with. 
	zh: 如果不为空，则这指示该候选与之关联的SDP中的媒体描述的索引（从零开始）。

`foundation` of type DOMString, readonly, nullable:
zh:DOMString类型的基础，只读，可空

	A unique identifier that allows ICE to correlate candidates that appear on multiple RTCIceTransports.
	zh:一个唯一标识符，允许ICE关联出现在多个RTCIceTransports上的候选项。

`component` of type RTCIceComponent, readonly, nullable:
zh:RTCIceComponent类型的组件，只读，可以为空

	The assigned network component of the candidate (rtp or rtcp). This corresponds to the component-id field in candidate-attribute, decoded to the string representation as defined in RTCIceComponent.
	zh:候选的指定网络组件（rtp或rtcp）。这对应于candidate-attribute中的component-id字段，解码为RTCIceComponent中定义的字符串表示。

`priority` of type unsigned long, readonly, nullable:
zh:unsigned long，readonly，nullable类型的优先级

	The assigned priority of the candidate.
	zh:候选人的指定优先顺序。

`address` of type DOMString, readonly, nullable:
zh:DOMString类型的地址，只读，可空

The address of the candidate, allowing for IPv4 addresses, IPv6 addresses, and fully qualified domain names (FQDNs). This corresponds to the connection-address field in candidate-attribute.

zh:候选地址，允许IPv4地址，IPv6地址和完全限定的域名（FQDN）。这对应于候选属性中的连接地址字段。

>NOTE:The addresses exposed in candidates gathered via ICE and made visibile to the application in RTCIceCandidate instances can reveal more information about the device and the user (e.g. location, local network topology) than the user might have expected in a non-WebRTC enabled browser.
>
>zh:通过ICE收集并在RTCIceCandidate实例中对应用程序进行访问的候选者中公开的地址可以揭示有关设备和用户的更多信息（例如，位置，本地网络拓扑），而不是用户在非WebRTC启用的浏览器中可能预期的信息。
>
>These addresses are always exposed to the application, and potentially exposed to the communicating party, and can be exposed without any specific user consent (e.g. for peer connections used with data channels, or to receive media only).
>
>zh:这些地址始终暴露给应用程序，并且可能暴露给通信方，并且可以在没有任何特定用户同意的情况下暴露（例如，用于与数据信道一起使用的对等连接，或仅用于接收媒体）。
>
>These addresses can also be used as temporary or persistent cross-origin states, and thus contribute to the fingerprinting surface of the device.
>
>zh:这些地址也可以用作临时或持久的跨源状态，因此有助于设备的指纹表面。
>
>Applications can avoid exposing addresses to the communicating party, either temporarily or permanently, by forcing the ICE Agent to report only relay candidates via the iceTransportPolicy member of RTCConfiguration.
>
>zh:应用程序可以通过强制ICE代理仅通过RTCConfiguration的iceTransportPolicy成员报告中继候选者来避免暂时或永久地向通信方公开地址。
>
>To limit the addresses exposed to the application itself, browsers can offer their users different policies regarding sharing local addresses, as defined in [RTCWEB-IP-HANDLING].
>
>zh:为了限制暴露给应用程序本身的地址，浏览器可以为其用户提供有关共享本地地址的不同策略，如[RTCWEB-IP-HANDLING]中所定义。

`protocol` of type RTCIceProtocol, readonly, nullable:
zh:RTCIceProtocol类型的协议，readonly，可空

	The protocol of the candidate (udp/tcp). This corresponds to the transport field in candidate-attribute.
	zh:候选协议（udp / tcp）。这对应于候选属性中的传输字段。

`port`of type unsigned short, readonly, nullable:
zh:unsigned short，readonly，nullable类型的端口

	The port of the candidate.
	zh:候选人的港口。

`type` of type RTCIceCandidateType, readonly, nullable:
zh:类型为RTCIceCandidateType，只读，可为空

	The type of the candidate. This corresponds to the candidate-types field in candidate-attribute.
	zh:候选人的类型。这对应于候选属性中的候选类型字段。

`tcpType` of type RTCIceTcpCandidateType, readonly, nullable:
zh:tcpType类型为RTCIceTcpCandidateType，readonly，nullable

	If protocol is tcp, tcpType represents the type of TCP candidate. Otherwise, tcpType is null. This corresponds to the tcp-type field in candidate-attribute.
	zh:如果protocol是tcp，则tcpType表示TCP候选的类型。否则，tcpType为null。这对应于candidate-attribute中的tcp-type字段。

`relatedAddress` of type DOMString, readonly, nullable:
zh:DOMString类型的相关地址，只读，可空

	For a candidate that is derived from another, such as a relay or reflexive candidate, the relatedAddress is the IP address of the candidate that it is derived from. For host candidates, the relatedAddress is null. This corresponds to the rel-address field in candidate-attribute.
	zh:对于从另一个派生的候选者（例如中继或自反候选者），relatedAddress是从其派生的候选者的IP地址。对于主机候选者，relatedAddress为空。这对应于candidate-attribute中的rel-address字段。

`relatedPort` of type unsigned short, readonly, nullable:
zh:relatedPort类型unsigned short，readonly，nullable

	For a candidate that is derived from another, such as a relay or reflexive candidate, the relatedPort is the port of the candidate that it is derived from. For host candidates, the relatedPort is null. This corresponds to the rel-port field in candidate-attribute.
	zh:对于从另一个派生的候选者（例如中继或反身候选者），relatedPort是从其派生的候选者的端口。对于候选主机，relatedPort为空。这对应于candidate-attribute中的rel-port字段。

`usernameFragment` of type DOMString, readonly, nullable:
zh:usernameSragment类型DOMString，readonly，nullable

	This carries the ufrag as defined in section 15.4 of [ICE].
	zh:这带有[ICE]第15.4节中定义的ufrag。
	
**Methods zh:方法**

`toJSON()`
zh:的toJSON（）

To invoke the toJSON() operation of the RTCIceCandidate interface, run the following steps:  Let json be a new RTCIceCandidateInit dictionary. For each attribute identifier attr in «"candidate", "sdpMid", "sdpMLineIndex", "usernameFragment"»: 
zh:要调用RTCIceCandidate接口的toJSON（）操作，请运行以下步骤：让json成为新的RTCIceCandidateInit字典。对于«“候选者”，“sdpMid”，“sdpMLineIndex”，“usernameFragment”中的每个属性标识符attr：

1. Let json be a new RTCIceCandidateInit dictionary.
zh:让json成为一个新的RTCIceCandidateInit字典。

2. For each attribute identifier attr in «"candidate", "sdpMid", "sdpMLineIndex", "usernameFragment"»:  

	1. Let value be the result of getting the underlying value of the attribute identified by attr, given this RTCIceCandidate object.
zh:在给定此RTCIceCandidate对象的情况下，将value设置为获取由attr标识的属性的基础值的结果。

	2. Set json[attr] to value.
zh:将json [attr]设置为value。

3. Return json.
zh:返回json。

```
dictionary RTCIceCandidateInit {
    DOMString       candidate = "";
    DOMString?      sdpMid = null;
    unsigned short? sdpMLineIndex = null;
    DOMString       usernameFragment;
};
```

**Dictionary RTCIceCandidateInit Members zh:字典RTCIceCandidateInit成员**

`candidate` of type DOMString, defaulting to "":
zh:DOMString类型的候选者，默认为“”

	This carries the candidate-attribute as defined in section 15.1 of [ICE]. If this represents an end-of-candidates indication, candidate is an empty string.
	zh:它携带[ICE]第15.1节中定义的候选属性。如果这表示候选者结束指示，则候选者是空字符串。

`sdpMid` of type DOMString, nullable, defaulting to null:
zh:DOMString类型的sdpMid，可为空，默认为null

	If not null, this contains the media stream "identification-tag" defined in [RFC5888] for the media component this candidate is associated with.
	zh:如果不为空，则其包含[RFC5888]中定义的媒体流“标识标签”，用于与该候选者相关联的媒体组件。

`sdpMLineIndex` of type unsigned short, nullable, defaulting to null:
zh:sdpMLineIndex类型unsigned short，nullable，默认为null

	If not null, this indicates the index (starting at zero) of the media description in the SDP this candidate is associated with.
	zh:如果不为空，则这指示该候选与之关联的SDP中的媒体描述的索引（从零开始）。

`usernameFragment` of type DOMString:
zh:DOMString类型的usernameFragment

	This carries the ufrag as defined in section 15.4 of [ICE].
	zh:这带有[ICE]第15.4节中定义的ufrag。
	
