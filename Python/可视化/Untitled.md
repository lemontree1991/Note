### 前言

源码地址：https://github.com/5zjk5/guanzgzhou_food

有两份广州的美食数据来自 A，B 两个网站，以及一份它们的地理信息数据：

![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AAvdl4hSjkzJyJb9u96F2WibzXgCpWxRf6nOINB472yqMWb0HGPOg0ibQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



为了给去广州的游玩的人提供一些美食的参考，制作一个 BI 仪表盘，需求如下：

1. 广州美食地图分布（广州地图）
2. 哪个行政区美食最多（饼图）
3. 集中在哪些商圈（前十）（柱状图）
4. 星级分布（圆环图）
5. 美食类型（条形）
6. 推荐美食词云（词云）
7. 评论数，人均价格，口味评分，环境评分，服务评分的相关性（热力图）
8. 综合评分=（口味评分+环境评分+服务评分）/3 与人均价格关系（散点图）
9. 制作可视化仪表盘







### **数据预处理**

导入库并查看数据：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AAsxFXK5SaPpricO6wJGjbTZ3PUZ2PkyaGftp0Gm9ia0t6gibdCme7B1eA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



A，B 两数据的结构是一样的，但有两列的列名不同，我们修改 A 的列名后，并把 A 数据中【人均价格】列中的【元】去掉，再纵向合并两个数据集，并去重，接着他们的地理信息数据以【店铺ID】为键进行连接：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AkvNBwVh1YxsLoovZruaLswbxUFOEz79yadxd3ACR26YvEBtuJe8blg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



根据我们的需求，选择需要用到的列并查看有无缺失值需要处理：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AT8XurP6xiaeicqGJIpNBonDPWEEtVrTLM22iazxB5icUgA6DPvRiaC2ibQSw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



从结果上看并没有缺失值，接下来就先制作每一个需求的图表。







### **图表制作**

绘制的每一张图表，需要封装成函数给仪表盘使用，每一张图表没有使用默认的主题，而是使用了一种紫色的主题。

**广州美食地图分布：**选取经纬度，以及店铺名称，在广州地图上绘制散点，一个点代表一家店铺：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3ABiaD6HpnZftRgoADeibrZricic4vjNH3nwW2ek2K2LVOEoj7kic4gEm0Mpg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AicMR7LMo0P2NalTXvJaG6e2SC50sOibMEYYt1RcwgGxudTPYdgqfV1Qg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



美食主要集中在天河，越秀，海珠，荔湾，番禺，白云，黄埔区。

**哪个行政区美食最多：**需要先计算各个行政区的美食数量，在绘制饼图：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3ACl3FrzUgGiceqMOfGaAu00ic0m3ZOIGankO6Lmk4EWALsIgwW4X2Cq1w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AGPPgeSoRnNRMxVnCuGZ6IpxDvW1cyNYmR9RVPYOxo0EFzATUVDmjZw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



可以看到美食数量最多行政区的是天河区。

**集中在哪些商圈：**需要先计算各个出现商圈的次数，在绘制柱状图：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3Av8zPPwAzH7V5VXWSY8UZsicJhUXX8YEfE7DhbqJ3wicAIN49LGxqMMgw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3A9xXIaQQl1ZqSlMHME0hJ0t3N8pHNYKAQkwyz6hGqicRbL32f3MatRow/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



美食数量最多的商圈是珠江新城。

**星级分布：**需要先计算各个出现的星级的数量，在绘制圆环图：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3Av7MTBONC6tea1yIwPNU37Ra2AYxatNjzQ6VrB5wSw0ROklbHLibDZ6w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3APX40tia33jicUKj2X8KZcL4TFrGEM5QSYELicWDmYaDMIzVLRibC2Y7R2A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



四星与准五星占了大多数。

**美食类型：**计算各个类型的数量，绘制条形图：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AeR6O6aJ5FB9z5oVEZ6XkdST7xkDS0vYfFmibOLbaPqyWIsRwSzwGTtw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AicxvfFvYUiapTCbrR4Qj5RZYF15WOaWPH8iaWZ4mejeMWotHU92Dlibscw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



从结果看，店铺美食类型为西餐的是比较多的。

**推荐美食：**在每个店的数据中，都有推荐美食，把所有美食连接起来，并计算词频，绘制词云：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AbxiaBnX4rYwmmfLbibKkvIYw6hSuPsycsrG3moLZibdkiaibhDWl7gRXJDw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AHmg4icibpVwhIJc2Hcr9ODsyibOpOQDxaLndvwWGXvUltLlZ89Ffo7Hpw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



**评论数，人均价格，口味评分，环境评分，服务评分的相关性：**绘制他们两两的相关性热力图，越偏红，正相关性越强：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AoHGwGRjRwTC8oiauibyAlJribsn5h2ThRLDBicSMvQmsMjQ8TjRkkRkB3g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3APhFEwAdltJeiaDqgRJOqokwSw7uyRNQUt8zpVmW5y2fVddsicicHERk7w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



**综合评分与人均价格关系：**综合评分=（环境评分+口味评分+服务评分）/3，新增一列保存起来，绘制它与人均价格散点图：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AicicGYXpticzSMPIh6KzTnWnwSxUKLTZKrJ2dsSQnRW9DKIJMZh8VhWrQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AmveOicAZsBp9RFsV2xmlgLhoRERYrFB7nY8QO5Rqvwh99qqO2cB6wNg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



接下来就把这些图合成仪表盘







### **仪表盘**

pyecharts 官网文档：

http://pyecharts.org/#/zh-cn/composite_charts?id=page%ef%bc%9a%e9%a1%ba%e5%ba%8f%e5%a4%9a%e5%9b%be





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AerhTkqS5pMJT8wctZVfwnvic2GnXHE3LEHC4D9drXVBUibFhUlLqibqDg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



我们上面的绘图，都是封装成函数的，接下来使用下面代码调用绘制函数（page.add 中就是，这里折叠了）：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AsqTB3XsnOoLCDUoSqUcKtoXmvyvJsxJn6Qw42yDW0pKiaKqWNhOOKiaw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



上面代码就绘制图表并保存为 html 文件，**需要注意的是 18-19 行为注释。**

调用绘制函数后生成了一个 page.html 文件，里面包含了所有图表，通过拖拽图表设计成我们想要布局的样子（下图是随便放的）然后点击左上角【save config】保存布局的 json 文件：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AuOHlicnC2wFI0iaAkPgA7F5jwFgUBiaYQQ0vMqY6cTL1yicp7jaKTia2icNA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



修改代码，17 行注释，18-19 行取消注释，因为我们已经生成了图表不需要再生成一次，在生成一次的话图表 id 会改变，那刚刚下载布局文件就用不了了：





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AFn0zic9ZHGw8WP03EC2iaqTWRkjK6SVB5SBaFbxlBqUrwR5fLXrZCmng/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



page.html 为生成的所有图表的文件

page.json 为下载的布局文件

仪表盘.html 为布局好的的仪表盘文件

打开仪表盘.html:





![img](https://mmbiz.qpic.cn/mmbiz_png/oNyOswO2YLcQfEnw8lawianLGDricCNA3AeyK3FzhPMy0aqjtIdgvOhRq2Qg9TubAPYD6cHtFMebtqSV60kRIf4w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



这样我们就完成了 pyecharts 仪表盘的制作。