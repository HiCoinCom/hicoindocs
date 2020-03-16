
2.17 用户充值异步回调通知
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 此接口仅定义了接口规范，具体接口需要开发者实现
:接口地址: 接口地址由开发者提供，联系管理员在平台进行配置即可
:请求方式: POST
:请求参数:

====================== ======= ======== ====================================================================================
Param                  Type    是否必须   说明
app_id                 string  必填      商户的唯一标识
charset                string  必填      编码
version                string  必填      版本
notify_time            string  必填      通知时间
id                     string  必填      充值id
uid                    string  必填      用户id
symbol                 string  必填      币种
amount                 string  必填      充值金额
address_to             string  必填      充值地址
created_at             string  必填      创建时间
updated_at             string  必填      修改时间
txid                   string  必填      区块链交易ID
confirmations          string  必填      区块链确认数
status                 string  必填      充值状态     0待确认，1 已完成，2 异常
====================== ======= ======== ====================================================================================

:响应参数:

返回字符串：SUCCESS表示成功，FAILURE表示失败
