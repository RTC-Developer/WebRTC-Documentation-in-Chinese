### [4.2.6 RTCBundlePolicy 枚举](http://w3c.github.io/webrtc-pc/#rtcbundlepolicy-enum)

如[JSEP]（第4.1.1节）中所述，如果远程端点不支持bundle策略，会影响协商哪些媒体轨道的协商，以及会收集那些 ICE 候选地址。如果远端支持 bundle 策略，则所有媒体轨道和数据通道都捆绑在同一传输路径上。

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
    为正在使用的每种媒体类型（音频，视频和数据）收集 ICE 候选地址。如果远程端点不支持 bundle 策略，则在一个传输路径上仅协商一个音频和视频轨道。
    </td>
  <tr>
    <td>
    max-compat
    </td>
    <td>
    收集每个媒体轨道的 ICE 候选地址。如果远程端点不支持 bundle，则在一个传输路径上协商所有媒体轨道。
    </td>
  </tr>
  <tr>
    <td>
    max-bundle
    </td>
    <td>
    只收集一个媒体轨道的 ICE 候选地址。如果远程端点不支持 bundle 策略，则仅协商一个媒体轨道。
    </td>
  </tr>
</table>


  
