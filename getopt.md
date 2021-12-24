# getopt 模块

`getopt` 模块是一个C风格的命令行选项解析器，其 API 设计会让 C `getopt()` 函数的用户感到熟悉。 不熟悉 C `getopt()` 函数或者希望写更少代码并获得更完善帮助和错误消息的用户应当考虑改用 `argparse` 模块。

此模块可协助脚本解析 `sys.argv` 中的命令行参数。 它支持与 `Unix getopt()` 函数相同的惯例（包括形式如 '-' 与 '--' 的参数的特殊含义）。 也能通过可选的第三个参数来使用与 GNU 软件所支持形式相类似的长选项。

```python
import sys
import getopt

def usage():
    print("usage: python3 getopt.py -t <template>")

def get_args(argv):
    try:
        opts, args = getopt.getopt(argv, "ht:", ["help", "template="])
    except getopt.GetoptError as err:
        print(err)
        usage()
        sys.exit(2)
    for opt, arg in opts:
        if opt in ("-h", "--help"):
            usage()
            sys.exit()
        elif opt in ("-t", "--template"):
            template = arg
        else:
            assert False, "unhandled option"
    return template

if __name__ == "__main__":
    if sys.argv[1:]:
        print(get_args(sys.argv[1:]))
    else:
        usage()
        sys.exit(2)
```