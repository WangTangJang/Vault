在Java中，`final` 关键字可以用来修饰类、方法和变量，其作用分别如下：
## final修饰类：
- 当类被声明为 `final` 时，该类不能被继承
- 这通常用于防止类的进一步修改和派生，以确保类的稳定性和安全性。
```java
final class FinalClass {
    // 类的内容
}
```
## final修饰方法：
- 当方法被声明为 `final` 时，该方法不能被子类重写，即子类不能对该方法进行修改。
- 这通常用于确保某个方法在继承体系中保持一致性，避免子类意外改变其行为。
```java
class BaseClass {
    final void finalMethod() {
        // 方法的内容
    }
}
```
## final修饰变量：
- 当变量被声明为 `final` 时，该变量成为常量，其值不能被修改。
- 这通常用于定义常量，使得程序中的某些数值保持固定不变，提高代码的可读性和可维护性。
```java
class MyClass {
    final int constantValue = 10;
}
```
### 注意
`final` 修饰的引用不能指向其他对象，但是这个引用所指向的对象的内部状态，即其[字段](字段.md##Summary)值，仍然可以被[修改](字段.md###字段值改变)。
```java
class MyClass {
    int field;

    MyClass(int value) {
        this.field = value;
    }

    void modifyField() {
        this.field = 42;
    }
}

class Example {
    final MyClass myObject = new MyClass(10);
	final int constantValue = 10;
	
    void modifyValues() {
        // 编译错误，final修饰的引用不能被重新指向其他对象
        // myObject = new MyClass(20);

		// 编译错误，常量值不能被修改
        // constantValue = 20;

        // 合法，虽然引用不能改变，但对象的状态（字段值）可以被修改
        myObject.modifyField();
        System.out.println(myObject.field); // 输出 42
    }
}
```
