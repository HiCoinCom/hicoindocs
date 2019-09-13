
开放平台(Open API)文档
==============

1 更新记录
------------
=================== ============= ========
更新日志             时间           更新人 
文档创建             2019/03/13    罗斌 
接口错误码更新        2019/03/13    钟鹏华
增加提现地址校验，     2019/07/17    罗斌 
更新错误             2019/07/17     罗斌
=================== ============= ========

2 接口说明
--------------
文档为钱包服务对第三方应用提供的接口。

.. image:: ../images/apiopen-instructions.png
   :width: 586px
   :height: 153px
   :align: center

以下文档中的接口提供方称为 **钱包服务**，接口调用方称为 **第三方应用**。

3 接口规则
-----------
:传输方式: https(测试环境暂时使用 http)
:签名字段: 除了 sign 字段，其他所有必填项都需要参与签名 
:响应状态码为: 0,表示处理成功，非 0 表示请求错误或系统异常 
:请求地址: 域名+接口地址
:签名算法: 详见附 1

4 接口列表
------------------------

4.1 用户手机注册
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 注册成为钱包的用户。 
:接口地址: api/user/createUser 
:请求方式: POST
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
country	string	必填	国家编号，如：+86；注意请求时需要对该参数进行urlencode
mobile	string	必填	手机号
app_id	string	必填	商户的唯一标识
time	long	必填	当前时间戳
sign	string	必填	签名
======= ======= ======== =================================================

:响应参数:

======= ======= ======== =================================================
param	type	是否必须	说明
uid	int	必填	用户在钱包服务的唯一标识
======= ======= ======== =================================================

:响应示例:

::

	{
	    "code": "0",
	    "msg": "suc",
	    "data": {
	        "uid"：10000
	    }
	}


4.2 用户邮箱注册
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 注册成为钱包的用户。
:接口地址: api/user/registerEmail
:请求方式: POST
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
email	string	必填	邮箱
app_id	string	必填	商户的唯一标识
time	long	必填	当前时间戳
sign	string	必填	签名
======= ======= ======== =================================================

:响应参数:

======= ======= ======== =================================================
param	type	是否必须	说明
uid	int	必填	用户在钱包服务的唯一标识
======= ======= ======== =================================================

:响应示例:

::

	{
	    "code": "0",
	    "msg": "suc",
	    "data": {
	        "uid"：10001
	    }
	}


4.3 查询用户信息
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 查询用户信息。
:接口地址: api/user/info
:请求方式:  GET
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
country	string	可选	国家编号，如：+86；注意请求时需要对该参数进行urlencode
mobile	string	可选	手机号，手机和邮箱需要保证其中之一不能为空
email	string	可选	邮箱，手机和邮箱需要保证其中之一不能为空
app_id	string	必填	商户的唯一标识
time	long	必填	当前时间戳
sign	string	必填	签名
======= ======= ======== =================================================

:响应参数:

========== ======= ======== =================================================
param       type   是否必须   说明
uid         int    必填       用户在钱包服务的唯一标识
nickname    string 必填       用户昵称
========== ======= ======== =================================================

:响应示例:

::

	{
	    "code": "0",
	    "msg": "suc",
	    "data": {
	        "uid"：10001,
	        "nickname":"135****7778"
	    }
	}

4.4 获取用户指定币账户
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 根据币种及用户ID查询用户的账户
:接口地址: /api/account/getByUidAndSymbol
:请求方式: GET
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
uid	string	必填	用户ID
symbol	string	必填	币种
app_id	string	必填	商户的唯一标识
time	long	必填	当前时间戳
sign	string	必填	签名
======= ======= ======== =================================================

:响应参数:

================ ======= ======== =================================================
param            type    是否必须  说明
normal_balance   String  必填      正常账户余额
lock_balance.    String  必填      冻结账户余额
================ ======= ======== =================================================

:响应示例:

::

	{
		"code": "0",
		"msg": "suc",
		"data": {
			"normal_balance ":"32323.233",
			"lock_balance ":"32323.233",
			"deposit_address": "123dsdfe46wefsfsgsdy5teq"
		}
	}



4.5 获取用户所有币账户
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 根据用户ID查询用户所有币种的账户
:接口地址: /api/account/getAllAccount
:请求方式: GET
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
uid	string	必填	用户ID
app_id	string	必填	商户的唯一标识
time	long	必填	时间戳
sign	string	必填	签名
======= ======= ======== =================================================

:响应参数:

================ ======= ======== =================================================
param            type    是否必须  说明
symbol           string  必填      币种名称
normal_balance   string  必填      正常余额
lock_balance     string  必填      冻结余额
================ ======= ======== =================================================

:响应示例:

::

	{
	  "code": "0",
	  "msg": "suc",
	  "data":[
	      {
	        "symbol": "BTC",
	        "normal_balance": "1.00211211",
	        "lock_balance": "0.00211002"
	      },
	      {
	        "symbol": "ETH",
	        "normal_balance": "1.00211211",
	        "lock_balance": "0.00211002"
	      }
	  ]
	}

4.6 获取用户指定币账户地址
~~~~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 获取用户指定币账户地址。如果没有地址，则给用户分配一个地址，此时不应生成账户，账户还是按需生成。
:接口地址: /api/account/getDepositAddress
:请求方式: POST
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
uid	string	必填	用户ID
symbol	string	必填	币种
app_id	string	必填	商户的唯一标识
time	long	必填	时间戳
sign	string	必填	签名
======= ======= ======== =================================================

:响应参数:

======= ======= ======== =================================================
param	type	是否必须	说明
uid	Int	必填	用户ID
address	string	必填	币种账户地址
======= ======= ======== =================================================

:响应示例:

::

	{
	    "code": "0",
	    "msg": "suc",
	    "data": {
	        "uid":10000,
	        "address": "1PiX4n37tGSf1zXEPpByYZ8m9Z7Rs3GQXZ"
	    }
	}


4.7 内部用户转账
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 内部用户转账
:接口地址: /api/billing/userTransfer
:请求方式: POST
:请求参数:

============ ======= ======== =================================================
param        type    是否必须   说明
request_id   string  必填      请求唯一标识
from_uid     string  必填      转出用户ID
to_uid       string  必填      转入用户ID
amount       string  必填      转账金额
symbol       string  必填      转账币种
app_id       string  必填      商户的唯一标识
time         long    必填      时间戳
sign         string  必填      签名
============ ======= ======== =================================================

:响应参数:

======= ======= ======== =================================================
param	type	是否必须	说明
code	string	必填	0：成功,其他:失败
msg	string	必填	
data	string	必填	status=0转账成功，status=1表示失败
======= ======= ======== =================================================

:响应示例:

::

	{
	    "code": "0",
	    "msg": "suc",
	    "data": {
		    "statuts": 0
	    }
	}


4.8 系统账户转账
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 系统账户转账
:接口地址: /api/billing/systemTransfer
:请求方式: POST
:请求参数:

============ ======= ======== =================================================
request_id   string   必填    请求唯一标识
to_uid       string   必填    转入用户ID
amount       string   必填    转账金额
symbol       string   必填    转账币种
app_id       string   必填    商户的唯一标识
time         long     必填    时间戳
sign         string   必填    签名
============ ======= ======== =================================================

:响应参数:

======= ======= ======== =================================================
param	type	是否必须	说明
code	string	必填	0：成功,其他:失败
msg	string	必填	
data	string	必填	status=0转账成功，status=1表示失败
======= ======= ======== =================================================

:响应示例:

::

	{
	    "code": "0",
	    "msg": "suc",
	    "data": {
		    "statuts": 0
	    }
	}

4.9 提现操作
~~~~~~~~~~~~~~~~~~~~~~~~
:说明: 提现操作,如果转入地址是我们的地址，则直接使用内部转账；否则使用之前的提现逻辑，即需要上链，审核走原有逻辑。
:接口地址: /api/billing/withdraw
:请求方式: POST
:请求参数:

============ ======= ======== =================================================
param         type   是否必须   说明
request_id    string 必填      请求唯一标识
from_uid      string 必填      转出用户ID
to_address    string 必填      转入用户地址
amount        string 必填      提现金额,包含提现手续费；手续费需要在商户后台配置；内部转账不收取手续费
symbol        string 必填      提现币种
app_id        string 必填      商户的唯一标识
focus_online  string 可选      1表示强制走链，不走内部转账; 0或者该字段为空，是否走内部转账会依据to_address来判断
time          long   必填      时间戳
sign          string 必填      签名
============ ======= ======== =================================================

**重点字段说明：**

- amount: 手续费需要在商户后台配置；内部转账不收取手续费
- focus_online: 1表示强制走链，不走内部转账; 0或者该字段为空，是否走内部转账会依据to_address来判断

:响应参数:

============== ======= ======== =================================================
param          type    是否必须   说明
status         string  必填      提现: 0 - 6 ；内部转账: 0,1。详见下面字段说明
withdraw_type  int     是        1表示外部地址提现，2内部转账
============== ======= ======== =================================================

**重点字段说明：**

- status: 提现状态: 0 未审核，1 审核通过，2 审核拒绝，3 支付中已经打币，4 支付失败，5 已完成，6 已撤销 ；内部转账: 0成功，1失败

:响应示例:

::

	{
	    "code": "0",
	    "msg": "suc",
	    "data": {
		    "statuts": 0
	    }
	}

4.10 获取支持的币列表
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 获取商户的币种列表
:接口地址: /api/user/getCoinList
:请求方式: GET
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
app_id	string	必填	商户的唯一标识
time	long	必填	时间戳
sign	string	必填	签名
======= ======= ======== =================================================

:响应参数:

======= ======= ======== =================================================
param	type	是否必须	说明
code	string	必填	0：成功,其他:失败
msg	string	必填	
data	json	必填	symbol:币种名称;icon：币种icon
======= ======= ======== =================================================

:响应示例:

::

	{
	    "code": "0",
	    "msg": "suc",
	    "data": [
	        {
	            "symbol"："BTC"
	             "icon": "https://hicoinvip.oss-cn-beijing.aliyuncs.com/saas/1547519554925.png"
	       }
	    ]
	}


4.11 批量获取提现记录
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


4.12 同步充值记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 同步充值记录
:接口地址: /api/billing/syncDepositList
:请求方式: GET
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
app_id	string	必填	商户的唯一标识
time	long	必填	时间戳
sign	string	必填	签名
max_id	int	必填	返回大于id的100条充值记录数据
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


4.13 批量获取充值记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 批量获取充值记录
:接口地址: /api/billing/depositList
:请求方式: GET
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
app_id	string	必填	商户的唯一标识
time	long	必填	时间戳
sign	string	必填	签名
ids	string	必填	多个id使用逗号隔开，最多100个id
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

4.14 批量获取内部用户转账记录
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 批量获取内部用户转账记录
:接口地址: /api/billing/transferList
:请求方式: GET
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
app_id	string	必填	商户的唯一标识
time	long	必填	时间戳
sign	string	必填	签名
ids	string	必填	多个request_id使用逗号隔开，最多100个id
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
request_id            String  必填      请求id
uid                   int     必填      用户id
symbol                String  必填      币种
amount                String  必填      充值金额
created_at            String  必填      创建时间,
updated_at            String  必填      修改时间
from_uid              int.    必填      来源uid
to_uid                int     必填      转出uid
status                int     必填      0成功，1 失败
===================== ======= ======== =================================================


:响应示例:

::

	{
		"code": "0",
		"msg": "suc",
		"data":[
			{  
				"request_id":"11",
				  "id": 1,
				"symbol" ："ETH",
				"amount"："0.0002000000000000",
				"created_at": 1545273830000,
				"updated_at":1545273830000,
				"from_uid": 10001,
				"to_uid": 10000,
				"status": "1"
			}
		]
	}


4.15 批量获取系统转账记录
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 批量获取系统转账记录
:接口地址: /api/billing/systemTransferList
:请求方式: GET
:请求参数:

======= ======= ======== =================================================
param	type	是否必须	说明
app_id	string	必填	商户的唯一标识
time	long	必填	时间戳
sign	string	必填	签名
ids	string	必填	多个request_id使用逗号隔开，最多100个id
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
request_id            String  必填      请求id
uid                   int     必填      用户id
symbol                String  必填      币种
amount                String  必填      充值金额
created_at            String  必填      创建时间,
updated_at            String  必填      修改时间
from_uid              int.    必填      来源uid
to_uid                int     必填      转出uid
status                int     必填      0成功，1 失败
===================== ======= ======== =================================================


:响应示例:

::

	{
		"code": "0",
		"msg": "suc",
		"data":[
			{  
				"request_id":"11",
				"id": 1,
				"symbol" ："ETH",
				"amount"："0.0002000000000000",
				"created_at": 1545273830000,
				"updated_at":1545273830000,
				"from_uid": 10001,
				"to_uid": 10000,
				"status": "1"
			}
		]
	}


5 域名及API密钥
------------------------
5.1.生产环境
~~~~~~~~~~~~~~~~~~~~~~~~
:域名: https://openapi.hicoin.vip 
:app_id: 待分配 
:app_secret: 待分配

5.2.测试环境
~~~~~~~~~~~~~~~~~~~~~~~~
:域名: http://awstestopenapi.hicoin.one/ 
:app_id: 16a9f17fc2ad61ca4339fdd6a8a37f21 
:app_secret: 4dedb14fae76dae682de02e671eac408

6 附录
------------------------
附 1:签名算法
~~~~~~~~~~~~~~~~~~~~~~~~

签名生成的通用步骤如下:

:第一步: 设所有发送或者接收到的数据为集合 M，将集合 M 内非空参数值的参 数按照参数名 ASCII 码从小到大排序(字典序)，使用 URL 键值对的格式(即 key1=value1&key2=value2...)拼接成字符串 stringA。

**特别注意以下重要规则**:

- 参数名 ASCII 码从小到大排序(字典序);
- 如果参数的值为空不参与签名;
- 参数名区分大小写;
- 验证调用返回时，传送的 sign 参数不参与签名，将生成的签名与该 sign 值作校验。

:第二步: 对 stringA 进行 md5，得到 sign 值 signValue 

**注**: 参与签名参数为，公共参数 + 接口参数

附 2:接口错误码表
~~~~~~~~~~~~~~~~~~~~~~~~
======  ==================================================================
code	msg
0	    成功
100001	系统错误
100004	请求参数不合法
100005	签名校验失败
100007	非法IP
100015	商户ID无效
100016	商户信息过期
110004	用户被冻结不可提现
110023	手机号已注册
110055	提现地址错误
110065	请求用户用户不存在（获取用户余额、提现或转账时用到）
110078	提现或转账金额小于最小转出金额（后台配置最小金额，暂时不支持）
110087	提现或转账金额大于最大转出金额（后台配置最大金额，暂时不支持）
110088	请勿重复提交请求
110089	注册手机号不正确
110101	用户注册失败
120202	币种不支持
120402	提现或转账余额不足
120403	提现手续费余额不足
120404	提现或转账金额太小, 小于等于手续费
======  ==================================================================

附 3:接口测试
~~~~~~~~~~~~~~~~~~~~~~~~

6.3.1 测试参数
************************

:app_id: 16a9f17fc2ad61ca4339fdd6a8a37f21
:app_secret: 4dedb14fae76dae682de02e671eac408
:地址: http://awstestopenapi.hicoin.one/api/user/createUser

6.3.2 Java签名示例代码
************************

::

	package com.chainup.coinxman.test;

	import org.apache.commons.httpclient.HttpClient;
	import org.apache.commons.httpclient.methods.PostMethod;
	import org.apache.commons.io.IOUtils;

	import java.io.InputStream;
	import java.io.UnsupportedEncodingException;
	import java.security.MessageDigest;
	import java.security.NoSuchAlgorithmException;
	import java.util.Map;
	import java.util.Set;
	import java.util.TreeMap;

	public class SignTest {

	    /**
	     * 测试
	     */
	    public static void main(String[] args) {
	        /** 请求参数，其中api_key,secret_key需要分配*/
	        String appId = "16a9f17fc2ad61ca4339fdd6a8a37f21";
	        String appSecret = "4dedb14fae76dae682de02e671eac408";
	        String country = "+86";
	        String mobile= "15004648456";
	        String time = "1551325752";

	        /** 封装需要签名的参数 */
	        TreeMap<String, String> params = new TreeMap<>();
	        params.put("app_id", appId);
	        params.put("country", country);
	        params.put("mobile", mobile);
	        params.put("time", time);

	        String sign = openApiSign(params, appSecret);
	        params.put("sign", sign);

	        /** http请求 */
	        String resultJson = post("http://awstestopenapi.hicoin.one/api/user/createUser", params);
	        System.out.println(resultJson);
	    }

	    /**
	     * 获取参数签名
	     * @param params
	     * @param appSecret
	     * @return
	     */
	    public static String openApiSign(TreeMap<String, String> params, String appSecret){
	        /** 拼接签名字符串，md5签名 */
	        StringBuilder result = new StringBuilder();
	        Set<Map.Entry<String, String>> entrys = params.entrySet();
	        for (Map.Entry<String, String> param : entrys) {
	            /** 去掉签名字段 */
	            if(param.getKey().equals("sign")){
	                continue;
	            }

	            /** 空参数不参与签名 */
	            if(param.getValue()!=null) {
	                result.append("&").append(param.getKey()).append("=").append(param.getValue().toString());
	            }
	        }
	        result.append(appSecret);
	        String signTemp = result.toString().replaceFirst("&","");
	        return getMD5(signTemp);
	    }
	    /**
	     * 通过post来提交数据，带参数的方法
	     *
	     * @param url 请求地址
	     * @param params 参数
	     * @return
	     */
	    public static String post(String url, Map<String, String> params) {
	        System.out.println(params);
	        String str = null;
	        try {
	            HttpClient client = new HttpClient();
	            PostMethod method = new PostMethod(url);
	            //设定请求头的样式
	            method.setRequestHeader("Content-Type", "application/x-www-form-urlencoded;charset=utf-8");
	            if (params != null && params.size() > 0) {
	                for (Map.Entry<String, String> entry : params.entrySet()) {
	                    method.setParameter(entry.getKey(), entry.getValue());
	                }
	            }
	            int code = client.executeMethod(method);
	            if (code >= 200 && code < 300) {
	                InputStream in = method.getResponseBodyAsStream();
	                str = IOUtils.toString(in);
	            }
	        } catch (Exception e) {
	            // TODO Auto-generated catch block
	            e.printStackTrace();
	        }
	        return str;
	    }



	    /**
	     * 获取String的MD5值
	     *
	     * @param info 字符串
	     * @return 该字符串的MD5值
	     */
	    public static String getMD5(String info) {
	        try {
	            MessageDigest md5 = MessageDigest.getInstance("MD5");
	            md5.update(info.getBytes("UTF-8"));
	            byte[] md5Array = md5.digest();
	            return bytesToHex(md5Array);
	        } catch (NoSuchAlgorithmException e) {
	            return "";
	        } catch (UnsupportedEncodingException e) {
	            return "";
	        }
	    }

	    private static String bytesToHex(byte[] md5Array) {
	        StringBuilder strBuilder = new StringBuilder();
	        for (int i = 0; i < md5Array.length; i++) {
	            int temp = 0xff & md5Array[i];
	            String hexString = Integer.toHexString(temp);
	            if (hexString.length() == 1) {//如果是十六进制的0f，默认只显示f，此时要补上0
	                strBuilder.append("0").append(hexString);
	            } else {
	                strBuilder.append(hexString);
	            }
	        }
	        return strBuilder.toString();
	    }



6.3.2 PHP签名示例代码
************************

::

	/**
	 * openApi 签名
	 * @param array $params 请求参数
	 * @param $secretKey app_id对应的app_secret
	 * @return string
	 */
	function openApiSign(array $params, $secretKey){
	    $stringBuffer = array();
	    ksort($params);
	    foreach ($params as $key => $value){
	        $value = trim($value);
	        if($key == "sign"){
	            continue;
	        }
	        if(!empty($value)){
	            $stringBuffer[] = "{$key}={$value}";
	        }
	    }
	    $str = implode("&", $stringBuffer);
	    return md5($str.$secretKey);
	}


7 FQA
------------------------

