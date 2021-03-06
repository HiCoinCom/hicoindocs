1 接口接入须知
====================
1.1 HiCoin开放平台
-------------------
1、HiCoin开放平台，测试环境地址链接： http://open.hicoin.one/;
                  生产环境地址链接： https://open.hicoin.com/;

2、分测试环境、生产环境两种情况，具体如下：

1)测试环境：
请先下载测试环境的钱包，手机号注册新账号， 注：该手机号对应的账户，可查看充值、提现及结算的相关资金信息，请根据实际情况选择。

钱包下载链接：
http://hicoin-open-test.oss-cn-hangzhou.aliyuncs.com/dev-v2.3.2-open-legu-testweb-1002.apk   
或者扫描二维码下载:


.. image:: images/HiCoin测试app下载.png
   :align: center

   
2)生产环境：
 请直接跳到下面第3步，登录开放平台的生产环境 https://open.hicoin.com/，用手机号注册用户，创建应用，详情请见第3步。

3、使用第二步钱包注册成功的手机号，登录测试环境(http://open.hicoin.one/)或生产环境(https://open.hicoin.com/)，点击应用中心，点击创建应用，填写相关应用信息，包括应用名称、应用头像、IP白名单、授权域名、支付成功回调地址， 创建成功后，请等待管理员后台审核，审核通过及失败会收到短信或邮箱通知，审核通过可以查看AppID、secretKey、支付密钥等信息，以供登录授权、支付接口使用，审核失败可重新编辑再次提交等待管理员审核。

4、开发文档，可查看HiCoin开放平台文档。

5、账户中心，可查看开发者在开放平台的资产管理、资金明细、业务记录(包括支付记录、转账记录、划转记录、结算记录)


1.2 公共参数与返回
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


1.3 测试帐号
-------------------

:爆点授权账号: **appId**: 10021111111 **secretKey**: 7777777a513585204568c088f4d845d8
:GC授权账号: **appId**: 10025555555 **secretKey**: 77732123513585204568c088f4drfrfd
:支付密钥mchKey: 1566486321
:授权支付域名: http://oauth.hicoin.one/api ，此项目接口需要用户授权token
:商户打款域名: http://avenger.hicoin.one/api ，此项目接口需要基础授权token
:支付页面: http://testweb.hicoin.one/hicoinfe/payment/?appId=10021235678&nonceStr=330b1d9b67e4440abff6d9c89ddb9b86&package=prepay_id%3D1074156653097672700214&signType=MD5&timeStamp=1566530976741&paySign=a7fe3487f19688b44196508ee7232c23



注：网页授权流程分为四步（具体接口参数，参考接口文档）
1.通过 http://oauth.hicoin.one/api/connect/oauth/authorize 获取 code 
2.通过 http://oauth.hicoin.one/api/sns/oauth/access_token 获取openid
3.通过 http://avenger.hicoin.one/api/cgi-bin/access_token 获取基础access_token
4.通过 http://oauth.hicoin.one/api/sns/user/info 获取用户信息 








