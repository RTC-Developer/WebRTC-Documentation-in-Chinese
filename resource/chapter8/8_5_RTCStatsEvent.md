## 8.5 `RTCStatsEvent`

`statsended`事件使用`RTCStatsEvent`。

```java
[ Constructor (DOMString type, RTCStatsEventInit
          eventInitDict), Exposed=Window]
          interface RTCStatsEvent : Event {
            readonly attribute RTCStatsReport report;
          };
```

**构造函数**

`RTCStatsEvent`

**属性**

RTCStatsReport类型的`report`:`report`属性包含RTCStats对象的相应子类的stats对象，给出生命周期结束时受监视对象的统计信息的值。

```java
dictionary RTCStatsEventInit : EventInit {
            required RTCStatsReport report;
          };
```

**字典RTCStatsEventInit成员**

RTCStatsReport类型的`report`，必需的:

包含`RTCStats`对象，为生命周期结束的对象提供统计信息。
