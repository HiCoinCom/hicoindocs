
2.11 批量获取充值记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 批量获取充值记录
:接口地址: /api/v2/billing/depositList
:请求方式: GET
:请求参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一表示
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

========= ======= ========== ===================================================
Param     类型     是否必须    说明
time      long    必填	      当前时间戳
charset   String  必填        编码格式，无特殊情况，传参数utf-8
version   String  必填        接口版本号，无特殊情况，传参数v2
ids       String  必填	      多个充值id使用逗号隔开，最多100个id
========= ======= ========== ===================================================

::

	appid=baaceb1e506e1b5d7d1f0a3b1622583b&data=L-GwqoS2NJAOIUHMM5NAqJJvBKxWLjANyh1UHRvQbFUCHfzJBxEpGi514sI_J051wO4QMK9xeZK6_f7p_CIQfVJ7kiq7FNmflHnyjPT9tGdL6h7GSnHcPFEUUyHA7hJlvt3BtPyYuaEN9s1cJ1c8DzlOLTnzRF5EiPPrw-Yq0wtBYORIjEtfOBEMChF5vxu-FIjb3Nx4usIeWEamkC5WpkjRcjPZlE7-pRnA59fgHMtA3-hvsxJYwhCKLFkq-fAPfpTf4IpgZWdmrCEfGAdExSDCoQVNEJZgZnonzy5bDsUBQIRWuJZbO5u0JYnjdBliqpOi_L6j_chbe_er2eT5_w



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

=============== ========= ========== ====================================================
Param            类型       是否必须   说明
id               int        必填       充值唯一id
uid              int        必填       充值 用户id
symbol           String     必填       币种
amount           String     必填       充值金额
created_at       String     必填       创建时间,
updated_at       String     必填       修改时间
txid             String     必填       区块链交易ID
confirmations    int        必填       区块链确认数
address_to       String     必填       充值到帐地址
status           int        必填       0待确认，1 已完成，2 异常
=============== ========= ========== ====================================================



:响应示例:

::

	{"data":"T1IaOzF2XfNaAOb3XqSFxCq6nu45SpiD9anDIlxHda_lOwX2kNNAl84OOsVnAsMg4IBQICD6_PMglpU5InzL_Q1AoNf_l1kPlk_fMXvmpEz25OAVJ499UYmBpH83TQclFfsxPKaFhIgeNGYgVGaS3BdT4Z0EBmfbMAz9aTa4n5z9Ns4q4b6En030GLINhC8PmaEQ5PDq5ZXZTKiKSrRNpNRi3_FR8hdIJGOLFU6t1Yb2nxqB1D-fY6eRtSHQnCCyas73kj-_kAhyW4dGss7vqKQZPmDe38qSYPrQUoDlJgK_8aCKG8fvJmoC9s3-o3InALAGp3yOawn32E1AxZtNbDQcUux6xbyAhhIOBhyN_V2LPR9yOtJQvm3XbdMxk58i-Y6oZl_YtBdfRncvhDJnAPqP3MN4sdbuC3JaC19bKikTDykXzFgD2_rHN4CO8QHUAefRAm-x9hj_sHFOwrJdL9g1H2Auzz1cES4zcp5RKHsduFnUNlvoKRNl9SUuIbDahTtBHlF1Gw9xy1my9KMB2X-u1vvnL83hvp4Rqnz0SyMfnpEnqRph43cCiyj7Ii3cf-Ai8h2i-5yIqr2qDKJoL5GqaOu6hr5atO4IZXZPzY175wZ4nNpCueBXRHoWB2foVmLu_F6xwq06XKDR9U5JYln3iol9DX2OhqM0Bs8cPqw"}

:响应数据解密后示例:


::

	{
		"code": "0",
		"msg": "suc",
		"data": [
			{
				"id" ：1,
				"uid" ：11,
				"symbol"："ETH",
				"amount"："0.0002000000000000",
				"created_at": 1545273830000,
				"updated_at": 1545273830000,
				"txid":"78d1edef3b3fd14365f88cf2d03e8c29ec49ac1a43cedde9e21d320b3268f4de",
				"confirmations":11,
				"status":1,
				"address_to":"0xcb03bfdccb50c9f62ec1c728f264bf453e037132"
			},
			{
				"id" ：2,
				"uid" ：12,
				"symbol" ："ETH",
				"amount"："0.0002000000000000",
				"created_at": 1545273830000,
				"updated_at": 1545273830000,
				"txid":"0xd609e050c3d573fb715431edbd36cc08eaa475f813de921026a65c0a96e8113e",
				"confirmations":11,
				"status":1,
				"address_to":"0xcb03bfdccb50c9f62ec1c728f264bf453e037132"
			}
		]
	}
