
2.13 批量获取充值记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 批量获取充值记录
:接口地址: /api/billing/depositList
:请求方式: GET
:请求参数:

======= ======= ======== =================================================
param   type    是否必须   说明
app_id  string  必填      商户的唯一标识
time    long    必填      时间戳
sign    string  必填      签名
ids     string  必填      充值id，多个id使用逗号分割，最多100个
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
id                    int     必填      充值唯一id
uid                   int     必填      充值 用户id
symbol                String  必填      币种
amount                String  必填      充值金额
created_at            String  必填      创建时间,
updated_at            String  必填      修改时间
txid                  String  必填      区块链交易ID
confirmations         int     必填      区块链确认数
address_to            String  必填      充值到帐地址
status                int     必填      0待确认，1 已完成，2 异常
===================== ======= ======== =================================================


:响应示例:

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
