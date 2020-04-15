
2.9 批量获取提现记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 批量获取提现记录
:接口地址: /api/v2/billing/withdrawList
:请求方式: GET
:请求参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一表示
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

========= ========== ============= ===================================================
Param	    类型        是否必须        说明
time	    long	     必填	          当前时间戳
charset   String     必填            编码格式，无特殊情况，传参数utf-8
version   String     必填           接口版本号，无特殊情况，传参数v2
ids       String	   必填	          多个request_id使用逗号隔开，最多100个request_id
========= ========== ============= ===================================================


:请求参数示例:

::

	appid=baaceb1e506e1b5d7d1f0a3b1622583b&data=GCJBk77n7epyOexdGZ20qvukd321TpJ62lIAtlCinW6TzHx8SIbm6evXGulO87UgLTzIWCtgupgeLJKDdZmC7msuPNBGK--Ec27WZXjuhI0gNWXcOVk5RW_VRVcyfJ1Ml-DMW8XVxZRgA2U1bt9BztiyfryzMGj8_jl1IXd5sOQfPYXulCdm70WyTJpjsDkuMSov6QUmOn-C_-HUoZ7s715EMeZ60D09uUsF0i6mKLhFZTEQZPGPeJITYSJNddAw7nvqvX2KzNc6YUeCQhEmU1Dfxp65W4e3SVOgpd_2Q-dLN1MpOlkUKwbmbpb-gEh_s68yl7ox6WSgKfCK4i_uvA


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

===================== ========= ========== ======================================================================================================
Param                 类型        是否必须     说明
request_id            String     必填        请求id
id                    int        必填        提现id
uid                   int        必填        提现用户id
symbol                String     必填        币种
amount                String     必填        提现金额
withdraw_fee_symbol   String     必填        提现手续费币种
withdraw_fee          String     必填        提现手续费
fee_symbol            String     必填        挖矿手续费币种
real_fee              String     必填        旷工费
created_at            String     必填        创建时间,
updated_at            String     必填        修改时间
address_from          String     必填        来源地址
address_to            String     必填        到账地址
txid                  String     必填        区块链交易ID
confirmations         int        必填        区块链确认数
saas_status           int        必填        平台审核状态
company_status        int        必填        商户审核状态
status                int        必填        提现状态: 0 未审核，1 审核通过，2 审核拒绝，3 支付中已经打币，4 支付失败，5 已完成，6 已撤销
===================== ========= ========== ======================================================================================================


:响应示例:

::

	{"data":"LK4D5mrtvTubDxCQM4lqyN2h8TTIkEBL_06FrrrzLrImyMO4Yuac-wdbk5VnGVfCKB5EFaUb162xXUJdTHhpA5CGBCAQKl64h_Dt10C-H8KIoap9dZI90qE4f-mAMAyjF1QzKXJ-f-R_3J3bRGqfHFBRXebh08R8MdRDssniopVOhsFUs4gBxUensKas3_ta15eFIqXPjIgJWfYQCD2DUi1gaKgmN-5Q_tgt-qXp5Y2uh3yfM4g4k71Ahyel3G8S_AktbWl2G9wU3cri3ZVQEo0faIpkX_CKsk9V1YoY5yRopvJbxNtkG9lBFxKnureAQo0KP3f1tsIMOzgcyEXPnA"}

:响应数据解密后示例:

::

	{
	    "code":"0",
	    "data":[
	        {
	            "withdraw_fee":"0.4",
	            "symbol":"LTC",
	            "amount":"10",
	            "real_fee":"0",
	            "fee":"0",
	            "address_to":"LhFrA5ZJL15UdRV1uEfFxfdqWJUbBhXpRk1",
	            "created_at":1551429063000,
	            "txid":"",
	            "confirmations":0,
	            "address_from":"",
	            "uid":10739,
	            "withdraw_fee_symbol":"ETH",
	            "fee_symbol":"LTC",
	            "saas_status":0,
	            "updated_at":1551429063000,
	            "company_status":0,
	            "id":48393,
	            "request_id":"123",
	            "status":0
	        }
	    ],
	    "msg":"成功"
	}
