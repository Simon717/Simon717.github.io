---
title: Python全局变量
typora-root-url: ..
date: 2019-05-30 16:38:22
tags:

---

在python脚本中 最外层的代码都是全局的操作

运行下面这段代码 

```python
a = 3
def Fuc():
    print (a)
    a = a + 1
Fuc()
```

会出现错误

```python
local variable 'a' referenced before assignment
```

![1559205953040](/images/1559205953040.png)

翻译一下就是 变量a还没有赋值就被引用了

为什么呢 因为在函数内部 遇到了和全局变量同名的变量 默认认为是局部变量

只有用global声明了这是全局变量之后 才可以引用外部的全局变量

```python
a = 3
def Fuc():
    global a
    print (a)
    a=a+1
Fuc()
```

这样就没问题了

![1559206723446](/images/1559206723446.png)

如果是下面的代码

```python
a = 2 # 定义的全局变量


def Fuc():
    global a # 函数中想要修改全局变量 需要用global声明
    print(a)
    a = a + 1

# 先执行上面的代码 之后执行下面的代码
if __name__ == "__main__":
    print(a) # 此处相当于最外层 所以可以直接修改全局变量
    a = a + 1
    Fuc()
    print(a)
```

执行结果就是

![1559206783151](/images/1559206783151.png)

[参考](<https://blog.csdn.net/songyunli1111/article/details/76095971>)