## [5.5 RTCDtlsTransport接口](http://w3c.github.io/webrtc-pc/#rtcdtlstransport-interface)

`RTCDtlsTransport`接口允许应用程序获取数据报传输层安全性协议(DTLS)传输的信息，通过此协议，RTP与RTCP数据包被`RTCRtpSender`和`RTCRtpReceiver`对象发送和接收，还有数据通道发送和接收的其它数据，例如STCP数据包。特别是DTLS为底层传输添加了安全性，并且`RTCDtlsTransport`接口允许获取底层传输和安全性的信息。因为需要调用`setLocalDescription()`和`setRemoteDescription()`函数，`RTCDtlsTransport`对象被创建。每个`RTCDtlsTransport`对象代表一个特定的`RTCRtpTransceiver`的RTP或RTCP组件的DTLS传输层，或是一组已经通过BUNDLE协商好的`RTCRtpTransceivers`。

> NOTE:现存RTCRtpTransceiver的一个新DTLS关联将会由一个现存RTCDtlsTransport对象代表，它的状态将会对应更新，而不是换做一个新的对象来表示。

一个`RTCDtlsTransport`有一个被初始化为`new`的[[DtlsTransportState]]内部插槽，和一个被初始化为空列表的[[RemoteCertificates]]的插槽。

当底层DTLS传输产生错误时，例如证书失效，或错误警报，用户代理必须对运行下列步骤的任务排序：

1. 让transport成为`RTCDtlsTransport`对象，用来接收状态更新和错误提示。
2. 如果transport的状态已经为failed，中断这些步骤。
3. 设置transport的[[DtlsTransportState]]插槽为`failed`。
4. 使用RTCErrorEvent接口和它的或者为dtlsfailure，或者为fingerprint-failure的errorDetail属性，发起一个名为error的事件，并且其它fields都按照RTCErrorDetailType枚举的那样恰当设置，在transport。
5. 在transport发起一个名为statechange的事件。

当底层DTLS传输由于任何其它原因需要更新相应RTCDtlsTransport对象的状态时，用户代理必须对运行下列步骤的任务排序：

1. 让transport成为RTCDtlsTransport对象来接收状态更新。
2. 让newState成为新状态。
3. 设置transport的[[DtlsTransportState]]插槽为newState。
4. 如果newState连接，那么让newRemoteCertificates成为远端使用的证书链，每个证书都使用二进制可辨别编码规则(DER)[X690]进行编码，饼设置transport的[[RemoteCertificates]]插槽为newRemoteCertificates。
5. 在transport发起一个名为statechange的事件。

```java
[Exposed=Window] interface RTCDtlsTransport : EventTarget {
    [SameObject]
    readonly        attribute RTCIceTransport       iceTransport;
    readonly        attribute RTCDtlsTransportState state;
    sequence<ArrayBuffer> getRemoteCertificates ();
                    attribute EventHandler          onstatechange;
                    attribute EventHandler          onerror;
};
```

**属性**

`iceTransport` of type `RTCIceTransport`, readonly:
iceTransport属性是用来发送接收数据包的底层传输。底层传输在多个活跃的RTCDtlsTransport对象间可能不会被共享。

`state` of type `RTCDtlsTransportState`, readonly:
当需要state属性时，它必须返回[[DtlsTransportState]]插槽的值。

`onstatechange` of type `EventHandler`:
此eventhandler的事件类型是statechange。

`onerror` of type `EventHandler`:
此eventhandler的事件类型是error。

**方法**

`getRemoteCertificates`返回[[RemoteCertificates]]的值。

`RTCDtlsTransportState` 枚举

```java
enum RTCDtlsTransportState {
    "new",
    "connecting",
    "connected",
    "closed",
    "failed"
};
```



| 枚举描述                                                     |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `new`                                                        | DTLS还没有开始协商。                                         |
| `connecing`                                                  | DTLS正在协商一个安全连接，并验证远端指纹。                   |
| `connected`[测试：1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCDtlsTransport-state.html) | DTLS已经完成安全连接的协商，并已经确认远端指纹。             |
| `closed`[测试：1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCDtlsTransport-state.html) | transport已经关闭，由于收到close_notify警报，或调用close()。 |
| `failed`                                                     | 由于产生了错误，transport已经失败(例如接收到错误警报或未能验证远端指纹)。 |
