# 12 事件总结

本章节不具有规范性。

下列事件触发`RTCDataChannel`对象：

| 事件名称            | 接口                       | 触发当...                                                    |
| ------------------- | -------------------------- | ------------------------------------------------------------ |
| `open`              | Event                      | `RTCDataChannel`对象的底层数据传输已经建立(或重新建立)。     |
| `message`           | MessageEvent[webmessaging] | 成功接收到一条信息。                                         |
| `bufferedamountlow` | Event                      | `RTCDataChannel`对象的`bufferedAmount`从它的`bufferedAmountLowThreshold`阈值降低到小于等于它的`bufferedAmountLowThreshold`阈值。 |
| `error`             | `RTCErrorEvent`            | 数据通道上产生了错误。                                       |
| `close`             | Event                      | `RTCDataChannel`对象的底层数据传输已经关闭。                 |



下列事件触发`RTCPeerConnection`对象：

| 事件名称                   | 接口                             | 触发当...                                                    |
| -------------------------- | -------------------------------- | ------------------------------------------------------------ |
| `track`                    | `RTCTrackEvent`                  | 新进入媒体已经协商好具体的`RTCRtpReceiver`，接收方的track已经被添加到任何相关联的远程媒体流中。 |
| `negotiationneeded`        | Event                            | 浏览器希望通知应用程序需要协商(换句话说，createOffer调用后继续调用setLocalDescription)。 |
| `signalingstatechange`     | Event                            | 发信状态已经改变。这是由于触发了`setLocalDescription`或者`setRemoteDescription`。 |
| `iceconnectionstatechange` | Event                            | `RTCPeerConnection`的ICE连接状态已经改变。                   |
| `icegatheringstatechange`  | Event                            | `RTCPeerConnection`的ICE收集状态已经改变。                   |
| `icecandidate`             | `RTCPeerConnectionIceEvent`      | 一个新的`RTCIceCandidate`对脚本可用。                        |
| `connectionstatechange`    | Event                            | `RTCPeerConnection`连接状态已经改变。                        |
| `icecandidateerror`        | `RTCPeerConnectionIceErrorEvent` | 收集ICE候选者时出现了失败。                                  |
| `datachannel`              | `RTCDataChannelEvent`            | 新的`RTCDataChannel`被分配给脚本，作为其它对等体创建通道的回应。 |
| `isolationchange`          | Event                            | 当`MediaStreamTrack`上的isolated属性改变，新的事件被分配给脚本。 |
| `statsended`               | `RTCStatsEvent`                  | 新的`RTCStatsEvent`被分配给脚本，作为同时删除一个或多个受控对象的回应。 |

下列事件触发`RTCDTMFSender`对象：

| 事件名称     | 接口                     | 触发当...                                                    |
| ------------ | ------------------------ | ------------------------------------------------------------ |
| `tonechange` | `RTCDTMFToneChangeEvent` | `RTCDTMFSender`对象或是刚刚开始播放tone(作为tone属性返回)，或是刚刚结束对`toneBuffer`中的tone的播放(在`tone`属性中作为空值返回)。 |

下列事件触发`RTCIceTransport`对象：

| 事件名称                      | 接口  | 触发当...                                 |
| ----------------------------- | ----- | ----------------------------------------- |
| `statechange`                 | Event | `RTCIceTransport`状态改变。               |
| `gatheringstatechange`        | Event | `RTCIceTransport`收集状态改变。           |
| `selectedcandidatepairchange` | Event | `RTCIceTransport`选定的候选者对发生改变。 |

下列事件触发`RTCDtlsTransport`对象：

| 事件名称      | 接口            | 触发当...                                                    |
| ------------- | --------------- | ------------------------------------------------------------ |
| `statechange` | Event           | `RTCDtlsTransport`状态改变。                                 |
| `error`       | `RTCErrorEvent` | `RTCDtlsTransport`上发生了一个错误(dtls-error或是fingerprint-failure)。 |

下列事件触发`RTCSctpTransport`对象：

| 事件名称      | 接口  | 触发当...                    |
| ------------- | ----- | ---------------------------- |
| `statechange` | Event | `RTCSctpTransport`状态改变。 |

