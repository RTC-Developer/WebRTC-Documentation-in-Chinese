### [4.2.6 RTCBundlePolicy 枚举](http://w3c.github.io/webrtc-pc/#rtcbundlepolicy-enum)

As described in [JSEP] (section 4.1.1.), bundle policy affects which media tracks are negotiated if the remote endpoint is not bundle-aware, and what ICE candidates are gathered. If the remote endpoint is bundle-aware, all media tracks and data channels are bundled onto the same transport.

zh:如[JSEP]（第4.1.1节）中所述，如果远程端点不支持bundle，并且收集了哪些ICE候选者，则bundle策略会影响协商哪些媒体轨道。如果远程端点可识别束，则所有媒体轨道和数据通道都捆绑在同一传输上。

```
enum RTCBundlePolicy {
  "balanced",
  "max-compat",
  "max-bundle"
};
```

<table>
  <tr>
    <td colspan="2">
    Enumeration description (non-normative)
    </td>
  </tr>
    <td>
    balanced
    </td>
    <td>
    Gather ICE candidates for each media type in use (audio, video, and data). If the remote endpoint is not bundle-aware, negotiate only one audio and video track on separate transports.
    zh:为正在使用的每种媒体类型（音频，视频和数据）收集ICE候选项。如果远程端点不支持bundle，则在单独的传输上仅协商一个音频和视频轨道。
    </td>
  <tr>
    <td>
    max-compat
    </td>
    <td>
    Gather ICE candidates for each track. If the remote endpoint is not bundle-aware, negotiate all media tracks on separate transports.
    zh:收集每个赛道的ICE候选人。如果远程端点不支持bundle，则在单独的传输上协商所有媒体跟踪。
    </td>
  </tr>
  <tr>
    <td>
    max-bundle
    </td>
    <td>
    Gather ICE candidates for only one track. If the remote endpoint is not bundle-aware, negotiate only one media track.
    zh:只收集一首赛道的ICE候选人。如果远程端点不支持bundle，则仅协商一个媒体轨道。
    </td>
  </tr>
</table>


  
