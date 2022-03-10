用户提现
======================


发起提现
------------

:说明: 如果提现地址为联盟内部地址，则不会上链；否则需要上链。另外，为了避免非法的提现请求，钱包服务在接收到第三方应用的提现请求时，会调用第三方提供的[提现二次确认接口]。
:接口地址: /api/v2/billing/withdraw
:请求方式: POST
:请求参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一表示
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

============ ======= ============= ===========================================================
Param        类型     是否必须        说明
time         long    必填	          当前时间戳
charset      String  必填           编码格式，无特殊情况，传参数utf-8
version      String  必填           接口版本号，无特殊情况，传参数v2
request_id   String  必填           请求唯一标识，最多支持64位
from_uid     String  必填           转出用户ID
to_address   String  必填           转入用户地址，memo类型，使用"_"进行拼接，如: eos_24545
amount       String  必填           提现金额，包含提现手续费；手续费需要在商户后台配置
symbol       String  必填           提现币种
============ ======= ============= ===========================================================


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



:响应参数data解密之后:

============== ======= ======== ===========================================================================
param          type    是否必须   说明
status         string  必填      0 未审核，1 审核通过，2 审核拒绝，3 支付中已经打币，4 支付失败，5 已完成，6 已撤销
============== ======= ======== ===========================================================================


:响应示例:

::

	{"data":"k4w5AijeFWF3AtYbgP1RYfej7ifW4R663pOt5bhQp8RIxFUVb6zKOy4snKukA_5T9DVwhjdhsHjSRpmxD5LwL2OtplwSUACRPnW39ANypjO5YeMJTpiY9_7jofZWYzAMB4gdkrAI3DAbvkjCFUKQIXfAGMl25sp05mdBZgfY1oEtveSyislYOwaLM3SfN_2bFvrKy7E2V0AkZhrYImKiCzmDZvE-i93cePVQ4ODiuusHgk1vH5QgvPv62Sh-xxQPb4TsWj2G_RBoo9dFlg4zbWOdb9z6SVzR86ouxKOX_RhE4vWsReVD4ukdsW8eO7SVCI74qc61hIS12X6u-Hv40g"}

:响应数据解密后示例:


::

	{"code":"0","data":{"id":48680,"status":0},"msg":"成功"}





提现信息二次确认
------------------------

:说明:  平台在接收到提现请求之后，会调用第三方提供的二次确认接口，来确认该请求为商户正常发起的提现请求。此接口仅定义了接口规范，具体接口需要开发者实现。
:接口地址: 接口地址由开发者提供，联系管理员在平台进行配置即可
:请求方式: POST
:请求参数:


========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

============== ========== ============= ===================================================
Param          类型        是否必须        说明
time	         long	       是            当前时间戳
charset        String      是            编码格式，无特殊情况，传参数utf-8
version        String      是            接口版本号，无特殊情况，传参数v2
request_id     String      是            请求唯一标识
from_uid       String      是            转出用户ID
to_address     String      是            转入用户地址
amount         String      是            提现金额，包含提现手续费；手续费需要在商户后台配置
symbol         String      是            提现币种
check_sum      String      是            随机校验码，第三方原样返回此字段平台认为成功
============== ========== ============= ===================================================


:请求参数示例:

::

  app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=UoJC0VeVSvdOCYbkUIQxnJ2k-MINFmdfhHo1bpgK1kqcCKEZ1MtBFmvMnrZsmpQKVyNbFyBmLHzOk_T5FTxKA0VROneKR4wyK0G6HPQM6pDeSz2BPwwaw-2uiBSiPeQEwOabWl0MLyoJyj1g4VLcBgazCYeD5YPJXFOzjAEgkhfbMEcoS1to_ooISnIMeQvhj8g3I3m5k519eJ9KWOv5R3_EGMaI-yLlCB5CIVd4byjnBxDJxsRMR7yuEhIjfvsy49MgglSTrddCFu3ZHNwGlv_DzTJIMhJHRV7z4x8YQV2atP-BBgY9eozPa0JIkjBctdqigvzJs5nsbl76wL5Gv5-icGv4qtOF0w11t0oPi051Y7fiuPJ20BK6GAPEu_HroTvcWh-3vh2_U03Donv306HMvC-vXrQH18TGVqjtOlVhQW_wg4PF9fjMgNCsk3k57vzVfuRruurLv6-FD6HRvoUe4WfgSAi-jMRpuwXC8mL44r-dLDfo4wUdrjEk8tkjSZea8O066bJeVVUU3rD7qqL32Uf-3Bkcy26jsHLf-QK8oYi2xjddd2PSoHnpSIbRdDYrYLdO_zUFZudg4FBHFzQ6sSLesS_jA63xJZS1xk6EjejaSpID3r-7YXDQtM3y5O1TG3URmF5sVbWL5iekubN2jEjkQ2QdV4hz0sBdmlx8GrPUWSnbtLMV7zcxAhyodzIeWeeZCKeu1AF903YJvKZls8eKMEvd__PYSnnRtXVxNUvFFo-GL3sOtDAAhjKdLLSWCVGqDQsKSrORffejbDeHVGsmtFxPC5kvKHLbJvAW6QDzpG8hqmZLrtjxvTmcVMt1_hn9-VSi-qFW8xPorYmF5Hw1G5nZca7NK5k2Qs6xieNgw34Sps-tj38WxhXacRwlEp1Yt3Jj3BlMlxCD9VWxWO17Yvj3MmJTNgf-d22PvPV_mZrJaqjm6BSfuz9DVYVjsIuZF_eOgMaVTm31FFuFZvPF9G_lhC4CQ0Zb5KfpYx0NMJjGfBPtxZ3MsF8H


:响应参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
data      String     可选           加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:data数据结构:

=============== ========= ========== ====================================================
Param            类型       是否必须   说明
check_sum        String    必填       请求参数中的check_sum
time             String    必须       时间戳
=============== ========= ========== ====================================================

:响应示例:


::

  {"data":"LK4D5mrtvTubDxCQM4lqyN2h8TTIkEBL_06FrrrzLrImyMO4Yuac-wdbk5VnGVfCKB5EFaUb162xXUJdTHhpA5CGBCAQKl64h_Dt10C-H8KIoap9dZI90qE4f-mAMAyjF1QzKXJ-f-R_3J3bRGqfHFBRXebh08R8MdRDssniopVOhsFUs4gBxUensKas3_ta15eFIqXPjIgJWfYQCD2DUi1gaKgmN-5Q_tgt-qXp5Y2uh3yfM4g4k71Ahyel3G8S_AktbWl2G9wU3cri3ZVQEo0faIpkX_CKsk9V1YoY5yRopvJbxNtkG9lBFxKnureAQo0KP3f1tsIMOzgcyEXPnA"}

:响应数据解密后示例:

::

  {"check_sum":"1234","time":"12345678"}




用户提现异步回调通知
------------------------

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

提现通知：

===================== ========== ============= ==========================================================================================
Param	                 类型        是否必须       说明
charset                String      是           编码格式，无特殊情况，传参数utf-8
version                String      是           接口版本号，无特殊情况，传参数v2
side                   String      是           通知类型， 充值通知：deposit， 提现通知： withdraw
notify_time            String      是           通知时间
request_id             String      是           提现请求ID，对应提现接口中的request_id
id                     String      是           提现id
uid                    String      是           提现用户id
symbol                 String      是           币种
amount                 String      是           提现金额
withdraw_fee_symbol    String      是           提现手续费币种
withdraw_fee           String      是           提现手续费
fee_symbol             String      是           挖矿手续费币种
real_fee               String      是           矿工费
address_to             String      是           充值地址
created_at             String      是           创建时间
updated_at             String      是           修改时间
txid                   String      是           区块链交易ID
confirmations          String      是           区块链确认数
status                 String      是           提现状态: 0 未审核，1 审核通过，2 审核拒绝，3 支付中已经打币，4 支付失败，5 已完成
===================== ========== ============= ==========================================================================================


:请求参数示例:

::

  app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=UoJC0VeVSvdOCYbkUIQxnJ2k-MINFmdfhHo1bpgK1kqcCKEZ1MtBFmvMnrZsmpQKVyNbFyBmLHzOk_T5FTxKA0VROneKR4wyK0G6HPQM6pDeSz2BPwwaw-2uiBSiPeQEwOabWl0MLyoJyj1g4VLcBgazCYeD5YPJXFOzjAEgkhfbMEcoS1to_ooISnIMeQvhj8g3I3m5k519eJ9KWOv5R3_EGMaI-yLlCB5CIVd4byjnBxDJxsRMR7yuEhIjfvsy49MgglSTrddCFu3ZHNwGlv_DzTJIMhJHRV7z4x8YQV2atP-BBgY9eozPa0JIkjBctdqigvzJs5nsbl76wL5Gv5-icGv4qtOF0w11t0oPi051Y7fiuPJ20BK6GAPEu_HroTvcWh-3vh2_U03Donv306HMvC-vXrQH18TGVqjtOlVhQW_wg4PF9fjMgNCsk3k57vzVfuRruurLv6-FD6HRvoUe4WfgSAi-jMRpuwXC8mL44r-dLDfo4wUdrjEk8tkjSZea8O066bJeVVUU3rD7qqL32Uf-3Bkcy26jsHLf-QK8oYi2xjddd2PSoHnpSIbRdDYrYLdO_zUFZudg4FBHFzQ6sSLesS_jA63xJZS1xk6EjejaSpID3r-7YXDQtM3y5O1TG3URmF5sVbWL5iekubN2jEjkQ2QdV4hz0sBdmlx8GrPUWSnbtLMV7zcxAhyodzIeWeeZCKeu1AF903YJvKZls8eKMEvd__PYSnnRtXVxNUvFFo-GL3sOtDAAhjKdLLSWCVGqDQsKSrORffejbDeHVGsmtFxPC5kvKHLbJvAW6QDzpG8hqmZLrtjxvTmcVMt1_hn9-VSi-qFW8xPorYmF5Hw1G5nZca7NK5k2Qs6xieNgw34Sps-tj38WxhXacRwlEp1Yt3Jj3BlMlxCD9VWxWO17Yvj3MmJTNgf-d22PvPV_mZrJaqjm6BSfuz9DVYVjsIuZF_eOgMaVTm31FFuFZvPF9G_lhC4CQ0Zb5KfpYx0NMJjGfBPtxZ3MsF8H


:响应参数:

返回字符串：SUCCESS表示成功，FAILURE表示失败 （注意此处返回参数无需进行加密）





同步提现记录
------------------------

:说明: 批量获取提现记录
:接口地址: /api/v2/billing/syncWithdrawList
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
max_id    String   必填	      返回大于id的100条充值记录数据
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

===================== ========= ========== =============================================================================================================
Param                 类型        是否必须   说明
request_id            String     必填       请求id,
id                    int        必填       提现id
uid                   int        必填       提现用户id
symbol                String     必填       币种
amount                String     必填       提现金额
withdraw_fee_symbol   String     必填       提现手续费币种
withdraw_fee          String     必填       提现手续费
fee_symbol            String     必填       挖矿手续费币种
real_fee              String     必填       矿工费
created_at            Long       必填       创建时间
updated_at            Long       必填       修改时间
address_from          String     必填       来源地址
address_to            String     必填       到账地址
txid                  String     必填       区块链交易ID
confirmations         int        必填       区块链确认数
saas_status           int        必填       平台审核状态:0 未审核，1 已审核，2 审核拒绝
company_status        int        必填       商户审核状态:0 未审核，1 已审核，2 审核拒绝
status                int        必填       提现状态: 0 未审核，1 审核通过，2 审核拒绝，3 支付中已经打币，4 支付失败，5 已完成，6 已撤销
===================== ========= ========== =============================================================================================================


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





批量获取提现记录
------------------------

:说明: 批量获取提现记录
:接口地址: /api/v2/billing/withdrawList
:请求方式: GET
:请求参数:

========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
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
real_fee              String     必填        矿工费
created_at            Long       必填        创建时间,
updated_at            Long       必填        修改时间
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
