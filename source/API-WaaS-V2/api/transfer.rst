商户转账
======================


WaaS商户转账
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: WaaS内部商户互相转账
:接口地址: /api/v2/account/transfer
:请求方式: POST
:请求参数:


========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

============ =========== ============= ===================================================
Param         类型        是否必须        说明
time          Long        必填           当前时间戳
charset       String      必填           编码格式，无特殊情况，传参数utf-8
version       String      必填           接口版本号，无特殊情况，传参数v2
request_id    String      必填           请求唯一标识，最多支持64位
symbol        String      必填           转账币种，WaaS获取币种名称
amount        String      必填           转账数量，包含转账手续费
to            String      必填           转入商户，目前填写商户APPID
remark        String      选填           备注字段
============ =========== ============= ===================================================


:请求参数示例:

::

	app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=pvcuCqVIu6aKQotQ1Z5WRzevdO3s81UReMZWvc_K7YGF1gCKkae0sPhlHogIU0slUWTME4bHzbZCl15Qg-RlnECqkTxiOazZTEmPi9vNJlO4V5awPYA9fbBM6pTvQxE-Qwsg9M6IyX6VcnRxiaqLJxRbZwoF0g4vBeRdcmGCqNOp3V6eY4s3-DTXmVDtF0eicPM0ROuWEjCThxNbPqy3CW2ldBtnigpxZ2A5ajlLLln8o9pb04kKrxdC4hVMJlrv0J5Bonn0gNP_355-ElB0L4ttyH-x8Uc3jfe2w6n46bODUaXUXsJoNmDZBC7bEJQj1axwrudFE7YasEfM9OCGdzvzOVgUFi-aHqLfA9aTwgK7vw3QOX4ypfK669qGiqiiJMBfGw6_209SquIn535eMZh8rrGZIb1I7xIifNWiYNtRkeHvIF16_jLNTCMZO0wVmMID3j4eEtxkO65RMYHMu0FUwehw1bQB7nVYafvcLa4tZqUDM_YcyK4BVqDgqcBSdVCCnppEMy-OHXMhebhuI6U81UG9YJ5E1eePg1kr_IPvMj-DFAaUXEde53k4AZsGR0vPP1N0k5lj0-GrmlsLtlt2GhubpgnGw0SyRExwu4zzpaBhU0Im1uwUvKxTOb1abD2ELB0mbMsucH47gKe-2-ta8opEpfDutsaf7B-6d8M

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
receipt               String      必填        转账唯一凭证
===================== ========== =========== =================================================



:响应示例:

::

	{"data":"k4w5AijeFWF3AtYbgP1RYfej7ifW4R663pOt5bhQp8RIxFUVb6zKOy4snKukA_5T9DVwhjdhsHjSRpmxD5LwL2OtplwSUACRPnW39ANypjO5YeMJTpiY9_7jofZWYzAMB4gdkrAI3DAbvkjCFUKQIXfAGMl25sp05mdBZgfY1oEtveSyislYOwaLM3SfN_2bFvrKy7E2V0AkZhrYImKiCzmDZvE-i93cePVQ4ODiuusHgk1vH5QgvPv62Sh-xxQPb4TsWj2G_RBoo9dFlg4zbWOdb9z6SVzR86ouxKOX_RhE4vWsReVD4ukdsW8eO7SVCI74qc61hIS12X6u-Hv40g"}

:响应数据解密后示例:


::

	{
	    "code":"0",
	    "data":[
	        {
	            "receipt":"abcdesd",
	        }
	    ],
	    "msg":"成功"
	}





转账信息异步确认
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 转账信息异步确认
:接口地址: /same-with-withdraw-check-sum
:请求方式: POST
:请求参数:


========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

============ =========== ============= ============================================
Param	         类型         是否必须        说明
time	         Long	        必填	         当前时间戳
charset        String       必填           编码格式，无特殊情况，传参数utf-8
version        String       必填           接口版本号，无特殊情况，传参数v2
request_id     String       必填           请求唯一标识，最多支持64位
symbol	       String       必填           币种
amount         String       必填           转账数量，包含转账手续费
to             String       必填           转入商户，目前填写商户APPID
check_sum      String       必填           随机校验码，第三方原样返回此字段平台认为成功
remark         String       选填           备注字段
============ =========== ============= ============================================


:请求参数示例:

::

   app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=pvcuCqVIu6aKQotQ1Z5WRzevdO3s81UReMZWvc_K7YGF1gCKkae0sPhlHogIU0slUWTME4bHzbZCl15Qg-RlnECqkTxiOazZTEmPi9vNJlO4V5awPYA9fbBM6pTvQxE-Qwsg9M6IyX6VcnRxiaqLJxRbZwoF0g4vBeRdcmGCqNOp3V6eY4s3-DTXmVDtF0eicPM0ROuWEjCThxNbPqy3CW2ldBtnigpxZ2A5ajlLLln8o9pb04kKrxdC4hVMJlrv0J5Bonn0gNP_355-ElB0L4ttyH-x8Uc3jfe2w6n46bODUaXUXsJoNmDZBC7bEJQj1axwrudFE7YasEfM9OCGdzvzOVgUFi-aHqLfA9aTwgK7vw3QOX4ypfK669qGiqiiJMBfGw6_209SquIn535eMZh8rrGZIb1I7xIifNWiYNtRkeHvIF16_jLNTCMZO0wVmMID3j4eEtxkO65RMYHMu0FUwehw1bQB7nVYafvcLa4tZqUDM_YcyK4BVqDgqcBSdVCCnppEMy-OHXMhebhuI6U81UG9YJ5E1eePg1kr_IPvMj-DFAaUXEde53k4AZsGR0vPP1N0k5lj0-GrmlsLtlt2GhubpgnGw0SyRExwu4zzpaBhU0Im1uwUvKxTOb1abD2ELB0mbMsucH47gKe-2-ta8opEpfDutsaf7B-6d8M

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

============ =========== ============= ===================================================
Param	       类型         是否必须       说明
time	       long	        必填	        当前时间戳
check_sum    String       必填          随机校验码，第三方原样返回此字段平台认为成功
============ =========== ============= ===================================================



:响应示例:

::

   {"data":"k4w5AijeFWF3AtYbgP1RYfej7ifW4R663pOt5bhQp8RIxFUVb6zKOy4snKukA_5T9DVwhjdhsHjSRpmxD5LwL2OtplwSUACRPnW39ANypjO5YeMJTpiY9_7jofZWYzAMB4gdkrAI3DAbvkjCFUKQIXfAGMl25sp05mdBZgfY1oEtveSyislYOwaLM3SfN_2bFvrKy7E2V0AkZhrYImKiCzmDZvE-i93cePVQ4ODiuusHgk1vH5QgvPv62Sh-xxQPb4TsWj2G_RBoo9dFlg4zbWOdb9z6SVzR86ouxKOX_RhE4vWsReVD4ukdsW8eO7SVCI74qc61hIS12X6u-Hv40g"}

:响应数据解密后示例:


::

	{
    "code":"0",
    "data":[
        {
            "time":1551429063111,
            "check_sum":"123124",
        }
    ],
    "msg":"成功"
	}




批量查询转账记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 批量查询转账记录
:接口地址: /api/v2/account/transferList
:请求方式: POST
:请求参数:


========= ========== ============= ===================================================
Param	    类型        是否必须       说明
app_id	  String	   可选	          商户唯一标识
data      String	   可选	          加密之后的字符串，解密之后的格式如下定义
========= ========== ============= ===================================================

:请求参数data解密之后数据结构:

========== =============== ================== ===================================================
Param	        类型           是否必须           说明
time	        long	         必填	             当前时间戳
charset       String         必填              编码格式，无特殊情况，传参数utf-8
version       String         必填              接口版本号，无特殊情况，传参数v2
ids           String         必填              请求唯一标识,多个之间用英文逗号分割，最多100个
ids_type      String         必填              request_id：请求ID（默认）；receipt：转账凭证
========== =============== ================== ===================================================


:请求参数示例:

::

   app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=pvcuCqVIu6aKQotQ1Z5WRzevdO3s81UReMZWvc_K7YGF1gCKkae0sPhlHogIU0slUWTME4bHzbZCl15Qg-RlnECqkTxiOazZTEmPi9vNJlO4V5awPYA9fbBM6pTvQxE-Qwsg9M6IyX6VcnRxiaqLJxRbZwoF0g4vBeRdcmGCqNOp3V6eY4s3-DTXmVDtF0eicPM0ROuWEjCThxNbPqy3CW2ldBtnigpxZ2A5ajlLLln8o9pb04kKrxdC4hVMJlrv0J5Bonn0gNP_355-ElB0L4ttyH-x8Uc3jfe2w6n46bODUaXUXsJoNmDZBC7bEJQj1axwrudFE7YasEfM9OCGdzvzOVgUFi-aHqLfA9aTwgK7vw3QOX4ypfK669qGiqiiJMBfGw6_209SquIn535eMZh8rrGZIb1I7xIifNWiYNtRkeHvIF16_jLNTCMZO0wVmMID3j4eEtxkO65RMYHMu0FUwehw1bQB7nVYafvcLa4tZqUDM_YcyK4BVqDgqcBSdVCCnppEMy-OHXMhebhuI6U81UG9YJ5E1eePg1kr_IPvMj-DFAaUXEde53k4AZsGR0vPP1N0k5lj0-GrmlsLtlt2GhubpgnGw0SyRExwu4zzpaBhU0Im1uwUvKxTOb1abD2ELB0mbMsucH47gKe-2-ta8opEpfDutsaf7B-6d8M

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


============ ========= =============== =========================================
Param	        类型      是否必须           说明
time	        long	    必填	            当前时间戳
charset       String    必填              编码格式，无特殊情况，传参数utf-8
version       String    必填              接口版本号，无特殊情况，传参数v2
id            String    必填              请求唯一标识，最多支持64位
symbol	      String    必填              币种
amount        String    必填              转账数量，包含转账手续费
from          String    必填              转出商户，转出商户APPID
to            String    必填              转入商户，转入商户APPID
created_at    Long      必填              创建时间
request_id    String    必填              三方ID
receipt       String    必填              转账凭证
remark        String    必填              最大支持32字符
============ ========= =============== =========================================



:响应示例:

::

   {"data":"k4w5AijeFWF3AtYbgP1RYfej7ifW4R663pOt5bhQp8RIxFUVb6zKOy4snKukA_5T9DVwhjdhsHjSRpmxD5LwL2OtplwSUACRPnW39ANypjO5YeMJTpiY9_7jofZWYzAMB4gdkrAI3DAbvkjCFUKQIXfAGMl25sp05mdBZgfY1oEtveSyislYOwaLM3SfN_2bFvrKy7E2V0AkZhrYImKiCzmDZvE-i93cePVQ4ODiuusHgk1vH5QgvPv62Sh-xxQPb4TsWj2G_RBoo9dFlg4zbWOdb9z6SVzR86ouxKOX_RhE4vWsReVD4ukdsW8eO7SVCI74qc61hIS12X6u-Hv40g"}

:响应数据解密后示例:


::

	{
    "code":"0",
    "data":[
        {
            "id":"123",
            "symbol":"ETH",
            "amount":"0.002",
            "from":"0xc0ff095a9f1608f6873e74b84671640364107dc4",
            "to":"0xc0ff095a9f1608f6873e74b84671640364107dc5",
            "created_at":1551429063000,
            "request_id":"123123",
            "receipt":"4444444",
            "remark":"备注信息"
        }
        {
            "id":"124",
            "symbol":"ETH",
            "amount":"0.002",
            "from":"0xc0ff095a9f1608f6873e74b84671640364107dc4",
            "to":"0xc0ff095a9f1608f6873e74b84671640364107dc5",
            "created_at":1551429063111,
            "request_id":"123124",
            "receipt":"4444445",
            "remark":"备注信息"
        }
    ],
    "msg":"成功"
	}





同步转账记录
~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 同步所有转账记录（分页）
:接口地址: /api/v2/account/syncTransferList
:请求方式: POST
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
max_id    String     必填           返回大于id的100条转账记录数据
========= ========== ============= ===================================================


:请求参数示例:

::

   app_id=baaceb1e506e1b5d7d1f0a3b1622583b&data=pvcuCqVIu6aKQotQ1Z5WRzevdO3s81UReMZWvc_K7YGF1gCKkae0sPhlHogIU0slUWTME4bHzbZCl15Qg-RlnECqkTxiOazZTEmPi9vNJlO4V5awPYA9fbBM6pTvQxE-Qwsg9M6IyX6VcnRxiaqLJxRbZwoF0g4vBeRdcmGCqNOp3V6eY4s3-DTXmVDtF0eicPM0ROuWEjCThxNbPqy3CW2ldBtnigpxZ2A5ajlLLln8o9pb04kKrxdC4hVMJlrv0J5Bonn0gNP_355-ElB0L4ttyH-x8Uc3jfe2w6n46bODUaXUXsJoNmDZBC7bEJQj1axwrudFE7YasEfM9OCGdzvzOVgUFi-aHqLfA9aTwgK7vw3QOX4ypfK669qGiqiiJMBfGw6_209SquIn535eMZh8rrGZIb1I7xIifNWiYNtRkeHvIF16_jLNTCMZO0wVmMID3j4eEtxkO65RMYHMu0FUwehw1bQB7nVYafvcLa4tZqUDM_YcyK4BVqDgqcBSdVCCnppEMy-OHXMhebhuI6U81UG9YJ5E1eePg1kr_IPvMj-DFAaUXEde53k4AZsGR0vPP1N0k5lj0-GrmlsLtlt2GhubpgnGw0SyRExwu4zzpaBhU0Im1uwUvKxTOb1abD2ELB0mbMsucH47gKe-2-ta8opEpfDutsaf7B-6d8M

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
============ =========== ============= =========================================
Param	         类型          是否必须       说明
time	         long	        必填	         当前时间戳
charset        String       必填           编码格式，无特殊情况，传参数utf-8
version        String       必填           接口版本号，无特殊情况，传参数v2
id             String       必填           请求唯一标识，最多支持64位
symbol	       String       必填           币种
amount         String       必填           转账数量，包含转账手续费
from           String       必填           转出商户，转出商户APPID
to             String       必填           转入商户，转入商户APPID
created_at     Long         必填           创建时间
request_id     String       必填           三方ID
receipt        String       必填           转账凭证
remark         String       必填           最大支持32字符
============ =========== ============= =========================================



:响应示例:

::

   {"data":"k4w5AijeFWF3AtYbgP1RYfej7ifW4R663pOt5bhQp8RIxFUVb6zKOy4snKukA_5T9DVwhjdhsHjSRpmxD5LwL2OtplwSUACRPnW39ANypjO5YeMJTpiY9_7jofZWYzAMB4gdkrAI3DAbvkjCFUKQIXfAGMl25sp05mdBZgfY1oEtveSyislYOwaLM3SfN_2bFvrKy7E2V0AkZhrYImKiCzmDZvE-i93cePVQ4ODiuusHgk1vH5QgvPv62Sh-xxQPb4TsWj2G_RBoo9dFlg4zbWOdb9z6SVzR86ouxKOX_RhE4vWsReVD4ukdsW8eO7SVCI74qc61hIS12X6u-Hv40g"}

:响应数据解密后示例:


::

	{
    "code":"0",
    "data":[
        {
            "id":"123",
            "symbol":"ETH",
            "amount":"0.002",
            "from":"0xc0ff095a9f1608f6873e74b84671640364107dc4",
            "to":"0xc0ff095a9f1608f6873e74b84671640364107dc5",
            "created_at":1551429063000,
            "request_id":"123123",
            "receipt":"4444444",
            "remark":"备注信息"
        }
        {
            "id":"124",
            "symbol":"ETH",
            "amount":"0.002",
            "from":"0xc0ff095a9f1608f6873e74b84671640364107dc4",
            "to":"0xc0ff095a9f1608f6873e74b84671640364107dc5",
            "created_at":1551429063111,
            "request_id":"123124",
            "receipt":"4444445",
            "remark":"备注信息"
        }
    ],
    "msg":"成功"
	}
