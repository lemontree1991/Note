# Value的构造函数：

```python
Value(typecode_or_type, *args[, lock])
```

该方法返回从共享内存中分配的一个[`ctypes`](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.python.org%2F2%2Flibrary%2Fctypes.html%23module-ctypes) 对象,其中typecode_or_type定义了返回的类型。它要么是一个ctypes类型，要么是一个代表ctypes类型的code。比如[`c_bool`](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.python.org%2F2%2Flibrary%2Fctypes.html%23ctypes.c_bool)和'b'是同样的，因为'b'是[`c_bool`](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.python.org%2F2%2Flibrary%2Fctypes.html%23ctypes.c_bool)的code。

ctypes是Python的一个外部函数库，它提供了和C语言兼任的数据类型，可以调用DLLs或者共享库的函数，能被用作在python中包裹这些库。

*args是传递给ctypes的构造参数

# Value的使用

对于共享整数或者单个字符，初始化比较简单，参照下图映射关系即可。如`i = Value('i', 1), c = Value('c', '0')`。

![img](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5C14623457-a5d23c805f54535f.png)



注意，如果我们使用的code在上表不存在，则会抛出：

```python
size = ctypes.sizeof(type_)
TypeError: this type has no size
```

如果共享的是字符串，则在上表是找不到映射关系的，就是没有code可用。所以我们需要使用原始的ctype类型

例如:

```python
from ctypes import c_char_p

ss = Value(c_char_p, 'ss')
```

ctype类型可从下表查阅:

![img](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5C14623457-d4ac752101ad53b6.png)

# 结构体





```python
from ctypes import Structure, c_float, c_int
class Point(Structure):
    _fields_ = [('x', c_int), ('y', c_int)]


point = Point(10, 20)
print('point.x =', point.x)
print('point.y =', point.y)

point = Point(y=5)
print('point.x =', point.x)
print('point.y =', point.y)


class Rect(Structure):
    _fields_ = [('upperleft', Point), ('lowerright', Point)]


rc = Rect(point)
print('rc.upperleft.x = %d, rc.upperleft.y = %d' % (rc.upperleft.x, rc.upperleft.y))
print('rc.lowerright.x = %d, rc.lowerright.y = %d' % (rc.lowerright.x, rc.lowerright.y))

rc = Rect(Point(1, 2), Point(3, 4))
print('rc.upperleft.x = %d, rc.upperleft.y = %d' % (rc.upperleft.x, rc.upperleft.y))
print('rc.lowerright.x = %d, rc.lowerright.y = %d' % (rc.lowerright.x, rc.lowerright.y))

```

输出

```python
point.x = 10
point.y = 20
point.x = 0
point.y = 5
rc.upperleft.x = 0, rc.upperleft.y = 5
rc.lowerright.x = 0, rc.lowerright.y = 0
rc.upperleft.x = 1, rc.upperleft.y = 2
rc.lowerright.x = 3, rc.lowerright.y = 4
```

