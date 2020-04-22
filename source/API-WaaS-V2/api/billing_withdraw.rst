
2.8 提现操作
~~~~~~~~~~~~~~~~~~~~~~~~
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

============ ======= ============= =================================================
Param        类型     是否必须        说明
time         long    必填	          当前时间戳
charset      String  必填           编码格式，无特殊情况，传参数utf-8
version      String  必填           接口版本号，无特殊情况，传参数v2
request_id   String  必填           请求唯一标识
from_uid     String  必填           转出用户ID
to_address   String  必填           转入用户地址
amount       String  必填           提现金额，包含提现手续费；手续费需要在商户后台配置
symbol       String  必填           提现币种
============ ======= ============= =================================================


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
