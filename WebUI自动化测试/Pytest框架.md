# Pytest
- Pytest 是一个针对 Python 的自动化测试框架，它可以使简单的和可扩展的测试变得容易。使用 Pytest 进行测试时简洁和可读的，不需要样板代码，这使得我们可以很方便地进行自动化测试。Pytest 是一个全平台通用的工具，支持的 Python 版本包括 Python2.7、3.4、3.5、3.6等
- Mac 平台安装 Python3.6，从官网下载吧
- 卸载 Mac 平台的 Python：一个思路是进入 Python Console
```
import sys
print(sys.path)
```
- 删除打印出来的目录
- 删除 /usr/local/bin 下的 python 相关文件和指向的链接

# 安装
- curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
- python3 get-pip.py
- pip3 install -U pytest

# assert
- Pytest 使用 Python 的 assert 进行条件判断，最简单的测试函数如：
```
def test_passing():
	assert (1, 2, 3) == (3, 2, 1)
```
判断 == 左右是否相等

- pytest 文件名进行测试函数
```
collected 1 item

tests\test1.py .                                                         [100%]

========================== 1 passed in 0.09 seconds ===========================
```
pytest 使用 . 标识测试成功（PASSED），也可以使用 -v 选项，显示测试的详细信息
