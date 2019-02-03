### [4.10.2 RTCCertificate Interface zh:4.10.2 RTCCertificate接口](http://w3c.github.io/webrtc-pc/#rtccertificate-interface)

The RTCCertificate interface represents a certificate used to authenticate WebRTC communications. In addition to the visible properties, internal slots contain a handle to the generated private keying materal ([[KeyingMaterial]]), a certificate ([[Certificate]]) that RTCPeerConnection uses to authenticate with a peer, and the origin ([[Origin]]) that created the object.

zh:RTCCertificate接口表示用于验证WebRTC通信的证书。除了可见属性之外，内部插槽还包含生成的私有密钥子集（[[KeyingMaterial]]）的句柄，RTCPeerConnection用于与对等体进行身份验证的证书（[[Certificate]]）和原点（[[[[Certificate]]） Origin]]）创建了对象。


```
[Exposed=Window,
 Serializable]
interface RTCCertificate {
    readonly attribute DOMTimeStamp expires;
    static sequence<AlgorithmIdentifier> getSupportedAlgorithms();
    sequence<RTCDtlsFingerprint>         getFingerprints();
};
```

**Attributes zh:属性**

expires of type DOMTimeStamp, readonly


he expires attribute indicates the date and time in milliseconds relative to 1970-01-01T00:00:00Z after which the certificate will be considered invalid by the browser. After this time, attempts to construct an RTCPeerConnection using this certificate fail.

zh:expires属性指示相对于1970-01-01T00：00：00Z的日期和时间（以毫秒为单位），之后浏览器将认为证书无效。在此之后，尝试使用此证书构造RTCPeerConnection失败。

Note that this value might not be reflected in a notAfter parameter in the certificate itself.

zh:请注意，此值可能不会反映在证书本身的notAfter参数中。

**Methods zh:方法**

getSupportedAlgorithms

Returns a sequence providing a representative set of supported certificate algorithms. At least one algorithm MUST be returned.

zh:返回提供一组有代表性的支持证书算法的序列。必须返回至少一个算法。

For example, the "RSASSA-PKCS1-v1_5" algorithm dictionary, RsaHashedKeyGenParams, contains fields for the modulus length, public exponent, and hash algorithm. Implementations are likely to support a wide range of modulus lengths and exponents, but a finite number of hash algorithms. So in this case, it would be reasonable for the implementation to return one AlgorithmIdentifier for each supported hash algorithm that can be used with RSA, using default/recommended values for modulusLength and publicExponent (such as 1024 and 65537, respectively).

zh:例如，“RSASSA-PKCS1-v1_5”算法字典RsaHashedKeyGenParams包含模数长度，公共指数和散列算法的字段。实现可能支持各种模数长度和指数，但是有限数量的散列算法。因此，在这种情况下，对于每个支持的可与RSA一起使用的哈希算法，使用modulusLength和publicExponent的默认/推荐值（分别为1024和65537），为实现返回一个AlgorithmIdentifier是合理的。

getFingerprints

Returns the list of certificate fingerprints, one of which is computed with the digest algorithm used in the certificate signature.

zh:返回证书指纹列表，其中一个是使用证书签名中使用的摘要算法计算的。

For the purposes of this API, the [[Certificate]] slot contains unstructured binary data. No mechanism is provided for applications to access the [[KeyingMaterial]] internal slot. Implementations MUST support applications storing and retrieving RTCCertificate objects from persistent storage. In implementations where an RTCCertificate might not directly hold private keying material (it might be stored in a secure module), a reference to the private key can be held in the [[KeyingMaterial]] internal slot, allowing the private key to be stored and used.

zh:出于此API的目的，[[Certificate]]插槽包含非结构化二进制数据。没有为应用程序提供访问[[KeyingMaterial]]内部插槽的机制。实现必须支持从持久存储中存储和检索RTCCertificate对象的应用程序。在RTCCertificate可能不直接保存私人密钥资料（可能存储在安全模块中）的实现中，私钥的引用可以保存在[[KeyingMaterial]]内部插槽中，允许私钥存储和用过的。

RTCCertificate objects are serializable objects [HTML]. Their serialization steps, given value and serialized, are:

zh:RTCCertificate对象是可序列化的对象[HTML]。它们的序列化步骤，给定值和序列化，是：

1. Set serialized.[[Expires]] to the value of value's expires attribute.
zh:将序列化。[[Expires]]设置为value的expires属性的值。

2. Set serialized.[[Certificate]] to a copy of the unstructured binary data in value's [[Certificate]] slot.
zh:将序列化。[[Certificate]]设置为值[[Certificate]]插槽中非结构化二进制数据的副本。

3. Set serialized.[[Origin]] to a copy of the unstructured binary data in value's [[Origin]] 
slot.
zh:将序列化。[[Origin]]设置为值[[Origin]]插槽中非结构化二进制数据的副本。

4. Set serialized.[[KeyingMaterial]] to a serialization of the private keying material represented by value's [[KeyingMaterial]] slot.
zh:将序列化。[[KeyingMaterial]]设置为由值[[KeyingMaterial]]槽表示的私有密钥材料的序列化。

Their deserialization steps, given serialized and value, are:

zh:根据序列化和价值，他们的反序列化步骤是：

1. Initialize value's expires attribute to contain serialized.[[Expires]].
zh:初始化value的expires属性以包含serialized。[[Expires]]。

2. Set value's [[Certificate]] slot to a copy of serialized.[[Certificate]].
zh:将值的[[Certificate]]插槽设置为序列化的副本。[[Certificate]]。

3. Set value's [[Origin]] slot to a copy of serialized.[[Origin]].
zh:将值的[[Origin]]插槽设置为序列化的副本。[[Origin]]。

4. Set value's [[KeyingMaterial]] slot to the private key material resulting from deserializing serialized.[[KeyingMaterial]]
zh:将值的[[KeyingMaterial]]槽设置为序列化反序列化产生的私钥材料。[[KeyingMaterial]]

Supporting structured cloning in this manner allows RTCCertificate instances to be persisted to stores. It also allows instances to be passed to other origins using APIs like postMessage [webmessaging]. However, the object cannot be used by any other origin than the one that originally created it.

zh:以这种方式支持结构化克隆允许将RTCCertificate实例持久化到商店。它还允许使用postMessage [webmessaging]等API将实例传递给其他来源。但是，该对象不能由最初创建它的任何其他来源使用。
