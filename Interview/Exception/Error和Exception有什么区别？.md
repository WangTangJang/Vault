`Error` 和 `Exception` 都是Java中处理异常的类，但它们之间有一些关键的区别：
## 继承层次关系：
   - `Error` 类和 `Exception` 类都直接继承自 `Throwable` 类。
   - `Throwable` 类是Java异常处理机制的根类。
## Error：
   - `Error` 表示严重的问题，通常是虚拟机无法解决的问题。
   - `Error` 不应该被程序员捕获和处理，因为它们通常表示虚拟机的运行时错误或系统级错误，例如内存溢出、栈溢出等。
   - 常见的 `Error` 包括 `OutOfMemoryError`、`StackOverflowError` 等。
## Exception：
   - `Exception` 表示程序运行过程中可能发生的异常情况，可以被程序员捕获和处理。
   - `Exception` 分为两类：
	   - [[异常的分类有哪些？#受检异常（Checked Exceptions）：|受检异常]]（Checked Exception）
	   - [[异常的分类有哪些？#非受检异常（Unchecked Exceptions）：|非受检异常]]（Unchecked Exception）。
## 总结：
- `Error` 表示程序运行时出现的严重问题，通常无法恢复。
- `Exception` 表示程序运行中可能出现的一般性问题，可以通过捕获和处理来处理。
- `Error` 一般是由虚拟机自身引起的，而 `Exception` 是由程序运行时引起的。
