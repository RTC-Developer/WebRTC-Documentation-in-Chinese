### 5.6.3 `RTCIceGathererState`枚举

```java
enum RTCIceGathererState {
    "new",
    "gathering",
    "complete"
};
```

| RTCIceGathererState枚举描述 |                                                              |
| :-------------------------- | :----------------------------------------------------------- |
| `new`                       | `RTCIceTransport`刚刚被创建，还未开始收集候选者。            |
| `gathering`                 | `RTCIceTransport`正在收集候选者。                            |
| `complete`                  | `RTCIceTransport`已经完成收集，并已发送此传输的候选者终止指示。在ICE重启导致它重启之前，它不会再次收集候选者。 |

