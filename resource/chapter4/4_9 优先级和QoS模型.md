## [4.9 优先级和QoS模型](http://w3c.github.io/webrtc-pc/#priority-and-qos-model)



许多应用程序中包含多路相同数据类型的媒体流，并且当中的某些媒体流相比于其他媒体流质量更为重要。WebRTC使用了在[RTCWEB-TRANSPORT]和[TSVWG-RTCWEB-QOS]中描述的优先级和服务质量（QoS）框架，来帮助在某些网络环境中标记特定类型数据包的优先级以及差分服务代码点（DSCP），以此来达到提升服务质量的目的。优先级设定可以用来标识不同媒体流的相对优先级。通过调用优先级设置API可以让JavaScript应用程序更改RTCRtpEncodingParameters对象的中priority属性来告诉浏览器特定媒体流的优先级是高，中，低还是非常低，priority属性可以设置为以下值。
