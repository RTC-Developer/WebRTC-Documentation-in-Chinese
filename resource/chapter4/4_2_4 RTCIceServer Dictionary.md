### [4.2.4 RTCIceServer字典](http://w3c.github.io/webrtc-pc/#rtciceserver-dictionary)

The RTCIceServer dictionary is used to describe the STUN and TURN servers that can be used by the ICE Agent to establish a connection with a peer.

zh:RTCIceServer字典用于描述ICE代理可用于与对等方建立连接的STUN和TURN服务器。

```
dictionary RTCIceServer {
  required (DOMString or sequence<DOMString>) urls;
  DOMString username;
  (DOMString or RTCOAuthCredential) credential;
  RTCIceCredentialType credentialType = "password";
};
```

字典[RTCIceServer](http://w3c.github.io/webrtc-pc/#dom-rtciceserver)成员

urls of type (DOMString or sequence<DOMString>), required:
zh:需要的类型的`URL`（DOMString或序列<DOMString>）

	 STUN or TURN URI(s) as defined in [RFC7064] and [RFC7065] or other URI types. 
	zh: [RFC7064]和[RFC7065]或其他URI类型中定义的STUN或TURN URI。


username of type DOMString:
zh:DOMString类型的`username`

If this RTCIceServer object represents a TURN server, and credentialType is "password", then this attribute specifies the username to use with that TURN server.

zh:如果此RTCIceServer对象表示TURN服务器，并且credentialType为“password”，则此属性指定用于该TURN服务器的用户名。

If this RTCIceServer object represents a TURN server, and credentialType is "oauth", then this attribute specifies the Key ID (kid) of the shared symmetric key, which is shared between the TURN server and the Authorization Server, as described in [RFC7635]. It is an ephemeral and unique key identifier. The kid allows the TURN server to select the appropriate keying material for decryption of the Access-Token, so the key identified by this kid is used in the Authenticated Encryption of the "access_token". The kid value is equal with the OAuth response "kid" parameter, as defined in [RFC7515] Section 4.1.4. 

zh:如果此RTCIceServer对象表示TURN服务器，并且credentialType为“oauth”，则此属性指定共享对称密钥的密钥ID（kid），该密钥在TURN服务器和授权服务器之间共享，如[RFC7635]中所述。它是一个短暂而独特的密钥标识符。孩子允许TURN服务器选择适当的密钥材料来解密Access-Token，因此这个孩子识别的密钥用于“access_token”的Authenticated Encryption。 kid值与OAuth响应“kid”参数相同，如[RFC7515]第4.1.4节中所定义。

credential of type (DOMString or RTCOAuthCredential) :
zh:`credential`（DOMString或RTCOAuthCredential）


If this RTCIceServer object represents a TURN server, then this attribute specifies the credential to use with that TURN server.

zh:如果此RTCIceServer对象表示TURN服务器，则此属性指定要与该TURN服务器一起使用的凭据。

If credentialType is "password", credential is a DOMString, and represents a long-term authentication password, as described in [RFC5389], Section 10.2.

zh:如果credentialType是“password”，则凭证是DOMString，并表示长期验证密码，如[RFC5389]第10.2节中所述。

If credentialType is "oauth", credential is an RTCOAuthCredential, which contains the OAuth access token and MAC key.

zh:如果credentialType是“oauth”，则凭证是RTCOAuthCredential，其中包含OAuth访问令牌和MAC密钥。

credentialType of type RTCIceCredentialType, defaulting to "password":
zh:类型为RTCIceCredentialType的`credentialType`，默认为“password”

If this RTCIceServer object represents a TURN server, then this attribute specifies how credential should be used when that TURN server requests authorization.

zh:如果此RTCIceServer对象表示TURN服务器，则此属性指定在该TURN服务器请求授权时应如何使用凭据。

An example array of RTCIceServer objects is:

zh:RTCIceServer对象的示例数组是：

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
