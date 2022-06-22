账户资产
==============


查询用户信息
-------------------

:说明: 查询用户信息。
:接口地址: /api/v2/user/info
:请求方式:  GET
:请求参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

========= ======= ========== ===================================================
Param     类型     是否必须    说明
time      long    必填	      当前时间戳
charset   String  必填        编码格式，无特殊情况，传参数utf-8
version   String  必填        接口版本号，无特殊情况，传参数v2
country	  String	可选	      国家编号，mobile不为空时，该字段必填。如：86
mobile	  String	可选	      手机号，手机和邮箱需要保证其中之一不能为空
email     string	可选	      邮箱，手机和邮箱需要保证其中之一不能为空
========= ======= ========== ===================================================


:请求参数示例:

::

	app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=GCJBk77n7epyOexdGZ20qvukd321TpJ62lIAtlCinW6TzHx8SIbm6evXGulO87UgLTzIWCtgupgeLJKDdZmC7msuPNBGK--Ec27WZXjuhI0gNWXcOVk5RW_VRVcyfJ1Ml-DMW8XVxZRgA2U1bt9BztiyfryzMGj8_jl1IXd5sOQfPYXulCdm70WyTJpjsDkuMSov6QUmOn-C_-HUoZ7s715EMeZ60D09uUsF0i6mKLhFZTEQZPGPeJITYSJNddAw7nvqvX2KzNc6YUeCQhEmU1Dfxp65W4e3SVOgpd_2Q-dLN1MpOlkUKwbmbpb-gEh_s68yl7ox6WSgKfCK4i_uvA



:响应参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
data      String     可选           加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================


:响应参数data解密之后:

========= ========== ============= ===================================================
Param	    类型        是否必须        说明
code	    String     是	           状态码
msg       String     是             响应结果说明
data      String     否             具体响应数据，数据结构定义如下
========= ========== ============= ===================================================

:data数据结构:

========= ========== ============= ===================================================
Param      类型       是否必须        说明
uid        int        是             用户在钱包服务的唯一标识
nickname   String     是             用户昵称
========= ========== ============= ===================================================



:响应示例:

::

	{"data":"LK4D5mrtvTubDxCQM4lqyN2h8TTIkEBL_06FrrrzLrImyMO4Yuac-wdbk5VnGVfCKB5EFaUb162xXUJdTHhpA5CGBCAQKl64h_Dt10C-H8KIoap9dZI90qE4f-mAMAyjF1QzKXJ-f-R_3J3bRGqfHFBRXebh08R8MdRDssniopVOhsFUs4gBxUensKas3_ta15eFIqXPjIgJWfYQCD2DUi1gaKgmN-5Q_tgt-qXp5Y2uh3yfM4g4k71Ahyel3G8S_AktbWl2G9wU3cri3ZVQEo0faIpkX_CKsk9V1YoY5yRopvJbxNtkG9lBFxKnureAQo0KP3f1tsIMOzgcyEXPnA"}

:响应数据解密后示例:

::

	{"code":"0","data":{"uid":3529218,"nickname":""},"msg":"成功"}






获取支持的币种列表
-------------------

:说明: 获取商户的币种列表
:接口地址: /api/v2/user/getCoinList
:请求方式: GET
:请求参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

========= ======= ========== ===================================================
Param     类型     是否必须     说明
time      long    必填	      当前时间戳
charset   String  必填        编码格式，无特殊情况，传参数utf-8
version   String  必填        接口版本号，无特殊情况，传参数v2
========= ======= ========== ===================================================


:请求参数示例:

::

  app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=GCJBk77n7epyOexdGZ20qvukd321TpJ62lIAtlCinW6TzHx8SIbm6evXGulO87UgLTzIWCtgupgeLJKDdZmC7msuPNBGK--Ec27WZXjuhI0gNWXcOVk5RW_VRVcyfJ1Ml-DMW8XVxZRgA2U1bt9BztiyfryzMGj8_jl1IXd5sOQfPYXulCdm70WyTJpjsDkuMSov6QUmOn-C_-HUoZ7s715EMeZ60D09uUsF0i6mKLhFZTEQZPGPeJITYSJNddAw7nvqvX2KzNc6YUeCQhEmU1Dfxp65W4e3SVOgpd_2Q-dLN1MpOlkUKwbmbpb-gEh_s68yl7ox6WSgKfCK4i_uvA


:响应参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
data      String     可选           加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================


:响应参数data解密之后:

========= ========== ============= ===================================================
Param	    类型        是否必须        说明
code	    String     是	           状态码
msg       String     是             响应结果说明
data      String     否             具体响应数据，数据结构定义如下
========= ========== ============= ===================================================

:data数据结构:

====================== ======= =========== ====================================================
Param                  类型     是否必须      说明
symbol                 String  是           币种（调用提币的接口，及任何查询接口时务必使用此字段返回的值）
icon                   String  是           币种icon
real_symbol            String  是           币种链上名称
decimals	       String  是           精度
name                   string  是	   币种全称
base_symbol	       string  是	   主链币币名
contract_address       string  是           合约地址
deposit_confirmation   string  是           币种充值确认数
explorer               string  是           区块浏览器 
support_memo  	       string  是           是否支持memo，0不支持1支持       
support_token          string  是           是否支持token币，0不支持1支持,主链币才有值,代币为空
====================== ======= =========== ====================================================



:响应示例:

::

  {"data":"LK4D5mrtvTubDxCQM4lqyN2h8TTIkEBL_06FrrrzLrImyMO4Yuac-wdbk5VnGVfCKB5EFaUb162xXUJdTHhpA5CGBCAQKl64h_Dt10C-H8KIoap9dZI90qE4f-mAMAyjF1QzKXJ-f-R_3J3bRGqfHFBRXebh08R8MdRDssniopVOhsFUs4gBxUensKas3_ta15eFIqXPjIgJWfYQCD2DUi1gaKgmN-5Q_tgt-qXp5Y2uh3yfM4g4k71Ahyel3G8S_AktbWl2G9wU3cri3ZVQEo0faIpkX_CKsk9V1YoY5yRopvJbxNtkG9lBFxKnureAQo0KP3f1tsIMOzgcyEXPnA"}

:响应数据解密后示例:

::

  {
    "code":"0",
    "data":[
        {
            "symbol":"BTC",
            "icon":"http://chainup-oss.oss-cn-beijing.aliyuncs.com/saas/1565681771193.png"
        },
        {
            "symbol":"ETH",
            "icon":"http://hicoin.oss-cn-hongkong.aliyuncs.com/coin/1530015263780.png"
        },
        {
            "symbol":"BCH",
            "icon":"http://hicoin.oss-cn-hongkong.aliyuncs.com/coin/1530016466295.png"
        }
    ],
    "msg":"成功"
  }






获取指定用户的账户信息
----------------------

:说明: 根据币种及用户ID查询用户的账户。另外，若商户开启自动归集后，用户账户将被转移到商户的归集账户中
:接口地址: /api/v2/account/getByUidAndSymbol
:请求方式: GET
:请求参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

========= ======= ========== ===================================================
Param     类型     是否必须     说明
time      long    必填        当前时间戳
charset   String  必填        编码格式，无特殊情况，传参数utf-8
vesion    String  必填        接口版本号，无特殊情况，传参数v2
uid       String  必填	      用户ID
symbol    String  必填	      币种
========= ======= ========== ===================================================



:请求参数示例:

::

	app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=gxakMvhB3jCRn05W6GnZHtLyvnW11n-OgF6KinF-0azrubfLG45H1TPd76cGTq7DccyVlNHGlXR7aNpa9bRsDmPHtcILn0HGno2glIOItQTGLuiS_DOQaNKBhtf5VD-CZyyC3hKPxyPUuTdEV3D57oUy2BUIykwUFpO_rhCyZKMVmUHuzYL2jIyAATb6-cbfrJuzdB8IlsyvkTOxbltI45Ie3V7JI31pMwsyN5Q8qW1kGSxjcaQOeT43-3Em8y9bl4KRHkGC5UJdlhnHJogPK3kPqATHS6zJsziBiKRpjBnrOtV4HndzoHMk4SQuijvy0fdQ0KCkOAFJL7lAtp8p4Q


:响应参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
data      String     可选           加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================


:响应参数data解密之后:

========= ========== ============= ===================================================
Param	    类型        是否必须        说明
code	    String     是	           状态码
msg       String     是             响应结果说明
data      String     否             具体响应数据，数据结构定义如下
========= ========== ============= ===================================================

:data数据结构:

================= ========== ============= ===================================================
Param	            类型        是否必须        说明
normal_balance    String     必填           正常账户余额
lock_balance      String     必填           冻结账户余额
deposit_address   String     必填           币种对应的充值地址
================= ========== ============= ===================================================



:响应示例:

::

	{"data":"LK4D5mrtvTubDxCQM4lqyN2h8TTIkEBL_06FrrrzLrImyMO4Yuac-wdbk5VnGVfCKB5EFaUb162xXUJdTHhpA5CGBCAQKl64h_Dt10C-H8KIoap9dZI90qE4f-mAMAyjF1QzKXJ-f-R_3J3bRGqfHFBRXebh08R8MdRDssniopVOhsFUs4gBxUensKas3_ta15eFIqXPjIgJWfYQCD2DUi1gaKgmN-5Q_tgt-qXp5Y2uh3yfM4g4k71Ahyel3G8S_AktbWl2G9wU3cri3ZVQEo0faIpkX_CKsk9V1YoY5yRopvJbxNtkG9lBFxKnureAQo0KP3f1tsIMOzgcyEXPnA"}

:响应数据解密后示例:

::

  {"code":"0","data":{"normal_balance":"2.99400066","deposit_address":"0x6956f9af53b22117f2fc94dfe7c74ff3893b2acd","lock_balance":"0"},"msg":"成功"}






获取商户归集账户余额
---------------------

:说明: 开启商户资金自动归集之后，商户可以通过该接口种获取商户归集账户余额
:接口地址: /api/v2/account/getCompanyBySymbol
:请求方式: GET
:请求参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

========= ======= ========== ===================================================
Param     类型     是否必须     说明
time      long    必填        当前时间戳
charset   String  必填        编码格式，无特殊情况，传参数utf-8
vesion    String  必填        接口版本号，无特殊情况，传参数v2
symbol    String  必填	      币种
========= ======= ========== ===================================================



:请求参数示例:

::

	app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=YepWL0rl-SK3qhhHrH-Nk-0ohFqkhV33cLXRHHmIIDJ1GJbfy5aUHWxrG342gxkPvdQF-Hnq3ajez2eqrJIisNCXiUw7-f2TgXUdSlShGF-6I7QeSinclCbKj-sqsRpRS9lFFTGWz-GUuUJiWkgK6mCsEH3xMKM-14nHKU6R1K7lbsPMn61E4P8lxtkWs9uwB97hHADzSJswXF-jTCqY2xYZDILXQTm6wwMFVL3ynIV9YWosprAVOrkQ9hawxRl9vmJDvF85JI8qNaNMcmwlLNzBPLdeQJHjRTEkj2BtiNk3gU8IYAWifwVv0alFb8zrVIJbEm4S_GfybB2oOzNmOQ

:响应参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
data      String     可选           加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================


:响应参数data解密之后:

========= ========== ============= ===================================================
Param	    类型        是否必须        说明
code	    String     是	           状态码
msg       String     是             响应结果说明
data      String     否             具体响应数据，数据结构定义如下
========= ========== ============= ===================================================

:data数据结构:

================= ========== ============= ===================================================
Param	            类型        是否必须        说明
symbol            String     必填           币种名称
balance           String     必填           归集账户余额
================= ========== ============= ===================================================



:响应示例:

::

	{"data":"jwtkGrhh2EVJS8xe93MpUYd-SQ-TyK0Bx5sXjE4hygFNg4wmctiahtIYXRpR2j8yDaEF5YzVstnUKbOH2p44FSMjXMQU4qFrhD00WOfW7v4LNALyiQXRb_5sakR0Zf573lGfLRTPlzLtTho3gqu3hMwuAv5e3r2dpb6_jxh1Z9BjkzSsNRX_bjLcHLUOPhMvo6rTUKSa9LQ6QnT8RX0eqzOZPlnCw3TeX_zcWWjxp6fcpKcdODxoI86gHwWRpSd-2qbEbFcaT12CJd9nPXA0KnLPNNHWz8sxQGiAg7Jg_-cN_yBHL9cS15zecTemYGqpOXRkojM1JwLsjM-7txf_dw"}


:响应数据解密后示例:

::

	{"code":"0","data":{"symbol":"ETH","balance":"64.97599802"},"msg":"成功"}
