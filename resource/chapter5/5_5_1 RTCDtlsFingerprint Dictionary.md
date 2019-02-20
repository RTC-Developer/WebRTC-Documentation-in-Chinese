### [5.5.1 RTCDtlsFingerprint Dictionary](http://w3c.github.io/webrtc-pc/#rtcdtlsfingerprint)

The RTCDtlsFingerprint dictionary includes the hash function algorithm and certificate fingerprint as described in [RFC4572].

zh:RTCDtlsFingerprint字典包括[RFC4572]中描述的散列函数算法和证书指纹。

```
dictionary RTCDtlsFingerprint {
             DOMString algorithm;
             DOMString value;
};
```

**Dictionary RTCDtlsFingerprint Members**

*algorithm* of type DOMString:
zh:DOMString类型的算法

One of the the hash function algorithms defined in the 'Hash function Textual Names' registry [IANA-HASH-FUNCTION].

zh:“哈希函数文本名称”注册表[IANA-HASH-FUNCTION]中定义的哈希函数算法之一。

*value* of type DOMString:
zh:DOMString类型的值

The value of the certificate fingerprint in lowercase hex string as expressed utilizing the syntax of 'fingerprint' in [RFC4572] Section 5.

zh:使用[RFC4572]第5节中“指纹”的语法表示的小写十六进制字符串中的证书指纹的值。
