授权
====================

1. 授权流程
::::::::::::::::
如果您熟悉通用OAuth授权流程，那么接下来对接授权流程会相对容易。如果您了解并不是很深刻，建议您先阅读`相关文献`__，这将有助于您接来下的对接过程顺利进行。下图描述了平台授权的整个流程：

.. __: https://oauth.net/2/

.. image:: images/openapi_oauth_flow.png
   :width: 600px
   :height: 455px
   :align: center

具体流程如下：

1) 用户访问第三方网站；
#) 第三方应用服务器判断用户是否已经通过授权，如果已经授权通过，用户即可正常访问第三方应用，否则第三方需要通过浏览器访问HiCoin的`2.1 授权页面`_进行授权。
#) 授权通过之后，HiCoin授权服务器会重定向到第三方网址，重定向地址为授权页面请求参数的redirect_uri。
#) 上一步重定向的地址会带上参数，类似如： redirect_uri/?code=CODE&state=STATE， 其中CODE为授权的临时凭证。调用接口使用CODE换取accss_token和openid。
#) 整个授权过程结束。

2. 授权相关接口
::::::::::::::::

2.1 授权页面
''''''''''''''''
:说明: 第三方静默授权页面，注意：此接口无需公共参数
:页面地址: /api/connect/oauth/authorize [附录3]
:请求参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
app_id                string     是         第三方标识
redirect_uri          string     是         授权后重定向的链接地址，请使用urlencode对链接进行处理
response_type         string     是         授权类型，传固定值code
scope                 string     是         应用授权作用域，说见下方重点字段说明
state                 string     是         重定向后会带上state参数，开发者可以填写a-zA-Z0-9的参数值，最多128字节
wallet_redirect       string     是         无论直接打开还是做页面302重定向时候，必须带此参数
===================== ========== ========== =================================================

**重点字段说明：**

- scope: snsapi_base（不弹出授权页面，直接跳转，只能获取用户openid），snsapi_userinfo（弹出授权页面，可通过openid拿到昵称、性别、所在地。并且， 即使在未关注的情况下，只要用户授权，也能获取其信息 ），目前snsapi_userinfo暂不支持，排期开发中，敬请期待。
- state: 重定向后会带上state参数，开发者可以填写a-zA-Z0-9的参数值，最多128字节
- wallet_redirect：该参数值请设置为 #wallet_redirect。类似于这种形式：/api/connect/oauth/authorize?state=abc&#wallet_redirect

授权通过之后，授权服务器会重定向到第三方网址（redirect_uri），并且会在redirect_uri拼接code和state参数。

::

  授权页面访问地址类似于： http://oauth.hicoin.one/api/connect/oauth/authorize?app_id=xx&redirect_uri=https%3a%2f%2fwww.xyz.com%3fa%3db%26c%3dd&response_type=code&scopesnsapi_base&state=xxx&#wallet_redirect

  重定向的地址类似于： https://www.xyz.com?a=b&c=d&code=12343455335&state=xxx


2.2 授权code换取access_token与openid
'''''''''''''''''''''''''''''''''''''''

说明: 授权code换取token
:接口地址: /sns/oauth/access_token
:请求方式: POST
:请求参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
app_id                string     是         第三方标识
secret                string     是         第三方key
code                  string     是         填写上面获取的code参数
grant_type            string     是         填写固定值： authorization_code
===================== ========== ========== =================================================


:响应参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
access_token          string     是         授权access_token，网页授权接口调用凭证。 注意：此access_token与基础access_token不同
expires_in            string     是         access_token接口调用凭证超时时间，单位（秒）
refresh_token         string     是         用户刷新access_token
openid                string     是         平台用户的唯一标识
scope                 string     是         用户授权的作用域，使用逗号（,）分隔
===================== ========== ========== =================================================

2.3 刷新access_token
'''''''''''''''''''''''''''''''''''''''
:说明: access_token一段时间之后会过期，通过此接口可以获取新的access_token
:接口地址: /sns/oauth/refresh_token
:请求方式: POST
:请求参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
app_id                string     是         第三方标识
grant_type            string     是         填写固定值：refresh_token
refresh_token         string     是         填写通过access_token获取到的refresh_token参数
===================== ========== ========== =================================================


:响应参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
access_token          string     是         网页授权接口调用凭证, 注意：此access_token与基础支持的access_token不同
expires_in            string     是         access_token接口调用凭证超时时间，单位（秒）
refresh_token         string     是         用户刷新access_token
openid                string     是         用户唯一标识
scope                 string     是         用户授权的作用域，使用逗号（,）分隔
===================== ========== ========== =================================================


2.4 获取用户基本信息
'''''''''''''''''''''''''''''''''''''''

:说明: 获取用户基本信息
:接口地址: /sns/user/info
:请求方式: GET
:请求参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须     说明
app_id                 string     是         应用ID
access_token           string     是         授权access_token
lang                   string     是         i18n 语言,固定zh_CN
version                string     是         接口版本固定1.0
charset                string     是         固定utf8
openid                 string     是         用户唯一标识
===================== ========== ========== =================================================


:响应参数:

===================== ========== ========== =================================================
参数名                 数据类型    是否必须    说明
openid                string     是         用户唯一标识
nickname              string     是         用户昵称
mobile_number         string     是         用户手机号
country_code          string     是         手机号对应的国家编码
email                 string     是         邮箱
origin                string     是         用户来源
role                  string     是         用户在经济人中的角色
parent_mobile_number  string     是         邀请人手机号
parent_country_code   string     是         邀请人手机号对应的国家编码
parent_email          string     是         邀请人邮箱
===================== ========== ========== =================================================
