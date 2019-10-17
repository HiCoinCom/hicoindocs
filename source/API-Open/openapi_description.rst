1 接口描述
====================
1.1 公共参数与返回
-------------------

**公共参数**

================ ========== ========== ===============================
参数名称          数据类型    是否必传     参数描述
app_id           String     是          应用ID
access_token     string     是          础授权接口
lang             string     是          i18n 语言,固定zh_CN
version          string     是          接口版本固定1.0
charset          string     是          固定utf8
================ ========== ========== ===============================

**重点字段说明：**

- access_token: 此文档用户授权access_token使用场景如下：1、支付预下单 /pay/preOrde  2、获取用户基本信息 /sns/user/info ;
                其它接口请使用基础授权接口access_token 。


**公共返回参数**

================ ========== ========== ===============================
参数名称          数据类型    是否必传     参数描述
code             String     是          状态码
msg              string     是          信息
data             T          是          业务数据具体为以下输出参数
================ ========== ========== ===============================


1.2 测试帐号
-------------------

:爆点授权账号: **appId**: 10021111111 **secretKey**: 7777777a513585204568c088f4d845d8
:GC授权账号: **appId**: 10025555555 **secretKey**: 77732123513585204568c088f4d845d8
:支付密钥mchKey: 1566486321
:授权支付域名: http://oauth.hicoin.one/api ，此项目接口需要用户授权token
:商户打款域名: http://avenger.hicoin.one/api ，此项目接口需要基础授权token
:支付页面: http://testweb.hicoin.one/hicoinfe/payment/?appId=10021235678&nonceStr=330b1d9b67e4440abff6d9c89ddb9b86&package=prepay_id%3D1074156653097672700214&signType=MD5&timeStamp=1566530976741&paySign=a7fe3487f19688b44196508ee7232c23
