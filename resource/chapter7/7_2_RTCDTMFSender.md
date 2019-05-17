## 7.2 RTCDTMFSender

为了创建RTCDTMFSender，用户代理必须运行以下步骤：

1. 让dtmf成为最新创建的`RTCDTMFSender`对象。
2. 让dtmf具有[Duration]内部插槽。
3. 让dtmf具有[InterToneGap]内部插槽。
4. 让dtmf具有[ToneBuffer]内部插槽。

```java
[Exposed=Window] interface RTCDTMFSender : EventTarget {
    void insertDTMF (DOMString tones, optional unsigned long duration = 100, optional unsigned long interToneGap = 70);
                    attribute EventHandler ontonechange;
    readonly        attribute boolean      canInsertDTMF;
    readonly        attribute DOMString    toneBuffer;
};
```

**属性**

事件处理程序类型的`ontonechange`:此事件处理程序的事件类型时候tonechange。[测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCDTMFSender-ontonechange-long.https.html)

boolean类型的`canInsertDTMF`,只读：不管`RTCDTMFSender` dtmfSender是否能发送DTMF。当获取时，用户代理必须返回结果，确定是否可以为dtmfSender发送DTMF。

DOMString类型的`toneBuffer`，只读：`toneBuffer`属性必须返回剩余需要播放的tone列表。关于此列表的语法，内容，解释，查看`insertDTMF`。

**方法**

`insertDTMF`：`RTCDTMFSender`对象的`insertDTMF`方法用于发送DTMF音调。

tone参数被视为一系列字符。字符0到9，A到D，`#`和`*`生成相关的DTMF音调。字符a到d必须在输入时标准化为大写，并且等同于A到D.如[RTCWEB-AUDIO]第3节所述，需要支持字符0到9，A到D，＃和*。必须支持字符'，'，并指示在处理tone参数中的下一个字符之前的2秒延迟。所有其他字符（以及仅其他字符）必须被视为无法识别。[测试1](https://github.com/web-platform-tests/wpt/blob/master/webrtc/RTCDTMFSender-insertDTMF.https.html)

持续时间参数指示用于在音调参数中传递的每个字符的持续时间（以毫秒为单位）。持续时间不能超过6000毫秒或小于40毫秒。每种音调的默认持续时间为100 ms。

interToneGap参数表示以ms为单位的音调间隙。用户代理将其钳位至少30毫秒，最多6000毫秒。默认值为70毫秒。

浏览器可以增加持续时间和interToneGap时间，以使DTMF开始和停止的时间与RTP数据包的边界对齐，但它不能增加它们中的任何一个超过单个RTP音频数据包的持续时间。

当调用`insertDTMF（)`方法时，用户代理必须运行以下步骤：

1. 让sender成为用来发送DTMF的`RTCRtpSender`。
2. 让transceiver成为与sender关联的`RTCRtpTransceiver`对象。
3. 如果transceiver的[Stopped]插槽为`true`，抛出`InvalidStateError`。
4. 如果transceiver的[CurrentDirection]插槽为`recvonly`或者`inactive`，抛出`InvalidStateError`。
5. 让dtmf成为与sender关联的`RTCDTMFSender`对象。
6. 如果决定是否可以为drmf发送DTMF返回`false`，抛出`InvalidStateError`。
7. 让tones成为方法的第一个参数。
8. 如果tones包含任意未识别的字符，抛出`InvalidCharacterError`。
9. 设置对象的[ToneBuffer]插槽为tones。
10. 设置dtmf的[Duration]插槽为`duration`参数的值。
11. 设置dtmf的[InterToneGap]插槽为`interToneGap`参数的值。
12. 如果`duration`参数的值小于40毫秒，设置dtmf的[Duration]插槽为40毫秒。
13. 如果`duration`参数的值大于6000 ms，请将dtmf的[[Duration]]插槽设置为6000 ms。
14. 如果`interToneGap`参数的值小于30 ms，则将dtmf的[[InterToneGap]]插槽设置为30 ms。
15. 如果`interToneGap`参数的值大于6000 ms，请将dtmf的[[InterToneGap]]插槽设置为6000 ms。
16. 如果[[ToneBuffer]]插槽为空字符串，则中止这些步骤。
17. 如果计划运行Playout任务，则中止这些步骤;否则运行以下步骤的任务排队（播出任务）：
    1. 如果收发器的[[Stopped]]插槽为真，则中止这些步骤。
    2. 如果收发器的[[CurrentDirection]]插槽是`recvonly`或`inactive`，则中止这些步骤。
    3. 如果[[ToneBuffer]]槽包含空字符串，则使用RTCDTMFToneChangeEvent接口触发名为`tonechange`的事件，并将`tone`属性设置为RTCDTMFSender对象的空字符串并中止这些步骤。
    4. 从[[ToneBuffer]]插槽中删除第一个字符，然后让该字符变为tone。
    5. 如果音调是“，”延迟在相关的RTP媒体流上发送tones 2000毫秒，并为2000毫秒后开始执行的任务排队，此任务运行标记为播出任务的步骤。
    6. 如果音调不是“，”使用适当的编解码器在相关的RTP媒体流上开始播放[[持续时间]] ms的音调，然后将要在[[持续时间]] + [[InterToneGap]] ms中执行的任务排队，此任务运行标记为播出任务的步骤。
    7. 使用`RTCDTMFToneChangeEvent`接口触发名为`tonechange`的事件，并将`tone`属性设置为`RTCDTMFSender`对象的tone。

由于`insertDTMF`替换了音调缓冲区，为了添加正在播放的DTMF音调，必须使用包含剩余音调（存储在[[ToneBuffer]]插槽中）和附加在一起的新音调的字符串调用`insertDTMF`。使用空音调参数调用`insertDTMF`可用于取消在当前播放音调之后排队等待播放的所有音调。
