### [5.4.2 "Hold" functionality](http://w3c.github.io/webrtc-pc/#hold-functionality)

Together, the direction attribute and the replaceTrack method enable developers to implement "hold" scenarios.

zh:direction属性和replaceTrack方法一起使开发人员能够实现“保持”方案。

To send music to a peer and cease rendering received audio (music-on-hold):

zh:要将音乐发送给对等方并停止呈现接收的音频（音乐保留）：

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


To respond to a remote peer's "sendonly" offer:

zh:要响应远程对等方的“sendonly”优惠：

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


To stop sending music and send audio captured from a microphone, as well to render received audio:

zh:停止发送音乐并发送从麦克风捕获的音频，以及呈现接收到的音频：

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


To respond to being taken off hold by a remote peer:

zh:响应被远程对等方取消：

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