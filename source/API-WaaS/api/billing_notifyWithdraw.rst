
2.16 用户提现异步回调通知
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:说明: 此接口仅定义了接口规范，具体接口需要开发者实现
:接口地址: 接口地址由开发者提供，联系管理员在平台进行配置即可
:请求方式: POST
:请求参数:

====================== ======= ======== ====================================================================================
param                  type    是否必须   说明
app_id                 string  必填      商户的唯一标识
charset                string  必填      编码
version                string  必填      版本
notify_time            string  必填      通知时间
id                     string  必填      提现id
uid                    string  必填      提现用户id
symbol                 string  必填      币种
amount                 string  必填      提现金额
withdraw_fee_symbol    string  必填      提现手续费币种
withdraw_fee           string  必填      提现手续费
fee_symbol             string  必填      挖矿手续费币种
real_fee               string  必填      矿工费
address_to             string  必填      充值地址
created_at             string  必填      创建时间
updated_at             string  必填      修改时间
txid                   string  必填      区块链交易ID
confirmations          string  必填      区块链确认数
status                 string  必填      提现状态: 0 未审核，1 审核通过，2 审核拒绝，3 支付中已经打币，4 支付失败，5 已完成，6 已撤销
====================== ======= ======== ====================================================================================

:响应参数:

返回字符串：SUCCESS表示成功，FAILURE表示失败
