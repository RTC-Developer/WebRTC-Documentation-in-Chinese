#### [6.1.1.1 Create an instance](http://w3c.github.io/webrtc-pc/#create-an-instance)

To create an RTCSctpTransport with an optional initial state, initialState, run the following steps:

zh:要创建具有可选初始状态initialState的RTCSctpTransport，请运行以下步骤：

1.  Let transport be a new  RTCSctpTransport object. 
zh: 让transport成为新的RTCSctpTransport对象。

2.  Let transport have a [[SctpTransportState]] internal slot initialized to initialState, if provided, otherwise "new". 
zh: 让transport有一个[[SctpTransportState]]内部槽初始化为initialState（如果提供），否则为“new”。

3.  Let transport have a [[MaxMessageSize]] internal slot and run the steps labeled update the data max message size to initialize it. 
zh: 让transport有一个[[MaxMessageSize]]内部插槽，并运行标记为update data data message size的步骤来初始化它。

4.  Let transport have a [[MaxChannels]] internal slot initialized to null. 
zh: 让transport将[[MaxChannels]]内部槽初始化为null。

5.  Return transport. 
zh: 回程运输。

