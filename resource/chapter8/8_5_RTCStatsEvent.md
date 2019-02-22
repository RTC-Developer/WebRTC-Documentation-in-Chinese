## [8.5 RTCStatsEvent zh:8.5 RTCStatsEvent](http://w3c.github.io/webrtc-pc/#rtcstatsevent)

The statsended event uses the RTCStatsEvent.

zh:statsended事件使用RTCStatsEvent。

```
[ Constructor (DOMString type, RTCStatsEventInit
          eventInitDict), Exposed=Window]
          interface RTCStatsEvent : Event {
            readonly attribute RTCStatsReport report;
          };
          
```

**Constructors**

`RTCStatsEvent`

	
**Attributes**

*report* of type RTCStatsReport :
zh:RTCStatsReport类型的报告


The report attribute contains the stats objects of the appropriate subclass of RTCStats object giving the value of the statistics for the monitored objects whose lifetime have ended, at the time that it ended.

zh:report属性包含RTCStats对象的相应子类的stats对象，给出生命周期结束时受监视对象的统计信息的值。

```
dictionary RTCStatsEventInit : EventInit {
            required RTCStatsReport report;
          };
```

**Dictionary RTCStatsEventInit members**

*report* of type RTCStatsReport, required:
zh:RTCStatsReport类型的报告，必需

Contains the RTCStats objects giving the stats for the objects whose lifetime have ended.

zh:包含RTCStats对象，为生命周期结束的对象提供统计信息。
