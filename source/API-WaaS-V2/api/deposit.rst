用户充值
======================


同步充值记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 同步充值记录
:接口地址: /api/v2/billing/syncDepositList
:请求方式: GET
:请求参数:


========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
time	    long	     必填	          当前时间戳
charset   String     必填           编码格式，无特殊情况，传参数utf-8
version   String     必填           接口版本号，无特殊情况，传参数v2
max_id	  int	       必填	          返回大于id的100条充值记录数据
========= ========== ============= ===================================================


:请求参数示例:

::

	app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=9fEODHjOOQ1vKGv4nm_EqWrE62XQOr5cFFYOC3Cr-v5d26MLpI7v4ymRFkANT64d5mjIXjkVj6qwrf4PeUbO3rTiRpKPGIQhyoZyR7QTBuv6A4CgxlVl_A2dNy_DZO_cGUNsRyyzUkf0uuuykhDtmBZg6o1oYA1OEWxZdexwjpnn8NSWB4WbPgntZKstbjpAW7xJR6HXekRf4CoEDjuKSYwhs08rk6HiB08Vx6x1KvG_0neBq7Z0hsSHxYKjrQTm9VQLeH5qsXtqPGk07RLHHY_EiT9Uh9hTC5xWx7uq70CsJ9GGIs9ZenQh-dda6gmNecgs94-qsZVUkfkSL07kTg


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
created_at            Long       必填         创建时间
updated_at            Long       必填         修改时间
txid                  String     必填         区块链交易ID
confirmations         int        必填         区块链确认数
address_to            String     必填         充值到帐地址
status                int        必填         0待确认，1 成功，2 失败，4 待KYT验证，5 待人工审核(KYT风险等级过高)，6 待人工审核(KYT充值熔断)
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





批量获取充值记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 批量获取充值记录
:接口地址: /api/v2/billing/depositList
:请求方式: GET
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
ids       String  必填	      多个充值id使用逗号隔开，最多100个id
========= ======= ========== ===================================================

::

	app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=L-GwqoS2NJAOIUHMM5NAqJJvBKxWLjANyh1UHRvQbFUCHfzJBxEpGi514sI_J051wO4QMK9xeZK6_f7p_CIQfVJ7kiq7FNmflHnyjPT9tGdL6h7GSnHcPFEUUyHA7hJlvt3BtPyYuaEN9s1cJ1c8DzlOLTnzRF5EiPPrw-Yq0wtBYORIjEtfOBEMChF5vxu-FIjb3Nx4usIeWEamkC5WpkjRcjPZlE7-pRnA59fgHMtA3-hvsxJYwhCKLFkq-fAPfpTf4IpgZWdmrCEfGAdExSDCoQVNEJZgZnonzy5bDsUBQIRWuJZbO5u0JYnjdBliqpOi_L6j_chbe_er2eT5_w



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
created_at       Long       必填       创建时间,时间戳
updated_at       Long       必填       修改时间，时间戳
txid             String     必填       区块链交易ID
confirmations    int        必填       区块链确认数
address_to       String     必填       充值到帐地址
status           int        必填       0待确认，1 成功，2 失败，4 待KYT验证，5 待人工审核(KYT风险等级过高)，6 待人工审核(KYT充值熔断)
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






用户充值异步回调通知
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 此接口仅定义了接口规范，具体接口需要开发者实现
:接口地址: 接口地址由开发者提供，联系管理员在平台进行配置即可
:请求方式: POST
:请求参数:


========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================


:请求参数data解密之后数据结构:

充值通知：

===================== ========== ============= ===================================================
Param	                 类型        是否必须       说明
charset                String      是           编码格式，无特殊情况，传参数utf-8
version                String      是           接口版本号，无特殊情况，传参数v2
side                   String      是           通知类型， 充值通知：deposit， 提现通知： withdraw
notify_time            string      是           通知时间
id                     string      是           充值id
uid                    string      是           提现用户id
symbol                 string      是           币种
amount                 string      是           提现金额
address_to             string      是           充值地址
created_at             string      是           创建时间
updated_at             string      是           修改时间
txid                   string      是           区块链交易ID
confirmations          string      是           区块链确认数
status                 string      是           充值状态     0待确认，1 成功，2 失败，4 待KYT验证，5 待人工审核(KYT风险等级过高)，6 待人工审核(KYT充值熔断)
===================== ========== ============= ===================================================



:请求参数示例:

::

  app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=UoJC0VeVSvdOCYbkUIQxnJ2k-MINFmdfhHo1bpgK1kqcCKEZ1MtBFmvMnrZsmpQKVyNbFyBmLHzOk_T5FTxKA0VROneKR4wyK0G6HPQM6pDeSz2BPwwaw-2uiBSiPeQEwOabWl0MLyoJyj1g4VLcBgazCYeD5YPJXFOzjAEgkhfbMEcoS1to_ooISnIMeQvhj8g3I3m5k519eJ9KWOv5R3_EGMaI-yLlCB5CIVd4byjnBxDJxsRMR7yuEhIjfvsy49MgglSTrddCFu3ZHNwGlv_DzTJIMhJHRV7z4x8YQV2atP-BBgY9eozPa0JIkjBctdqigvzJs5nsbl76wL5Gv5-icGv4qtOF0w11t0oPi051Y7fiuPJ20BK6GAPEu_HroTvcWh-3vh2_U03Donv306HMvC-vXrQH18TGVqjtOlVhQW_wg4PF9fjMgNCsk3k57vzVfuRruurLv6-FD6HRvoUe4WfgSAi-jMRpuwXC8mL44r-dLDfo4wUdrjEk8tkjSZea8O066bJeVVUU3rD7qqL32Uf-3Bkcy26jsHLf-QK8oYi2xjddd2PSoHnpSIbRdDYrYLdO_zUFZudg4FBHFzQ6sSLesS_jA63xJZS1xk6EjejaSpID3r-7YXDQtM3y5O1TG3URmF5sVbWL5iekubN2jEjkQ2QdV4hz0sBdmlx8GrPUWSnbtLMV7zcxAhyodzIeWeeZCKeu1AF903YJvKZls8eKMEvd__PYSnnRtXVxNUvFFo-GL3sOtDAAhjKdLLSWCVGqDQsKSrORffejbDeHVGsmtFxPC5kvKHLbJvAW6QDzpG8hqmZLrtjxvTmcVMt1_hn9-VSi-qFW8xPorYmF5Hw1G5nZca7NK5k2Qs6xieNgw34Sps-tj38WxhXacRwlEp1Yt3Jj3BlMlxCD9VWxWO17Yvj3MmJTNgf-d22PvPV_mZrJaqjm6BSfuz9DVYVjsIuZF_eOgMaVTm31FFuFZvPF9G_lhC4CQ0Zb5KfpYx0NMJjGfBPtxZ3MsF8H


:响应参数:

返回字符串：SUCCESS表示成功，FAILURE表示失败 （注意此处返回参数无需进行加密）


获取归集矿工费
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 账户类型的币种充值后需要进行归集，UTXO无归集矿工费费用
:接口地址: /api/v2/billing/syncMinerFeeList
:请求方式: GET
:请求参数:


========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================


:请求参数data解密之后数据结构:


===================== ========== ============= ===================================================
Param	                 类型        是否必须       说明
time                   long       必填           当前时间戳
charset                String     必填           编码格式，无特殊情况，传 参数 utf-8
version                String     必填           接口版本号，无特殊情况， 传参数 v2
max_id                 int        必填           返回大于 id 的 100 条归集矿 工费记录数据
===================== ========== ============= ===================================================



:请求参数示例:

::

  app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=L-GwqoS2NJAOIUHMM5NAqJJvBKxWLjANyh1UHRvQbFUCHfzJBxEpGi514sI_J051wO4QMK9xeZK6_f7p_CIQfVJ7kiq7FNmflHnyjPT9tGdL6h7GSnHcPFEUUyHA7hJlvt3BtPyYuaEN9s1cJ1c8DzlOLTnzRF5EiPPrw-Yq0wtBYORIjEtfOBEMChF5vxu-FIjb3Nx4usIeWEamkC5WpkjRcjPZlE7-pRnA59fgHMtA3-hvsxJYwhCKLFkq-fAPfpTf4IpgZWdmrCEfGAdExSDCoQVNEJZgZnonzy5bDsUBQIRWuJZbO5u0JYnjdBliqpOi_L6j_chbe_er2eT5_w


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

================== ========== ============= ===================================================
Param              类型        是否必须        说明
id                 int         是             归集唯一ID
symbol             String      是             币种
amount             String      是             归集金额
fee                String      是             归集手续费
created_at         Long        是             创建时间
updated_at         Long        是             修改时间
txid               String      是             区块链交易ID
confirmations      int         是             区块链确认数
status             int         是             0待确认，1 成功，2 失败，4 待KYT验证，5 待人工审核(KYT风险等级过高)，6 待人工审核(KYT充值熔断)
address_to         String      是             充值到账地址
address_from       String      是             充值发送地址
txid_type          String      是             0 链上交易，1 联盟转账交易
base_symbol        String      是             主链币名称
contract_address   String      是             币种合约地址
email              String      是             邮箱
================== ========== ============= ===================================================



:响应示例:

::

	{"data":"T1IaOzF2XfNaAOb3XqSFxCq6nu45SpiD9anDIlxHda_lOwX2kNNAl84OOsVnAsMg4IBQICD6_PM glpU5InzL_Q1AoNf_l1kPlk_fMXvmpEz25OAVJ499UYmBpH83TQclFfsxPKaFhIgeNGYgVGaS3BdT4Z0EBm fbMAz9aTa4n5z9Ns4q4b6En030GLINhC8PmaEQ5PDq5ZXZTKiKSrRNpNRi3_FR8hdIJGOLFU6t1Yb2nxqB1D -fY6eRtSHQnCCyas73kj-_kAhyW4dGss7vqKQZPmDe38qSYPrQUoDlJgK_8aCKG8fvJmoC9s3-o3InAL AGp3yOawn32E1AxZtNbDQcUux6xbyAhhIOBhyN_V2LPR9yOtJQvm3XbdMxk58i-Y6oZl_YtBdfRncvhDJ nAPqP3MN4sdbuC3JaC19bKikTDykXzFgD2_rHN4CO8QHUAefRAm-x9hj_sHFOwrJdL9g1H2Auzz1cES4zc p5RKHsduFnUNlvoKRNl9SUuIbDahTtBHlF1Gw9xy1my9KMB2X-u1vvnL83hvp4Rqnz0SyMfnpEnqRph43cCi yj7Ii3cf-Ai8h2i-5yIqr2qDKJoL5GqaOu6hr5atO4IZXZPzY175wZ4nNpCueBXRHoWB2foVmLu_F6xwq06 XKDR9U5JYln3iol9DX2OhqM0Bs8cPqw"}


:响应数据解密后示例:

::

  { "code":"0",
    "data":[
           {
           "id":1,
            "symbol":"BTC",
            "amount":"11",
            "fee":"0.00111",
            "created_at":1539050731000,
            "updated_at":1543483252000,
            "txid":"",
            "confirmations":0,
            "status":2,
            "address_from":"",
            "address_to":"",
            "txid_type":"1",
            "base_symbol":"",
            "contract_address":"123",
            "email":""
            }
       ],
    "msg": "成功"
    }
