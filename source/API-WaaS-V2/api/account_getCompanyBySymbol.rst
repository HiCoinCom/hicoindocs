
2.6 获取商户归集账户余额
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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
