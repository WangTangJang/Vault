# equals 方法：
- `equals`方法是字符串类中的一个方法，用于比较两个字符串的内容是否相同。
- 它比较的是字符串的实际内容，而不是[[什么是对象引用？|对象的引用]]。
- 例子：
 ```java
 String str1 = "Hello";
 String str2 = new String("Hello");
 
 // 使用equals方法比较字符串内容
 boolean isEqual = str1.equals(str2); // 返回true
 ```
# \==运算符
- `==`运算符用于比较两个对象的引用是否相同，即它比较对象在内存中的地址。
- 对于字符串，`==`比较的是字符串对象的引用，而不是它们的内容。
- 例子：
 ```java
 String str1 = "Hello";
 String str2 = new String("Hello");
 
 // 使用==比较字符串对象的引用
 boolean isReferenceEqual = (str1 == str2); // 返回false
 ```