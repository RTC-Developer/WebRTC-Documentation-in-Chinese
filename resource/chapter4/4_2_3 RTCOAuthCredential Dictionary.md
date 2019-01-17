### [4.2.3 RTCOAuthCredential Dictionary](http://w3c.github.io/webrtc-pc/#rtcoauthcredential-dictionary)

The RTCOAuthCredential dictionary is used to describe the OAuth auth credential information which is used by the STUN/TURN client (inside the ICE Agent) to authenticate against a STUN/TURN server, as described in [RFC7635]. Note that the kid parameter is not located in this dictionary, but in RTCIceServer's username member. 

zh:RTCOAuthCredential字典用于描述OAuth auth凭证信息，STUN / TURN客户端（在ICE代理内部）使用该信息对STUN / TURN服务器进行身份验证，如[RFC7635]中所述。请注意，kid参数不在此字典中，而是在RTCIceServer的用户名成员中。

```
dictionary RTCOAuthCredential {
  required DOMString macKey;
  required DOMString accessToken;
};
```

Dictionary RTCOAuthCredential Members

字典RTCOAuthCredential会员

macKey of type DOMString, required:
zh:需要DOMString类型的`macKey`

	 The "mac_key", as described in [RFC7635], Section 6.2, in a base64-url encoded format. It is used in STUN message integrity hash calculation (as the password is used in password based authentication). Note that the OAuth response "key" parameter is a JSON Web Key (JWK) or a JWK encrypted with a JWE format. Also note that this is the only OAuth parameter whose value is not used directly, but must be extracted from the "k" parameter value from the JWK, which contains the needed base64-encoded "mac_key". 
	zh: `mac_key`，如[RFC7635]第6.2节中所述，采用base64-url编码格式。它用于STUN消息完整性哈希计算（因为密码用于基于密码的身份验证）。请注意，OAuth响应“key”参数是JSON Web Key（JWK）或使用JWE格式加密的JWK。另请注意，这是唯一不直接使用其值的OAuth参数，但必须从JWK的“k”参数值中提取，该参数值包含所需的base64编码的“mac_key”。


accessToken of type DOMString, required:
zh:需要DOMString类型的`accessToken`

	 The "access_token", as described in [RFC7635], Section 6.2, in a base64-encoded format. This is an encrypted self-contained token that is opaque to the application. Authenticated encryption is used for message encryption and integrity protection. The access token contains a non-encrypted nonce value, which is used by the Authorization Server for unique mac_key generation. The second part of the token is protected by Authenticated Encryption. It contains the mac_key, a timestamp and a lifetime. The timestamp combined with lifetime provides expiry information; this information describes the time window during which the token credential is valid and accepted by the TURN server.  
	zh: `access_token`，如[RFC7635]第6.2节中所述，采用base64编码格式。这是一个加密的自包含令牌，对应用程序不透明。经过身份验证的加密用于邮件加密和完整性保护。访问令牌包含非加密的nonce值，授权服务器使用该值来生成唯一的mac_key。令牌的第二部分受Authenticated Encryption保护。它包含mac_key，时间戳和生命周期。时间戳与生命周期相结合提供了到期信息;此信息描述了令牌凭证有效并由TURN服务器接受的时间窗口。


An example of an RTCOAuthCredential dictionary is:

zh:RTCOAuthCredential字典的一个示例是：

```

{
  macKey: 'WmtzanB3ZW9peFhtdm42NzUzNG0=',
  accessToken: 'AAwg3kPHWPfvk9bDFL936wYvkoctMADzQ5VhNDgeMR3+ZlZ35byg972fW8QjpEl7bx91YLBPFsIhsxloWcXPhA=='
}
        
```
