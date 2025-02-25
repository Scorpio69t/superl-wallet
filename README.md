# 简介
**项目地址:https://github.com/Scorpio69t/superl-wallet**

**作者:Scorpio69t**

**邮箱:yangruitao6@gmail.com**

**博客:https://blog.csdn.net/qq_32019341?type=blog**

**QQ: 3324729792**

使用GO语言原创研发的一款基于区块链技术的数字代币钱包信息生成工具，并且带有丰富的注释与算法的步骤说明。

目前已经实现【比特币】、【以太坊】钱包相关基础功能(非确定性钱包（nondeterministic wallet）)

-  可生成原始公钥
-  可生成比特币压缩公钥
-  可生成比特币未压缩公钥

-  可生成16进制格式私钥
-  可生成比特币WIF未压缩格式私钥
-  可生成比特币WIF压缩格式私钥

-  可把比特币未压缩WIF格式私钥转为原始16进制
-  可把比特币压缩WIF格式私钥转为原始16进制

-  可通过私钥计算出比特币压缩公钥和未压缩公钥，以及椭圆曲线的X,Y坐标
-  可通过私钥计算出以太坊公钥，以及地址

-  可通过指定公钥，计算出比特币公钥对应的地址
-  可通过指定公钥，计算出以太坊公钥对应的地址

-  可验证比特币地址的有效性

-  可计算签名

-  可验证签名

### 可用性说明

   目前网上的大部分GO语言的实例代码中的椭圆曲线算法，都使用的是GO语言官方包中的比特币当中的曲线是secp256r1，而比特币等数字代币使用的是比特币当中的曲线是secp256k1。

   其他项目代码中的椭圆曲线选得不对，两条曲线的参数不同！踩了坑！

   这将导致相同的私钥在不同的曲线上会计算出不同的公钥，进而导致计算出不同的地址。 所以secp256r1的私钥在比特币区块链上是无法控制代码里的比特币地址的。

   本项目中使用了github.com/decred/dcrd/dcrec/secp256k1 中的secp256k1算法。规避了此问题。

   同时，本程序生成的私钥，经过本人实际测试，是可以导入目前主流的钱包中的。导入钱包后的地址等也与程序生成的地址相吻合！

### 运行效果[最新]
    ================正在生成测试信息================
    原始公钥XY:0983b59d1b92ff664d1af848507233af2a664e3385187778ad8112cbf39e76435624df60086d711bdf880b3b725bc668813da384eb30bd65d4770441617b08a7
    公钥(未压缩):040983b59d1b92ff664d1af848507233af2a664e3385187778ad8112cbf39e76435624df60086d711bdf880b3b725bc668813da384eb30bd65d4770441617b08a7
    公钥(压缩):030983b59d1b92ff664d1af848507233af2a664e3385187778ad8112cbf39e7643

    根据压缩公钥获取地址:1FRAYik87LhvDzTMj5sdtCEnDzCS8xsHz
    根据未压缩公钥获取地址:1MHdYBWyuy76PGb4ZyQ5n5HNtruSZ1YwEG

    私钥(原始16进制格式):af964398cfc6448d533f9d1518de3d3bb0dbf1a03d86dea8d7a6ceeafa0849a2
    私钥(未压缩WIF格式):5K9ciRQZemVXXSWVbyogxqMSpf6dhfJrBxy8yV4Nrw4osVtqhG6
    私钥(压缩WIF格式):L372dpj17hNujMbBFPj5PSREyM9rzU5n7Q2nCJquVPdosjD8xPF4

    逆向解密测试(未压缩WIF格式私钥转原始16进制):af964398cfc6448d533f9d1518de3d3bb0dbf1a03d86dea8d7a6ceeafa0849a2
    逆向解密测试(压缩WIF格式私钥转原始16进制):af964398cfc6448d533f9d1518de3d3bb0dbf1a03d86dea8d7a6ceeafa0849a2


    ================通过公钥计算出地址的算法测试==================
    当前录入的公钥:030983b59d1b92ff664d1af848507233af2a664e3385187778ad8112cbf39e7643
    比特币地址:1FRAYik87LhvDzTMj5sdtCEnDzCS8xsHz
    比特币地址是否有效:true

    ================通过私钥计算出公钥的算法测试==================
    当前录入的原始16进制格式私钥:af964398cfc6448d533f9d1518de3d3bb0dbf1a03d86dea8d7a6ceeafa0849a2
    计算出的未压缩公钥:040983b59d1b92ff664d1af848507233af2a664e3385187778ad8112cbf39e76435624df60086d711bdf880b3b725bc668813da384eb30bd65d4770441617b08a7
    计算出的压缩公钥:030983b59d1b92ff664d1af848507233af2a664e3385187778ad8112cbf39e7643
    计算出的椭圆曲线X坐标:0983b59d1b92ff664d1af848507233af2a664e3385187778ad8112cbf39e7643
    计算出的椭圆曲线Y坐标:5624df60086d711bdf880b3b725bc668813da384eb30bd65d4770441617b08a7

    ================签名算法测试==================
    待签名字符:hello,dsa签名
    计算出的签名:3045022100df4c10e2dc3e25e7f52fa6bfc36898a5d5619214f21ca88c31736973cdfeceaf022008605187dea82f87bf665c0043a1fedb417a6e59474428cb0a9460fccd948466
    待验证字符:hello,dsa签名
    【签名测试】:hello,dsa签名 【结果】:通过,数据未被修改
    待验证字符:hello,dsa签名2
    【签名测试】:hello,dsa签名2 结果】:异常,数据被修改

    ================通过[16进制公钥字符串]计算出[地址]的算法测试==================
    当前录入的公钥:0384a6728273ddb4b769d9c4dc45fe73594bed3d8364ec50d156b5564f2301e1ca
    比特币地址:19XW8CZnsB96D62fdWnVm3RCmGvztt8aJh
    比特币地址是否有效:true

    ================根据指定16进制私钥，计算出公钥和地址 算法测试==================
    当前录入的原始16进制格式私钥:a343a91fa1f377ee4f92b402e17cda8b88d00584de555d5194742fea00f18a14
    计算出的未压缩公钥:041f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f9180e1b828f69dfa6a4046305924703a373bab892209b8b7e38da02aee44d90ab1
    计算出的压缩公钥:031f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f91
    计算出的椭圆曲线X坐标:1f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f91
    计算出的椭圆曲线Y坐标:80e1b828f69dfa6a4046305924703a373bab892209b8b7e38da02aee44d90ab1
    根据计算出的压缩公钥，再计算出地址为:19EnjPYjPSLovhjZURyCQ6wws3ix9LhiMB

    ================根据指定的压缩WIF格式私钥，计算出16进制私钥 算法测试==================
    当前录入的压缩WIF格式私钥:L2h5KiLDR5oPb7wiedHs2MQRCaA28LCkgLFKpamrHdVBtCjxkqum
    计算出的16进制私钥:a343a91fa1f377ee4f92b402e17cda8b88d00584de555d5194742fea00f18a14

    ================根据公钥，生成以太坊地址==================
    当前录入的以太坊公钥字符串：156f94de5208dd2ac61c301d51a4c93f1db00a92185b74f545984e8007de214132a0a20edb8019bd049f292f1fe8122e05d4d32ea206674a4fbd6d2376654da7
    生成以太坊地址：0x49622e2649ab7b517321b1f1582fd8d46482c053


    ================根据私钥，生成公钥和以太坊地址==================
    当前录入的以太坊私钥字符串：6101eedcc7f11d60baeb4346a7e9810fc42dc9fc267254163bea19fe75bba16e
    根据私钥计算出公钥结果：156f94de5208dd2ac61c301d51a4c93f1db00a92185b74f545984e8007de214132a0a20edb8019bd049f292f1fe8122e05d4d32ea206674a4fbd6d2376654da7
    以太坊地址：0x49622e2649ab7b517321b1f1582fd8d46482c053

### 运行效果[上一版本]

    ================正在创建钱包信息================
    原始公钥XY:1f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f9180e1b828f69dfa6a4046305924703a373bab892209b8b7e38da02aee44d90ab1
    公钥(未压缩):041f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f9180e1b828f69dfa6a4046305924703a373bab892209b8b7e38da02aee44d90ab1
    公钥(压缩):031f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f91

    根据压缩公钥获取地址:19EnjPYjPSLovhjZURyCQ6wws3ix9LhiMB
    根据未压缩公钥获取地址:1ETKBpawDfu1GZAoVbzVnjdDRabuxMoTCc

    私钥(原始16进制格式):a343a91fa1f377ee4f92b402e17cda8b88d00584de555d5194742fea00f18a14
    私钥(未压缩WIF格式):5K4BwzPw1vehTmAgLrTUeTpu9xzn7eRsDzNpmK5GhUJG9wGbYwr
    私钥(压缩WIF格式):L2h5KiLDR5oPb7wiedHs2MQRCaA28LCkgLFKpamrHdVBtCjxkqum

    逆向解密测试(未压缩WIF格式私钥转原始16进制):a343a91fa1f377ee4f92b402e17cda8b88d00584de555d5194742fea00f18a14
    逆向解密测试(压缩WIF格式私钥转原始16进制):a343a91fa1f377ee4f92b402e17cda8b88d00584de555d5194742fea00f18a14


    ================通过公钥计算出地址的算法测试==================
    当前录入的公钥:031f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f91
    比特币地址:19EnjPYjPSLovhjZURyCQ6wws3ix9LhiMB
    比特币地址是否有效:true

    ================通过私钥计算出公钥的算法测试==================
    当前录入的原始16进制格式私钥:a343a91fa1f377ee4f92b402e17cda8b88d00584de555d5194742fea00f18a14
    计算出的未压缩公钥:041f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f9180e1b828f69dfa6a4046305924703a373bab892209b8b7e38da02aee44d90ab1
    计算出的压缩公钥:031f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f91
    计算出的椭圆曲线X坐标:1f84dbf77dd950d661b223717b7163237a9836c45cd4d8ba87ca9b5ceb761f91
    计算出的椭圆曲线Y坐标:80e1b828f69dfa6a4046305924703a373bab892209b8b7e38da02aee44d90ab1

### 算法说明
-  比特币地址生成算法

        1. 获取到公钥
        2. 计算公钥的 SHA-256 哈希值（对公钥进行第一次hash256运算）
        3. 计算 RIPEMD-160 哈希值（对第一次hash256的结果进行ripeMD160运算）
        4. 添加版本前缀（将ripeMD160运算的结果前增加版本编号）
        5. 计算两次hash（对加上版本编号的hash值计算两次hash）
        6. 获取校验码（获取两次hash后前四个字节，作为校验码）
        7. 形成比特币地址的16进制格式（将校验码作为比特币地址的后缀，与添加版本前缀的hash值拼接）
        8. 进行Base58编码处理（对比特币地址的16进制格式进行Base58编码，就形成了比特币地址）

    具体可以查看本项目wallet包中的wallet.go文件中的GetAddress()方法！里面有注释。

-  未压缩公钥

        是椭圆曲线算法中的一个点，前缀(04) + x, y 坐标值 (x,y 为 32 字节数)组成。


-  压缩公钥

        因为在交易中包含了公钥，为了优化交易的数据结构、压缩硬盘储存区块链数据，且根据椭圆曲线算法公式根据 x 就能推导出 y 轴的值，所以引进了 压缩公钥 (Compressed public keys)，只包含前缀(02 或 03) + x 。以此压缩公钥相比原生公钥减少了一半的存储，每天面临比特币网络成千上万币交易时，构建交易的数据结构时极大地优化了存储。在这里 y 如果为偶数前缀为 02, 为奇数前缀为 03。


-  16进制格式私钥

        如：a343a91fa1f377ee4f92b402e17cda8b88d00584de555d5194742fea00f18a14

-  WIF压缩格式私钥

        WIF-compressed（WIF压缩格式），K 或者 L 开头
        在原始16进制格式私钥的后面加上01，然后再做计算。即为"压缩格式私钥"(其实并没有压缩，反而更长)
        如：L2h5KiLDR5oPb7wiedHs2MQRCaA28LCkgLFKpamrHdVBtCjxkqum


-  WIF未压缩格式私钥

        如：5K4BwzPw1vehTmAgLrTUeTpu9xzn7eRsDzNpmK5GhUJG9wGbYwr

-  16进制格式的私钥转换成WIF格式

        1：在16进制私钥前面加上0x80版本号
        2：对第1步结果进行SHA256哈希计算
        3：将第2步结果进行SHA256哈希计算
        4：取第3步结果的前4字节(c47e83ff)，加到第1步结果的末尾
        5：对第4步结果进行Base58编码，就是最后得到的WIF格式私钥了

-  WIF格式私钥转换成16进制格式私钥

        1：Base58解码
        2：将解码结果去掉80版本号，以及去掉最后面的4字节校验位。

-  椭圆曲线算法

        比特币使用椭圆曲线来产生私钥。椭圆曲线是一个复杂的数学概念，我们并不打算在这里作太多解释（如果你真的十分好奇，可以查看这篇文章(http://andrea.corbellini.name/2015/05/17/elliptic-curve-cryptography-a-gentle-introduction/)，注意：有很多数学公式！）我们只要知道这些曲线可以生成非常大的随机数就够了。在比特币中使用的曲线可以随机选取在 0 与 2 ^ 2 ^ 56（大概是 10^77, 而整个可见的宇宙中，原子数在 10^78 到 10^82 之间） 的一个数。有如此高的一个上限，意味着几乎不可能发生有两次生成同一个私钥的事情。

        椭圆曲线算法（ECC，Elliptic Curve Cryptography）

        椭圆曲线算法是不可逆的，很容易向一个方向计算，但是不可以向相反方向倒推。
        比特币使用SECP256K1算法（椭圆曲线算法的一种），将私钥生成公钥。
        SECP256K1是不可逆的，因此公钥公开暴露，也对私钥的安全性不会造成影响。
        比特币使用的是 ECDSA（Elliptic Curve Digital Signature Algorithm）算法来对交易进行签名，我们也会使用该算法。

-  Base58编码和解码

        Base58是一种基于文本的二进制编码格式，是用于Bitcoin中使用的一种独特的编码方式，主要用于产生Bitcoin的钱包地址。

        相比Base64，Base58不使用数字"0"，大写字母"O"，大写字母"I"和小写字母"l"，以及"+"和"/"符号。目的就是去除容易混淆的字符。
        这种编码格式不仅实现了数据压缩，保持了易读性，还具有错误诊断功能

        Base58字符集：
        ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz123456789

      具体可以查看本项目crypto包中的base58.go文件中的方法！
