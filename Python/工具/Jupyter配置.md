[toc]

# 安装
```
pip install jupyter
# 测试
jupyter notebook --ip=*  # root下换成：jupyter notebook --ip=* --allow-root

```
# 配置
## 已有配置
```
mkdir ~/my_configs
cp config.py ~/my_configsjupyter_my_config.py
```

## 自动生成配置文件
```
# 生成配置文件
jupyter notebook --generate-config

c = get_config()

c.IPKernelApp.pylab = "inline"

c.NotebookApp.ip = "*" # 允许访问的IP地址，设置为*代表允许任何客户端访问
# 允许远程访问
c.NotebookApp.allow_remote_access = True
c.NotebookAPp.open_browser = False # 不开启浏览器

c.NotebookApp.port= 8888 # 端口
c.NotebookApp.notebook_dir = "/home/lemon/jupyterNote"

# 密码
c.NotebookApp.password = 'sha1:b39d2445079f:9b9ab99f65150e113265cb99a841a6403aa52647'
# 证书
c.NotebookApp.certfile = u'/root/.jupyter/mycert.pem'

```

### 密码

```
ipython

from IPython.lib import passwd                                                                                  
passwd()                                                                                                     
Enter password: 
Verify password: 
Out[2]: 'sha1:cc49ca6e1cdc:e6166a72029e9d5eb646781f704afe419b89dcea'
                              
```
### 证书

```
# 中间的交互信息可以随便填
openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem
```

## 后台运行
```
# 日志会写入到 my.log
# 想要日志的话也可以重定向到 /dev/null
nohup jupyter notebook --config jupyter_notebook_config.py --allow-root 2>&1 > my.log & 

nohup jupyter notebook 2>&1 > /dev/null &
```

# 插件
```
# 安装 nbextensions
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user

# 常用插件
Autopep8     (代码格式化)
Hinterland （代码自动补全）
Codefolding （代码折叠）
Notify       （Notify功能就能在任务处理完后及时向你发送通知）
Collapsible Headings(使得各级标题可缩进)
Table of Contents (2)(生成目录)

```
- 