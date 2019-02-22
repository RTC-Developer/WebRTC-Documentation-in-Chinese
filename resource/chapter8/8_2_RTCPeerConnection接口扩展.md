## [8.2 RTCPeerConnection Interface Extensions zh:8.2 RTCPeerConnection接口扩展](http://w3c.github.io/webrtc-pc/#rtcpeerconnection-interface-extensions-1)

The Statistics API extends the RTCPeerConnection interface as described below.

zh:Statistics API扩展了RTCPeerConnection接口，如下所述。

```
partial interface RTCPeerConnection {
    Promise<RTCStatsReport> getStats (optional MediaStreamTrack? selector = null);
    attribute EventHandler onstatsended;
          };
```

**Attributes**

*onstatsended* of type EventHandler:
zh:onstatsended类型为EventHandler

The event type of this event handler is statsended. 

zh:此事件处理程序的事件类型是statsended。

To delete stats for a set of monitored objects associated with an RTCPeerConnection, connection, the UA MUST run the following steps in parallel:

zh:要删除与RTCPeerConnection连接关联的一组受监视对象的统计信息，UA必须并行运行以下步骤：

1.  Gather stats only for the set of monitored objects to be deleted. These stats MUST represent final values at the time of deletion. Stats for these monitored objects MUST NOT appear in subsequent calls to getStats(). 
zh: 仅为要删除的受监视对象集合收集统计信息。这些统计数据必须代表删除时的最终值。这些受监视对象的统计信息不得出现在后续的getStats（）调用中。

2.  Queue a task that runs the following steps:  Let report be a new RTCStatsReport object. For each monitored object, create a new relevant stats object object with the stats gathered above for that monitored object, and add it to report.   Fire an event named statsended using the RTCStatsEvent interface with the report attribute set to report at connection.   
zh: 对运行以下步骤的任务进行排队：让报告成为新的RTCStatsReport对象。对于每个受监视对象，使用上面针对该受监视对象收集的统计信息创建新的相关统计信息对象对象，并将其添加到报告中。使用RTCStatsEvent接口触发名为statsended的事件，并将报告属性设置为在连接时报告。

3. Let report be a new RTCStatsReport object.
zh:让report成为一个新的RTCStatsReport对象。

4. For each monitored object, create a new relevant stats object object with the stats gathered above for that monitored object, and add it to report. 
zh:对于每个受监视对象，使用上面针对该受监视对象收集的统计信息创建新的相关统计信息对象对象，并将其添加到报告中。

5.  Fire an event named statsended using the RTCStatsEvent interface with the report attribute set to report at connection. 
zh: 使用RTCStatsEvent接口触发名为statsended的事件，并将报告属性设置为在连接时报告。

**Methods**

`getStats`

Gathers stats for the given selector and reports the result asynchronously.

zh:收集给定选择器的统计信息并异步报告结果。

When the  getStats() method is invoked, the user agent MUST run the following steps:

zh:当调用getStats（）方法时，用户代理必须运行以下步骤：

1.  Let selectorArg be the method's first argument. 
zh: 让selectorArg成为方法的第一个参数。
2.  Let connection be the RTCPeerConnection object on which the method was invoked. 
zh: 让connection成为调用方法的RTCPeerConnection对象。
3.  If selectorArg is null, let selector be null. 
zh: 如果selectorArg为null，则让selector为null。
4.  If selectorArg is a MediaStreamTrack let selector be an RTCRtpSender or RTCRtpReceiver on connection which track member matches selectorArg. If no such sender or receiver exists, or if more than one sender or receiver fit this criteria, return a promise rejected with a newly created InvalidAccessError. 
zh: 如果selectorArg是MediaStreamTrack，则let选择器是连接上的RTCRtpSender或RTCRtpReceiver，哪个跟踪成员匹配selectorArg。如果不存在此类发件人或收件人，或者如果多个发件人或收件人符合此条件，则返回使用新创建的InvalidAccessError拒绝的承诺。
5.  Let p be a new promise. 
zh: 让p成为新的承诺。
6.  Run the following steps in parallel:   
zh: 并行运行以下步骤：
	1.  Gather the stats indicated by selector according to the stats selection algorithm. 
	zh: 根据统计选择算法收集选择器指示的统计数据。
	2.  Resolve p with the resulting RTCStatsReport object, containing the gathered stats. 
zh: 使用生成的RTCStatsReport对象解析p，其中包含收集的统计信息。
7.  Return p. 
zh: 返回p。