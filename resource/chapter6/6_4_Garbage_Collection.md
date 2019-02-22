## [6.4 Garbage Collection](http://w3c.github.io/webrtc-pc/#garbage-collection-0)

An RTCDataChannel object MUST not be garbage collected if its

zh:如果一个RTCDataChannel对象不能被垃圾收集

*  [[ReadyState]] slot is connecting and at least one event listener is registered for open events, message events, error events, or close events. 
zh: [[ReadyState]]插槽正在连接，并且至少有一个事件侦听器已注册打开事件，消息事件，错误事件或关闭事件。

*  [[ReadyState]] slot is open and at least one event listener is registered for message events, error events, or close events. 
zh: [[ReadyState]]插槽已打开，并且至少为消息事件，错误事件或关闭事件注册了一个事件侦听器。

*  [[ReadyState]] slot is closing and at least one event listener is registered for error events, or close events. 
zh: [[ReadyState]]插槽正在关闭，并且至少有一个事件侦听器已注册错误事件或关闭事件。

*  underlying data transport is established and data is queued to be transmitted. 
zh: 建立基础数据传输并将数据排队等待传输。
