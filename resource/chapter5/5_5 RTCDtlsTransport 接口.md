## [5.5 RTCDtlsTransport 接口](http://w3c.github.io/webrtc-pc/#rtcdtlstransport-interface)

The RTCDtlsTransport interface allows an application access to information about the Datagram Transport Layer Security (DTLS) transport over which RTP and RTCP packets are sent and received by RTCRtpSender and RTCRtpReceiver objects, as well other data such as SCTP packets sent and received by data channels. In particular, DTLS adds security to an underlying transport, and the RTCDtlsTransport interface allows access to information about the underlying transport and the security added. RTCDtlsTransport objects are constructed as a result of calls to setLocalDescription() and setRemoteDescription(). Each RTCDtlsTransport object represents the DTLS transport layer for the RTP or RTCP component of a specific RTCRtpTransceiver, or a group of RTCRtpTransceivers if such a group has been negotiated via [BUNDLE].

zh:RTCDtlsTransport接口允许应用程序访问有关RTCRtpSender和RTCRtpReceiver对象发送和接收RTP和RTCP数据包的数据报传输层安全性（DTLS）传输的信息，以及数据通道发送和接收的其他数据，如SCTP数据包。特别是，DTLS为底层传输增加了安全性，RTCDtlsTransport接口允许访问有关底层传输和添加的安全性的信息。由于调用setLocalDescription（）和setRemoteDescription（），RTCDtlsTransport对象被构造。每个RTCDtlsTransport对象表示特定RTCRtpTransceiver的RTP或RTCP组件的DTLS传输层，或者一组RTCRtpTransceivers（如果已通过[BUNDLE]协商这样的组）。

>NOTE
>
>A new DTLS association for an existing RTCRtpTransceiver will be represented by an existing RTCDtlsTransport object, whose state will be updated accordingly, as opposed to being represented by a new object.
>
>zh:现有RTCRtpTransceiver的新DTLS关联将由现有RTCDtlsTransport对象表示，其状态将相应更新，而不是由新对象表示。

An RTCDtlsTransport has a [[DtlsTransportState]] internal slot initialized to  new and a [[RemoteCertificates]] slot initialized to an empty list.

zh:RTCDtlsTransport的[[DtlsTransportState]]内部插槽初始化为new，[[RemoteCertificates]]插槽初始化为空列表。

When the underlying DTLS transport needs to update the state of the corresponding RTCDtlsTransport object, the user agent MUST queue a task that runs the following steps:

zh:当底层DTLS传输需要更新相应RTCDtlsTransport对象的状态时，用户代理必须对运行以下步骤的任务进行排队：

1.  Let transport be the  RTCDtlsTransport object to receive the state update. 
zh: 让transport成为RTCDtlsTransport对象以接收状态更新。

2.  Let newState be the new state. 
zh: 让newState成为新状态。

3.  Set transport's [[DtlsTransportState]] slot to newState. 
zh: 将transport的[[DtlsTransportState]]槽设置为newState。

4.  If newState is connected then let newRemoteCertificates be the certificate chain in use by the remote side, with each certificate encoded in binary Distinguished Encoding Rules (DER) [X690], and set transport's [[RemoteCertificates]] slot to newRemoteCertificates. 
zh: 如果连接了newState，则让newRemoteCertificates成为远程端使用的证书链，每个证书都以二进制可分辨编码规则（DER）[X690]编码，并将传输的[[RemoteCertificates]]槽设置为newRemoteCertificates。

5.  Fire an event named statechange at transport. 
zh: 在运输中发起名为statechange的事件。


```
[Exposed=Window] interface RTCDtlsTransport : EventTarget {
    [SameObject]
    readonly        attribute RTCIceTransport       iceTransport;
    readonly        attribute RTCDtlsTransportState state;
    sequence<ArrayBuffer> getRemoteCertificates ();
                    attribute EventHandler          onstatechange;
                    attribute EventHandler          onerror;
};
```

**Attributes**

*iceTransport* of type RTCIceTransport, readonly:
zh:iceTransport类型RTCIceTransport，readonly

The iceTransport attribute is the underlying transport that is used to send and receive packets. The underlying transport may not be shared between multiple active RTCDtlsTransport objects.

zh:iceTransport属性是用于发送和接收数据包的基础传输。多个活动的RTCDtlsTransport对象之间可能不共享底层传输。

*state* of type RTCDtlsTransportState, readonly:
zh:RTCDtlsTransportState类型的状态，只读

The state attribute MUST, on getting, return the value of the [[DtlsTransportState]] slot.

zh:获取时，状态属性必须返回[[DtlsTransportState]]槽的值。

*onstatechange* of type EventHandler:
zh:eventHandler类型的onstatechange

The event type of this event handler is  statechange. 
zh: 此事件处理程序的事件类型是statechange。

*onerror* of type EventHandler:
zh:eventHandler类型的错误

The event type of this event handler is error.
zh:此事件处理程序的事件类型是错误的。

**Methods**

`getRemoteCertificates`
zh:getRemoteCertificates

Returns the value of [[RemoteCertificates]]. 
zh: 返回[[RemoteCertificates]]的值。


**RTCDtlsTransportState Enum**

```
enum RTCDtlsTransportState {
    "new",
    "connecting",
    "connected",
    "closed",
    "failed"
};
```
<table>
	<tr>
		<td colspan="2">
		Enumeration description
		</td>
	</tr>
	<tr>
		<td>
		new
		</td>
		<td>
		DTLS has not started negotiating yet.
		zh:DTLS 还未开始协商。
		</td>
	</tr>
	<tr>
		<td>
		connecting
		</td>
		<td>
		DTLS is in the process of negotiating a secure connection and verifying the remote fingerprint.
		zh：DTLS 正在处理安全连接并确认远端指纹。
		</td>
	</tr>
	<tr>
		<td>
		connected	
		</td>
		<td>
		DTLS has completed negotiation of a secure connection and verified the remote fingerprint.
		zh：DTLS 已经完成安全连接的协商，并确认了远端指纹。
		</td>
	</tr>
	<tr>
		<td>
		closed
		</td>
		<td>
		The transport has been closed intentionally as the result of receipt of a close_notify alert, or calling close().
		zh：在收到 close_notify alert 或 calling close()后，传输结束。
		</td>
	</tr>
	<tr>
		<td>
		failed
		</td>
		<td>
		The transport has failed as the result of an error (such as receipt of an error alert or failure to validate the remote fingerprint).
		zh：当收到 error 时，传输失败（例如收到 error alert 或 远端 fingerprint 认证失败）。
		</td>
	</tr>
<table>