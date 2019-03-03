3. Terminology zh:[3.术语](http://w3c.github.io/webrtc-pc/#terminology)

The EventHandler interface, representing a callback used for event handlers, and the ErrorEvent interface are defined in [HTML51].

zh:事件处理器接口，代表用于响应事件的回调函数，错误事件的接口定义可以在[HTML51]中找到。

The concepts queue a task and networking task source are defined in [HTML51].

zh:队列任务与网络任务源的概念可以在[HTML51]中找到定义。

The concept fire an event is defined in [DOM].

zh:事件触发的概念可以在[DOM]中找到定义。

The terms event, event handlers and event handler event types are defined in [HTML51].

zh:术语"事件"、"事件处理器"和"事件类型"可以在[HTML51]中找到定义。

performance.timeOrigin and performance.now() are defined in [HIGHRES-TIME].

zh:performance.timeOrigin 和 performance.now() 分别可以在[HIGHRES-TIME]中找到定义。

The terms serializable objects, serialization steps, and deserialization steps are defined in [HTML].

zh:术语"可序列化对象"，"序列化步骤"和"反序列化步骤"可以在[HTML]中找到定义。

The terms MediaStream, MediaStreamTrack, and MediaStreamConstraints are defined in [GETUSERMEDIA]. Note that MediaStream is extended in the MediaStream section in this document while MediaStreamTrack is extended in the MediaStreamTrack section in this document.

zh:术语"MediaStream"，"MediaStreamTrack" 和 "MediaStreamConstraints" 可以在[GETUSERMEDIA]中找到定义。请注意，MediaStream 在本文档的 MediaStream 部分中进行了扩展，而 MediaStreamTrack 在本文档的 MediaStreamTrack 部分中进行了扩展。

The term Blob is defined in [FILEAPI].

zh:术语"Blob"可以在[FILEAPI]中找到定义。

The term media description is defined in [RFC4566].

zh:术语"媒体描述"可以在[RFC4566]中找到定义。

The term media transport is defined in [RFC7656].

zh:术语"媒体传输"可以在[RFC7656]中找到定义。

The term generation is defined in [TRICKLE-ICE] Section 2.

zh:术语"生成"可以在[TRICKLE-ICE]第2节中找到定义。

The terms RTCStatsType, stats object and monitored object are defined in [WEBRTC-STATS].

zh:术语"RTCStatsType"，"stats对象"和"被监控对象"可以在[WEBRTC-STATS]中找到定义。

When referring to exceptions, the terms throw and create are defined in [WEBIDL-1].

zh:在讨论异常时，术语 "throw" 和 "create" 可以在[WEBIDL-1]中找到定义。

The term "throw" is used as specified in [INFRA]: it terminates the current processing steps.

zh:术语 "throw" 按[INFRA]中的规定使用：它会即时终止当前的处理步骤。

The terms fulfilled, rejected, resolved, pending and settled used in the context of Promises are defined in [ECMASCRIPT-6.0].

zh:在Promises的上下文中使用的满足，拒绝，解决，待决和结算的术语可以在[ECMASCRIPT-6.0]中找到定义。

The terms bundle, bundle-only and bundle-policy are defined in [JSEP].

zh:术语"bundle"，"bundle-only"和"bundle-policy"可以在[JSEP]中找到定义。

The OAuth Client and Authorization Server roles are defined in [RFC6749] Section 1.1.

zh:OAuth客户端和授权服务器角色可以在[RFC6749]第1.1节中找到定义。

The terms isolated stream, peeridentity, request an identity assertion and validate the identity are defined in [WEBRTC-IDENTITY].

zh: 术语"隔离流"，"同等性"，"请求身份断言"和"验证身份"可以在[WEBRTC-IDENTITY]中找到定义。

The general principles for Javascript APIs apply, including the principle of run-to-completion and no-data-races as defined in [API-DESIGN-PRINCIPLES]. That is, while a task is running, external events do not influence what's visible to the Javascript application. For example, the amount of data buffered on a data channel will increase due to "send" calls while Javascript is executing, and the decrease due to packets being sent will be visible after a task checkpoint. It is the responsibility of the user agent to make sure the set of values presented to the application is consistent - for instance that getContributingSources() (which is synchronous) returns values for all sources measured at the same time.

zh: 本文档遵循基本的 Javascript 接口原则，包括[API-DESIGN-PRINCIPLES]中定义的 run-to-completion 和 no-data-race 的原则。也就是说，在任务运行时，外部事件不会影响 Javascript 应用程序可见的内容。例如，在执行 JavaScript 应用时，数据通道上缓冲的数据量将因为"发送"的调用增加，而由于数据发送成功导致的数据通道上缓冲数据量的减少，只有在这个任务的检查点之后才能观察到。用户端需要确保在这一刻展现给应用的数值是恒定不变的 - 例如同一时间内 getContributingSources（）（同步调用）返回的值。
