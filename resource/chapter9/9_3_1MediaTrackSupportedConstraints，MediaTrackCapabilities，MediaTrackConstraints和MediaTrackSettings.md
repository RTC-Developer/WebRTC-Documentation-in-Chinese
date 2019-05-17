
### 9.3.1 MediaTrackSupportedConstraints, MediaTrackCapabilities, MediaTrackConstraints 和 MediaTrackSettings

[GETUSERMEDIA]概述了`MediaTrackSupportedConstraints`，`MediaTrackCapabilites`，`MediaTrackConstraints`和`MediaTrackSettings`的基础知识。然而，由`RTCPeerConnection`提供的`MediaStreamTrack`的`MediaTrackSettings`只会填充成员，以便通过由`setRemoteDescription`和实际RTP数据应用的远程`RTCSessionDescription`提供数据。这意味着某些成员（例如`facingMode`，`echoCancellation`，`latency`，`deviceId`和`groupId`）将始终缺失。

