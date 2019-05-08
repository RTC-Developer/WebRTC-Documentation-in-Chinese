### 5.6.4 RTCIceTransportState枚举

```java
enum RTCIceTransportState {
    "new",
    "checking",
    "connected",
    "completed",
    "disconnected",
    "failed",
    "closed"
};
```

| `RTCIceTransportState`枚举描述 |                                                              |
| ------------------------------ | ------------------------------------------------------------ |
| `new`                          | `RTCIceTransport`正在收集候选者并/或等待被提供远程候选者，并且还未开始校验。 |
| `checking`                     | `RTCIceTransport`已经接收至少一个远程候选者并且正在校验候选者对，或是未发现连接，或是对之前成功的候选者对的校验已经失败。除此之外，它还可能继续收集。 |
| `connected`                    | `RTCIceTransport`已经发现一个可用的连接，但是仍在校验其它候选者对试图找到一个更好的连接。它还可能继续收集并且/或等待另外的远程候选者。如果对正在使用的连接的consent check[RFC7675]失败，并且不存在其它成功的候选者对，那么状态转变为"checking"(如果还存在需要校验的候选者对)，或"disconnected"(如果没有候选者对需要校验，但是对等体仍在收集并且/或等待其它的远程候选者)。 |
| `completed`                    | `RTCIceTransport`已经完成收集，接收到 没有更多远程候选者的指示，完成校验所有候选者对，并且已经发现一个连接。如果对于所有成功的候选者对的consent checks[RFC7675]接连失败，状态转变为"`failed`". |
| `disconnected`                 | ICE代理已经确定当前`RTCIceTransport`的连接丢失。这是一个暂态，在片段网络中可能会间歇触发。确定状态的方式与实现方式相关。例如:丢失正在使用的连接的网络接口，或是接收对STUN请求的响应反复失败。另外，`RTCIceTransport`已经完成校验所有现存候选者对，还没有发现一个连接，但是它仍在收集或等待额外的远程候选者。 |
| `failed`                       | RTCIceTransport已经完成收集，接收了没有更多远程候选者的指示，完成了对所有候选者对的校验，这是最终状态。 |
| `closed`                       | RTCIceTransport已经断开，不再对STUN请求响应。                |

ICE重启导致候选收集和连接检查重新开始，如果在`completed`状态下开始，则转换为`connected`。如果在暂态`disconnected`开始，则会导致转变为`checking`，从而有效的忘记之前丢失的连接。

`failed`和`completed`状态需要一个不再有额外远程候选者的指示。这可以通过调用`addIceCandidate`来实现，其中候选者值的`candidate`属性被设置为空字符串或者通过`canTrickleIceCandidates`被设置为`false`。

一些状态转变的例子包括：

- (`RTCIceTransport`首次创建，作为`setLocalDescription`或`setRemoteDescription`的结果)：`new`
- (`new`,接收远程候选者)：`checking`
- (`checking`，发现可用连接)：`connected`
- (`checking`,校验失败，仍在收集过程)：`disconnected`
- (`checking`,放弃)：`failed`
- (`disconnected`,新的本地候选者)：`checking`
- (`connected`,完成所有校验)：`completed`
- (`completed`,丢失连接)：`disconnected`
- (`disconnected`或`failed`，出现ICE重启)：`checking`
- (`completed`,出现ICE重启)：`connected`
- `RTCPeerConnection.close()`:`closed`

![](/image/5_6_4pic.png)

