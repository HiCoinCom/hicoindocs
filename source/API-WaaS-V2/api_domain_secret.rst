
3 域名及API密钥
======================
3.1 生产环境
~~~~~~~~~~~~~~~~~~~~~~~~
:域名: https://openapi.hicoin.vip
:app_id: 请创建钱包后获取
:rsa_wallet_pub: WaaS系统公钥；请创建钱包后从WaaS系统获取
:rsa_third_prv: 客户私钥；自主生成、保存
:rsa_third_pub: 客户公钥；自主生成；请创建钱包后配置到WaaS系统

**RSA 公私钥生成地址**
http://www.metools.info/code/c80.html

推荐密码长度：2048

推荐密钥格式：PKCS#8


说明：

a) rsa_third_prv为第三方应用私钥，主要用于加密请求参数。如果是生产环境，rsa_third_prv由开发者生成，然后将对应的公钥提供给平台。测试环境为了简化开发者对接流程，此处直接提供了一套第三方的公私钥，便于开发者快速对接。

b)目前不支持测试环境对接，请根据**接入指引**自主注册创建钱包后，获取生产环境的API相关信息。
