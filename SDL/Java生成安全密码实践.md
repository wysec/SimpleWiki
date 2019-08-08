# Java生成安全密码实践


依据[OWASP's Password Storage Cheat Sheet](https://www.owasp.org/index.php/Password_Storage_Cheat_Sheet)中的最佳实践。

## 1. PBKDF2

Password Based Key Derivation Function 2 (PBKDF2)


```java
public static byte[] hashPassword( final char[] password, final byte[] salt, final int iterations, final int keyLength ) {

	try {
		SecretKeyFactory skf = SecretKeyFactory.getInstance( "PBKDF2WithHmacSHA512" );
		PBEKeySpec spec = new PBEKeySpec( password, salt, iterations, keyLength );
		SecretKey key = skf.generateSecret( spec );
		byte[] res = key.getEncoded( );
		return res;

	} catch( NoSuchAlgorithmException | InvalidKeySpecException e ) {
		throw new RuntimeException( e );
	}
}
```
- 这个密码和盐值参数是数组，就像hashPassword函数的结果一样。敏感数据应该在使用后被清除（设置数据元素为0）。
- 盐值（salt）参数应该是随机数，并且对于每个用户都是变化的。它应该至少32 bytes长度。盐值与哈希密码保存一起。
- 迭代（iterations）参数指定PBKDF2执行其基础算法的次数。更高的次数是更安全的。需要在与生产系统等效的硬件上进行实验。作为一个起点，找到一个需要半秒钟执行的值。扩展到大量的用户超出了本文档的范围。与哈希密码一起保存此迭代值。
- 密钥长度（keyLength）256位是安全的。
- 如果示例代码生成NoSuchAlgorithmException，则用PBKDF2WithHmacSHA1替换PBKDF2WithHmacSHA512。两者都足以完成任务（SHA1在PBKDF2的上下文之外是不安全的）。
- SecretKeyFactory和PBEKeySpec类从1.4版本开始已经是Java SE的一部分了。

