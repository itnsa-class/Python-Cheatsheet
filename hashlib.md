通过hashlib计算文件的hash值时，不应该一次性读取整个文件，而是要分块读取。因为如果文件过大，会耗尽电脑的内存资源，而分块读取每次只将一小部分数据load进内存，内存使用量很小。同时应使用update方法会对每一个block进行计算，而不是将其存储起来等到调用hexdigest方法时进行计算，否则，文件过大时，内存还是会耗尽。

hash_file 以二进制方式打开文件，分块读取文件内容，每读出一块内容，就调用一次update方法，最后返回h对象和文件长度，h并不是hash值，想要获取hash值需要使用hexdigest方法。

分块读取文件是一种基于内存考虑的安全选择。

```python
import io
import sys
import hashlib

def hash_sum(path):
    def read_chunks(file, size=io.DEFAULT_BUFFER_SIZE):
        """Yield pieces of data from a file-like object until EOF."""
        while True:
            chunk = file.read(size)
            if not chunk:
                break
            yield chunk


    def hash_file(path, blocksize=1 << 20):
        # type: (Text, int) -> Tuple[Any, int]
        """Return (hash, length) for path using hashlib.sha256()
        """
        h = hashlib.sha256()
        length = 0
        with open(path, 'rb') as f:
            for block in read_chunks(f, size=blocksize):
                length += len(block)
                h.update(block)
        return h, length
    return hash_file(path)

path = sys.argv[1]
hash_value, file_size = hash_sum(path)
print(hash_value.hexdigest())
print(file_size)
```