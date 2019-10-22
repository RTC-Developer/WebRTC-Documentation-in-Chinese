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

基于OAuth 2.0的身份验证方法，如[RFC7635]中所述。
<br>
<br>
对于OAuth身份验证，ICE代理需要三个凭据信息。凭证由用于 kid，macKey 和 accessToken 组成。其中kid用于 RTCIceServer 成员变量，macKey 和 accessToken放置在RTCOAuthCredential字典中的。
<br>
<br>
此规范未定义应用程序（充当OAuth客户端）如何从授权服务器获取accessToken，kid和macKey，因为WebRTC仅处理ICE代理和TURN服务器之间的交互。例如，应用程序可以使用OAuth 2.0 Implicit Grant类型和PoP（Proof-of-Possession）令牌类型，如[RFC6749]和[OAUTH-POP-KEY-DISTRIBUTION]中所述; [RFC7635]附录B中提供了这方面的一个例子。
<br>
<br>
NOTE：作为OAuth客户端的应用程序负责在accessToken到期之前刷新凭据信息并使用新的凭据更新ICE代理。 OAuth客户端可以使用 RTCPeerConnection 的 setConfiguration 方法定期刷新 TURN 凭据。
<br>
<br>
HMAC密钥的长度（RTCOAuthCredential.macKey）可以是大于 20（160位）的任何整数字节数。
<br>
<br>
NOTE：根据[RFC7635]第 4.1 节，HMAC密钥必须是对称密钥，因为非对称密钥会导致大的访问令牌，这可能不适合单个 STUN 消息。
<br>
<br>
NOTE：目前，STUN / TURN 协议仅使用SHA-1和SHA-2系列哈希算法进行消息完整性保护，如[RFC5389]第15.4节和[STUN-BIS]第14.6节中所定义。
</td>
</tr>
</table>
