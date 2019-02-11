### [4.2.2 RTCIceCredentialType Enum](http://w3c.github.io/webrtc-pc/#rtcicecredentialtype-enum)

```
enum RTCIceCredentialType {
  "password",
  "oauth"
};
```

<table>
	<tr>
		<td colspan="2"> Enumeration description</td>
	</tr>
	<tr>
		<td>password</td>
		<td>The credential is a long-term authentication username and password, as described in [RFC5389], Section 10.2.</td>
	</tr>
	<tr>
		<td> oauth</td>
		<td>
		An OAuth 2.0 based authentication method, as described in [RFC7635].<br> 
<br>
zh:基于OAuth 2.0的身份验证方法，如[RFC7635]中所述。<br>
<br>
For OAuth Authentication, the ICE Agent requires three pieces of credential information. The credential is composed of a kid, which the RTCIceServer username member is used for, and macKey and  accessToken, which are placed in the RTCOAuthCredential dictionary. 
<br>
<br>
zh:对于OAuth身份验证，ICE代理需要三个凭据信息。凭证由用于RTCIceServer用户名成员的kid和用于放置在RTCOAuthCredential字典中的macKey和accessToken组成。
<br>
<br>
 This specification does not define how an application (acting as the OAuth Client) obtains the accessToken, kid and macKey from the Authorization Server, as WebRTC only handles the interaction between the ICE agent and TURN server. For example, the application may use the OAuth 2.0 Implicit Grant type, with PoP (Proof-of-Possession) Token type, as described in [RFC6749] and [OAUTH-POP-KEY-DISTRIBUTION]; an example of this is provided in [RFC7635], Appendix B. 
<br>
<br>
zh: 此规范未定义应用程序（充当OAuth客户端）如何从授权服务器获取accessToken，kid和macKey，因为WebRTC仅处理ICE代理和TURN服务器之间的交互。例如，应用程序可以使用OAuth 2.0 Implicit Grant类型和PoP（Proof-of-Possession）令牌类型，如[RFC6749]和[OAUTH-POP-KEY-DISTRIBUTION]中所述; [RFC7635]附录B中提供了这方面的一个例子。
<br>
<br>
NOTE: The application, acting as the OAuth Client, is responsible for refreshing the credential information and updating the ICE Agent with fresh new credentials before the accessToken expires. The OAuth Client can use the RTCPeerConnection  setConfiguration method to periodically refresh the TURN credentials.
<br><br>
zh: NOTE：作为OAuth客户端的应用程序负责在accessToken到期之前刷新凭据信息并使用新的凭据更新ICE代理。 OAuth客户端可以使用RTCPeerConnection setConfiguration方法定期刷新TURN凭据。
<br>
<br>
The length of the HMAC key (RTCOAuthCredential.macKey) MAY be any integer number of bytes greater than 20 (160 bits).
<br>
<br>
zh:HMAC密钥的长度（RTCOAuthCredential.macKey）可以是大于20（160位）的任何整数字节数。
<br>
<br>
NOTE:According to [RFC7635] Section 4.1, the HMAC key MUST be a symmetric key, as asymmetric keys would result in large access tokens which may not fit in a single STUN message. 
<br>
<br>
zh:NOTE：根据[RFC7635]第4.1节，HMAC密钥必须是对称密钥，因为非对称密钥会导致大的访问令牌，这可能不适合单个STUN消息。
<br>
<br>
NOTE:Currently the STUN/TURN protocols use only SHA-1 and SHA-2 family hash algorithms for Message Integrity Protection, as defined in [RFC5389] Section 15.4, and [STUN-BIS] Section 14.6. 
<br>
<br>
zh:NOTE：目前，STUN / TURN协议仅使用SHA-1和SHA-2系列哈希算法进行消息完整性保护，如[RFC5389]第15.4节和[STUN-BIS]第14.6节中所定义。
</td>
</tr>
</table>
