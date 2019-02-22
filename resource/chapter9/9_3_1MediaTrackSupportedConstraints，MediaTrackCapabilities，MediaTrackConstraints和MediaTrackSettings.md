
### [9.3.1 MediaTrackSupportedConstraints，MediaTrackCapabilities，MediaTrackConstraints和MediaTrackSettings](http://w3c.github.io/webrtc-pc/#mediatracksupportedconstraints-mediatrackcapabilities-mediatrackconstraints-and-mediatracksettings)

The basics of MediaTrackSupportedConstraints, MediaTrackCapabilites, MediaTrackConstraints and MediaTrackSettings is outlined in [GETUSERMEDIA]. However, the MediaTrackSettings for a MediaStreamTrack sourced by an RTCPeerConnection will only be populated with members to the extent that data is supplied by means of the remote RTCSessionDescription applied via setRemoteDescription and the actual RTP data. This means that certain members, such as facingMode, echoCancellation, latency, deviceId and groupId, will always be missing.

zh:[GETUSERMEDIA]概述了MediaTrackSupportedConstraints，MediaTrackCapabilites，MediaTrackConstraints和MediaTrackSettings的基础知识。但是，由RTCPeerConnection提供的MediaStreamTrack的MediaTrackSettings将仅填充成员，以便通过setRemoteDescription应用的远程RTCSessionDescription和实际的RTP数据提供数据。这意味着某些成员（例如facingMode，echoCancellation，latency，deviceId和groupId）将始终缺失。
