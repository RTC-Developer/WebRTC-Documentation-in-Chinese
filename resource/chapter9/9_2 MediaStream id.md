## [9.2 MediaStream](http://w3c.github.io/webrtc-pc/#mediastream)
### [9.2.1 id](http://w3c.github.io/webrtc-pc/#id)

The id attribute specified in MediaStream returns an id that is unique to this stream, so that streams can be recognized at the remote end of the RTCPeerConnection API.

zh:在MediaStream中指定的id属性返回此流唯一的ID，以便可以在RTCPeerConnection API的远程端识别流。

When a MediaStream is created to represent a stream obtained from a remote peer, the id attribute is initialized from information provided by the remote source.

zh:创建MediaStream以表示从远程对等方获取的流时，将根据远程源提供的信息初始化id属性。

>NOTE
>
>The id of a MediaStream object is unique to the source of the stream, but that does not mean it is not possible to end up with duplicates. For example, the tracks of a locally generated stream could be sent from one user agent to a remote peer using RTCPeerConnection and then sent back to the original user agent in the same manner, in which case the original user agent will have multiple streams with the same id (the locally-generated one and the one received from the remote peer).
>
>zh:MediaStream对象的id对于流的源是唯一的，但这并不意味着不可能最终得到重复项。例如，本地生成的流的轨道可以使用RTCPeerConnection从一个用户代理发送到远程对等，然后以相同的方式发送回原始用户代理，在这种情况下，原始用户代理将具有多个流相同的id（本地生成的id和从远程peer发送的id）。
