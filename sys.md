# sys 模块

`sys` 模块提供了一些系统相关的变量和函数。

```python
>>> import sys
```

## sys.version

一个包含 `Python` 解释器版本号加编译版本号以及所用编译器等额外信息的字符串。 此字符串会在交互式解释器启动时显示。 请不要从中提取版本信息，而应当使用 `version_info` 以及 `platform` 模块所提供的函数。

```python
>>> print(sys.version)
3.10.1 (tags/v3.10.1:2cd268a, Dec  6 2021, 19:10:37) [MSC v.1929 64 bit (AMD64)]
```

## sys.version_info

一个包含版本号五部分的元组: `major`, `minor`, `micro`, `releaselevel` 和 `serial`。 除 `releaselevel` 外的所有值均为整数；发布级别值则为 'alpha', 'beta', 'candidate' 或 'final'。 对应于 `Python` 版本 2.0 的 `version_info` 值为 (2, 0, 0, 'final', 0)。 这些部分也可按名称访问，因此 `sys.version_info[0]` 就等价于 `sys.version_info.major`，依此类推。

```python
>>> print(sys.version_info)
sys.version_info(major=3, minor=10, micro=1, releaselevel='final', serial=0)
>>> list(sys.version_info)
[3, 10, 1, 'final', 0]
>>> print(sys.version_info[0])
3
```

## sys.exit([arg])

从 `Python` 中退出。实现方式是抛出一个 `SystemExit` 异常，因此异常抛出后 `try` 语句的 `finally` 分支的清除动作将被触发，这样可能会打断外层的退出尝试。

可选参数 `arg` 可以是表示退出状态的整数（默认为 `0`），也可以是其他类型的对象。如果它是整数，则 `shell` 等将 `0` 视为“成功终止”，非零值视为“异常终止”。大多数系统要求该值的范围是 `0`--`127`，否则会产生不确定的结果。`Unix` 程序通常用 `2` 表示命令行语法错误，用 `1` 表示所有其他类型的错误。传入其他类型的对象，如果传入 `None` 等同于传入 `0`，如果传入其他对象则将其打印至 `stderr`，且退出代码为 `1`。特别地，`sys.exit("some error message")` 可以在发生错误时快速退出程序。

由于 `exit()` 最终“只是”抛出一个异常，因此当从主线程调用时，只会从进程退出；而异常不会因此被打断。

```python
>>> exit()
```

## sys.argv

一个列表，其中包含了被传递给 `Python` 脚本的命令行参数。 `argv[0]` 为脚本的名称（是否是完整的路径名取决于操作系统）。如果是通过 `Python` 解释器的命令行参数 `-c` 来执行的， `argv[0]` 会被设置成字符串 '-c' 。如果没有脚本名被传递给 Python 解释器， `argv[0]` 为空字符串。

为了遍历标准输入，或者通过命令行传递的文件列表，参照 `fileinput` 模块。

```python
if sys.argv[1:]:
    start_path = sys.argv[1]
else:
    start_path = '.'
```