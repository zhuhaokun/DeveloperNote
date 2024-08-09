使用cipher，BouncyCastle对数据进行加解密
1. 使用KeyPairGenerator生成密钥对。
2. 使用KeyFactory对已有密钥字符串进行处理，用处理后的密钥对数据加解密。
```java
// 1. 使用KeyPairGenerator生成密钥对

// Add BouncyCastleProvider  
Security.addProvider(new BouncyCastleProvider());  
  
// Generate SM2 key pair  
KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("EC", "BC");  // "EC"表示椭圆曲线加密算法，"BC"表使BouncyCastle。
keyPairGenerator.initialize(new ECNamedCurveGenParameterSpec("sm2p256v1")); 
// 用于生成特定命名曲线的参数规格
KeyPair keyPair = keyPairGenerator.generateKeyPair();  
BCECPublicKey publicKey = (BCECPublicKey) keyPair.getPublic();  
BCECPrivateKey privateKey = (BCECPrivateKey) keyPair.getPrivate();  
  
System.out.println("Public Key: " + Hex.toHexString(publicKey.getEncoded()));  
System.out.println("Private Key: " + Hex.toHexString(privateKey.getEncoded()));  
  
// Encrypt using SM2  
Cipher cipher = Cipher.getInstance("SM2", "BC");  
cipher.init(Cipher.ENCRYPT_MODE, publicKey);  
byte[] plaintext = "Hello, SM2!".getBytes();  
byte[] ciphertext = cipher.doFinal(plaintext);  
System.out.println("Ciphertext: " + Hex.toHexString(ciphertext));  
  
// Decrypt using SM2  
cipher.init(Cipher.DECRYPT_MODE, privateKey);  
byte[] decryptedText = cipher.doFinal(ciphertext);  
System.out.println("Decrypted Text: " + new String(decryptedText));


```

```java
// 2. 使用KeyFactory对已有密钥字符串进行处理，用处理后的密钥对数据加解密。
// 假设我们有一个Base64编码的公钥字符串  
String base64PublicKey = "MIIBIjANBgkqhkiG9w0BACAQEArf...";  
  
// 解码Base64编码的公钥  
byte[] publicKeyBytes = Base64.getDecoder().decode(base64PublicKey);  
  
// 使用X509EncodedKeySpec创建密钥规范  
// 密钥规范有`X509EncodedKeySpec`或`PKCS8EncodedKeySpec`等
X509EncodedKeySpec keySpec = new X509EncodedKeySpec(publicKeyBytes);  
  
// 获取KeyFactory实例，并指定算法  
KeyFactory keyFactory = KeyFactory.getInstance("EC","BC");  
  
// 生成公钥对象  
PublicKey publicKey = keyFactory.generatePublic(keySpec);
```




