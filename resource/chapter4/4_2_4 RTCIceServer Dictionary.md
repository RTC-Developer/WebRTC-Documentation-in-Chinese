### [4.2.4 RTCIceServer字典](http://w3c.github.io/webrtc-pc/#rtciceserver-dictionary)

RTCIceServer 字典用于描述可以被 ICE 代理用于与对等方建立连接的STUN和TURN服务器。

```
dictionary RTCIceServer {
  required (DOMString or sequence<DOMString>) urls;
  DOMString username;
  (DOMString or RTCOAuthCredential) credential;
  RTCIceCredentialType credentialType = "password";
};
```

字典[RTCIceServer](http://w3c.github.io/webrtc-pc/#dom-rtciceserver)成员

`URL`的类型是 DOMString或序列<DOMString>，必填

	zh: [RFC7064]和[RFC7065]或其他URI类型中定义的STUN或TURN URI。

`username`的类型是 DOMString

如果此 RTCIceServer 对象表示 TURN 服务器，并且 credentialType 为 “password”，则此属性指定用于该TURN服务器的用户名。

如果此RTCIceServer对象表示TURN服务器，并且credentialType为“oauth”，则此属性指定共享对称密钥的密钥ID（kid），该密钥在TURN服务器和授权服务器之间共享，如[RFC7635]中所述。它是一个短暂而唯一的密钥标识符。密钥ID（kid）允许TURN服务器选择适当的密钥材料来解密Access-Token，因此这个密钥ID（kid）识别的密钥被用于“access_token”的加密。 kid值与OAuth响应“kid”参数相同，如[RFC7515]第4.1.4节中所定义。

`credential`的类型是 DOMString 或 RTCOAuthCredential

如果此 RTCIceServer 对象表示 TURN 服务器，则此属性是要与该 TURN 服务器一起使用的证书。

如果credentialType是“password”，则证书是DOMString类型，并表示长期验证密码，如[RFC5389]第10.2节中所述。

如果credentialType是“oauth”，则证书是RTCOAuthCredential类型，其中包含OAuth访问令牌和MAC密钥。

`credentialType`的类型是 RTCIceCredentialType，默认为“password”

如果此RTCIceServer对象表示TURN服务器，则此属性指定如何在该 TURN 服务器请求授权时使用证书。

An example array of RTCIceServer objects is:

一个 RTCIceServer 数组的例子：

```

[
  {urls: 'stun:stun1.example.net'},
  {urls: ['turns:turn.example.org', 'turn:turn.example.net'],
    username: 'user',
    credential: 'myPassword',
    credentialType: 'password'},
  {urls: 'turns:turn2.example.net',
    username: '22BIjxU93h/IgwEb',
    credential: {
      macKey: 'WmtzanB3ZW9peFhtdm42NzUzNG0=',
      accessToken: 'AAwg3kPHWPfvk9bDFL936wYvkoctMADzQ5VhNDgeMR3+ZlZ35byg972fW8QjpEl7bx91YLBPFsIhsxloWcXPhA=='
    },
    credentialType: 'oauth'}
];
        
```
