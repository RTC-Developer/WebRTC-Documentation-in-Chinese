### 5.6.6 RTCIceComponent枚举

```java
enum RTCIceComponent {
    "rtp",
    "rtcp"
};
```



| RTCIceComponent枚举描述 |                                                              |
| ----------------------- | ------------------------------------------------------------ |
| `rtp`                   | ICE传输被用到[ICE],4.1.1.1中定义的`RTP`(或`RTCP`复用)。与RTP复用的协议(例如数据通道)共享其组件ID。这表示在候选属性中编码时`component-id`值为1。 |
| `rtcp`                  | ICE传输用于RTCP，如[ICE]第4.1.1.1节中所定义。这表示在候选属性中编码时的`component-id`值2。 |

