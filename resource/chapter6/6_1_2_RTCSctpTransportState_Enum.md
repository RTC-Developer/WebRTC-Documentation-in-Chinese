### 6.1.2 RTCSctpTransportState枚举

RTCSctpTransportState表示SCTP传输状态。

```java
enum RTCSctpTransportState {
    "connecting",
    "connected",
    "closed"
};
```

| 枚举描述     |                                                              |
| ------------ | ------------------------------------------------------------ |
| `connecting` | `RTCSctpTransport`正在协商一个关联。这是当`RTCSctpTransport`被创建时[SctpTransportState]插槽的初始状态。 |
| `connected`  | 当协商完成后，会出现一个更新[SctpTransportState]插槽为`“connected”`的任务。 |
| `closed`     | 当接收到SHUTDOWN或者ABORT时，或是SCTP关联被有意关闭，例如通过关闭对等连接或应用拒绝数据，改变SCTP端口的远程描述，[SctpTransportState]插槽的值会被更新为`“closed”`。 |

