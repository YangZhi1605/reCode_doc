# flask框架+layui骨架解读

记住:FlaskTest1是没有那个登录之后的跳转问题的，现在把flaskTest1复刻一下，然后研究编写的逻辑

## 1、flask框架的认知

**1、render_template来引入页面**



**render_template()函数是[flask](https://so.csdn.net/so/search?q=flask&spm=1001.2101.3001.7020)函数，它从模版文件夹templates中呈现给定的模板上下文。** 



 Flask中render_template的使用和模板的继承_GeekLeee的博客-CSDN博客
https://blog.csdn.net/GeekLeee/article/details/52505605#:~:text=%E8%AF%B4%E7%99%BD%E4%BA%86%EF%BC%8C%E5%85%B6%E5%AE%9Erender_template%E7%9A%84,%E5%AF%B9html%E8%BF%9B%E8%A1%8C%E4%BF%AE%E6%94%B9%E6%B8%B2%E6%9F%93%E3%80%82



![1675832576928](E:\文档_Typora\代码梳理解读\flask+layui项目.assets\1675832576928.png)





## 2、layui框架的认知

javascript - 前端框架LayUI介绍及用法 - 个人文章 - SegmentFault 思否
https://segmentfault.com/a/1190000039037413



**一个一个板块的分析吧**



>**关闭标签页**

 Layui 框架的点击事件：layadmin-event 

![1675827595753](E:\文档_Typora\代码梳理解读\flask+layui项目.assets\1675827595753.png)



>**ajax**

**登录注册这里用的ajax**





## 3、页面处理

一个页面一个页面的啃。

### 3.1、首页图云数据展示

![1675833156999](E:\文档_Typora\代码梳理解读\flask+layui项目.assets\1675833156999.png)

这个HTML页面的内容特别简单。只是展示了图片

大抵是因为这个骨架的原因，我们返回的页面，会展示在这个右侧

![1675833557352](E:\文档_Typora\代码梳理解读\flask+layui项目.assets\1675833557352.png)



###  3.2、市场需求页面



**关于Python的sqlite模块。**

 sqlite3 模块程序，可以满足您在 Python 程序中使用 SQLite 数据库的需求。

SQLite – Python | 菜鸟教程
https://www.runoob.com/sqlite/sqlite-python.html





**关于正则**



```
people_str = re.sub("\D","",item[1]) # 通过正则提取数字
```



**关于pyecharts**

Python数据可视化三部曲之 Pyecharts 从上手到上头_侯小啾的博客-CSDN博客
https://skylarkprogramming.blog.csdn.net/article/details/124241048?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-124241048-blog-127569944.pc_relevant_3mothn_strategy_and_data_recovery&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-124241048-blog-127569944.pc_relevant_3mothn_strategy_and_data_recovery&utm_relevant_index=5



数据可视化之Pyecharts制作酷炫图表 - 知乎
https://zhuanlan.zhihu.com/p/133816584



Pyecharts教程——Line折线图_echarts_Plum_Steven-DevPress官方社区
https://huaweicloud.csdn.net/638088eedacf622b8df89c96.html?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EOPENSEARCH%7Eactivity-3-123517595-blog-107074164.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EOPENSEARCH%7Eactivity-3-123517595-blog-107074164.pc_relevant_default&utm_relevant_index=6

![1675836944060](E:\文档_Typora\代码梳理解读\flask+layui项目.assets\1675836944060.png)

在pyecharts中，图表完成制作后通过 **render () 函数输出为html文件**，你可以在 render () 中传递输出地址参数，将html文件保存到自定义的位置。 



**关于iframe标签**

<iframe> 标签是一个内联框架，即**用来在当前HTML 页面中嵌入另一个文档的**，且所有主流浏览器都支持iframe标签。 以上属性可以根据需要进行设置。 

![1675837696007](E:\文档_Typora\代码梳理解读\flask+layui项目.assets\1675837696007.png)



**关于SQLite 数据库转 MySQL数据库**

sqlite导出的.db数据库文件转存入mysql的方式 - 腾讯云开发者社区-腾讯云
https://cloud.tencent.com/developer/article/1888637



**关于报错**

手动修改一些库的版本就可



**关于layui骨架**



## 4、补一下SQLite数据库的知识



第77天：Python 操作 SQLite - 纯洁的微笑博客
http://www.ityouknow.com/python/2019/12/03/python-SQLite-077.html



**冷静冷静，一步一步来吧，先玩熟悉SQLite数据库，再把数据爬取了存储进数据库。**



**关于python字符串拼接**

Python字符串拼接（包含字符串拼接数字）
http://c.biancheng.net/view/4237.html



使用sqlite数据库 | python数据批量写入sqlite3 - Lookcos的网络日志
https://lookcos.cn/archives/722.html



SQLite简单学了一下，现在重新回到主线，去处理那个放扒模块的问题



## Selenium学习



>chromedriver' executable needs to be in PATH 报错解决



问题解决：

Python解决'chromedriver' executable needs to be in PATH问题_The Future is mine的博客-CSDN博客
https://blog.csdn.net/yhj198927/article/details/88806824



这个模块，简单的过了一下，现在是回到了数据库的数据获取环节，数据库没有学好就是痛苦呀

我现在是不是该考虑找个教程学学数据库的相关操作

