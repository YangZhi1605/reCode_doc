# 基于python 的豆瓣电影数据可视化

# 数据获取 和 清洗存储



## 1、爬虫模块

### 1.1、虚拟解释器 也就是 python.exe的选择

我感觉保持这里有就行

![1671846833589](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671846833589.png)

因为主要是要有这个文件夹，至于为什么要有它，我后续去补，我这会先做项目

我的理解是，这个文件夹是虚拟解释器的家，也就是虚拟解释器自带的库、包，我们手动安装的库，都会放到这里。

![1671846905422](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671846905422.png)

### 1.2、装需要的库

目前有两种方式：

>一、比较老实的，在pycharm中一个一个的搜，一个一个的安装，虽然慢，但是特别稳

![1671847908796](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671847908796.png)



> 第二种是通过cmd执行脚本文件

先进入当前虚拟解释器的Script文件夹下，然后通过终端cmd打开，然后运行里面的active.bat。然后输入pip install这个安装库的命令，同时找到我们写好的所有库名称以及版本的文件，回车即可



![1671848088888](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671848088888.png)



![1671848407978](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671848407978.png)





### 1·3、创建数据库 —— 存储爬取的数据

这儿假如没有安装数据库或者没有Navicat的话，我再补充。





### 1.4、爬取网页的分析



要区分数据类型：客户端渲染（数据直接存在页面的html中——查看源代码）。还是网络请求(检查)



> 这个部分会根据网页的变化而变化，比较灵活，我着重一点一点吃透。



整个流程我完成之后来补充，因为网站是别人的，其实随时都可能变化的，先会一个大纲，到时候调整就好。



**`插曲`**

**① url 和 uri的区别**

 [URL和URI的区别](https://maizitoday.github.io/post/url%E5%92%8Curi%E7%9A%84%E5%8C%BA%E5%88%AB/#:~:text=URL%E6%98%AF%E4%B8%80%E7%A7%8D%E5%85%B7%E4%BD%93,%E8%B6%B3%E5%A4%9F%E7%9A%84%E4%BF%A1%E6%81%AF%E6%9D%A5%E5%AE%9A%E4%BD%8D%E3%80%82&text=%E4%BE%8B%E5%A6%82%EF%BC%9A%20www.baidu.com,%E6%98%AFURL%20%E5%90%8C%E6%97%B6%E4%B9%9F%E6%98%AFURI%E3%80%82)

> 最初拿到的URI：douban://douban.com/movie/1292052
>
> 我自己加了HTTP协议，然后后面的www.douban.com应该是主机了吧，其他是目录movie下的1292052了。感觉逻辑没有错,,,
>
> http://www.douban.com/movie/1292052 /
>
> 下面是可以访问的路径：
>
> https://movie.douban.com/subject/1292052/ 【这是代表我还得自己拼接字符串吗】—— 答案是：是的。
>
> **我需要拿到的是电影编号，然后再拼接：**https://movie.douban.com/subject/ 
>
> 
>
> 我不是药神的URI 和 URL（顶部导航栏粘贴下来的，应该是叫URL吧(菜狗发问)）
>
> URI：douban://douban.com/movie/26752088
>
> URL：https://movie.douban.com/subject/26752088/
>
> 

>目前来说，处理页面数据的时候，说直白一点就是看人家是不是直接把数据写到页面中的，直接写的，就能够在页面中拿到，不是的，救救需要通过一写请求响应来处理。



> 分析URL的格式
>
> 第一个页面的Request URL：
>
> https://m.douban.com/rexxar/api/v2/movie/recommend?refresh=0&start=0&count=20&selected_categories={}&uncollect=false&sort=T&tags=&ck=1F3O
>
> 点击"加载更多"，到第二个页面，看刷新出来的地址：
>
> https://m.douban.com/rexxar/api/v2/movie/recommend?refresh=0&start=20&count=20&selected_categories={}&uncollect=false&sort=T&tags=&ck=1F3O
>
> 再点击"加载更多"，到第三个页面，看刷新出来的地址：
>
> https://m.douban.com/rexxar/api/v2/movie/recommend?refresh=0&start=40&count=20&selected_categories={}&uncollect=false&sort=T&tags=&ck=1F3O
>
> 应该可以发现规律了



### 1.5、代码编写

#### 1.5.1、需要的字段先存到csv文件

#### 1.5.2、连接数据库 + 写 sql语句

### 1.5.3、在主函数里拿到当前一整个主页内容的requests.get请求了



>这里需要普及一下requests.get这个方法是怎么玩的。
>
>[requests](https://so.csdn.net/so/search?q=requests&spm=1001.2101.3001.7020)是一个简单的请求库，其中的get方法可以像指定服务器发送get请求，该库是外部库，需要手动安装。

首先理解一下常规的URL + get请求的玩法

**参数① —— url（请求的url地址，必需 ）**

![1671896056630](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671896056630.png)



**参数② —— headers参数（请求头，可选）**

![1671896080260](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671896080260.png)

**参数③ —— params参数 （请求参数，可选）**

这个参数这里着重解释一下：

![1671896143972](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671896143972.png)

意思这个字典的内容（键 和 值会附在问号后面，作为URL的访问参数）

那我们需要还是不需要这个参数，需要根据实际的URL，比如视频中的链接

![1671896233418](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671896233418.png)

所以他教程中代码的requestUrl就只用写到`subjects`，然后写一个字典parms，里面放`{'start':xxx}`

，然后放到get方法中，就能够还原这个URL了，但是现在这个网址变得复杂了,,,



## 1.2、回溯学爬虫的基础知识



>我现在感觉视频演示的那个链接不是特别的典型，然后我自己对爬虫也不是特别熟悉。我先去做几个小案例
>
>再回来看，为什么没法像视频中那种，获取到一个整页面的信息

![1671980222887](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671980222887.png)





问题描述：

![1671980429277](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671980429277.png)

这个请求网址粘贴到顶部搜索栏，出现的是一个字典信息

![1671980486765](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671980486765.png)





>问题解决收集：返回418是因为反爬机制

[解决Python爬取:response.status_code为418 问题](https://blog.csdn.net/weixin_42422090/article/details/104705631)

![1671981955643](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1671981955643.png)

[使用BeautifulSoup中的find()和findAll()函数时关键字参数的注意事项](https://blog.csdn.net/IMW_MG/article/details/78109199)

[Python学习日记5|BeautifulSoup中find和find_all的用法](https://www.jianshu.com/p/ef2f246cae46)

><em> 标签是一个短语标签，用来呈现为被强调的文本。 



>目前的总结：确定好标签和属性，属性class这儿因为python 也有关键字class。所以使用了class_
>
>其二是注意find 和 findAll。

![1672024913632](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672024913632.png)







爬虫学习阶段一结束：目前收获：

别杠，我们的目的是实现可视化。那么先解决比较容易实现的，然后再逐渐迭代中，解决那个让我头痛的粘贴到搜索栏之后是一个集合的问题。

其他就是SoupBeautiful模块的使用了。时刻记住：不要迷失在项目中，记得抽身出来抬头看天。



这个问题还是没有解决。

我现在拿到了可以爬取数据的网址，但是需要解析。不是直接的json，然后得学学什么是json了。它演示视频里，就是纯纯的json数据，好神奇



简单的json:

![1672048010235](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672048010235.png)





>补知识点了：
>
>**这是集合：**
>
>创建集合用花括号或 [`set()`](https://docs.python.org/zh-cn/3.10/library/stdtypes.html#set) 函数。注意，创建空集合只能用 `set()`，不能用 `{}`，`{}` 创建的是空字典。
>
>`basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}`
>
>**这是字典：**
>
>`tel = {'jack': 4098, 'sape': 4139}`





先看大节奏吧。



##  2、切实爬取豆瓣信息

### 2.1、Xpath爬取

[XPath 语法](https://www.runoob.com/xpath/xpath-syntax.html)







### 2.2、正则匹配数据









### 2.3、零散函数积累

[Python strip()方法](https://www.runoob.com/python/att-string-strip.html)

>Python strip() 方法用于移除字符串头尾指定的字符（默认为空格或换行符）或字符序列。
>
>**注意：**该方法只能删除开头或是结尾的字符，不能删除中间部分的字符。



[python中json.dumps()和json.dump() 以及 json.loads()和json.load()的区分](https://blog.csdn.net/chenmozhe22/article/details/81434081)

>json.dumps



[list.append(*x*) ]([5. 数据结构 — Python 3.11.1 文档](https://docs.python.org/zh-cn/3/tutorial/datastructures.html#more-on-lists) )

> append:在列表末尾添加一个元素，相当于 `a[len(a):] = [x]` 。 





[Pyhon join()方法](https://www.runoob.com/python/att-string-join.html)

>Python join() 方法用于将序列中的元素以指定的字符连接生成一个新的字符串。 



```python
 symbol = "-";
seq = ("a", "b", "c"); # 字符串序列
print symbol.join( seq );
```







## 3、关于处理结果

![1672141629116](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672141629116.png)

这是视频中的。这是我的，特别在一些地方

比如这种：

![1672141660539](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672141660539.png)

是不一样的。它是直接在一个串里，彼此是联动的，我的是在一个列表里，彼此独立。

我大概知道怎么调整了，意思是，我`剧情`、`罪犯`这里应该用`,`的规则链接成新的字符串







## 4、第一个电影信息爬取完毕后的分析

因为我的数据信息在HTML中，然后是以这方式存储的

![1672471467457](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672471467457.png)

![1672471484157](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672471484157.png)

那么。我现在想实现遍历这个页面的`20个li`,应该先拿到这些`li`。然后逐个去里面爬取具体的信息

现在先拿到这个`20个li`吧。准确来说，我是要拿到其中的链接：

![1672473198272](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672473198272.png)



## 5、现在拿一个页面的20个数据

> **现在的目标是先拿一个页面的20个数据，然后再拿10个页面**



### 5.1、现在的问题

>**第一个页面中，阿甘正传的导演拿不到**

视频里也有我这儿的类似报错。我看看他是怎么解决的

![1672474346500](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672474346500.png)

![1672474360865](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672474360865.png)



他的解决办法：

![1672474631096](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672474631096.png)

因为是html中属性的值不是完全匹配的，所以就改成了`contains`这个属性的那个ul标签



> **冷静冷静。看报错看报错**



他解决的部分电影没有时长问题

![1672474893864](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672474893864.png)



他出现的报错：

![1672474941882](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672474941882.png)



>**冷静分析是有好处的**

![1672475920243](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672475920243.png)



再次遇到问题：拿第23个页面数据的时候，出现这个报错

![1672475976513](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672475976513.png)



![1672478396823](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672478396823.png)

![1672478530502](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672478530502.png)





>**抓评论数字的时候 —— 调整Xpath语法解决了**

25个页面的数据初步爬取成功

![1672477294031](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672477294031.png)







## 6、拿一页一页的数据，存储到csv中

他教的是递归爬取所有页面的所有数据，我这里就常规的使用循环去爬取吧。他那个源码。我试着能不能去理解。

![1672484714692](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672484714692.png)



![1672484741480](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672484741480.png)



现在有个问题是，对于已经爬取过的数据，会重复的爬取。 —— 暂时不处理重复爬取，我数据一次性拿完就好，是在需要了，我再改成递归，然后再实现，主要我不太会python的循环结束的判断。

![1672486292260](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672486292260.png)



视频里采取的角度是开启一个txt，标记已经爬取过的页面信息。



是时候再去补补这个model了

![1672485234323](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672485234323.png)

`strip()`方法可以去除制表符





> **目前的问题是，为什么循环拿一个数据了，URL都是不同的**

![1672487565299](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672487565299.png)





## 7、数据清洗和爬取存储到数据库

![1672479855287](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672479855287.png)



他这个数据清洗出来好整齐

![1672489132818](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672489132818.png)



预料之中，纯纯报错

![1672489530412](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672489530412.png)

现在研究一下吧。



### 7.1、1054报错解决的记录

> **重新梳理梳理逻辑，然后解决报错的事儿吧**



```sql
sqlalchemy.exc.OperationalError: (pymysql.err.OperationalError) (1054, "Unknown column 'directors,rate,title,actor,cover,detailLink,year,types,country, langue,time, movieTime,comment_len,stars,summary,comments(cuser,cstar,ctime,ccontent),imgList,movieUrl' in 'field list'")
[SQL: INSERT INTO movie (`directors,rate,title,actor,cover,detailLink,year,types,country, langue,time, movieTime,comment_len,stars,summary,comments(cuser,cstar,ctime,ccontent),imgList,movieUrl`) VALUES (%(directors,rate,title,actor,cover,detailLink,year,types,country, langue,time, movieTime,comment_len,stars,summary,commentsAcuser,cstar,ctime,ccontentZ,imgList,movieUrl)s)]
```



> **创建数据库的语句应该是对的**

![1672491282207](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672491282207.png)



> **那么现在的问题是，csv是怎么存储到SQL文件中的**



> **现在的问题，为什么把我的数据，写成一列了,应该是19列的**



```python
(0, 1)
Empty DataFrame
Columns: [directors,rate,title,actor,cover,detailLink,year,types,country, langue,time, movieTime,comment_len,stars,summary,comments(cuser,cstar,ctime,ccontent),imgList,movieUrl]
Index: []
(0, 1)
```





> **太好了，上一个1054解决了，是我创建csv文件的时候，把各个列，都写到一块了（~~应该是被格式化了~~然后插入的时候，确实找不到列了）**

![1672492802215](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672492802215.png)

列数是和视频里同步了

![1672492848177](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672492848177.png)



但是另一个问题出现了

![1672492779015](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672492779015.png)



# flask框架 

## 1、前期准备



### 1.1、项目的创建和初始化

> 保证网络好一点

![1672798375653](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672798375653.png)

和爬虫一样，需要初始化一个虚拟解释器。wc,我解释器了...

![1672798534895](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672798534895.png)



自己补充了`venv`之后，得到这个结果。应该是成了

![1672801850456](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672801850456.png)



### 1.2、安装需要的包（通过venv）

进入Scripts打开终端，启动activate.bat

![1672802476723](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672802476723.png)

启动结果

![1672802540653](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672802540653.png)

然后先退出Scripts。再退出venv,`pip install` 那个`requirements`文件

我是有部分包没有装上的，说是远程网络的问题，我暂时不处理。假如确实需要这个包了，我再装。

这是视频里的

![1672803817874](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672803817874.png)



大部分是装上了的

**![1672803970255](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672803970255.png)**



![1672805385378](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672805385378.png)



### 1.3、放置静态资源

![1672804725630](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672804725630.png)



### 1.4、导入需要的包



## 2、代码编写



### 2.1、启动测试

![1672805485541](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672805485541.png)

### 2.2、根据请求决定页面

我暂时不知道为什么要写GET请求，然后我大致感觉是因为这里

![1672805615175](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672805615175.png)





### 2.3、改HTML结构



记录一下改图片。

因为css是压缩过的，不好处理，这里直接改框架上的

![1672806845461](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672806845461.png)

![1672806859066](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672806859066.png)

注册那儿也是一样的逻辑，改图片竣工，现在改改文字样式



### 2.4、改页面的数据响应

![1672808038969](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672808038969.png)



> **创建存储登录信息的数据库**



```sql
CREATE TABLE user(
	id int PRIMARY KEY auto_increment,
	email VARCHAR(255),
	password VARCHAR(255)
)
```



> **注意他改html的时候，都是写了name属性，这里需要倒腾一下**

![1672808419349](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672808419349.png)



> 自己写ERROR页面

![1672808933161](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672808933161.png)









### 2.底 、这里记录需要解决的代码

>`@app.route`得学一下这个了

>`return render_template('login.html')`



这个flask写网页，都不用重新启动，直接刷新，太爽了

>为什么写半斜杠



![1672806461936](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672806461936.png)



这里同时积累一个报错，原因是我使用函数的语法不当

![1672810245995](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672810245995.png)



应该是使用filter函数进行加载，我需要去搞清楚这个函数的工作原理



```python
 filter_list = list(filter(filter_fn,users) )
```





## 3、写主页 拿数据

准备逐渐写成这种来展示数据

![1672885241901](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672885241901.png)



> ① 拿到session里的用户名

![1672885674136](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672885674136.png)

然后剩下的没有什么大事，主要是调整页面



> 解决一个没有登录，就直接进入主页的问题。需要用到生命周期函数来解决。

![1672886902853](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672886902853.png)





### 3.1、写工具类

>**① 负责数据库连接**

![1672920254167](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672920254167.png)



然后需要拿到这个连接。确实执行sql文件去分析数据了。

>**临时学了一手lamba表达式**

匿名函数lambda：是指一类无需定义标识符（函数名）的函数或子程序。所谓匿名函数，通俗地说就是没有名字的函数，lambda函数**没有名字**，是一种**简单的**、**在同一行中定义函数**的方法。 



*lambda x, y: x*y；函数输入是x和y，输出是它们的积x*y 



> **临时了解一下split函数**

[Python split()方法](https://www.runoob.com/python/att-string-split.html)

Python **split()** 通过指定分隔符对字符串进行切片，如果参数 num 有指定值，则分隔 num+1 个子字符串 

- str -- 分隔符，默认为所有的空字符，包括空格、换行(\n)、制表符(\t)等。
- num -- 分割次数。默认为 -1, 即分隔所有。



```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
txt = "Google#Runoob#Taobao#Facebook"
 
# 第二个参数为 1，返回两个参数列表
x = txt.split("#", 1)
 
print x

# 输出结果
['Google', 'Runoob#Taobao#Facebook']
```





>这个函数`render_template`是拿来干嘛的



![1672923351868](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672923351868.png)







### 3.2、饼状图、折线图、数据统计表

这里是使用的echarts来解决

其一是需要引入echarts.min.js的文件

然后需要引入自己要用来制图的js的脚本代码的具体内容



> 封装数据

![1672969548171](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672969548171.png)



>为了处理出这种数据，临时学一下字典的get方法

![1672971514993](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672971514993.png)



> **学一个python字典的items方法**

![1672971764864](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672971764864.png)





> **新学一个meta标签**

![1672978382398](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672978382398.png)

图片不显示可以使用这种方式弄弄

![1672978528258](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672978528258.png)







#  

#总结板块

## 12月24日总结

今天

其一是知道了拿数据要区分是服务器渲染的还是请求给数据，服务器渲染的，那么数据就直接在HTML中，假如是请求的，在HTML中就直接拿不到，需要在拿到请求之后，才能在根据链接找页面

其二是python 安装库的方法好快

其三是python 创建数据表以及连接数据库

其三是requests.get这个方法的使用，当然，也是有困难的，这个链接现在解析不了。

## 12月25日总结

第一：爬虫418 和 403的处理

第二：BeautifulSoup的find函数的认识

## 12月26日总结

第一：json格式的认知 + 要看情况自己爬取到的信息的格式是`text`还是`json`

第二：完整的简单爬虫的完成，数据的存储

第三：项目的流程认识。① 爬虫爬取数据，存到数据库，为后面写网页的时候，提取处理，做数据分析。那么无论什么类型的网页，我的目的是拿到数据，存起来，就行了，后面会拿SQL语句去数据库里逐一查需要的东西。

第四：争取这周天之前把这个东西做完 + 复盘吧。

## 12月27日总结

爬取一个页面中需要的18个信息完成。

xpath语法比较熟悉了 + 知道匹配数字的正则表达式。但是最后匹配图片的还是没有解决

对爬取的流程稍微有点清晰了，待会改成一个页面的25个数据，以及总共十个页面。最后数据存到数据库，然后就可以开始写下个模块了的网页来拿数据并展示了。

今天是认识了好几个函数append,join,去掉首位空格strip



## 12月31日总结

爬虫模块完成+数据存储到数据库完成

![1672494387329](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672494387329.png)

虽然我不知道为什么csv就存储到数据库了，感觉是底层写的，暂时不研究吧。这批数据后续可能还要精华，不然可能查询不出来，也就是数据还需要清洗到方便查询的地步。

到时候再不会什么学什么吧。

然后对处理报错更加冷静了 好事。能够精心梳理逻辑这儿挺好的。

最后是代码层面。巩固一个 `strip()` 函数清除首尾的空格、换行等等。





## 1月4日总结

数据库连接以及设置一个游标，下面就是一个简单的工具类了



```sql
from pymysql import *

conn = connect(host='localhost',user='root',password='123456',database='dbm',port=3306)
cursor = conn.cursor() # 这里是数据库链接去调用cursor方法


def querys(sql,params,type='no_select'):
    params = tuple(params)
    cursor.execute(sql,params)
    if type != 'no_select':
        data_list = cursor.fetchall()
        conn.commit()
        return data_list
    else:
        conn.commit()
        return '数据库语句执行成功'
```



第二是学了，判断两次密码是否一致

第三是学了，判断用户是否已经存在。这里有部分函数是我都不太懂的。可能需要深化

第四，今天主要学的是登录注册逻辑的实现，~~这个数据库管理软件好难用了~~

![1672810377444](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672810377444.png)





然后今天还学了，`filter`实现过滤。



```
filer_user = list(filter(filer_fn,users))
```



注册到数据库以及拿信息实现登录完成

![1672811146229](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672811146229.png)





## 1月5号总结

第一个学到的知识点是重定向的事儿

![1672918846343](E:\文档_Typora\工程相关\python数据分析\基于python 的豆瓣电影数据可视化.assets\1672918846343.png)



第二个知识点是flask框架中的网页拿到数据也是通过`{{ }}`



第三个是lambda表达式



