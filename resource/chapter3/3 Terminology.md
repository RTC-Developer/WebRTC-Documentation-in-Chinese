3. Terminology zh:[3.术语](http://w3c.github.io/webrtc-pc/#terminology)

The EventHandler interface, representing a callback used for event handlers, and the ErrorEvent interface are defined in [HTML51].

zh:表示用于事件处理程序的回调的EventHandler接口和ErrorEvent接口在[HTML51]中定义。

The concepts queue a task and networking task source are defined in [HTML51].

zh:概念队列任务和网络任务源在[HTML51]中定义。

The concept fire an event is defined in [DOM].

zh:触发事件的概念在[DOM]中定义。

The terms event, event handlers and event handler event types are defined in [HTML51].

zh:术语事件，事件处理程序和事件处理程序事件类型在[HTML51]中定义。

performance.timeOrigin and performance.now() are defined in [HIGHRES-TIME].

zh:performance.timeOrigin和performance.now（）在[HIGHRES-TIME]中定义。

The terms serializable objects, serialization steps, and deserialization steps are defined in [HTML].

zh:术语可序列化对象，序列化步骤和反序列化步骤在[HTML]中定义。

The terms MediaStream, MediaStreamTrack, and MediaStreamConstraints are defined in [GETUSERMEDIA]. Note that MediaStream is extended in the MediaStream section in this document while MediaStreamTrack is extended in the MediaStreamTrack section in this document.

zh:术语MediaStream，MediaStreamTrack和MediaStreamConstraints在[GETUSERMEDIA]中定义。请注意，MediaStream在本文档的MediaStream部分中进行了扩展，而MediaStreamTrack在本文档的MediaStreamTrack部分中进行了扩展。

The term Blob is defined in [FILEAPI].

zh:术语Blob在[FILEAPI]中定义。

The term media description is defined in [RFC4566].

zh:术语媒体描述在[RFC4566]中定义。

The term media transport is defined in [RFC7656].

zh:术语媒体传输在[RFC7656]中定义。

The term generation is defined in [TRICKLE-ICE] Section 2.

zh:术语生成在[TRICKLE-ICE]第2节中定义。

The terms RTCStatsType, stats object and monitored object are defined in [WEBRTC-STATS].

zh:术语RTCStatsType，stats对象和被监视对象在[WEBRTC-STATS]中定义。

When referring to exceptions, the terms throw and create are defined in [WEBIDL-1].

zh:在引用异常时，术语throw和create在[WEBIDL-1]中定义。

The term "throw" is used as specified in [INFRA]: it terminates the current processing steps.

zh:术语“throw”按[INFRA]中的规定使用：它终止当前的处理步骤。

The terms fulfilled, rejected, resolved, pending and settled used in the context of Promises are defined in [ECMASCRIPT-6.0].

zh:在Promises的上下文中使用的满足，拒绝，解决，待决和结算的术语在[ECMASCRIPT-6.0]中定义。

The terms bundle, bundle-only and bundle-policy are defined in [JSEP].

zh:术语bundle，bundle-only和bundle-policy在[JSEP]中定义。

The OAuth Client and Authorization Server roles are defined in [RFC6749] Section 1.1.

zh:OAuth客户端和授权服务器角色在[RFC6749]第1.1节中定义。

The terms isolated stream, peeridentity, request an identity assertion and validate the identity are defined in [WEBRTC-IDENTITY].

zh: 术语隔离流，同等性，请求身份断言和验证身份在[WEBRTC-IDENTITY]中定义。

The general principles for Javascript APIs apply, including the principle of run-to-completion and no-data-races as defined in [API-DESIGN-PRINCIPLES]. That is, while a task is running, external events do not influence what's visible to the Javascript application. For example, the amount of data buffered on a data channel will increase due to "send" calls while Javascript is executing, and the decrease due to packets being sent will be visible after a task checkpoint. It is the responsibility of the user agent to make sure the set of values presented to the application is consistent - for instance that getContributingSources() (which is synchronous) returns values for all sources measured at the same time.

zh: 适用Javascript API的一般原则，包括[API-DESIGN-PRINCIPLES]中定义的run-to-completion和no-data-race的原理。也就是说，在任务运行时，外部事件不会影响Javascript应用程序可见的内容。例如，在Javascript执行时，由于“发送”调用，数据通道上缓冲的数据量将增加，并且在任务检查点之后，由于发送的数据包导致的减少将是可见的。用户代理负责确保呈现给应用程序的值集合是一致的 - 例如getContributingSources（）（同步）返回同时测量的所有源的值。
