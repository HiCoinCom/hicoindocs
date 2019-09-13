
4 附录
==========
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



