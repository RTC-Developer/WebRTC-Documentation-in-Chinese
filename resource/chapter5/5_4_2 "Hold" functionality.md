### [5.4.2 "待机" 功能](http://w3c.github.io/webrtc-pc/#hold-functionality)

`direction`属性和`replaceTrack`方法一起使开发人员能够实现“待机”方案。

要将音乐发送给对等方并停止呈现接收的音频（音乐待机）：

```
EXAMPLE 5
async function playMusicOnHold() {
  try {
    // Assume we have an audio transceiver and a music track named musicTrack
    await audio.sender.replaceTrack(musicTrack);
    // Mute received audio
    audio.receiver.track.enabled = false;
    // Set the direction to send-only (requires negotiation)
    audio.direction = 'sendonly';
  } catch (err) {
    console.error(err);
  }
}
```


要响应远程对等方的“sendonly” 提议：

```
EXAMPLE 6
async function handleSendonlyOffer() {
  try {
    // Apply the sendonly offer first,
    // to ensure the receiver is ready for ICE candidates.
    await pc.setRemoteDescription(sendonlyOffer);
    // Stop sending audio
    await audio.sender.replaceTrack(null);
    // Align our direction to avoid further negotiation
    audio.direction = 'recvonly';
    // Call createAnswer and send a recvonly answer
    await doAnswer();
  } catch (err) {
    // handle signaling error
  }
}
```


停止发送音乐并发送从麦克风捕获的音频，以及呈现接收到的音频：

```
EXAMPLE 7
async function stopOnHoldMusic() {
  // Assume we have an audio transceiver and a microphone track named micTrack
  await audio.sender.replaceTrack(micTrack);
  // Unmute received audio
  audio.receiver.track.enabled = true;
  // Set the direction to sendrecv (requires negotiation)
  audio.direction = 'sendrecv';
}
```


响应被远程对等方取消待机：

```
EXAMPLE 8
async function onOffHold() {
  try {
    // Apply the sendrecv offer first, to ensure receiver is ready for ICE candidates.
    await pc.setRemoteDescription(sendrecvOffer);
    // Start sending audio
    await audio.sender.replaceTrack(micTrack);
    // Set the direction sendrecv (just in time for the answer)
    audio.direction = 'sendrecv';
    // Call createAnswer and send a sendrecv answer
    await doAnswer();
  } catch (err) {
    // handle signaling error
  }
}
```
