### 5.2.8 `RTCDegradationPreference`枚举

```java
enum RTCDegradationPreference {
    "maintain-framerate",
    "maintain-resolution",
    "balanced"
};
```

| RTCDegradationPreference枚举描述 |                                  |
| -------------------------------- | -------------------------------- |
| `maintain-framerate`             | 降低分辨率以便维持帧率。         |
| `maintain-resolution`            | 降低帧率以便维持分辨率。         |
| `balanced`                       | 在降低帧率和分辨率之间保持平衡。 |

