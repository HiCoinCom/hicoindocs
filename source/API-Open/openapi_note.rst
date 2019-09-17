6 附录
==========

附录1 网页授权
-------------------

如果用户在HiCoin客户端中访问第三方网页，第三方平台可以通过HiCoin网页授权机制，来获取用户基本信息，进而实现业务逻辑。

**关于网页授权回调域名的说明**

1、在HiCoin第三方平台请求用户网页授权之前，开发者需要先到HiCoin申请appid与appsecret，**申请前需要提前准备服务器IP白名单与授权域名**；

2、授权回调域名配置规范为全域名，比如需要网页授权的域名为：www.hicoin.com，配置以后此域名下面的页面http://www.hicoin.com/music.html 、 http://www.hicoin.com/login.html 都可以进行OAuth2.0鉴权。但http://pay.hicoin.com 、 http://music.hicoin.com 、 http://hicoin.com无法进行OAuth2.0鉴权
 
**关于网页授权的两种SCOPE的区别说明**

1、以snsapi_base为scope发起的网页授权，是用来获取进入页面的用户的openid的，并且是静默授权并自动跳转到回调页的。用户感知的就是直接进入了回调页（往往是业务页面）

2、以snsapi_userinfo为scope发起的网页授权，是用来获取用户的基本信息的。但这种授权需要用户手动同意，并且由于用户同意过，所以无须关注，就可在授权后获取该用户的基本信息(开发中)。
 
**关于网页授权ACCESS_TOKEN和普通ACCESS_TOKEN的区别**

1、HiCoin网页授权是通过OAuth2.0机制实现的，在用户授权给第三方平台后，第三方平台可以获取到一个网页授权特有的接口调用凭证（网页授权access_token），通过网页授权access_token可以进行授权后接口调用，如获取用户基本信息，用户发起支付等；

2、其他HiCoin接口，需要通过基础支持中的“获取access_token”接口来获取到的普通access_token调用。
 
**关于特殊场景下的静默授权**

1、上面已经提到，对于以snsapi_base为scope的网页授权，就静默授权的，用户无感知；
 
**具体而言，网页授权流程分为四步（具体接口参数，参考接口文档）**

1、引导用户进入授权页面同意授权或静默授权，获取code，通过接口： < `/connect/oauth/authorize <http://docs.hicoin.vip/zh/latest/API-Open/openapi_oauth.html#h5>`_>。

2、通过code换取网页授权access_token（与基础支持中的access_token不同，通过接口：< `/sns/oauth/access_token <http://docs.hicoin.vip/zh/latest/API-Open/openapi_oauth.html#codetokenopenid>`_>。

3、如果需要，开发者可以刷新网页授权access_token，避免过期，通过接口：< `/sns/oauth/refresh_token <http://docs.hicoin.vip/zh/latest/API-Open/openapi_oauth.html#access-token>`_>。

4、通过网页授权access_token和openid获取用户基本信息，通过接口：/sns/user/info。



附录2 签名管理
-------------------

1、签名算法
~~~~~~~~~~~~~~~

签名生成的通用步骤如下：

**第一步**，设所有发送或者接收到的数据为集合M，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串stringA。

**特别注意以下重要规则：**

1. 参数名ASCII码从小到大排序（字典序）；
2. 如果参数的值为空不参与签名；
3. 参数名区分大小写；
4. 验证调用返回或主动通知签名时，传送的sign参数不参与签名，将生成的签名与该sign值作校验。
5. 接口可能增加字段，验证签名时必须支持增加的扩展字段

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
	stringSignTemp=stringA+"&key=15133223342" //注：key为商户平台设置的密钥mchKey
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
 
2、生成随机数算法
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



附录3 名词
-------------------
:网页授权access_token: 通过用户同意授权或静默授权产生的access_token，用户获取用户信息与用户账户信息，只作用于授权用户

:授权域名: 用户同意授权或静默授权回跳地址的域名，第三方必填提前与平台约定好，如果回跳地址域名与约定域名不一致，则授权失败

:基础授权access_token: 相对于网页授权access_token，基础授权access_token作用于开发者，基础授权access_token可以开发者在平台的信息，比如开发者账户余额

:支付密钥: 用于验证与生成所有支付相关接口的sign

:接口ip白名单: 访问平台接口的来源ip，非白名单中ip将无权限访问相应接口




