## 查询Github的DNS解析
访问[IPAddress.com](https://www.ipaddress.com/)，分别查询下面三个域名的DNS地址。

```bash
github.com
assets-cdn.github.com
github.global.ssl.fastly.net
```



```BAS

```

## 修改本地hosts文件

管理员身份打开cmd或者powershell

``` 
 cd C:\Windows\System32\drivers\etc
 notepad hosts
```

添加

```bash
140.82.113.4 github.com 
185.199.109.153 assets-cdn.github.com 
199.232.69.194 github.global.ssl.fastly.net
```

## 刷新系统DNS缓存

```
ipconfig /flushdns
```

