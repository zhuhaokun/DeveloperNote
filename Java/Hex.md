byte[]类型以十六进制打印
```java
// byte[]类型以十六进制
String s = "Hello";  
byte[] b = s.getBytes();  
for (byte b1 : b) {  
    System.out.printf("0x%02X ", b1);  
}
```