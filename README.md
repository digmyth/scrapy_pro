##  爬虫基础知识
### 简介
爬虫：利用python模块伪造浏览器行为，读取网页源码，再经过正则匹配取出HTML文本的一系列处理，数据分析称为爬虫

基本内容： 
```
 - python实现浏览器行为： requests
 - beautifulsoup4  对HTML内容进行分析
 - HTTP相关知识：
   - cookie
   - csftToken
   - 请求头：其中ContenType表明什么格式封装的数据，服务器需要用相应格式解数据
     请求： 请求头(cookie)/请求体(发送的内容)
     响应： 响应头（浏览器读取头数据）/响应体（我们看到的网页或网页源码）
 - 数据持久化（数据库存储）       
```             
            
### 具备技能
```            
性能相关：批量get URL可想而知性能重要性
1 线程池，进程池，

2 协程coroutine（微线程）：
     协程本身没有用，只做切换，具有切换特性,要想性能很高，刚好遇到IO时切换
     
3 异步非阻塞（如twisted,gevent,asyncio,tornado内部集成）

  其中gevent异步模块由2个东西组成:
	   greenlet协程: greenlet就是利用yield实现的协程
	   libevent: libevent做异步IO库
```
[七牛云进程线程分享](https://segmentfault.com/a/1190000001813992)　

异步非阻塞
```
遇到IO请求不等待继续执行其它任务,如果IO请求响应内容回来了,自动回调某个函数.
异步： 回调（相关于通知机制）
非阻塞： 不等待

```
后面会学到爬虫框架：scrapy
```
 1 内部是twisted实现异步
 2 写入URL自动下载网页
 3 自动将下载的网页解析为对象方便我们处理
```     
后面也会学到分布式爬虫组件redis-scrapy

### 爬虫实现

基本模块：
```
pip3 install requests
pip3 install beautifulsoup4   （将网页字符串解析为对象，用于直接取文本内容）
``` 

爬虫实现
```
 1 代码发送get请求： 请求头+请求体
 2 接收返回值： 响应头+响应体（本质字符串）
 3 获取响应体后进行解析，方便获取文本内容
	 import requests
	 from bs4 import BeautifulSoup
```

注意几点：
```
1 回车时得到token和cookies,如果有token和cookies的话取出来,一般get请求
2 提交用户名密码时带上token和cookies,一般post请求,并且取出登录成功后的cookies
3 登录后才能看到的网页(前2次请求的cookies都带上)
```

### 示例
  * github或汽车之家
  * 抽届点赞
  * 博客园用户名密码密文发送给服务器的情况，其实是利用js三方模块在浏览器端加密再发送的（python rsa模块加密）
  * 知乎，新浪微博这种有图形验证码的网站，需要第三方平台做图像识别（类似滑动验证码这种验证其实是向后台发送鼠标坐标）
  
  
