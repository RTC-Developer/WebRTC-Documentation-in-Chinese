#### 6.1.1.1创建一个实例

为了创建一个可选初始状态的`RTCSctpTransport`，`initialState`，运行下列步骤。

1.让transport成为一个新的`RTCSctpTransport`对象。

2.让transport具有一个[SctpTransportState]内部插槽，初始化为`initialState`，如果提供，否则为`"new"`。

3.让transport具有[MaxMessageSize]内部插槽，运行标记为`update the data max message size`的标签对其初始化。

4.让transport具有[MaxChannels]内部插槽初始化为`null`。

5.返回transport。

