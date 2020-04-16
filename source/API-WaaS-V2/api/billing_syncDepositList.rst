
2.12 同步充值记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 同步充值记录
:接口地址: /api/v2/billing/syncDepositList
:请求方式: GET
:请求参数:


========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一表示
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
time	    long	     必填	          当前时间戳
charset   String     必填            编码格式，无特殊情况，传参数utf-8
version   String     必填            接口版本号，无特殊情况，传参数v2
max_id	  int	       必填	          返回大于id的100条充值记录数据
========= ========== ============= ===================================================


:请求参数示例:

::

	appid=baaceb1e506e1b5d7d1f0a3b1622583b&data=9fEODHjOOQ1vKGv4nm_EqWrE62XQOr5cFFYOC3Cr-v5d26MLpI7v4ymRFkANT64d5mjIXjkVj6qwrf4PeUbO3rTiRpKPGIQhyoZyR7QTBuv6A4CgxlVl_A2dNy_DZO_cGUNsRyyzUkf0uuuykhDtmBZg6o1oYA1OEWxZdexwjpnn8NSWB4WbPgntZKstbjpAW7xJR6HXekRf4CoEDjuKSYwhs08rk6HiB08Vx6x1KvG_0neBq7Z0hsSHxYKjrQTm9VQLeH5qsXtqPGk07RLHHY_EiT9Uh9hTC5xWx7uq70CsJ9GGIs9ZenQh-dda6gmNecgs94-qsZVUkfkSL07kTg


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


===================== ========== =========== =================================================
Param                 类型        是否必须     说明
id                    int        必填         充值唯一id
uid                   int        必填         充值用户id
symbol                String     必填         币种
amount                String     必填         充值金额
created_at            String     必填         创建时间
updated_at            String     必填         修改时间
txid                  String     必填         区块链交易ID
confirmations         int        必填         区块链确认数
address_to            String     必填         充值到帐地址
status                int        必填         0待确认，1 已完成，2 异常
===================== ========== =========== =================================================



:响应示例:

::

	{"data":"T1IaOzF2XfNaAOb3XqSFxCq6nu45SpiD9anDIlxHda_lOwX2kNNAl84OOsVnAsMg4IBQICD6_PMglpU5InzL_Q1AoNf_l1kPlk_fMXvmpEz25OAVJ499UYmBpH83TQclFfsxPKaFhIgeNGYgVGaS3BdT4Z0EBmfbMAz9aTa4n5z9Ns4q4b6En030GLINhC8PmaEQ5PDq5ZXZTKiKSrRNpNRi3_FR8hdIJGOLFU6t1Yb2nxqB1D-fY6eRtSHQnCCyas73kj-_kAhyW4dGss7vqKQZPmDe38qSYPrQUoDlJgK_8aCKG8fvJmoC9s3-o3InALAGp3yOawn32E1AxZtNbDQcUux6xbyAhhIOBhyN_V2LPR9yOtJQvm3XbdMxk58i-Y6oZl_YtBdfRncvhDJnAPqP3MN4sdbuC3JaC19bKikTDykXzFgD2_rHN4CO8QHUAefRAm-x9hj_sHFOwrJdL9g1H2Auzz1cES4zcp5RKHsduFnUNlvoKRNl9SUuIbDahTtBHlF1Gw9xy1my9KMB2X-u1vvnL83hvp4Rqnz0SyMfnpEnqRph43cCiyj7Ii3cf-Ai8h2i-5yIqr2qDKJoL5GqaOu6hr5atO4IZXZPzY175wZ4nNpCueBXRHoWB2foVmLu_F6xwq06XKDR9U5JYln3iol9DX2OhqM0Bs8cPqw"}

:响应数据解密后示例:


::

	{
	    "code":"0",
	    "data":[
	        {
	            "withdraw_fee":"0",
	            "symbol":"BTC",
	            "amount":"0.0001",
	            "real_fee":"0",
	            "fee":"0",
	            "address_to":"1CfYiePwcf3mWhLBQH2ac35C7jmE2udQqH",
	            "created_at":1539050731000,
	            "txid":"",
	            "confirmations":0,
	            "address_from":"",
	            "uid":10596,
	            "withdraw_fee_symbol":"BTC",
	            "fee_symbol":"BTC",
	            "saas_status":0,
	            "updated_at":1543483252000,
	            "company_status":2,
	            "id":45325,
	            "request_id":"",
	            "status":2
	        },
	        {
	            "withdraw_fee":"0.0000001",
	            "symbol":"BTC",
	            "amount":"0.0001",
	            "real_fee":"0",
	            "fee":"0.0000001",
	            "address_to":"17m2GM8aRrrnxPt5JhYPJd4qUFqF8rJDop",
	            "created_at":1539065092000,
	            "txid":"",
	            "confirmations":0,
	            "address_from":"",
	            "uid":10595,
	            "withdraw_fee_symbol":"BTC",
	            "fee_symbol":"BTC",
	            "saas_status":1,
	            "updated_at":1543851222000,
	            "company_status":2,
	            "id":45332,
	            "request_id":"",
	            "status":2
	        }
	    ],
	    "msg":"成功"
	}
