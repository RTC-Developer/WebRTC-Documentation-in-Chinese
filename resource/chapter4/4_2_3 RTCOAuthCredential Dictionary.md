### [4.2.3 RTCOAuthCredential Dictionary](http://w3c.github.io/webrtc-pc/#rtcoauthcredential-dictionary) 

RTCOAuthCredential字典用于描述OAuth auth凭证信息，STUN / TURN 客户端（在 ICE 代理内部）使用该信息对 STUN / TURN 务器进行身份验证，如[RFC7635]中所述。请注意，kid参数不在此字典中，而是在RTCIceServer的成员变量 username 中。

```
dictionary RTCOAuthCredential {
  required DOMString macKey;
  required DOMString accessToken;
};
```

字典RTCOAuthCredential成员

DOMString类型的`macKey`，需要：

	`mac_key`，如[RFC7635]第 6.2 节中所述，采用 base64-url 编码格式。它用于 STUN 消息完整性哈希计算（因为密码用于基于密码的身份验证）。请注意，OAuth 响应“key”参数是 JSON Web Key（JWK）或使用 JWE 格式加密的 JWK 。另请注意，这是唯一不直接使用其值的OAuth参数，但必须从JWK的“k”参数值中提取，该参数值包含所需的base64编码的“mac_key”。

DOMString类型的`accessToken`，需要：

	 `access_token`，如[RFC7635]第6.2节中所述，采用 base64 编码格式。这是一个加密的自包含令牌，对应用程序不透明。认证加密用于消息加密和完整性保护。访问令牌包含非加密的nonce值，授权服务器使用该值来生成唯一的mac_key。令牌的第二部分受认证加密保护。它包含 mac_key ，时间戳和生命周期。时间戳与生命周期相结合提供了到期信息;此信息描述了令牌凭证有效并能被TURN服务器接受的时间窗口。


RTCOAuthCredential字典的一个示例是：

```

{
  macKey: 'WmtzanB3ZW9peFhtdm42NzUzNG0=',
  accessToken: 'AAwg3kPHWPfvk9bDFL936wYvkoctMADzQ5VhNDgeMR3+ZlZ35byg972fW8QjpEl7bx91YLBPFsIhsxloWcXPhA=='
}
        
```
