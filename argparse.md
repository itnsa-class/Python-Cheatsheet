# argparse 模块

`argparse` 模块是一个命令行选项、参数和子命令解析器，可以让人轻松编写用户友好的命令行接口。程序定义它需要的参数，然后 `argparse` 将弄清楚如何从 `sys.argv` 解析出那些参数。 `argparse` 模块还会自动生成帮助文档和使用手册，并在用户给程序传入无效参数时报出错误信息。

```python
from pathlib import Path
import sys
import argparse

Version = 1.0

def get_sections():
    return 'DEFAULT', 'tlc', 'tls'

def get_args():
    parser = argparse.ArgumentParser(
        description="Markdown file coverted to html and pdf file with python-markdown2 and wkhtmltopdf", 
        formatter_class=argparse.RawTextHelpFormatter)
    parser.add_argument('-v', '--version', action='version',
                        version='%(prog)s {}'.format(str(Version)))
    parser.add_argument('-t', '--template', required=False, nargs='?', const='DEFAULT', default='DEFAULT',
                        help='select a HTML template: {}\n(default: %(default)s)'.format(get_sections()))
    parser.add_argument('-i', required=True,
                        metavar='markdown_file', help='input a markdown file')
    parser.add_argument('-o', metavar='directory',
                        default='.', help='output directory\n(default: current directory)')
    args = parser.parse_args()

    md_file = Path(args.i)
    output_dir = Path(args.o)
    template = args.template

#    if not md_file.is_file():
#        print('Error: {} not found'.format(md_file))
#        sys.exit(1)
#   if not output_dir.is_dir():
#        output_dir.mkdir()
    if template not in get_sections():
        print('Warnning: template \'{}\' not found, use \'DEFAULT\''.format(template))
        template = 'DEFAULT'
    return md_file, output_dir, template

if __name__ == '__main__':
    md_file, output_dir, template = get_args()
    print(md_file, output_dir, template)
```