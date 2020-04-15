
4 附录
==========

附 1:加解密方式
~~~~~~~~~~~~~~~~~~~~~~~~

请求参数data与响应字段data的值都是经过rsa加密后再通过base64urlsafe加密的结果

*注意事项*

1）base64urlsafe将普通base64的 +/ 替换成了 _-

2）rsa加密与解密使用分段加密

:请求参数加密示例:

::

	 // 原始请求参数
	 String originReqData = '{"charset":"utf-8","symbol":"eth","sign":"","time":"1586420916306","app_id":"baaceb1e506e1b5d7d1f0a3b1622583b","version":"2.0"}'

	 // encryptByPrivate方法封装在下列公共类RSAHelper.java中
	 String encryptReqData = base64urlsafe.encode( RSAHelper.encryptByPrivate(originReqData, "第三方自己的私钥")

	 //http post
	 String httpBuildParams = "appid=baaceb1e506e1b5d7d1f0a3b1622583b&data=" + encryptReqData



:响应数据解密示例:

::

	// 响应的原始数据
  String originResp= '{"data":"jwtkGrhh2EVJS8xe93MpUYd-SQ-TyK0Bx5sXjE4hygFNg4wmctiahtIYXRpR2j8yDaEF5YzVstnUKbOH2p44FSMjXMQU4qFrhD00WOfW7v4LNALyiQXRb_5sakR0Zf573lGfLRTPlzLtTho3gqu3hMwuAv5e3r2dpb6_jxh1Z9BjkzSsNRX_bjLcHLUOPhMvo6rTUKSa9LQ6QnT8RX0eqzOZPlnCw3TeX_zcWWjxp6fcpKcdODxoI86gHwWRpSd-2qbEbFcaT12CJd9nPXA0KnLPNNHWz8sxQGiAg7Jg_-cN_yBHL9cS15zecTemYGqpOXRkojM1JwLsjM-7txf_dw"}'

	// 解密响应数据
	String encryptRespData = JSON.parse(originResp)['data']
	// decryptByPublic 方法封装在下列公共类 RSAHelper.java中
  String decryptRespData = RSAHelper.decryptByPublic( base64urlsafe.decode(encryptRespData), "托管平台提供的公钥" )


:公共类RSAHelper.java:

::

	import org.apache.commons.codec.binary.Base64;
	import org.apache.commons.lang3.StringUtils;

	import sun.misc.BASE64Decoder;
	import sun.misc.BASE64Encoder;
	import sun.security.rsa.RSAPrivateCrtKeyImpl;

	import javax.crypto.Cipher;
	import java.io.ByteArrayOutputStream;
	import java.security.*;
	import java.security.interfaces.RSAPrivateKey;
	import java.security.interfaces.RSAPublicKey;
	import java.security.spec.PKCS8EncodedKeySpec;
	import java.security.spec.RSAPublicKeySpec;
	import java.security.spec.X509EncodedKeySpec;
	import java.util.*;

	@SuppressWarnings("restriction")
	public class RSAHelper {
		/**
		 * 加密算法RSA
		 */
		public static final String KEY_ALGORITHM = "RSA";

		/** *//**
		 * RSA最大加密明文大小
		 */
		private static final int MAX_ENCRYPT_BLOCK = 234;

		/** *//**
		 * RSA最大解密密文大小
		 */
		private static final int MAX_DECRYPT_BLOCK = 256;


		private static final String CHARSET ="UTF-8";



		/**
		 * 公钥解密
		 *
		 * @param encryptedData 已加密数据
		 * @param publicKey 公钥(BASE64编码)
		 * @return
		 * @throws Exception
		 */
		public static byte[] decryptByPublicKey(byte[] encryptedData, String publicKey)
				throws Exception {
			byte[] keyBytes =  (new BASE64Decoder()).decodeBuffer(publicKey);
			X509EncodedKeySpec x509KeySpec = new X509EncodedKeySpec(keyBytes);
			KeyFactory keyFactory = KeyFactory.getInstance(KEY_ALGORITHM);
			Key publicK = keyFactory.generatePublic(x509KeySpec);
			Cipher cipher = Cipher.getInstance(keyFactory.getAlgorithm());
			cipher.init(Cipher.DECRYPT_MODE, publicK);
			int inputLen = encryptedData.length;
			ByteArrayOutputStream out = new ByteArrayOutputStream();
			int offSet = 0;
			byte[] cache;
			int i = 0;
			// 对数据分段解密
			while (inputLen - offSet > 0) {
				if (inputLen - offSet > MAX_DECRYPT_BLOCK) {
					cache = cipher.doFinal(encryptedData, offSet, MAX_DECRYPT_BLOCK);
				} else {
					cache = cipher.doFinal(encryptedData, offSet, inputLen - offSet);
				}
				out.write(cache, 0, cache.length);
				i++;
				offSet = i * MAX_DECRYPT_BLOCK;
			}
			byte[] decryptedData = out.toByteArray();
			out.close();
			return decryptedData;
		}

		/**
		 *  公钥分段解密
		 * @param encryptedData 加密的base64数据
		 * @param publicKey rsa 公钥
		 * @return
		 */
		public static String decryptByPublicKey(String encryptedData, String publicKey){
			if(StringUtils.isBlank(encryptedData) || StringUtils.isBlank(publicKey)){
				return "";
			}

			try {
			    encryptedData = encryptedData.replace("\r", "").replace("\n", "");
	            Base64 decoder = new Base64(true);
				byte[] data = decryptByPublicKey(decoder.decode(encryptedData), publicKey);
				if(data == null || data.length < 1){
					return  "";
				}
				return new String(data);
			}catch (Exception ex){
				ex.printStackTrace();
			}
			return "";
		}

		/**
		 * 私钥加密
		 *
		 * @param data 源数据
		 * @param privateKey 私钥(BASE64编码)
		 * @return
		 * @throws Exception
		 */
		public static byte[] encryptByPrivateKey(byte[] data, String privateKey)
				throws Exception {
			byte[] keyBytes =  (new BASE64Decoder()).decodeBuffer(privateKey);
			PKCS8EncodedKeySpec pkcs8KeySpec = new PKCS8EncodedKeySpec(keyBytes);
			KeyFactory keyFactory = KeyFactory.getInstance(KEY_ALGORITHM);
			Key privateK = keyFactory.generatePrivate(pkcs8KeySpec);
			Cipher cipher = Cipher.getInstance(keyFactory.getAlgorithm());
			cipher.init(Cipher.ENCRYPT_MODE, privateK);
			int inputLen = data.length;
			ByteArrayOutputStream out = new ByteArrayOutputStream();
			int offSet = 0;
			byte[] cache;
			int i = 0;
			// 对数据分段加密
			while (inputLen - offSet > 0) {
				if (inputLen - offSet > MAX_ENCRYPT_BLOCK) {
					cache = cipher.doFinal(data, offSet, MAX_ENCRYPT_BLOCK);
				} else {
					cache = cipher.doFinal(data, offSet, inputLen - offSet);
				}
				out.write(cache, 0, cache.length);
				i++;
				offSet = i * MAX_ENCRYPT_BLOCK;
			}
			byte[] encryptedData = out.toByteArray();
			out.close();
			return encryptedData;
		}

		/**
		 *  私钥分段加密数据
		 * @param data 待加密数据
		 * @param privateKey  私钥
		 * @return
		 */
		public static String encryptByPrivateKey(String data, String privateKey){
			if(StringUtils.isBlank(data) || StringUtils.isBlank(privateKey)){
				return "";
			}

			try {
				byte[] encryptedData = encryptByPrivateKey(data.getBytes("UTF-8"), privateKey);
				if(encryptedData == null || encryptedData.length < 1){
					return  "";
				}

	            Base64 encoder = new Base64(true);
	            byte[] dataBytes = encoder.encode(encryptedData);
	            return new String(dataBytes).replace("\r", "").replace("\n", "");
			}catch (Exception ex){
				ex.printStackTrace();
			}
			return "";
		}

  }


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
