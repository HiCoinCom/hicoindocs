附录二
==============

1. 签名算法
~~~~~~~~~~~~~~~

签名生成的通用步骤如下：

**第一步**，设所有发送或者接收到的数据为集合M，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串stringA。

**特别注意以下重要规则：**

1) 参数名ASCII码从小到大排序（字典序）；
#) 如果参数的值为空不参与签名；
#) 参数名区分大小写；
#) 验证调用返回或主动通知签名时，传送的sign参数不参与签名，将生成的签名与该sign值作校验。
#) 接口可能增加字段，验证签名时必须支持增加的扩展字段

**第二步**，在stringA最后拼接上key得到stringSignTemp字符串，并对stringSignTemp进行sha256运算，再将得到的字符串所有字符转换为大写，得到sign值signValue。

举例：

::

	假设传送的参数如下：
	appid： 123456789
	mch_id： 10000100
	device_info： 1000
	body： test
	nonce_str： ibuaiVcKdpRxkhJA

	第一步：对参数按照key=value的格式，并按照参数名ASCII字典序排序如下：
	stringA="appid=wxd930ea5d5a258f4f&body=test&device_info=1000&mch_id=10000100&nonce_str=ibuaiVcKdpRxkhJA"; 所有值需要url_encode处理

	第二步：拼接API 支付密钥mchKey：
	stringSignTemp=stringA+"&key=15133223342" //注：key为商户平台设置的密钥mchKey或者secretKey
	sign=hash_hmac("sha256",stringSignTemp,key).toUpperCase()="6A9AE1657590FD6257D693A078E1C3E4BB6BA4DC30B23E0EE2496E54170DACD6" //注：HMAC-SHA256签名方式

示例：

::

	public function getSignature($arrdata,$method="sha256",$extend='') {
	    if (!function_exists($method)) return false;
	    ksort($arrdata);
	    $paramstring = "";
	    foreach($arrdata as $key => $value)
	    {
	        if(strlen($paramstring) == 0)
	            $paramstring .= $key . "=" . $value;
	        else
	            $paramstring .= "&" . $key . "=" . $value;
	    }
	    $Sign = $method($paramstring.$extend);
	    return $Sign;
	}

2. 生成随机数算法
~~~~~~~~~~~~~~~~~~~~~~~~
支付API接口协议中包含字段nonce_str，主要保证签名不可预测
示例：

::

	public function generateNonceStr($length=16){
	    // 密码字符集，可任意添加你需要的字符
	    $chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
	    $str = "";
	    for($i = 0; $i < $length; $i++)
	    {
	        $str .= $chars[mt_rand(0, strlen($chars) - 1)];
	    }
	    return $str;
	}
