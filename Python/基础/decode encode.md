### 引言

decode英文意思是 解码

encode英文原意 编码

**字符串在Python内部的表示是unicode编码**，因此，在做编码转换时，通常需要以unicode作为中间编码， 即先将其他编码的字符串解码（decode）成unicode，再从unicode编码（encode）成另一种编码。

![img](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5C1419341-20181020215002430-563015786.png)



### str

#### decode

decode的作用是将其他编码的字符串转换成unicode编码

如str1.decode('gb2312')，表示将gb2312编码的字符串str1转换成unicode编码

#### encode

encode的作用是将unicode编码转换成其他编码的字符串

如str2.encode('gb2312')，表示将unicode编码的字符串str2转换成gb2312编码。

#### 总结

想要将其他的编码转换成utf-8必须先将其解码成unicode然后重新编码成utf-8,它是以unicode为转换媒介的 

如：s='中文' 如果是在utf8的文件中，该字符串就是utf8编码，如果是在gb2312的文件中，则其编码为gb2312。这种情况下，要进行编码转换，都需要先用 decode方法将其转换成unicode编码，再使用encode方法将其转换成其他编码。

通常，在没有指定特定的编码方式时，都是使用的系统默认编码创建的代码文件

### byte

字节串（bytes）和字符串（string）的对比：

- 字符串由若干个字符组成，以字符为单位进行操作；字节串由若干个字节组成，以字节为单位进行操作。
- 字节串和字符串除了操作的数据单元不同之外，它们支持的所有方法都基本相同。
- 字节串和字符串都是不可变序列，不能随意增加和删除数据。
bytes 只负责以字节序列的形式（二进制形式）来存储数据，至于这些数据到底表示什么内容（字符串、数字、图片、音频等），完全由程序的解析方式决定。如果采用合适的字符编码方式（字符集），字节串可以恢复成字符串；反之亦然，字符串也可以转换成字节串。

说白了，bytes 只是简单地记录内存中的原始数据，至于如何使用这些数据，bytes 并不在意，你想怎么使用就怎么使用，bytes 并不约束你的行为。

bytes 类型的数据非常适合在互联网上传输，可以用于网络通信编程；bytes 也可以用来存储图片、音频、视频等二进制格式的文件。

字符串和 bytes 存在着千丝万缕的联系，我们可以通过字符串来创建 bytes 对象，或者说将字符串转换成 bytes 对象。有以下三种方法可以达到这个目的：

- 如果字符串的内容都是 ASCII 字符，那么直接在字符串前面添加`b`前缀就可以转换成 bytes。
- bytes 是一个类，调用它的构造方法，也就是 bytes()，可以将字符串按照指定的字符集转换成 bytes；如果不指定字符集，那么默认采用 UTF-8。
- 字符串本身有一个 encode() 方法，该方法专门用来将字符串按照指定的字符集转换成对应的字节串；如果不指定字符集，那么默认采用 UTF-8。

#### 使用不同方式创建 bytes 对象

```python
#通过构造函数创建空 bytes
b1 = bytes()
#通过空字符串创建空 bytes
b2 = b''
#通过b前缀将字符串转换成 bytes
b3 = b'http://c.biancheng.net/python/'
print("b3: ", b3)
print(b3[3])
print(b3[7:22])
#为 bytes() 方法指定字符集
b4 = bytes('C语言中文网8岁了', encoding='UTF-8')
print("b4: ", b4)
#通过 encode() 方法将字符串转换成 bytes
b5 = "C语言中文网8岁了".encode('UTF-8')
print("b5: ", b5)
```

输出

```python
b3:  b'http://c.biancheng.net/python/'
112
b'c.biancheng.net'
b4:  b'C\xe8\xaf\xad\xe8\xa8\x80\xe4\xb8\xad\xe6\x96\x87\xe7\xbd\x918\xe5\xb2\x81\xe4\xba\x86'
b5:  b'C\xe8\xaf\xad\xe8\xa8\x80\xe4\xb8\xad\xe6\x96\x87\xe7\xbd\x918\xe5\xb2\x81\xe4\xba\x86'
```

从运行结果可以发现，对于非 ASCII 字符，print 输出的是它的字符编码值（十六进制形式），而不是字符本身。非 ASCII 字符一般占用两个字节以上的内存，而 bytes 是按照单个字节来处理数据的，所以不能一次处理多个字节。

#### str byte互转

![在这里插入图片描述](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5C294be603fc6b3b2b64cb8fab0a5eec0d.png)

```
a: str = "你好！"
b: bytes = a.encode('gbk')
print(b)
c: str = b.decode('gbk')
print(c)
```

输出

```python
b'\xc4\xe3\xba\xc3\xa3\xa1'
你好！
```

可以看到 str 使用 encode() 方法就可以转换成 byte ，byte 使用 decode 方法就能转变成 str 。这两种方法都可以给一个编码解码的方式，只有方式一样才能正确解码。没有参数则按照当前代码编写所指定的编码方式进行编码解码。