## Problem
### Description
用native-image构建一个java类（.class)，这个**应该**是将其变成可执行程序（.exe)的工具，可能。
但是为什么还要我装个VisualStudio？
### Presentation

C:\Users\Administrator\Desktop>native-image HelloWorld
Error: Failed to find 'vcvarsall.bat' in a Visual Studio installation.
Please make sure that Visual Studio 2022 version 17.1.0 or later is installed on your system. You can download it at https://visualstudio.microsoft.com/downloads/.https://visualstudio.microsoft.com/downloads/ If this error persists, please try and run GraalVM Native Image in an x64 Native Tools Command Prompt or file a ticket.
## Solution
