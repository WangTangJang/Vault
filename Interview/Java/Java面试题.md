# 基础知识

[[基本数据类型有哪些？]]
byte short int long float double char boolean
[[自动装箱和自动拆箱是什么？]]
自动装箱是将基本数据类型转换成包装类，自动拆箱是将包装类转换成基本数据类型
[[基本数据类型和包装类之间转换的意义？]]

[[访问修饰符有哪些？]]

[[final关键字的作用是什么？]]

[[Java的编译模式是什么？]]
# 面向对象编程

[[什么是面向对象编程？]]
面向对象编程就是将程序的设计与实现由多个相互关联的对象组成，对象是程序的基本单元。
[[什么是封装？]]
封装是将一个对象的属性和方法捆绑在一起，对外部隐藏实现细节。
[[什么是继承？]]
继承指的是一个类可以使用其他类的属性和方法。
[[什么是多态？]]
同一类型的对象在不同的情况下表现出不同的行为。
[[重载和重写的区别是什么]]
重载发送在一个对象的内部，重写是一个对象的子类写了一个与父类相同的方法，但是传入的参数不同。重载发生在编译时，重写发生在运行时
[[什么是抽象类？]]
抽象类不能被实例化，只能被继承，可以包含普通方法，也可以包含抽象方法。
[[什么是接口？]]
接口提供了一组方法的签名但是不提供这些方法的实现。其他类可以使用implamets 来实现某个接口，实现了某个接口类，必须实现这个接口中的所有抽象方法。
[[抽象类和接口区别]]
一个类只能继承一个抽象类，但能实现多个接口。
[[Object类常用方法有那些？]]
hashcode()
equal()
toString()
getClass()
clone()
[[什么是对象引用？]]
对象引用是指向对象的指针，它存储了对象在内存中的地址。
[[类之间有哪些关系？]]
继承、实现、聚合、组合、依赖、关联。
# 集合框架

[[Java集合框架有哪些？]]

[[HashMap的实现原理]]

[[ArrayList的实现原理]]

[[ArrayList和普通数组的区别？]]

[[LinkedList的实现原理]]

[[HashSet的实现原理]]

[[TreeMap的实现原理]]

[[HashMap和TreeMap的区别是什么？]]
# 线程
[[什么是线程？如何创建线程？]]

[[线程和进程的区别是什么？]]

[[如何实现线程安全的代码？]]

[[synchronized关键字的作用是什么？]]
# IO流
[[什么是流？有哪两种流？]]

[[文件操作的常用类有哪些？]]

[[什么是序列化和反序列化？]]

[[什么是缓冲流？]]

[[FileInputStream和FileReader的区别]]
# 异常
[[Java中如何处理异常？]]

[[Error和Exception有什么区别？]]

[[异常的分类有哪些？]]
# 数据库
![[Database知识分类]]
# Spring框架
[[什么是Spring框架？]]

[[什么是依赖注入？]]

[[什么是控制反转？]]

[[什么是 Spring inner beans？]]

[[控制反转和依赖注入的区别和联系？]]

[[什么是面向切面编程？]]

[[请解释 Spring Bean 的生命周期？]]

[[请解释 Spring Bean 的自动装配？]]

[[Spring Bean 的作用域之间有什么区别？]]

