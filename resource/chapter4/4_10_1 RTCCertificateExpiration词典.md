### [4.10.1 RTCCertificateExpiration词典](http://w3c.github.io/webrtc-pc/#rtccertificateexpiration-dictionary)

RTCCertificateExpiration用于设置generateCertificate生成的证书的到期日期。


```
dictionary RTCCertificateExpiration {
    [EnforceRange]
    DOMTimeStamp expires;
};
```

expires

可选的expires属性可以添加到传递给generateCertificate的算法的定义中。如果此参数存在，则表示RTCCertificate相对于当前时间有效的最长时间。

当使用object参数调用generateCertificate时，用户代理会尝试将对象转换为RTCCertificateExpiration。如果这不成功，立即返回一个被新创建的TypeError和中止处理拒绝的promise。

用户代理生成的证书的到期日期设置为当前时间加上expires属性的值。返回的RTCCertificate的expires属性设置为证书的到期时间。用户代理可以选择限制expires属性的值。
