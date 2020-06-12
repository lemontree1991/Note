近期遇到一个需求就是我们需要把当前比较耗费资源的接口开发成异步通讯的机制，简单来说就是有一个消息队列来不停地进行消息的集中分发与任务处理，这里应用端给出的方案是使用`kafka`来做，但是这个我在之前没有接触过，所以没有头绪，就想着在本机搭建一下`kafka`的环境，来去熟悉整个操作过程。

接下来就先开始kafka环境的安装。`kafka`的安装需要依赖于`zooeleeper`模块，虽然说`kafka`自带了`zooeleeper`模块，但是网上清一色的教程都说还是需要自己手动提前去安装`zooeleeper`模块才行的，所以这里的第一步就是安装`zooeleeper`模块，下载地址在这里：

```
http://mirror.bit.edu.cn/apache/zookeeper/zookeeper-3.4.14/
```

我下载的是3.4.14版本的：

![img](https://mmbiz.qpic.cn/mmbiz_png/5mt0ewv9OS2qlM6iaJ64iawbkPrqnQso9aAq30lfXStcaxy4azmU3Aj8qOZXk29JFsgicbhuia09jm4ib6N3vCJaLfA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

安装的话是很简单的，直接解压缩到本地，之后按照下面的步骤进行操作即可：

```
1、解压后进入目录conf下，将“zoo_sample.cfg”重命名为“zoo.cfg”
（zookeeper的默认端口是2181，如需改变可以在对zoo.cfg进行编辑）
2、进入bin目录下，点击zkServer.cmd运行
3、命令行显示如下，表示运行成功
```

![img](https://mmbiz.qpic.cn/mmbiz_png/5mt0ewv9OS2qlM6iaJ64iawbkPrqnQso9a1l01dfnsmcIib4744ictjE86b2XCuIEMhIibria4vWAxoNdlw8ibgAAB42w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

安装和启动成功`zooeleeper`模块后，就可以下载和安装`kafka`模块了，这里需要注意一下下载合适的版本才可以的，网上很多教程都是比较早的了，所以给出来的版本信息可能找不到了也可能不再合适了，这里我是摸索进行尝试安装了，在第一次安装失败之后，我查了很多教程，后面发现自己安装的`scala`不对，这里需要注意的就是`kafka`是基于`scala`编写的，所以想要成功安装`kafka`就必须保证`scala`成功安装好了。

下载kafka另一个比较重要的点或者是需要注意的点就是需要下载和安装二进制的文件，这里我的下载链接如下：

```
http://kafka.apache.org/downloads
```

我下载的是下面的版本:

![img](https://mmbiz.qpic.cn/mmbiz_png/5mt0ewv9OS2qlM6iaJ64iawbkPrqnQso9a89QIx9fpIjHibGlAvvUGwptForOdhuUHd6IW6qe5Op5fjnKNC1mR9ZQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

下载到本地后，直接解压缩即可，结果截图如下所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/5mt0ewv9OS2qlM6iaJ64iawbkPrqnQso9a9cxkrm54QZkPFhBVAOfJmf7w6W7Sv1kdYiacQJWTeTpgsibV3KTOflzA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

进入到当前目录后，打开CMD窗口，执行下面的命令：

```
.\bin\windows\kafka-server-start.bat .\config\server.properties
```

不出意外，只要前面的环境条件都满足了，这里应该是可以正常启动的，终端会输出一大堆密密麻麻的日志。

![img](https://mmbiz.qpic.cn/mmbiz_png/5mt0ewv9OS2qlM6iaJ64iawbkPrqnQso9aQnPeyKPxKU2jFaIHYtqqtDa4UEXf2sC6SdBmTxFYRmTlHUrZQpS5mw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

到这里kafka就安装成功了，下面就可以进行自己的使用了。

这里简单说一下，在编写程序的时候遇到了一些问题，报错如下：

```
Exception in thread kafka-python-producer-1-network-thread (most likely raised during interpreter sh
```

解决上面的报错需要处理两个地方，分别如下：

**1、修改系统hosts文件**

- 进入  `C:\Windows\System32\drivers\etc` 下 以管理者身份打开`hosts`文件
- 在后面新增一行内容  `127.0.0.1 localhost`
- 保存退出

**2、修改kafka对应的配置文件**

- 进入到 `config` 文件夹下面
- 打开 `server.properties`
- 在文件第31行 `#listeners=PLAINTEXT://:9092` 下面加入下面两行内容

```
advertised.listeners = PLAINTEXT://localhost:9092
advertised.listeners = PLAINTEXT://127.0.0.1:9092
```

- 保存退出

效果图如下所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/5mt0ewv9OS2qlM6iaJ64iawbkPrqnQso9abZxXWUWy3TxRQtn7RrrtdRNF83icFBdjmicz22SM4cV0wpzqVnCeVSng/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

处理完上面两个部分就可以了，接下来我们基于Python来开发对应的实例。

**实例一：**

这个是官方提供的实例，比较简单，主要是编写对应的生产者和消费者，下面是具体的代码实现：

生产者代码：

```
#!usr/bin/env python
#encoding:utf-8
from __future__ import division
 
'''
__Author__:沂水寒城
功能：kafka 学习实例
'''
 
from kafka import KafkaConsumer,KafkaProducer
 
producer=KafkaProducer(bootstrap_servers='localhost:9092')
msg="HelloWorld".encode('utf-8')
print(msg)
producer = KafkaProducer(bootstrap_servers='localhost:9092')
producer.send('demo',msg,partition=0)
producer.close()
```

消费者代码：

```
#!usr/bin/env python
#encoding:utf-8
from __future__ import division
 
'''
__Author__:沂水寒城
功能：  kafka 消费者
'''
 
from kafka import KafkaConsumer
 
consumer=KafkaConsumer('demo',bootstrap_servers=['localhost:9092'])
for msg in consumer:
    info="%s:%d:%d: key=%s  value=%s" % (msg.topic, msg.partition, msg.offset, msg.key, msg.value)
    print info
```

接下来在终端启动消费者，然后执行生产者，观察消费者终端的输出：

![img](https://mmbiz.qpic.cn/mmbiz_png/5mt0ewv9OS2qlM6iaJ64iawbkPrqnQso9aicaCtEmBWm6iaSn3z0aoU8n2MocJ78qKPuHibLEdxjIlavEUSPOc78pkA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，生产者发出对应的demo  Topic之后，消费者消费了这个Topic产生的数据，这是一个比较简单的实例应用。

**实例二：**

这部分主要是贴合自己的应用来构建的实例，这里需要传输的是json数据对象，下面是具体的代码实现：

生产者代码：

```
#!usr/bin/env python
#encoding:utf-8
from __future__ import division
 
'''
__Author__:沂水寒城
功能：kafka 学习实例
'''
 
import json
import base64
import datetime
from kafka import KafkaProducer
 
TS=str(datetime.datetime.now().strftime('%Y%m%d%H%M%S'))
files = {
        "name": TS,
        "data": base64.b64encode(open('demo.png', "rb").read())
        }
producer = KafkaProducer(
                            value_serializer=lambda v: json.dumps(v).encode('utf-8'),
                            bootstrap_servers='localhost:9092'
                         )
for i in range(3):
    print 'i: ', files
    producer.send('D', files)
producer.close()
```

消费者代码：

```
#!usr/bin/env python
#encoding:utf-8
from __future__ import division
 
'''
__Author__:沂水寒城
功能：  kafka 消费者
'''
 
import sys
import json
from kafka import KafkaConsumer
 
KAFKA_TOPIC = 'D'
KAFKA_BROKERS = 'localhost:9092'
consumer = KafkaConsumer(bootstrap_servers=KAFKA_BROKERS,auto_offset_reset='earliest')
consumer.subscribe([KAFKA_TOPIC])
try:
    for message in consumer:
        print(message.value)
except KeyboardInterrupt:
    sys.exit()
```

接下来在终端启动消费者，然后执行生产者，生产者的输出如下：

```
i:  {'data': '/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/9k=', 'name': '20200326203003'}
i:  {'data': '/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/9k=', 'name': '20200326203003'}
i:  {'data': '/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/9k=', 'name': '20200326203003'}
[Finished in 0.9s]
```

消费者输出如下：

![img](https://mmbiz.qpic.cn/mmbiz_png/5mt0ewv9OS2qlM6iaJ64iawbkPrqnQso9aAOOYUVfPc07rG7UNzdIXBD3ROtVtKB18pz0yj3QdTVsdoxgfQPXczA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，生产者发出去的json数据对象已经被消费者“消费”了，本部分主要是演示json数据的处理与应用。到这里，本文的主要内容就结束了。

作者：沂水寒城，CSDN博客专家，个人研究方向：机器学习、深度学习、NLP、CV

Blog: http://yishuihancheng.blog.csdn.net