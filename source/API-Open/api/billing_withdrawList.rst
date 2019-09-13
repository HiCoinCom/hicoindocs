
2.11 批量获取提现记录
~~~~~~~~~~~~~~~~~~~~~~~~
:说明: 批量获取提现记录
:接口地址: /api/billing/withdrawList
:请求方式: GET
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
app_id	string	必填	商户的唯一标识
time	long	必填	时间戳
sign	string	必填	签名
ids	string	必填	多个request_id使用逗号隔开，最多100个request_id
======= ======= ======== =================================================

:响应参数:

======= ======= ======== =================================================
param	type	是否必须	说明
code	string	必填	
msg	string	必填	
data	json	必填	详见下方data响应参数说明
======= ======= ======== =================================================

:Data响应参数:

===================== ======= ======== =================================================
param                 type    是否必须  说明
request_id            String  必填      请求id,
id                    int     必填      提现id
uid                   int     必填      提现用户id
symbol                String  必填      币种
amount                String  必填      提现金额
withdraw_fee_symbol   String  必填      提现手续费币种
withdraw_fee          String  必填      提现手续费
fee_symbol            String  必填      挖矿手续费币种
real_fee              String  必填      旷工费
created_at            String  必填      创建时间,
updated_at            String  必填      修改时间
address_from          String  必填      来源地址
address_to            String  必填      到账地址
txid                  String  必填      区块链交易ID
confirmations         int     必填      区块链确认数
saas_status           int     必填      平台审核状态
company_status        int     必填      商户审核状态
status                int     必填      提现状态
===================== ======= ======== =================================================

:响应示例:

::

	{
		"code": "0",
		"msg": "suc",
		"data": [
			{ 
				"request_id":"11",
				"id": 123,
				"uid"：2,
				"symbol "："ETH",
				"amount"："0.0002",
				"withdraw_fee_symbol"："BTC"，
				"withdraw_fee"："1"，
				"fee_symbol"：""，
				"real_fee": "0.0000000000000001",
				"created_at":1545273830000,
				"updated_at":1545273830000,
				"address_from"："0x794b0c610e011d0d40c810ef146b4dd989a67152"，
				"address_to": "0x754b0c610e311d0d00c810ef857b4dd989a67162",
				"txid":"78d1edef3b3fd14365f88cf2d03e8c29ec49ac1a43cedde9e21d320b3268f4de",
				"confirmations":11,
				"saas_status":1,
				"company_status":1,
				"status":1
			}
		]
	}

