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

- Pytest 使用 Python 的 assert 进行条件判断

- pytest 文件名进行测试函数（成功的案例）

```
def test_passing():
	assert (1, 2, 3) == (3, 2, 1)
```
判断 == 左右是否相等

```
collected 1 item

tests\test1.py .                                                         [100%]

========================== 1 passed in 0.09 seconds ===========================
```
Pytest 使用 . 标识测试成功（PASSED），也可以使用 -v 选项，显示测试的详细信息

- Pytest 文件名进行测试函数（失败的案例）
```
def test_failing():
	assert(1, 2, 3) == (3, 2, 1)

其结果为：
tests\test2.py F                                                         [100%]

================================== FAILURES ===================================
________________________________ test_failing _________________________________

    def test_failing():
>       assert (1, 2, 3) == (3, 2, 1)
E       assert (1, 2, 3) == (3, 2, 1)
E         At index 0 diff: 1 != 3
E         Use -v to get the full diff

tests\test2.py:2: AssertionError
========================== 1 failed in 0.19 seconds ===========================
```
Pytest 使用 F 标识测试失败（FAILED）



##

## 断言 assert
- Pytest 允许使用标准的 python assert 用于验证 Python 测试中的期望和值
```
def f():
	return 3

def test_function():
	assert f() == 4
```
断言函数返回某个值

- Pytest 支持显示最常见的子表达式的值，包括调用、属性、比较以及二进制和一元运算符。这允许在不丢失自省信息的情况下使用不带样板代码的调用 Python 构造。
```
assert a % 2 == 0, "value was odd, should be even"
```
然后根本不进行断言内省，消息将简单地显示在回溯中。


## 关于预期异常的断言
```
import pytest
def test_zero_divsion():
	with pytest.raises(ZeroDivisionError):
		1 / 0
```
如果需要访问实际的异常信息，可以使用：
```
def test_recursion_depth():
	with pytest.raises(RuntimeError) as excinfo:
		def f():
			f()
		f()
	assert "maximum recursion" in str(excinfo.value)
```
excinfo 是一个 ExceptionInfo 实例，它是引发的实际异常的包装。主要特征：.type、.value 和 .traceback
```
import pytest

def myfunc():
	raise ValueError("Exception 123 raised")

def test_match():
	with pytest.raises(ValueError, match=r".* 123 .*"):
		myfunc()
```
可通过 match 上下文管理器的关键字参数，用于测试正则表达式是否匹配异常的字符串表达形式（类似于 TestCase.assertRaisesRegexp 方法从 unittest)的 regexp 参数 match 方法与 re.search 函数，因此在上面的示例中 match='123' 也会起作用的。
另一种形式的 pytest.raises() 函数，其中传递的函数将用给定的 *args 和 **kwargs 并断言引发了给定的异常

https://www.osgeo.cn/pytest/assert.html