## 8.2 RTCPeerConnection接口扩展

统计API对RTCPeerConnection接口的扩展如下。

```java
partial interface RTCPeerConnection {
    Promise<RTCStatsReport> getStats (optional MediaStreamTrack? selector = null);
    attribute EventHandler onstatsended;
          };
```

**属性**

事件处理程序类型的`onstatsended`:

此事件处理程序的事件类型是`statsended`。

为了删除与一个`RTCPeerConnection`，connection相关联的一系列被监控对象的统计信息，用户代理必须并行运行以下步骤：

1. 收集将要删除的一系列被监控对象的统计信息。这些信息必须代表删除时的最终值。这些信息不能出现在接下来对getStats()的调用中。
2. 对运行以下步骤的任务进行排队：
   1. 让report成为新的`RTCStatsReport`对象。
   2. 对于每个受监视对象，使用上面针对该受监视对象收集的统计信息创建新的相关统计信息对象对象，并将其添加到报告中。
   3. 使用`RTCStatsEvent`接口发起一个名为`statsended`的事件，在connection将`report`属性设置为report。

**方法**

`getStats`

收集给定选择器的统计信息并异步报告结果。

当调用`getStats（）`方法时，用户代理必须运行以下步骤：

1. 让selectorArg成为方法的第一个参数。
2. 让connection成为调用方法的`RTCPeerConnection`对象。
3. 如果selectorArg为`null`，则让selector为`null`。
4. 如果selectorArg是MediaStreamTrack，让选择器成为connection上的`RTCRtpSender`或`RTCRtpReceiver`，并且connection的`track`成员匹配selectorArg。如果不存在此类发件人或收件人，或者如果多个发件人或收件人符合此条件，则返回承诺，拒绝条件是新创建`InvalidAccessError`。
5. 让p成为新的承诺。
6. 并行运行以下步骤：
   1. 根据统计选择算法收集选择器指示的统计数据。
   2. 使用生成的`RTCStatsReport`对象解析p，其中包含收集的统计信息。
7. 返回p。

