#### [5.4.1.1 编码参数示例](http://w3c.github.io/webrtc-pc/#rtcrtpencodingspatialsim-example*)

本节不具有规范性。

使用编码参数实现的联播场景示例：

```
EXAMPLE 4
// Example of 3-layer spatial simulcast with all but the lowest resolution layer disabled
var encodings = [
  {rid: 'f', active: false},
  {rid: 'h', active: false, scaleResolutionDownBy: 2.0},
  {rid: 'q', active: true, scaleResolutionDownBy: 4.0}
];

// Example of 3-layer framerate simulcast with the middle layer disabled
var encodings = [
  {rid: 'f', active: true, maxFramerate: 60},
  {rid: 'h', active: false, maxFramerate: 30},
  {rid: 'q', active: true, maxFramerate: 15}
];
```
