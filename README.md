# Python Syntax Cheatsheet

Python 语法备忘清单

## 目录

1. 集合

    [List](#List)

2. 类型

    Type

3. 语法

    Args

4. Python标准库

    [sys](#sys) [getopt](#getopt) [argparse](#argparse) [hashlib](#hashlib)


5. 第三方模块


6. [Python coding tips](#Python_coding_tips)


## 内容

### List

### [sys](sys.md)

`sys` 模块提供了一些系统相关的变量和函数。

[sys.version](sys.md#sysversion)

一个包含 `Python` 解释器版本号加编译版本号以及所用编译器等额外信息的字符串。

[sys.version_info](sys.md#sysversion_info)

一个包含版本号五部分的元组: `major`, `minor`, `micro`, `releaselevel` 和 `serial`。 

[sys.exit([arg])](sys.md#sysexitarg)

从 `Python` 中退出。

[sys.argv](sys.md#sysargv)

一个列表，其中包含了被传递给 `Python` 脚本的命令行参数。

### [getopt](getopt.md)

`getopt` 模块是一个C风格的命令行选项解析器。

### [argparse](argparse.md)

`argparse` 模块是一个命令行选项、参数和子命令解析器。

### [hashlib](hashlib.md)

`hashlib` 模块针对许多不同的安全哈希和消息摘要算法实现了一个通用接口。包括SHA1, SHA224, SHA256, SHA384, SHA512 和 MD5。


## Python_coding_tips

[18 个坏习惯，你一定要抛弃](bad-habits.md)


## 参考资料

- [Comprehensive Python Cheatsheet](https://github.com/gto76/python-cheatsheet)
- [中文技术文档的写作规范](https://github.com/ruanyf/document-style-guide)
