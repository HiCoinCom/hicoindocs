
2.5 获取用户指定币账户
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 根据币种及用户ID查询用户的账户。另外，若商户开启自动归集后，用户账户将被转移到商户的归集账户中
:接口地址: /api/v2/account/getByUidAndSymbol
:请求方式: GET
:请求参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一表示
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
