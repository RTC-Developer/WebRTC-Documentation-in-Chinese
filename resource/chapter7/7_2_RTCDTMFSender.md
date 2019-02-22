## [7.2 RTCDTMFSender zh:7.2 RTCDTMFSender](http://w3c.github.io/webrtc-pc/#rtcdtmfsender)

To create an RTCDTMFSender, the user agent MUST run the following steps:

zh:要创建RTCDTMFSender，用户代理必须运行以下步骤：

1.  Let dtmf be a newly created RTCDTMFSender object. 
zh: 让dtmf成为新创建的RTCDTMFSender对象。

2.  Let dtmf have a [[Duration]] internal slot. 
zh: 让dtmf有一个[[Duration]]内部插槽。

3.  Let dtmf have a [[InterToneGap]] internal slot. 
zh: 让dtmf有一个[[InterToneGap]]内部插槽。

4.  Let dtmf have a [[ToneBuffer]] internal slot. 
zh: 让dtmf有一个[[ToneBuffer]]内部插槽。

```
[Exposed=Window] interface RTCDTMFSender : EventTarget {
    void insertDTMF (DOMString tones, optional unsigned long duration = 100, optional unsigned long interToneGap = 70);
                    attribute EventHandler ontonechange;
    readonly        attribute boolean      canInsertDTMF;
    readonly        attribute DOMString    toneBuffer;
};

```

**Attributes**

*ontonechange* of type EventHandler:
zh:EventHandler类型的ontonechange

The event type of this event handler is tonechange.

zh:此事件处理程序的事件类型是tonechange。

*canInsertDTMF* of type boolean, readonly:
zh:canInsertDTMF类型为boolean，readonly

Whether the RTCDTMFSender dtmfSender is capable of sending DTMF. On getting, the user agent MUST return the result of running determine if DTMF can be sent for dtmfSender.

zh:RTCDTMFSender dtmfSender是否能够发送DTMF。获取时，用户代理必须返回运行结果，确定是否可以为dtmfSender发送DTMF。

*toneBuffer* of type DOMString, readonly:
zh:DOMString类型的toneBuffer，readonly

The toneBuffer attribute MUST return a list of the tones remaining to be played out. For the syntax, content, and interpretation of this list, see insertDTMF.

zh:toneBuffer属性必须返回剩余要播放的音调列表。有关此列表的语法，内容和解释，请参阅insertDTMF。

**Methods**

`insertDTMF`

An RTCDTMFSender object's insertDTMF method is used to send DTMF tones.

zh:RTCDTMFSender对象的insertDTMF方法用于发送DTMF音调。

The tones parameter is treated as a series of characters. The characters 0 through 9, A through D, #, and * generate the associated DTMF tones. The characters a to d MUST be normalized to uppercase on entry and are equivalent to A to D. As noted in [RTCWEB-AUDIO] Section 3, support for the characters 0 through 9, A through D, #, and * are required. The character ',' MUST be supported, and indicates a delay of 2 seconds before processing the next character in the tones parameter. All other characters (and only those other characters) MUST be considered unrecognized.

zh:tone参数被视为一系列字符。字符0到9，A到D，＃和*生成相关的DTMF音调。字符a到d必须在输入时标准化为大写，并且等同于A到D.如[RTCWEB-AUDIO]第3节所述，需要支持字符0到9，A到D，＃和*。必须支持字符'，'，并指示在处理tone参数中的下一个字符之前的2秒延迟。所有其他字符（以及仅其他字符）必须被视为无法识别。

The duration parameter indicates the duration in ms to use for each character passed in the tones parameters. The duration cannot be more than 6000 ms or less than 40 ms. The default duration is 100 ms for each tone.

zh:持续时间参数指示用于在音调参数中传递的每个字符的持续时间（以毫秒为单位）。持续时间不能超过6000毫秒或小于40毫秒。每种音调的默认持续时间为100 ms。

The interToneGap parameter indicates the gap between tones in ms. The user agent clamps it to at least 30 ms and at most 6000 ms. The default value is 70 ms.

zh:interToneGap参数表示以ms为单位的音调间隙。用户代理将其钳位至少30毫秒，最多6000毫秒。默认值为70毫秒。

The browser MAY increase the duration and interToneGap times to cause the times that DTMF start and stop to align with the boundaries of RTP packets but it MUST not increase either of them by more than the duration of a single RTP audio packet.

zh:浏览器可以增加持续时间和interToneGap时间，以使DTMF开始和停止的时间与RTP数据包的边界对齐，但它不能增加它们中的任何一个超过单个RTP音频数据包的持续时间。

When the insertDTMF() method is invoked, the user agent MUST run the following steps:

zh:当调用insertDTMF（）方法时，用户代理必须运行以下步骤：

1. Let sender be the RTCRtpSender used to send DTMF.
zh:让发件人成为用于发送DTMF的RTCRtpSender。

2.  Let transceiver be the RTCRtpTransceiver object associated with sender. 
zh: 让收发器成为与发送者关联的RTCRtpTransceiver对象。

3. If transceiver's [[Stopped]] slot is true, throw an InvalidStateError.
zh:如果收发器的[[Stopped]]插槽为true，则抛出InvalidStateError。

4. If transceiver's [[CurrentDirection]] slot is recvonly or inactive, throw an InvalidStateError.
zh:如果收发器的[[CurrentDirection]]插槽是recvonly或非活动状态，则抛出InvalidStateError。

5. Let dtmf be the RTCDTMFSender associated with sender.
zh:让dtmf成为与发件人关联的RTCDTMFSender。

6. If determine if DTMF can be sent for dtmf returns false, throw an InvalidStateError.
zh:如果确定是否可以发送DTMF以使dtmf返回false，则抛出InvalidStateError。

7. Let tones be the method's first argument.
zh:让音调成为方法的第一个参数。

8. If tones contains any unrecognized characters, throw an InvalidCharacterError. 
zh:如果音调包含任何无法识别的字符，则抛出InvalidCharacterError。

9. Set the object's [[ToneBuffer]] slot to tones.
zh:将对象的[[ToneBuffer]]插槽设置为音调。

10. Set dtmf's [[Duration]] slot to the value of the duration parameter.
zh:将dtmf的[[Duration]]槽设置为duration参数的值。

11. Set dtmf's [[InterToneGap]] slot to the value of the interToneGap parameter.
zh:将dtmf的[[InterToneGap]]槽设置为interToneGap参数的值。

12. If the value of the duration parameter is less than 40 ms, set dtmf's [[Duration]] slot to 40 ms.
zh:如果duration参数的值小于40 ms，请将dtmf的[[Duration]]插槽设置为40 ms。

13. If the value of the duration parameter is greater than 6000 ms, set dtmf's [[Duration]] slot to 6000 ms.
zh:如果duration参数的值大于6000 ms，请将dtmf的[[Duration]]插槽设置为6000 ms。

14. If the value of the interToneGap parameter is less than 30 ms, set dtmf's [[InterToneGap]] slot to 30 ms.
zh:如果interToneGap参数的值小于30 ms，则将dtmf的[[InterToneGap]]插槽设置为30 ms。

15. If the value of the interToneGap parameter is greater than 6000 ms, set dtmf's [[InterToneGap]] slot to 6000 ms.
zh:如果interToneGap参数的值大于6000 ms，请将dtmf的[[InterToneGap]]插槽设置为6000 ms。

16. If [[ToneBuffer]] slot is an empty string, abort these steps.
zh:如果[[ToneBuffer]]插槽为空字符串，则中止这些步骤。

17. If a Playout task is scheduled to be run, abort these steps; otherwise queue a task that runs the following steps (Playout task):  
zh:如果计划运行Playout任务，则中止这些步骤;否则运行以下步骤的任务排队（播出任务）：

	1. If transceiver's [[Stopped]] slot is true, abort these steps.
	zh:如果收发器的[[已停止]]插槽为真，则中止这些步骤。
	
	2. If transceiver's [[CurrentDirection]] slot is recvonly or inactive, abort these steps.
zh:如果收发器的[[CurrentDirection]]插槽是recvonly或非活动状态，则中止这些步骤。

	3. If the [[ToneBuffer]] slot contains the empty string, fire an event named tonechange using the RTCDTMFToneChangeEvent interface with the tone attribute set to an empty string at the RTCDTMFSender object and abort these steps.
zh:如果[[ToneBuffer]]槽包含空字符串，则使用RTCDTMFToneChangeEvent接口触发名为tonechange的事件，并将音调属性设置为RTCDTMFSender对象的空字符串并中止这些步骤。

	4. Remove the first character from the [[ToneBuffer]] slot and let that character be tone.
zh:从[[ToneBuffer]]插槽中删除第一个字符，然后让该字符变为音调。

	5. If tone is "," delay sending tones for 2000 ms on the associated RTP media stream, and queue a task to be executed in 2000 ms from now that runs the steps labelled Playout task.
zh:如果音调是“，”延迟在相关的RTP媒体流上发送2000毫秒的音调，并将从现在开始执行标记为播出任务的步骤的2000毫秒的任务排队。

	6. If tone is not "," start playout of tone for [[Duration]] ms on the associated RTP media stream, using the appropriate codec, then queue a task to be executed in [[Duration]] + [[InterToneGap]] ms from now that runs the steps labelled Playout task.
zh:如果音调不是“，”使用适当的编解码器在相关的RTP媒体流上开始播放[[持续时间]] ms的音调，然后将要在[[持续时间]] + [[InterToneGap]] ms中执行的任务排队从现在开始运行标记为Playout task的步骤。

	7. Fire an event named tonechange using the RTCDTMFToneChangeEvent interface with the tone attribute set to tone at the RTCDTMFSender object.
zh:使用RTCDTMFToneChangeEvent接口触发名为tonechange的事件，并将音调属性设置为RTCDTMFSender对象的音调。

Since insertDTMF replaces the tone buffer, in order to add to the DTMF tones being played, it is necessary to call insertDTMF with a string containing both the remaining tones (stored in the [[ToneBuffer]] slot) and the new tones appended together. Calling insertDTMF with an empty tones parameter can be used to cancel all tones queued to play after the currently playing tone.

zh:由于insertDTMF替换了音调缓冲区，为了添加正在播放的DTMF音调，必须使用包含剩余音调（存储在[[ToneBuffer]]插槽中）和附加在一起的新音调的字符串调用insertDTMF。使用空音调参数调用insertDTMF可用于取消在当前播放音调之后排队等待播放的所有音调。