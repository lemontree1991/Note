### 1.基本概念

1.什么是客户端/服务器架构？
服务器就是一系列硬件或软件，为一个或多个客户端（服务的用户）提供所需的“服务”。它存在唯一目的就是等待客户端的请求，
并响应它们（提供服务），然后等待更多请求。
说白了就是一个提供服务，一个请求服务得到相应的一个过程。

2.套接字：通信端点
套接字是计算机网络数据结构，它体现了上节中描述的“通信端点”的概念。在任何类型的通信开始之前，网络应用程序必须创建套接字。
可以将它们比作电话插孔，没有它将无法进行通信。

Python只支持AF_UNIX、AF_NETLINK、AF_TIPC 和 AF_INET ，重点使用基于网络的AF_INET.

3.套接字地址：主机-端口对
它是网络通信过程中端点的抽象表示，python使用元组保存:ADDR = (HOST,PORT)。

4.套接字类型
流式套接字(SOCK_STREAM):用于提供面向连接、可靠的数据传输服务。

数据报套接字(SOCK_DGRAM):提供了一种无连接的服务。该服务并不能保证数据传输的可靠性，数据有可能在传输过程中丢失或出现数据重复，且无法保证顺序地接收到数据。

#### 1.1框架图

![img](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5CaHR0cHM6Ly9pbWFnZXMuY25ibG9ncy5jb20vY25ibG9nc19jb20vZ29vZGNhbmRsZS9zb2NrZXQyLmpwZw)

------

### 2.Python网络编程

#### 2.1 常见的套接字对象方法和属性

| 名 称               | 描 述                                                        |
| ------------------- | ------------------------------------------------------------ |
| **服务端**          | **服务器套接字方法**                                         |
| s.bind(ADDR)        | 将地址（主机名、端口号对）绑定到套接字上                     |
| s.listen([backlog]) | 设置并启动 TCP 监听器，如果指定backlog，则必须至少为0（如果低于0，则设置为0）； |
| s.accept()          | 被动接受 TCP 客户端连接，一直等待直到连接到达（阻塞）        |
| **客户端**          | **客户端套接字方法**                                         |
| s.connect()         | 主动发起 TCP 服务器连接                                      |
| s.connect_ex()      | connect()的扩展版本，此时会以错误码的形式返回问题，而不是抛出一个异常 |
| **普通通用**        | **普通的套接字方法**                                         |
| s.recv()            | 接收 TCP 消息                                                |
| s.recv_into()       | 接收 TCP 消息到指定的缓冲区                                  |
| s.send()            | 发送 TCP 消息                                                |
| s.sendall()         | 完整地发送 TCP 消息                                          |
| s.recvfrom()        | 接收 UDP 消息                                                |
| s.recvfrom_into()   | 接收 UDP 消息到指定的缓冲区                                  |
| s.sendto()          | 发送 UDP 消息                                                |
| s.getpeername()     | 连接到套接字（TCP）的远程地址                                |
| s.getsockname()     | 当前套接字的地址                                             |
| s.getsockopt()      | 返回给定套接字选项的值                                       |
| s.setsockopt()      | 设置给定套接字选项的值                                       |
| s.shutdown()        | 关闭连接                                                     |
| s.close()           | 关闭套接字                                                   |
| s.detach()          | 在未关闭文件描述符的情况下关闭套接字，返回文件描述符         |
| s.ioctl()           | 控制套接字的模式（仅支持 Windows）                           |
| **阻塞**            | **面向阻塞的套接字方法**                                     |
| s.setblocking()     | 设置套接字的阻塞或非阻塞模式                                 |
| s.settimeout()      | 设置阻塞套接字操作的超时时间                                 |
| s.gettimeout()      | 获取阻塞套接字操作的超时时间                                 |
| **文件方法**        | **面向文件的套接字方法**                                     |
| s.fileno()          | 套接字的文件描述符                                           |
| s.makefile()        | 创建与套接字关联的文件对象                                   |
| **属性**            | **数据属性**                                                 |
| s.family            | 套接字家族                                                   |
| s.type              | 套接字类型                                                   |
| s.proto             | 套接字协议                                                   |

#### 2.2 创建服务和客户端

![img](D:%5C%E7%AC%94%E8%AE%B0%5Cassets%5CaHR0cHM6Ly9pbWFnZXMuY25ibG9ncy5jb20vY25ibG9nc19jb20vZ29vZGNhbmRsZS9zb2NrZXQzLmpwZw)

先从服务器端说起。服务器端先初始化Socket，然后与端口绑定(bind)，对端口进行监听(listen)，调用accept阻塞，等待客户端连接。在这时如果有个客户端初始化一个Socket，然后连接服务器(connect)，如果连接成功，这时客户端与服务器端的连接就建立了。客户端发送数据请求，服务器端接收请求并处理请求，然后把回应数据发送给客户端，客户端读取数据，最后关闭连接，一次交互结束。

##### 2.2.1 创建TCP服务

**一般的创建流程：**



```php
ss = socket()       #  创建服务器套接字
ss.bind(ADDR)       #  套接字与地址绑定
ss.listen()         #  监听连接
while True:         #  服务器无限循环
cs = ss.accept()    #  接受客户端连接
comm_loop:          #  通信循环
cs.recv()/cs.send() #  对话（接收 / 发送）
cs.close()          #  关闭客户端套接字
ss.close()          #  关闭服务器套接字 # （可选）
```

##### 2.2.2 创建 TCP 客户端

**一般的创建流程：**



```bash
cs = socket()       #  创建客户端套接字
cs.connect()        #  尝试连接服务器
comm_loop:          #  通信循环
cs.send()/cs.recv() #  对话（发送 / 接收）
cs.close()          #  关闭客户端套接字
```

##### 2.2.3 创建UDP服务

**一般的创建流程：**



```php
ss = socket()       #  创建服务器套接字
ss.bind(ADDR)       #  套接字与地址绑定
while True:         #  服务器无限循环
ss.sendto()         #  发送 
ss.recvfrom()       #  接收
ss.close()          #  关闭服务器套接字 # （可选）
```

##### 2.2.4 创建 UDP 客户端

**一般的创建流程：**



```bash
cs = socket()       #  创建客户端套接字
comm_loop:          #  通信循环
cs.sendto()         #  发送 
cs.recvfrom()       #  接收
cs.close()          #  关闭客户端套接字
```

------

**server.py**代码



```python
'''
遇到问题没人解答？小编创建了一个Python学习交流QQ群：857662006 
寻找有志同道合的小伙伴，互帮互助,群里还有不错的视频学习教程和PDF电子书！
'''
import socket
from time import ctime
import json
import time
HOST = ''
PORT = 9001
ADDR = (HOST, PORT)
BUFFSIZE = 1024
MAX_LISTEN = 5


def tcpServer():
    # TCP服务
    # with socket.socket() as s:
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        # 绑定服务器地址和端口
        s.bind(ADDR)
        # 启动服务监听
        s.listen(MAX_LISTEN)
        print('等待用户接入。。。。。。。。。。。。')
        while True:
            # 等待客户端连接请求,获取connSock
            conn, addr = s.accept()
            print('警告，远端客户:{} 接入系统！！！'.format(addr))
            with conn:
                while True:
                    print('接收请求信息。。。。。')
                    # 接收请求信息
                    data = conn.recv(BUFFSIZE)
                    print('data=%s' % data)
                    print('接收数据：{!r}'.format(data.decode('utf-8')))

                    # 发送请求数据
                    conn.send(data.encode('utf-8'))
                    print('发送返回完毕！！！')
            s.close()


# 创建UDP服务
def udpServer():
    # 创建UPD服务端套接字
    with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as s:
        # 绑定地址和端口
        s.bind(ADDR)
        # 等待接收信息
        while True:
            print('UDP服务启动，准备接收数据。。。')
            # 接收数据和客户端请求地址
            data, address = s.recvfrom(BUFFSIZE)

            if not data:
                break

            print('接收请求信息：{}'.format(data.decode('utf-8')))

            s.sendto(b'i am udp,i got it', address)

        s.close()

if __name__ == '__main__':

    while True:
        choice = input('input choice t-tcp or u-udp:')

        if choice != 't' and choice != 'u':
            print('please input t or u,ok?')
            continue

        if choice == 't':
            print('execute tcpsever')
            tcpServer()
        else:
            print('execute udpsever')
            udpServer()
```

**client.py**代码



```python
'''
遇到问题没人解答？小编创建了一个Python学习交流QQ群：857662006 
寻找有志同道合的小伙伴，互帮互助,群里还有不错的视频学习教程和PDF电子书！
'''
import socket

from time import ctime
HOST = 'localhost'
PORT = 9001
ADDR = (HOST, PORT)
ENCODING = 'utf-8'
BUFFSIZE = 1024


def tcpClient():
    # 创建客户套接字
    with socket.socket(family=socket.AF_INET, type=socket.SOCK_STREAM) as s:
        # 尝试连接服务器
        s.connect(ADDR)
        print('连接服务成功！！')
        # 通信循环
        while True:
            inData = input('pleace input something:')
            if inData == 'q':
                break
            # 发送数据到服务器
            inData = '[{}]:{}'.format(ctime(), inData)

            s.send(inData.encode(ENCODING))
            print('发送成功！')

            # 接收返回数据
            outData = s.recv(BUFFSIZE)
            print('返回数据信息：{!r}'.format(outData))

        # 关闭客户端套接字
        s.close()


def udpClient():
    # 创建客户端套接字
    with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as s:
        while True:
            # 发送信息到服务器
            data = input('please input message to server or input \'quit\':')
            if data == 'quit':
                break
            data = '[{}]:{}'.format(ctime(), data)

            s.sendto(data.encode('utf-8'), ADDR)

            print('send success')

            # 接收服务端返回信息
            recvData, addrs = s.recvfrom(BUFFSIZE)

            print('recv message : {}'.format(recvData.decode('utf-8')))

        # 关闭套接字
        s.close()


if __name__ == '__main__':

    while True:
        choice = input('input choice t-tcp or u-udp or q-quit:')
        if choice == 'q':
            break
        if choice != 't' and choice != 'u':
            print('please input t or u,ok?')
            continue

        if choice == 't':
            print('execute tcpsever')
            tcpClient()
        else:
            print('execute udpsever')
            udpClient()
```

**代码说明**：先执行 `python server.py`,在执行`python client.py`,就可以测试TPC/UDP简单的通信了。