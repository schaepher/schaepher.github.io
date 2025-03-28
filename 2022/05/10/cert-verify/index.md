# 手动验证 TLS 证书


## 证书验证

### 证书结构

我们现在使用的 TLS 证书的标准是 X.509，版本号为 V3。版本号可从证书的 Version 字段看到。

根据 [RFC 3280](https://datatracker.ietf.org/doc/html/rfc3280.html?msclkid=a0a5d923cf8211ec99debd4d1b18e2b5#section-4.1) 定义的证书结构，证书由三个部分组成：

1. 证书主体（TBSCertificate，To Be Signed Certificate，待签名证书）  
2. 签名算法
3. 签名值

<!-- more -->

证书主体包括版本、序列号、公钥等内容。签名值是对证书主体使用签名算法计算并经过证书签名机构私钥加密后的值。

证书的数据组织格式为 ASN.1 DER 格式（distinguished encoding rules）。这是一种 TLV 编码，其中的每个元素都包含 Tag、Length、Value。通常我们获得的证书是经由 Base64 编码后的 PEM 文件，为了节省不必要的麻烦，后续内容会提前将证书转回 DER 格式。

PEM 文件的格式是这样的：

```
-----BEGIN CERTIFICATE-----
这里是 Base64 编码后的内容
-----END CERTIFICATE-----
```

### 证书验证

为了验证证书，我们需要获取以下内容：

1. 证书主体。用于通过签名算法得到其 hash 值
2. 证书签名值。
3. CA 的公钥。用于解密签名，得到证书主体的 hash 值

如果 1 和 3 的 hash 值相等，则说明此次验证通过。

我们以博客园的证书为例。

#### 证书下载

1. 下载博客园证书  
   ```bash
   echo -n | openssl s_client -connect www.cnblogs.com:443 | openssl x509 -outform DER > www.cnblogs.com.crt
   ```  
   证书原文是用 Base64 编码后的 PEM 格式文件，这里将其直接转换为 DER 格式。
2. 查看博客园的 CA 证书地址  
   ```bash
   openssl x509 -inform DER -in www.cnblogs.com.crt -noout -text  | grep "CA Issuers"
   ```  
   得到：
   ```bash
   CA Issuers - URI:http://cacerts.digicert.com/EncryptionEverywhereDVTLSCA-G1.crt
   ```
3. 下载 CA 证书  
   ```bash
   curl -O http://cacerts.digicert.com/EncryptionEverywhereDVTLSCA-G1.crt
   ```  
   这个证书已经是 DER 格式，无需转换。

现在，我们得到了：

- 博客园证书
- 给博客园证书签名的 CA 的证书

#### DER 证书解析

在开始验证之前，再次了解证书的格式，便于理解后续的获取操作。

证书由证书主体、签名算法和签名值三个部分组成。DER 格式每个元素以 SEQUENCE 作为开头。由于完整的证书是一个 SEQUENCE，因此证书最外层有个 SEQUENCE。里面三个部分都各自有一个 SEQUENCE。

执行命令查看内容：

```bash
openssl asn1parse -i -inform DER -in www.cnblogs.com.crt
```

解析的格式为：开头数字是偏移量，d 表示深度（depth），d 相同的表示是同一个层级。hl 表示头部长度（header length），l 表示不包含头部的数据长度（lenght）。

```
    0:d=0  hl=4 l=1534 cons: SEQUENCE
    4:d=1  hl=4 l=1254 cons:  SEQUENCE
    8:d=2  hl=2 l=   3 cons:   cont [ 0 ]
   10:d=3  hl=2 l=   1 prim:    INTEGER           :02
   13:d=2  hl=2 l=  16 prim:   INTEGER           :03E3AC5347CD4A3862C2855A71A6F94F
   31:d=2  hl=2 l=  13 cons:   SEQUENCE
   33:d=3  hl=2 l=   9 prim:    OBJECT            :sha256WithRSAEncryption
   44:d=3  hl=2 l=   0 prim:    NULL
   46:d=2  hl=2 l= 110 cons:   SEQUENCE
   48:d=3  hl=2 l=  11 cons:    SET
   50:d=4  hl=2 l=   9 cons:     SEQUENCE
   52:d=5  hl=2 l=   3 prim:      OBJECT            :countryName
   57:d=5  hl=2 l=   2 prim:      PRINTABLESTRING   :US
   61:d=3  hl=2 l=  21 cons:    SET
   63:d=4  hl=2 l=  19 cons:     SEQUENCE
   65:d=5  hl=2 l=   3 prim:      OBJECT            :organizationName
   70:d=5  hl=2 l=  12 prim:      PRINTABLESTRING   :DigiCert Inc
   84:d=3  hl=2 l=  25 cons:    SET
   86:d=4  hl=2 l=  23 cons:     SEQUENCE
   88:d=5  hl=2 l=   3 prim:      OBJECT            :organizationalUnitName
   93:d=5  hl=2 l=  16 prim:      PRINTABLESTRING   :www.digicert.com
  111:d=3  hl=2 l=  45 cons:    SET
  113:d=4  hl=2 l=  43 cons:     SEQUENCE
  115:d=5  hl=2 l=   3 prim:      OBJECT            :commonName
  120:d=5  hl=2 l=  36 prim:      PRINTABLESTRING   :Encryption Everywhere DV TLS CA - G1
  158:d=2  hl=2 l=  30 cons:   SEQUENCE
  160:d=3  hl=2 l=  13 prim:    UTCTIME           :220228000000Z
  175:d=3  hl=2 l=  13 prim:    UTCTIME           :230301235959Z
  190:d=2  hl=2 l=  24 cons:   SEQUENCE
  192:d=3  hl=2 l=  22 cons:    SET
  194:d=4  hl=2 l=  20 cons:     SEQUENCE
  196:d=5  hl=2 l=   3 prim:      OBJECT            :commonName
  201:d=5  hl=2 l=  13 prim:      UTF8STRING        :*.cnblogs.com
  216:d=2  hl=4 l= 290 cons:   SEQUENCE
  220:d=3  hl=2 l=  13 cons:    SEQUENCE
  222:d=4  hl=2 l=   9 prim:     OBJECT            :rsaEncryption
  233:d=4  hl=2 l=   0 prim:     NULL
  235:d=3  hl=4 l= 271 prim:    BIT STRING
  510:d=2  hl=4 l= 748 cons:   cont [ 3 ]
  514:d=3  hl=4 l= 744 cons:    SEQUENCE
  518:d=4  hl=2 l=  31 cons:     SEQUENCE
  520:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Authority Key Identifier
  525:d=5  hl=2 l=  24 prim:      OCTET STRING      [HEX DUMP]:3016801455744FB2724FF560BA50D1D7E6515C9A01871AD7
  551:d=4  hl=2 l=  29 cons:     SEQUENCE
  553:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Subject Key Identifier
  558:d=5  hl=2 l=  22 prim:      OCTET STRING      [HEX DUMP]:04149DE559358AA4C25E1A52193A745F007F101B1C17
  582:d=4  hl=2 l=  37 cons:     SEQUENCE
  584:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Subject Alternative Name
  589:d=5  hl=2 l=  30 prim:      OCTET STRING      [HEX DUMP]:301C820D2A2E636E626C6F67732E636F6D820B636E626C6F67732E636F6D
  621:d=4  hl=2 l=  14 cons:     SEQUENCE
  623:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Key Usage
  628:d=5  hl=2 l=   1 prim:      BOOLEAN           :255
  631:d=5  hl=2 l=   4 prim:      OCTET STRING      [HEX DUMP]:030205A0
  637:d=4  hl=2 l=  29 cons:     SEQUENCE
  639:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Extended Key Usage
  644:d=5  hl=2 l=  22 prim:      OCTET STRING      [HEX DUMP]:301406082B0601050507030106082B06010505070302
  668:d=4  hl=2 l=  62 cons:     SEQUENCE
  670:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Certificate Policies
  675:d=5  hl=2 l=  55 prim:      OCTET STRING      [HEX DUMP]:30353033060667810C0102013029302706082B06010505070201161B687474703A2F2F7777772E64696769636572742E636F6D2F435053
  732:d=4  hl=3 l= 128 cons:     SEQUENCE
  735:d=5  hl=2 l=   8 prim:      OBJECT            :Authority Information Access
  745:d=5  hl=2 l= 116 prim:      OCTET STRING      [HEX DUMP]:3072302406082B060105050730018618687474703A2F2F6F6373702E64696769636572742E636F6D304A06082B06010505073002863E687474703A2F2F636163657274732E64696769636572742E636F6D2F456E6372797074696F6E457665727977686572654456544C5343412D47312E637274
  863:d=4  hl=2 l=   9 cons:     SEQUENCE
  865:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Basic Constraints
  870:d=5  hl=2 l=   2 prim:      OCTET STRING      [HEX DUMP]:3000
  874:d=4  hl=4 l= 384 cons:     SEQUENCE
  878:d=5  hl=2 l=  10 prim:      OBJECT            :CT Precertificate SCTs
  890:d=5  hl=4 l= 368 prim:      OCTET STRING      [HEX DUMP]:0482016C016A007700E83ED0DA3EF5063532E75728BC896BC903D3CBD1116BECEB69E1777D6D06BD6E0000017F3E1A44D10000040300483046022100D8162F949F2820F1C3CCF73AD2826F04CDD3EA09C16BAD2441AE07C69D149DE1022100AC4C3B8EB60C5613C32B85C5303ACC67F62888DFB7925861088B21B550E16E9600760035CF191BBFB16C57BF0FAD4C6D42CBBBB627202651EA3FE12AEFA803C33BD64C0000017F3E1A45110000040300473045022100A4D6915799132F3997B16F009F7011520A3BB30A040DAE42B73D905975DBADBD02206165D6DA0CB72F87B8FA7F309806919893FA962126F6D94512DB700CDF019B84007700B3737707E18450F86386D605A9DC11094A792DB1670C0B87DCF0030E7936A59A0000017F3E1A45370000040300483046022100B31A83931E8A4D8BD4FD2F28E8C42D3B1083D79E9F5E7F9F8B8D1C4D33DE8C65022100E6D91B7986CA850272265DEDBD4C40180BB73B69447304F423BDA19B29F4ADE3
 1262:d=1  hl=2 l=  13 cons:  SEQUENCE
 1264:d=2  hl=2 l=   9 prim:   OBJECT            :sha256WithRSAEncryption
 1275:d=2  hl=2 l=   0 prim:   NULL
 1277:d=1  hl=4 l= 257 prim:  BIT STRING
```

例如第一行：  
`0:d=0  hl=4 l=1534 cons: SEQUENCE`

开头 0 表示偏移量为 0，就是整个文件的开头。d=0 表示最顶层，为整个证书的对象。头部长度为 4 字节，数据字段（也就是三个部分）总共 1534 字节，加起来整个文件共 1538 字节。

再看最后一行，

` 1277:d=1  hl=4 l= 257 prim:  BIT STRING`

开头 1277 表示偏移量，d=1 表示顶层的下一层，而这个位置在最后一部分，那么就代表是签名值。头部长度为 4 字节，数据长度为 257 字节，加起来共 261 字节。加上偏移量 1277 + 261 = 1538 字节，与第一行的计算结果吻合。

#### 获取证书主体（待签名证书）

根据定义，第一个部分就是待签名证书。因此从第一个 d=1 的地方开始，即文件的第二行。

`4:d=1  hl=4 l=1254 cons:  SEQUENCE`

表示偏移量为 4，头部 4 字节，数据 1254 字节。hash 的时候会连头部都算上，所以总共获取 1258 字节。

```bash
dd if=www.cnblogs.com.crt of=www.cnblogs.com.tbs bs=1 skip=4 count=1258
```

这里 bs=1 表示每次读取一个字节，count 表示读取 1258 次，两者组合起来就是读取 1258 个字节。

#### 计算证书 hash 值

获取签名和加密算法：

```
openssl x509 -inform DER -in www.cnblogs.com.crt -noout -text | grep 'Signature Algorithm' | tail -n 1
```

sha256WithRSAEncryption 表示使用 sha256 hash，并使用 RSA 加密。

计算：

```
sha256sum www.cnblogs.com.tbs
```

得到结果：

```
bca9d80920262764ca037b51a1f7bfd8a240c8059c7564dafdaf12ded366d6f5  www.cnblogs.com.tbs
```

#### 签名值

从 ASN.1 解析后的数据，可以知道签名值的偏移量是 1277。

截取签名值：

```bash
openssl asn1parse  -inform DER -in www.cnblogs.com.crt --strparse 1277 -noout -out www.cnblogs.com.sig
```

验证这个数据：

```bash
xxd -p www.cnblogs.com.sig  | tr -d '\n'
```

得到：

```
49aa4a0ff0052f53f27fd1681b11f6247a75b6da247b589a8cec50a7abd3e1ddc9cbbd09a221e529466bdacb34d3bf9555fa4714731b33326cf341d2cd5ac6b5996d22a682dcd8a97ea2245b3318fddc423d17d16318cd925c6d5873a40f16d9b0a6393c18e66d57be6c30688d10faf55b833479cb2735835210c7c6869bc2c33edf7acb531e1e96d3a47796d0f2fe3c3784d3f35e0e7824094bb4b388e8d95861b864a71c50e3b6da9512be585a14196dc7ec2e80f74a06fead44b7340f1a6c3fa1451bd64eadf8ec71d866dee43e44cfcaae3ecc9804e12037400e6548ce77c080d2b09840aa7297aa862679f228a7fac1187a68355946d49a5ae7389d6a38
```


查看得到的结果是否与以下命令的最后一部分一致：

```bash
openssl x509 -inform DER -in www.cnblogs.com.crt -noout -text
```

```
49:aa:4a:0f:f0:05:2f:53:f2:7f:d1:68:1b:11:f6:24:7a:75:
b6:da:24:7b:58:9a:8c:ec:50:a7:ab:d3:e1:dd:c9:cb:bd:09:
a2:21:e5:29:46:6b:da:cb:34:d3:bf:95:55:fa:47:14:73:1b:
33:32:6c:f3:41:d2:cd:5a:c6:b5:99:6d:22:a6:82:dc:d8:a9:
7e:a2:24:5b:33:18:fd:dc:42:3d:17:d1:63:18:cd:92:5c:6d:
58:73:a4:0f:16:d9:b0:a6:39:3c:18:e6:6d:57:be:6c:30:68:
8d:10:fa:f5:5b:83:34:79:cb:27:35:83:52:10:c7:c6:86:9b:
c2:c3:3e:df:7a:cb:53:1e:1e:96:d3:a4:77:96:d0:f2:fe:3c:
37:84:d3:f3:5e:0e:78:24:09:4b:b4:b3:88:e8:d9:58:61:b8:
64:a7:1c:50:e3:b6:da:95:12:be:58:5a:14:19:6d:c7:ec:2e:
80:f7:4a:06:fe:ad:44:b7:34:0f:1a:6c:3f:a1:45:1b:d6:4e:
ad:f8:ec:71:d8:66:de:e4:3e:44:cf:ca:ae:3e:cc:98:04:e1:
20:37:40:0e:65:48:ce:77:c0:80:d2:b0:98:40:aa:72:97:aa:
86:26:79:f2:28:a7:fa:c1:18:7a:68:35:59:46:d4:9a:5a:e7:
38:9d:6a:38
```

这部分直接从完整的 text 中复制然后手动编辑也可以。

#### CA 证书公钥

解析并查看位置：

```bash
openssl asn1parse -i -inform DER -in EncryptionEverywhereDVTLSCA-G1.crt
```

```
    0:d=0  hl=4 l=1194 cons: SEQUENCE
    4:d=1  hl=4 l= 914 cons:  SEQUENCE
    8:d=2  hl=2 l=   3 cons:   cont [ 0 ]
   10:d=3  hl=2 l=   1 prim:    INTEGER           :02
   13:d=2  hl=2 l=  16 prim:   INTEGER           :0279AC458BC1B245ABF98053CD2C9BB1
   31:d=2  hl=2 l=  13 cons:   SEQUENCE
   33:d=3  hl=2 l=   9 prim:    OBJECT            :sha256WithRSAEncryption
   44:d=3  hl=2 l=   0 prim:    NULL
   46:d=2  hl=2 l=  97 cons:   SEQUENCE
   48:d=3  hl=2 l=  11 cons:    SET
   50:d=4  hl=2 l=   9 cons:     SEQUENCE
   52:d=5  hl=2 l=   3 prim:      OBJECT            :countryName
   57:d=5  hl=2 l=   2 prim:      PRINTABLESTRING   :US
   61:d=3  hl=2 l=  21 cons:    SET
   63:d=4  hl=2 l=  19 cons:     SEQUENCE
   65:d=5  hl=2 l=   3 prim:      OBJECT            :organizationName
   70:d=5  hl=2 l=  12 prim:      PRINTABLESTRING   :DigiCert Inc
   84:d=3  hl=2 l=  25 cons:    SET
   86:d=4  hl=2 l=  23 cons:     SEQUENCE
   88:d=5  hl=2 l=   3 prim:      OBJECT            :organizationalUnitName
   93:d=5  hl=2 l=  16 prim:      PRINTABLESTRING   :www.digicert.com
  111:d=3  hl=2 l=  32 cons:    SET
  113:d=4  hl=2 l=  30 cons:     SEQUENCE
  115:d=5  hl=2 l=   3 prim:      OBJECT            :commonName
  120:d=5  hl=2 l=  23 prim:      PRINTABLESTRING   :DigiCert Global Root CA
  145:d=2  hl=2 l=  30 cons:   SEQUENCE
  147:d=3  hl=2 l=  13 prim:    UTCTIME           :171127124610Z
  162:d=3  hl=2 l=  13 prim:    UTCTIME           :271127124610Z
  177:d=2  hl=2 l= 110 cons:   SEQUENCE
  179:d=3  hl=2 l=  11 cons:    SET
  181:d=4  hl=2 l=   9 cons:     SEQUENCE
  183:d=5  hl=2 l=   3 prim:      OBJECT            :countryName
  188:d=5  hl=2 l=   2 prim:      PRINTABLESTRING   :US
  192:d=3  hl=2 l=  21 cons:    SET
  194:d=4  hl=2 l=  19 cons:     SEQUENCE
  196:d=5  hl=2 l=   3 prim:      OBJECT            :organizationName
  201:d=5  hl=2 l=  12 prim:      PRINTABLESTRING   :DigiCert Inc
  215:d=3  hl=2 l=  25 cons:    SET
  217:d=4  hl=2 l=  23 cons:     SEQUENCE
  219:d=5  hl=2 l=   3 prim:      OBJECT            :organizationalUnitName
  224:d=5  hl=2 l=  16 prim:      PRINTABLESTRING   :www.digicert.com
  242:d=3  hl=2 l=  45 cons:    SET
  244:d=4  hl=2 l=  43 cons:     SEQUENCE
  246:d=5  hl=2 l=   3 prim:      OBJECT            :commonName
  251:d=5  hl=2 l=  36 prim:      PRINTABLESTRING   :Encryption Everywhere DV TLS CA - G1
  289:d=2  hl=4 l= 290 cons:   SEQUENCE
  293:d=3  hl=2 l=  13 cons:    SEQUENCE
  295:d=4  hl=2 l=   9 prim:     OBJECT            :rsaEncryption
  306:d=4  hl=2 l=   0 prim:     NULL
  308:d=3  hl=4 l= 271 prim:    BIT STRING
  583:d=2  hl=4 l= 335 cons:   cont [ 3 ]
  587:d=3  hl=4 l= 331 cons:    SEQUENCE
  591:d=4  hl=2 l=  29 cons:     SEQUENCE
  593:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Subject Key Identifier
  598:d=5  hl=2 l=  22 prim:      OCTET STRING      [HEX DUMP]:041455744FB2724FF560BA50D1D7E6515C9A01871AD7
  622:d=4  hl=2 l=  31 cons:     SEQUENCE
  624:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Authority Key Identifier
  629:d=5  hl=2 l=  24 prim:      OCTET STRING      [HEX DUMP]:3016801403DE503556D14CBB66F0A3E21B1BC397B23DD155
  655:d=4  hl=2 l=  14 cons:     SEQUENCE
  657:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Key Usage
  662:d=5  hl=2 l=   1 prim:      BOOLEAN           :255
  665:d=5  hl=2 l=   4 prim:      OCTET STRING      [HEX DUMP]:03020186
  671:d=4  hl=2 l=  29 cons:     SEQUENCE
  673:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Extended Key Usage
  678:d=5  hl=2 l=  22 prim:      OCTET STRING      [HEX DUMP]:301406082B0601050507030106082B06010505070302
  702:d=4  hl=2 l=  18 cons:     SEQUENCE
  704:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Basic Constraints
  709:d=5  hl=2 l=   1 prim:      BOOLEAN           :255
  712:d=5  hl=2 l=   8 prim:      OCTET STRING      [HEX DUMP]:30060101FF020100
  722:d=4  hl=2 l=  52 cons:     SEQUENCE
  724:d=5  hl=2 l=   8 prim:      OBJECT            :Authority Information Access
  734:d=5  hl=2 l=  40 prim:      OCTET STRING      [HEX DUMP]:3026302406082B060105050730018618687474703A2F2F6F6373702E64696769636572742E636F6D
  776:d=4  hl=2 l=  66 cons:     SEQUENCE
  778:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 CRL Distribution Points
  783:d=5  hl=2 l=  59 prim:      OCTET STRING      [HEX DUMP]:30393037A035A0338631687474703A2F2F63726C332E64696769636572742E636F6D2F4469676943657274476C6F62616C526F6F7443412E63726C
  844:d=4  hl=2 l=  76 cons:     SEQUENCE
  846:d=5  hl=2 l=   3 prim:      OBJECT            :X509v3 Certificate Policies
  851:d=5  hl=2 l=  69 prim:      OCTET STRING      [HEX DUMP]:3043303706096086480186FD6C0102302A302806082B06010505070201161C68747470733A2F2F7777772E64696769636572742E636F6D2F4350533008060667810C010201
  922:d=1  hl=2 l=  13 cons:  SEQUENCE
  924:d=2  hl=2 l=   9 prim:   OBJECT            :sha256WithRSAEncryption
  935:d=2  hl=2 l=   0 prim:   NULL
  937:d=1  hl=4 l= 257 prim:  BIT STRING
```

找到 `rsaEncryption`，它在 d=4 的层级，公钥所在位置为下方的 d=3 层级的 BIT STRING：

`308:d=3  hl=4 l= 271`

根据 [rfc 3279](https://datatracker.ietf.org/doc/html/rfc3279#section-2.3.1) 的定义，RSA PublickKey 由系数 (modulus) 和指数 (exponent) 两部分组成。因此 271 字节里面的两部分要分开获取。这两部分也是使用 DER 格式编码的，可以直接使用工具解析：

```
openssl asn1parse -inform DER -in EncryptionEverywhereDVTLSCA-G1.crt --strparse 308 -noout -out EncryptionEverywhereDVTLSCA-G1.rsa

openssl asn1parse -i -inform DER -in EncryptionEverywhereDVTLSCA-G1.rsa
```

得到：

```
    0:d=0  hl=4 l= 266 cons: SEQUENCE
    4:d=1  hl=4 l= 257 prim:  INTEGER           :B3DE3FAC2469BE35772421EA629CA07AADDE3448C56E4C0EF7FD43288E47B55F1702BAE7A7ACD1416221BEF837DA519EDCC5D54818CC31AEDE9A5954C76895BC619BA7564BD38AFE515E84A353D0E608F5AAA4E85F94EDC03A8F1482FA20C13D7C1D178AECDCA472A776909FAA63A69D72AFB201E98E33BFBD847BF3E567FEAB2BA2270BA5A92B49CF54E611EE7F620EE3DED44E08C543011FF4F7DFEDE1CAE1F776F7E089650E5248DDA4C6F2C57F973657B9B84222C81B22E08BDB7130A1F2BBA27C2222E660D7919AE7313F27C1F60257ABFA90375791B80644B2AC478A6E71B26D6CAA889141B1B99236B7BA5F7B02917399D679CBC30597F7FA9D4CA40F
  265:d=1  hl=2 l=   3 prim:  INTEGER           :010001
```

其中第一个 INTEGER 是 modulus，第二个 INTEGER 是 exponent。由于可以直接复制，不再使用 xxd 命令。

验证这个信息：

```
openssl x509 -inform DER -in EncryptionEverywhereDVTLSCA-G1.crt -noout -text
```

在 `Subject Public Key Info` 一节里可以看到：

```
00:b3:de:3f:ac:24:69:be:35:77:24:21:ea:62:9c:
a0:7a:ad:de:34:48:c5:6e:4c:0e:f7:fd:43:28:8e:
47:b5:5f:17:02:ba:e7:a7:ac:d1:41:62:21:be:f8:
37:da:51:9e:dc:c5:d5:48:18:cc:31:ae:de:9a:59:
54:c7:68:95:bc:61:9b:a7:56:4b:d3:8a:fe:51:5e:
84:a3:53:d0:e6:08:f5:aa:a4:e8:5f:94:ed:c0:3a:
8f:14:82:fa:20:c1:3d:7c:1d:17:8a:ec:dc:a4:72:
a7:76:90:9f:aa:63:a6:9d:72:af:b2:01:e9:8e:33:
bf:bd:84:7b:f3:e5:67:fe:ab:2b:a2:27:0b:a5:a9:
2b:49:cf:54:e6:11:ee:7f:62:0e:e3:de:d4:4e:08:
c5:43:01:1f:f4:f7:df:ed:e1:ca:e1:f7:76:f7:e0:
89:65:0e:52:48:dd:a4:c6:f2:c5:7f:97:36:57:b9:
b8:42:22:c8:1b:22:e0:8b:db:71:30:a1:f2:bb:a2:
7c:22:22:e6:60:d7:91:9a:e7:31:3f:27:c1:f6:02:
57:ab:fa:90:37:57:91:b8:06:44:b2:ac:47:8a:6e:
71:b2:6d:6c:aa:88:91:41:b1:b9:92:36:b7:ba:5f:
7b:02:91:73:99:d6:79:cb:c3:05:97:f7:fa:9d:4c:
a4:0f
```

以及： Exponent: 65537 (0x10001)。

与上述获取的一致。

#### 使用 CA 公钥解密

已知的内容：

- 签名值 sig ：

   ```
   49aa4a0ff0052f53f27fd1681b11f6247a75b6da247b589a8cec50a7abd3e1ddc9cbbd09a221e529466bdacb34d3bf9555fa4714731b33326cf341d2cd5ac6b5996d22a682dcd8a97ea2245b3318fddc423d17d16318cd925c6d5873a40f16d9b0a6393c18e66d57be6c30688d10faf55b833479cb2735835210c7c6869bc2c33edf7acb531e1e96d3a47796d0f2fe3c3784d3f35e0e7824094bb4b388e8d95861b864a71c50e3b6da9512be585a14196dc7ec2e80f74a06fead44b7340f1a6c3fa1451bd64eadf8ec71d866dee43e44cfcaae3ecc9804e12037400e6548ce77c080d2b09840aa7297aa862679f228a7fac1187a68355946d49a5ae7389d6a38
   ```

- CA 公钥系数 modulus：

   ```
   B3DE3FAC2469BE35772421EA629CA07AADDE3448C56E4C0EF7FD43288E47B55F1702BAE7A7ACD1416221BEF837DA519EDCC5D54818CC31AEDE9A5954C76895BC619BA7564BD38AFE515E84A353D0E608F5AAA4E85F94EDC03A8F1482FA20C13D7C1D178AECDCA472A776909FAA63A69D72AFB201E98E33BFBD847BF3E567FEAB2BA2270BA5A92B49CF54E611EE7F620EE3DED44E08C543011FF4F7DFEDE1CAE1F776F7E089650E5248DDA4C6F2C57F973657B9B84222C81B22E08BDB7130A1F2BBA27C2222E660D7919AE7313F27C1F60257ABFA90375791B80644B2AC478A6E71B26D6CAA889141B1B99236B7BA5F7B02917399D679CBC30597F7FA9D4CA40F
   ```

- CA 公钥指数 exponent：
   
   ```
   0x10001
   ```

根据公式 decrypted_value = (modulus^exponent)%sig，使用 python 计算：

```python
modulus=0xB3DE3FAC2469BE35772421EA629CA07AADDE3448C56E4C0EF7FD43288E47B55F1702BAE7A7ACD1416221BEF837DA519EDCC5D54818CC31AEDE9A5954C76895BC619BA7564BD38AFE515E84A353D0E608F5AAA4E85F94EDC03A8F1482FA20C13D7C1D178AECDCA472A776909FAA63A69D72AFB201E98E33BFBD847BF3E567FEAB2BA2270BA5A92B49CF54E611EE7F620EE3DED44E08C543011FF4F7DFEDE1CAE1F776F7E089650E5248DDA4C6F2C57F973657B9B84222C81B22E08BDB7130A1F2BBA27C2222E660D7919AE7313F27C1F60257ABFA90375791B80644B2AC478A6E71B26D6CAA889141B1B99236B7BA5F7B02917399D679CBC30597F7FA9D4CA40F

sig=0x49aa4a0ff0052f53f27fd1681b11f6247a75b6da247b589a8cec50a7abd3e1ddc9cbbd09a221e529466bdacb34d3bf9555fa4714731b33326cf341d2cd5ac6b5996d22a682dcd8a97ea2245b3318fddc423d17d16318cd925c6d5873a40f16d9b0a6393c18e66d57be6c30688d10faf55b833479cb2735835210c7c6869bc2c33edf7acb531e1e96d3a47796d0f2fe3c3784d3f35e0e7824094bb4b388e8d95861b864a71c50e3b6da9512be585a14196dc7ec2e80f74a06fead44b7340f1a6c3fa1451bd64eadf8ec71d866dee43e44cfcaae3ecc9804e12037400e6548ce77c080d2b09840aa7297aa862679f228a7fac1187a68355946d49a5ae7389d6a38

exponent=0x10001

print("%x" % pow(sig, exponent, modulus))
```

得到：

```
1ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff003031300d060960864801650304020105000420bca9d80920262764ca037b51a1f7bfd8a240c8059c7564dafdaf12ded366d6f5
```

开头的 `1fff...` 是 RSA 算法的填充字节，接下来的 `3031300D060960864801650304020105000420` 是 sha256 的填充字节。剩下的 `bca9d80920262764ca037b51a1f7bfd8a240c8059c7564dafdaf12ded366d6f5` 是证书 hash 值。

我们将该值与前面手动计算的 TBS 证书 hash 值做对比，得到完全一致。

至此，验证完毕。

### 证书链

上面只验证了第一步。从浏览器中可以看出，上述 CA 证书不是根证书，还需要验证 CA 证书的可信。步骤与上述差不多，只是根证书是安装在设备的操作系统上或者浏览器上。

## 参考

参考[^1]^[^2]^[^3]^[^4]^[^5]^[^6]^[^7]^[^8]

[^1]: https://blog.yuantops.com/tech/validate_a_digital_certificate_step_by_step/ (手工验证一张数字证书的有效性)
[^2]: https://yongbingchen.github.io/blog/2015/04/09/verify-the-signature-of-a-x-dot-509-certificate/ (https://yongbingchen.github.io/blog/2015/04/09/verify-the-signature-of-a-x-dot-509-certificate/)
[^3]: https://datatracker.ietf.org/doc/html/rfc3279 (RFC 3279) 
[^4]: https://datatracker.ietf.org/doc/html/rfc2313 (RFC 2313)
[^5]: https://datatracker.ietf.org/doc/html/rfc3280 (RFC 3280)
[^6]: https://docs.microsoft.com/en-us/windows/win32/seccertenroll/about-encoded-length-and-value-bytes (Encoded Length and Value Bytes)
[^7]: https://linux.die.net/man/1/asn1parse (asn1parse(1) - Linux man page)
[^8]: https://stackoverflow.com/questions/2614764/how-to-create-a-hex-dump-of-file-containing-only-the-hex-characters-without-spac (How to create a hex dump of file containing only the hex characters without spaces in bash?)


