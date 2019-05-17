# 11 错误处理

某些操作抛出或引起`RTCError`。这是`DOMException`的扩展，包含了额外的WebRTC信息。

## 11.1 `RTCError`接口

```java
[
    Exposed=Window,
    Constructor(RTCErrorInit init, optional DOMString message = "")
] interface RTCError /*: DOMException*/ {
    readonly attribute RTCErrorDetailType errorDetail;
    readonly attribute long? sdpLineNumber;
    readonly attribute long? httpRequestStatusCode;
    readonly attribute long? sctpCauseCode;
    readonly attribute unsigned long? receivedAlert;
    readonly attribute unsigned long? sentAlert;
};
```

### 11.1.1 构造函数

`RTCError`

运行下列步骤：

1. 让init成为构造函数的第一个参数。

2. 让message成为构造函数的第二个参数。

3. 让e成为新的`RTCError`对象。

4. 将`message`参数设置为message，`name`参数设置为`“RTCError”`，触发e的`DOMException`构造函数。

   > NOTE:这个name不具有对legacy的映射，因此e的`code`属性返回0。

5. 设置e的所有`RTCError`属性为init中的对应属性的值，如果存在，否则设置为`null`。[测试：1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCError.html)

6. 返回e。

### 11.1.2 属性

RTCErrorDetailType类型的`errorDetail`，只读：针对出现错误类型的WebRTC特定错误代码。

[测试：2](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCPeerConnection-setRemoteDescription-offer.html)

[测试：2](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCError.html)

long类型的`sdpLineNumber`,只读，可以为null：如果`errorDetail`为`“sdp-syntax-error”`,这是错误被检测到的行号(第一行行号为1)。

long类型的`httpRequestStatusCode`,只读，可以为null：如果`errorDetail`为`“idp-load-failure”`，这是IdP URI回应的HTTP状态码。

long类型的`sctpCauseCode`,只读，可以为null：如果`errorDetail`是`“actp-failure”`，这是SCTP协商失败的SCTP原因代码。

unsigned long类型的`receiveAlert`,只读，可以为null：如果`errorDetail`是`“dtls-failure”，并且接收到致命的DTLS警报，这是接收到的DTLS警报的值。`

unsigned long类型的`sentAlert`，只读，可以为null：如果`errorDetail`是`"dtls-failure"，并且发送了`致命的DTLS警报，这是发送的DTLS警报值。

**RTCErrorInit字典**

```java
dictionary RTCErrorInit {
    required RTCErrorDetailType errorDetail;
    long sdpLineNumber;
    long httpRequestStatusCode;
    long sctpCauseCode;
    unsigned long receivedAlert;
    unsigned long sentAlert;
};
```

`RTCErrorInit`的`errorDetail`,`sdpLineNumber`,`httpRequestStatusCode`,`sctpCauseCode`,`receivedAlert`和`sentAlert`成员与`RTCError`的同名属性具有相同的定义。

### 11.1.3 字典`RTCError`成员

RTCErrorDetailType类型的`errorDetail`，必需的：查看`RTCError`的`errorDetail`。

long类型的`sdpLineNumber`:查看`RTCError`的`sdpLineNumber`。

long类型的`httpRequestStatusCode`:查看`RTCError`的`httpRequestStatusCode`。

long类型的`sctpCauseCode`:查看`RTCError`的`sctpCauseCode`。

unsigned long类型的`receivedAlert`:查看`RTCError`的`receivedAlert`。

unsigned long类型的`sentAlert`：查看`RTCError`的`sentAlert`。

### 11.1.4 `RTCErrorDetailType`枚举

```java
enum RTCErrorDetailType {
              "data-channel-failure",
              "dtls-failure",
              "fingerprint-failure",
              "idp-bad-script-failure",
              "idp-execution-failure",
              "idp-load-failure",
              "idp-need-login",
              "idp-timeout",
              "idp-tls-failure",
              "idp-token-expired",
              "idp-token-invalid",
              "sctp-failure",
              "sdp-syntax-error",
              "hardware-encoder-not-available",
              "hardware-encoder-error"
          };
```

名称以“idp”为前缀的错误详细信息类型由[WEBRTC-IDENTIFY]规范使用。这里描述了它们，因为WebIDL枚举必须只能在一个地方描述。

| 枚举描述                                                     |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `data-channel-failure`                                       | 数据通道已经失败。                                           |
| `dtls-failure`                                               | DTLS协商已经失败，或者连接由于致命错误被中断。`message`包含关于error的信息。如果接收到致命DTLS警报，`receivedAlert`属性被设置为接收到的DTLS警报。如果发送了致命TLS警报，`sentAlert`属性被设置为发送的DTLS警报的值。 |
| `fingerprint-failure`                                        | `RTCDtlsTransport`的远程证书与SDP提供的指纹不匹配。如果远程对等体不能将本地证书与提供的指纹匹配，则不会生成此错误。可能会从远程对等体接收到一个"bad-certificate" DTLS警报，这会导致“dtls-failure”。 |
| `idp-bad-script-failure`                                     | 从身份提供方加载的脚本不是有效的JavaScript或没有实现正确的接口。 |
| `idp-execution-failure`                                      | 身份提供方抛出异常或返回了rejected的承诺。                   |
| `idp-load-failure`                                           | Idp URI的加载已经失败。`httpRequestStatusCode`属性被设置为回应的HTTP状态码。 |
| `idp-need-login`                                             | 身份提供方需要用户登录。`idpLoginUrl`属性被设置为可以被用来登录的URL。 |
| `idp-timeout`                                                | Idp timer已经失效。                                          |
| `idp-tls-failure`                                            | 用户Idp HTTPS连接的TLS证书不受信任。                         |
| `idp-token-expired`                                          | Idp token已经失效。                                          |
| `idp-token-invalid`                                          | Idp token是无效的。                                          |
| `sctp-failure`                                               | SCTP协商已经失败，或者连接由于致命错误而被终止。`sctpCauseCode`属性被设置为SCTP原因码。 |
| `sdp-syntax-error`[测试:1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCPeerConnection-setRemoteDescription-offer.html) | SDP语法无效。`sdpLineNumber`属性被设置为SDP中检测到语法错误的行号。 |
| `hardware-encoder-not-available`                             | 请求的操作所需的硬件编码器资源不可用。                       |
| `hardware-encoder-error`                                     | 硬件编码器不支持提供的参数。                                 |

