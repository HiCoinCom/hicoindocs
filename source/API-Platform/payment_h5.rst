H5支付
====================

1. 业务流程图
::::::::::::::::::::::::::::::::

.. image:: images/openapi_h5_payment.png
   :width: 600px
   :height: 675px
   :align: center

2. 支付预下单接口
::::::::::::::::::::::::::::::::

:说明: 用户支付预下单
:接口地址: /pay/preOrder
:请求方式: POST
:请求参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
app_id                 string    是         应用ID
access_token           string    是         授权access_token
lang                   string    是         i18n 语言,固定zh_CN
version                string    是         接口版本固定1.0
charset                string    是         固定utf8
nonce_str              string    是         32位随机数
sign                   string    是         参数签名 (此处签名请使用mch_key)
biz_content            string    是         业务请求参数的集合json。注意，此处不需要urlencode，json格式的字符串即可
===================== ========== ========== =================================================


**biz_content结构体**

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
openid                 string    是         用户openid
body                   string    是         订单说明，最多支持64字符
subject                string    是         订单标题，最多支持32字符
out_trade_no           string    是         第三方网站唯一订单号，32字符0-9A-Za-z
total_amount           long      是         支付币种数量，注意：所有币种使用8位精度，如1eth则传100000000
settle_currency        string    是         支付币种大写，USDT
passback_params        string    否         公用回传参数， 如果请求时传递了该参数， 则返回给商户时会回传该参数
trade_type             string    是         固定JSAPI、H5
trade_timeout_express  int       是         超时时间，单位秒 固定为600
return_url             string    是         支付成功跳转地址，注意，此处不需要urlencode
===================== ========== ========== =================================================


:响应参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
out_trade_no          string     是         第三方网站唯一订单号
trade_no              string     是         平台订单号(prepay_id)
trade_type            string     是         JSAPI、H5
nonce_str             string     是         32位随机数
sign                  string     是         返回数据签名
===================== ========== ========== =================================================

3. H5唤起支付
::::::::::::::::::::::::::::::::

:说明: h5支付页面地址 ，浏览器直接HTTP 302
:支付页面: https://XXX/hicoinfe/payment  [参考 `附录一 <http://docs.hicoin.vip/zh/latest/API-Platform/appendix_1.html>`_ ]
:请求方式: GET
:请求参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
appId                 String     是          应用id：8888888888888888 ,16位
timeStamp             String     是          当前的时间戳：1414561699， 32位
nonceStr              String     是          随机字符串，见下方说明
package               String     是          统一下单接口返回的prepay_id参数值，见下方说明
signType              String     是          签名类型，见下方说明
paySign               String     是          签名，见下方说明，(此处签名请使用mch_key)
===================== ========== ========== =================================================

**重点字段说明：**

- nonceStr: 随机字符串，不长于32位。 例如：2K426TILTKCH16CQ25145I8ZNMTM67VS
- package: 统一下单接口返回的prepay_id参数值， 提交格式如：prepay_id=***：prepay_id=123456789 ，该参数请URLEncoder按utf-8编码， 128位
- signType: 支持HMAC-SHA256。 注意此处需与统一下单的签名类型一致： HMAC-SHA256， 32位
- paySign: 详见签名生成算法(附录二)

**页面访问示例：**

::

  https://api.hicoin.vip/hicoinfe/payment/?appId=4f95ab748e204c65d0bdaa61b4e3f1d7&nonceStr=2K426TILTKCH16CQ25145I8ZNMTM67VS&package=prepay_id%3D1048157710522051678581&signType=HMAC-SHA256&timeStamp=1577105620&paySign=30505B59FC77D4B44C989AA48024DC8F1DF59F533FCEA3BCD832032E94F37819


4. 支付订单查询
::::::::::::::::::::::::::::::::

:说明: 用户支付订单查询, 注意此接口需要公共参数
:接口地址: /pay/queryOrder
:请求方式: POST
:请求参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
app_id                 string    是         应用ID
access_token           string    是         基础access_token
lang                   string    是         i18n 语言,固定zh_CN
version                string    是         接口版本固定1.0
charset                string    是         固定utf8
nonce_str              string    是         32位随机数
sign                   string    是         参数签名 (此处签名请使用mch_key)
biz_content            string    是         业务请求参数的集合json
===================== ========== ========== =================================================


**biz_content结构体**

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
out_trade_no          string     是         第三方网站唯一订单号
===================== ========== ========== =================================================


:响应参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
out_trade_no          string     是         第三方网站唯一订单号
trade_no              string     是         平台订单号(prepay_id)
trade_type            string     是         JSAPI或H5
trade_status          string     是         订单状态,说见下方说明
total_amount          long       是         订单币种数量,精度8位
settle_currency       string     是         购买币种：固定为USDT
settle_trans_amount   long       是         平台实际收到币数量,精度8位
subject               string     是         订单标题
body                  string     是         订单说明
trade_time            string     是         订单时间
timeout_express       string     是         订单过期时间
openid                string     是         用户openid
nonce_str             string     是         32位随机数
sign                  string     是         返回数据签名
===================== ========== ========== =================================================

**重点字段说明：**

- trade_status: NOTPAY (待支付)，SUCCESS（已支付）， CLOSED（订单过期或关闭） UNKNOW（未知状态）

5. 异步通知支付订单
::::::::::::::::::::::::::::::::

:说明: 异步通知支付订单
:接口地址: 地址由第三方提供
:请求方式: POST
:请求参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
app_id                string     是         应用app_id
trade_status          string     是         订单状态
trade_no              string     是         平台订单号
out_trade_no          string     是         第三方订单号
openid                string     是         用户openid
trade_type            string     是         JSAPI或者H5，与预下单接口中trade_type一致
total_amount          string     是         支付币数量，8位精度
settle_currency       string     是         支付币种
passback_params       string     是         回传参数
body                  string     是         订单说明
subject               string     是         订单标题
nonce_str             string     是         32位随机数
sign                  string     是         参数签名 (此处签名请使用mch_key)
===================== ========== ========== =================================================


:响应参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
无                    string     是         输出SUCCESS或FAIL文本
===================== ========== ========== =================================================
