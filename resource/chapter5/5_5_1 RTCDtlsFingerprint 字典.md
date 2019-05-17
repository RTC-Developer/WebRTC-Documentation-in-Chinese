### 5.5.1 RTCDtlsFingerprint字典

`RTCDtlsFingerprint`字典包含[RFC4572]中描述的哈希函数算法和证书指纹。

```java
dictionary RTCDtlsFingerprint {
             DOMString algorithm;
             DOMString value;
};
```

#### 字典RTCDtlsFingerprint成员

DOMString类型的`算法`:它是哈希函数文本名称注册表[IANA-HASH-FUNCTION]中定义的一个哈希函数算法。

DOMString类型的`值`:使用[RFC4572]第五节中“指纹”语法表示的小写十六进制字符串中的指纹证书的值。
