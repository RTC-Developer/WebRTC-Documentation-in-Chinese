# 《WebRTC 官方文档-中文版》贡献历史

|章节|贡献者 认领者|进度（审校or完成）|
|---|---|---|---|
|1 介绍| plutoless|审校|
|2 一致性| plutoless|审校|
|3 术语 | plutoless|审校|
|4.1 点对点连接| yusicheng|审校|
|4.2.1 RTCConfiguration字典 | yusicheng|审校|
|4.2.2 RTCIceCredentialType 枚举 | yusicheng|审校|
|4.2.3 RTCOAuthCredential Dictionary| yusicheng|审校|
|4.2.4 RTCIceServer字典| yusicheng|审校|
|4.2.5 RTCIceTransportPolicy 枚举| yusicheng|审校|
|4.2.6 RTCBundlePolicy 枚举| yusicheng|审校|
|4.2.7 RTCRtcpMuxPolicy 枚举| yusicheng|审校|
|4.2.8 Offer/answer option 提供、应答选项| yusicheng|审校|
|4.3.1 RTCSignalingState 枚举| yusicheng|审校|
|4.3.2 RTCIceGatheringState 枚举| yusicheng|审校|
|4.3.3 RTCPeerConnectionState 枚举| yusicheng|审校|
|4.3.4 RTCIceConnectionState 枚举| yusicheng|审校|
|4.4 RTCPeerConnection 接口| yusicheng|审校|
|4.4.1 操作| yusicheng|审校|
|4.4.1.1 构造函数| yusicheng|审校|
|4.4.1.2 将操作排入队列| yusicheng|审校|
|4.4.1.3 更新连接状态| yusicheng|审校|
|4.4.1.4 更新 ICE 收集状态| yusicheng|审校|
|4.4.1.5 更新 ICE 连接状态| yusicheng|审校|
|4.4.1.6 设置 RTCSessionDescription| yusicheng|审校|
|4.4.2 接口定义| yusicheng|审校|
|4.4.3 旧接口扩展| yusicheng|审校|
|4.4.3.1方法扩展| yusicheng|审校|
|4.4.3.2 旧版配置扩展| yusicheng|审校|
|4.4.4 垃圾回收| yusicheng|审校|
|4.5 错误处理| neo|审校|
|4.6 会话描述类型| neo|审校|
|4.6.2 RTCSessionDescription 类| neo|审校|
|4.7 会话谈判模型| neo|审校|
|4.7.1 Setting Negotiation-Needed zh:4.7.1设置协商需要| neo|审校|
|4.7.2 Clearing Negotiation-Needed| neo|审校|
|4.7.3 Updating the Negotiation-Needed flag| neo|审校|
|4.8 连接建立接口| neo|审校|
|4.8.1.1 候选属性语法| neo|审校|
|4.8.1.2 RTCIceProtocol枚举| neo|审校|
|4.8.1.3 RTCIceTcpCandidateType枚举| neo|审校|
|4.8.1.4 RTCIceCandidateType枚举| neo|审校|
|4.8.2 RTCPeerConnectionIceEvent| neo|审校|
|4.8.3 RTCPeerConnectionIceErrorEvent| neo|审校|
|4.9优先级和QoS模型| maojie|审校|
|4.9.1 RTCPriorityType枚举| maojie|审校|
|5. RTP Media API | Gong|审校|
|5.1 RTCPeerConnection Interface Extensions| liaojun||
|5.1.1 Processing Remote MediaStreamTracks| liaojun||
|5.2 RTCRtpSender Interface|潘|审校|
|5.2.1 RTCRtpParameters Dictionary|潘|审校|
|5.2.2 RTCRtpSendParameters Dictionary|潘|审校|
|5.2.3 RTCRtpReceiveParameters Dictionary|潘|审校|
|5.2.4 RTCRtpCodingParameters Dictionary|潘|审校|
|5.2.5 RTCRtpDecodingParameters Dictionary|潘|审校|
|5.2.6 RTCRtpEncodingParameters Dictionary|潘|审校|
|5.2.7 RTCDtxStatus Enum|潘|审校|
|5.2.8 RTCDegradationPreference Enum|潘|审校|
|5.2.9 RTCRtcpParameters Dictionary|潘|审校|
|5.2.10 RTCRtpHeaderExtensionParameters Dictionary|潘|审校|
|5.2.11 RTCRtpCodecParameters Dictionary|潘|审校|
|5.2.12 RTCRtpCapabilities Dictionary|潘|审校|
|5.2.13 RTCRtpCodecCapability Dictionary|潘|审校|
|5.2.14 RTCRtpHeaderExtensionCapability Dictionary|潘|审校|
|5.3 RTCRtpReceiver Interface|arthurwufeng|审校|
|5.4 RTCRtpTransceiver Interface|arthurwufeng|审校|
|5.4.1 Simulcast functionality|arthurwufeng|审校|
|5.4.1.1 Encoding Parameter Examples|arthurwufeng|审校|
|5.4.2 "Hold" functionality|arthurwufeng|审校|
|5.5 RTCDtlsTransport Interface|||
|5.5.1RTCDtlsFingerprint Dictionary|||
|5.6RTCIceTransport Interface|||
|5.6.1 RTCIceParameters Dictionary|||
|5.6.2 RTCIceCandidatePair Dictionary|||
|5.6.3 RTCIceGathererState Enum|||
|5.6.4 RTCIceTransportState Enum|||
|5.6.5 RTCIceRole Enum|||
|5.6.6 RTCIceComponent Enum|||
|5.7 RTCTrackEvent|||
|6. Peer-to-peer Data API|||
|6.1 RTCPeerConnection Interface Extensions|||
|6.1.1 RTCSctpTransport Interface|||
|6.1.1.1 Create an instance|||
|6.1.1.2 Update max message size|||
|6.1.1.3 Connected procedure|||
|6.1.2 RTCSctpTransportState Enum|||
|6.2 RTCDataChannel|||
|6.3 RTCDataChannelEvent|||
|6.4 Garbage Collection|||
|7. Peer-to-peer DTMF|||
|7.1 RTCRtpSender Interface Extensions|||
|7.2 RTCDTMFSender|||
|7.3 canInsertDTMF algorithm|||
|7.4 RTCDTMFToneChangeEvent|||
|8.1 Statistics Model|||
|8.2 RTCPeerConnection Interface Extensions|||
|8.3 RTCStatsReport Object|||
|8.4 RTCStats Dictionary|||
|8.5 RTCStatsEvent|||
|8.6 The stats selection algorithm|||
|8.7 Mandatory To Implement Stats|||
|8.8 GetStats Example|||
|9.1 Media Stream API Extensions for Network Use|||
|9.2 MediaStream|||
|9.3 MediaStreamTrack|||
|9.3.1 MediaTrackSupportedConstraints, MediaTrackCapabilities, MediaTrackConstraints and MediaTrackSettings|||
|10. 示例和呼叫流程|||
|待上传11、12、13章节|||
