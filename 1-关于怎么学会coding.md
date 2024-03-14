# 关于怎么学会Coding

## Start——关于前面想说什么

>**在你重新学编码之前，我嘱咐几点**
>**①闭嘴，除了请教，不要把你的担忧或者开心放出来，除非你觉得有用，没有谁值得你信任，再次巩固，没有人值得你信任，**
>**②记住切忌着急。急了以后你会跳过很多题，少做很多事，你到后面，还是会要补上去的。**
>**③冷静冷静冷静，多动脑子去思考，谢绝使用体力劳动来换取脑力上的偷懒。**
>**④我应该是项目为导向，那就专心怼`项目`，一层一层的完善上去，别再犯之前想十分细的错误了，把握大节奏。**
>**⑤卡好时间，时间到就换，不可以无限喂时间给某个进程。照顾全大盘。**
>**⑥为自己设置'限制'，也不为自己设置'限制'**

 

**关于怎么学**：

1、`先视频上手再是文本`。倘若是看视频，视频可以倍数不要跳 —— 这里我再实践一下。

2、听-照抄-模改

![1703740056044](E:\文档_Typora\关于怎么学会coding.assets\1703740056044.png)















## Body——关于执行

### 1、由登录案例展开的内容

#### 1.1、基础认识



（1）flask 和 DJango 算是一个是轻量版，一个是完整版的区别

（2）简单的flask项目是三部曲，那么主体就是在写路由了

#### 1.2、关于GET和POST

从主观形式而言，get是把信息放到URL中传输过去了。POST则不是。

从宏观而言，两者都是HTTP的，其实都不安全，HTTPS是安全的。

从代码而言，flask的`@app.route()中没有自动提示指定get还是post的提示`，得自己写。注意是`methods`

```python
@app.route('/login',methods=['GET','POST'])
def login():
    # return "登录"
    return render_template('login.html')
```
#### 1.3、关于前端标签

<span>操作的是一行文本，其比较灵活。HTML可以用的属性，也就是它可以用的属性

HTML 全局属性 | 菜鸟教程
https://www.runoob.com/tags/ref-standardattributes.html

#### 1.4、关于session会话信息

**可用于处理不登录就可以访问的问题**

主要就是在登录的时候，将登录信息存储到session中，再需要登录的地方，就检验有没有这个session，大型点的项目就不用session了，其实更多是数据库的匹对。

#### 1.5、关于装饰器的知识

**①什么是闭包了？**

```python
def outer(x):
    def inner(y):
        return x + y
    return inner

print(outer(6)(5))
```

我们可以看到，闭包就是在函数内部定义函数，故而有内层函数和外层函数的说法了。内层函数在自己有输入参数的情况，再将外层参数进行处理。最后返回内层函数给外层。这种就为原本的函数增加了功能。



**②那么装饰器了？**

**装饰器即闭包的一种特殊化**

装饰器就是以函数作为参数。将外层函数中的参数丢到内层中加载，`注意是函数作为参数`，加载后，将这个函数返回给内层嘛，再将内层函数返回给外层，也就是将执行结果返回给外层了，因为外层是接收的return是内层运算后的结果，即通过内层，为外层再拓展了功能。
python的装饰器是从低下执行到头上：

例如：

```python
@app.route('/login')
@auth2
@auth1
def login():
	return "登录"
	
```

也就是先把login放给auth1处理，在放给auth2处理，再放给app.route处理。

③ 在运用的时候注意事项是什么了？

注意在加了装饰器之后，在flask中，会改变函数名称，有时候，`endpoint`会等于函数名，所以小心这里，endpoint是不能重复的，但是装饰器可以加在多个函数上改变函数名称。

```python
import functools
def auth(func):
    @functools.wraps(func)
    def inner(*args,**kwargs):
        return func(*args,**kwargs)
    return inner # 注意这里不要有括号，我返回的是一个对象，不是一个函数

@auth
def login():
    pass

# print(login.__name__) # 这是不加装饰器的函数名称：login
# print(login.__name__) # 这是加装饰器的函数名称：inner。我就理解为login函数被装饰了吧。。。好牵强。
print(login.__name__) # 这是加装饰器和@functools的函数名称：login。

```







#### 1.6、关于蓝图的运用



何谓蓝图？相当于一个构建flask项目的规范，`构建为业务功能可拆分的目录结构`。
按照蓝图来创建项目，会使得项目清晰，核心主线跑主线的任务，额外的视图可以散发给小弟。

- ① 创建项目的时候，创建普通的python项目。

- ② 创建相应目录
  1、项目名叫啥，就创建一个啥名的目录
  2、`在当前项目的顶层，随意取名一个启动文件`（叫app.py、start.py、manage.py等等都可以，随意），启动文件是和1中目录同层次的。
  3、在1中的目录中，创建`static`目录、`templates`目录、`views`目录、`__init__.py`文件
  最终得到的层次结构如图：
  ![1704186912494](E:\文档_Typora\关于怎么学会coding.assets\1704186912494.png)

- ③ 在各个文件中填充代码
  `__init__.py`文件 —— 主要newFlask对象，并返回对象

  ```python
  from flask import Flask
  
  def create_app():
      app = Flask(__name__)
      app.secret_key = 'yangzhi823823'
  
      return app
  ```

  

  init的代码中，还可以补充一些路由函数，“表征`我`的部分”

  ```python
  from flask import Flask
  
  def create_app():
      app = Flask(__name__)
      app.secret_key = 'yangzhi823823'
  
      @app.route('/index')
      def index():
          return 'index'
  
      return app
  ```

  

  

  `manager.py`

  ```python
  from BluePrint_example import create_app
  # 上一行代码导入函数
  
  app = create_app()
  
  
  if __name__ == '__main__':
      app.run()
  ```

- ④ 在`views`文件下开始写蓝图（招小弟处理事务了）
  
  ![1704187805774](E:\文档_Typora\关于怎么学会coding.assets\1704187805774.png)
  `bro1.py`的视图处理代码：

  ```python
  from flask import Blueprint
  
  xbro1 = Blueprint('bro1',__name__)
  
  # 创建新的视图的对应关系
  
  @xbro1.route('/f1')
  def f1():
      return 'f1'
  
  @xbro1.route('/f2')
  def f2():
      return 'f2'
  ```


  ​	`bro2.py`的视图处理代码也类似的编写。

  

  - ⑤ 到`__init__.py`文件中注册蓝图（让小弟们和主要的干线挂接关系），然后就完成蓝图的构建了

    ```python
    from flask import Flask
    
    # 这个导入可以提到代码首行去
    from .views.bro1 import xbro1
    from .views.bro2 import xbro2
    
    
    def create_app():
        app = Flask(__name__)
        app.secret_key = 'yangzhi823823'
    
        @app.route('/index')
        def index():
            return 'index'
    
        app.register_blueprint(xbro1)
        app.register_blueprint(xbro2)
        # 这个register_blueprint不但可以指定注册小弟，还可以加前缀，这种就分发路由或者说，姑且是前后端分离（doge）
        # app.register_blueprint(xbro1,url_prefix='/web')
        # app.register_blueprint(xbro2,url_prefix='/admin')
    
        return app
    
    
    ```

**补充一个蓝图的使用遗忘：**

在访问它的小弟时，不用加上大哥的前缀，比如我的主程序是`/index`。那么访问时候不用管这个老大，盯着`url_prefix`就好。

![1710127724612](E:\文档_Typora\1-关于怎么学会coding.assets\1710127724612.png)

```python
from flask import Flask

# 将蓝图注册到主程序上
from .views.axios1 import axios
def create_app():
    app = Flask(__name__)
    app.secret_key = 'yangzhi823823'

    @app.route('/index',methods=['GET','POST'])
    def index():
        return 'index'
	
    # 注册
    app.register_blueprint(axios,url_prefix='/admin')


    return app
```









### 2、由任务一—— excel表格的后台处理系统编写的展开

#### 2.1、关于静态资源的目录

>"./"：代表目前所在的目录
>
>"../"：代表上一层目录
>
>以"/"开头：代表根目录

![1704377640484](E:\文档_Typora\关于怎么学会coding.assets\1704377640484.png)





#### 2.2、关于flask框架的路由

我有个这种感觉，flask中，一切操作均是在操作路由。那么就要写好路由以及写好`render_template`。诸如：



```python
from flask import Blueprint,render_template

page_index_welcome = Blueprint('page_index_welcome',__name__)

@page_index_welcome.route('/index')
def def_pageIndex():
    return render_template('index_lay.html')

@page_index_welcome.route('/index/weblcome-1')
def def_pageWelcome1():
    return render_template('/page/welcome-1.html')

#############################下面是layuimini中指定页面路径的代码###############################
  "homeInfo": {
    "title": "首页",
    "href": "/index/weblcome-1"
  },

```



也就是，即使是交给框架托管，也要把路由写好。把框架中的页面返回给flask，然后才可以实现路径的响应。

而且这种交付过去的HTML页面，是嵌套在后端模板框架中的，诸如这个自己的写的书籍表CURD的THML页面。

![1704768394320](E:\文档_Typora\关于怎么学会coding.assets\1704768394320.png)





#### 2.3、关于操作数据库

- 操作数据库？那先建立数据库连接

  ```python
  db_book = pymysql.connect(host="localhost", user="root", password="123456", database="lib_book")
  cursor = db_book.cursor()
  ```

  

- 执行SQL语句执行查询，并且掉方法来获取查询结果

  ```python
    # 执行查询
      query = f"SELECT * FROM lib_book WHERE email='{email}' AND pwd='{pwd}'"
      cursor.execute(query)
      # 获取查询结果
      result = cursor.fetchone()
  ```

  

  

  

- 处理业务

- 关于细节
  注意到查询的结果是一个元组。后续假如要读取，要按照元组的格式进行读取数据。

  ```
  result= (4, 'John', 'Doe', 'john.doe@example.com', '1111')
  ```

  

- 

#### 2.4、关于IDE中的调试

![1705035813138](E:\文档_Typora\关于怎么学会coding.assets\1705035813138.png)

这里有几个按钮：

- 第一个是`step over`：其执行是将当前位置包含的函数，作为一个完整的对象进行执行，执行完后拿到执行结果，回到当前行。在不存在子函数的情况下是和step into效果一样的（简而言之，越过子函数，但子函数会执行） 
- 第二个是`step into`:这个应该是最为常用的，一行一行的执行，即是遇到子函数，也进到子函数中去逐行执行。
- 第三个是`step into my code`目前用的比较少
- 第三个是`step out`。要么是进入子函数之后，将当前位置之后的代码执行完毕，要么是没有子函数时，将断点后面的代码一并执行完
- 小总
  ![1705036133458](E:\文档_Typora\关于怎么学会coding.assets\1705036133458.png)

  





### 3、由数据库连接池展开

#### 3.1、最基础的版本

```python
from flask import Flask
import pymysql

# 创建Flask对象
app = Flask(__name__)
# 创建数据库连接对象
CONN = pymysql.connect(host='127.0.0.1',port=3306,user='root',password='123456',database='lib_book')

# 编写获取所有数据的函数
def def_fetchall(sql):
    # 创建游标对象
    cursor = CONN.cursor(cursor=pymysql.cursors.DictCursor)
    # 执行sql语句
    cursor.execute(sql)
    # 获取查询结果
    ret = cursor.fetchall()
    # 关闭游标对象，不关闭链接 —— 这种链接就不会重复创建，而是一直使用同一个链接。
    cursor.close()
    # 返回查询结果
    return ret


@app.route('/login')
def def_login():
    result = def_fetchall("select * from users")
    print(result)
    return 'xxx'


@app.route('/index')
def def_index():
    return 'xxx'


@app.route('/order')
def def_order():
    return 'xxx'

```

这种做法的问题在于，假如需要处理有并发能力的项目的时候，是无能为力的。

#### 3.2、在写原生SQL（即不用ORM）时候，使用数据库连接池去做

- 先安装好`dbutils`和`pymysql`

- 具体使用数据库连接池的代码编写

  ```python
  import pymysql
  from DBUtils.PooledDB import PooledDB
  
  # 创建数据库连接池
  POOL = PooledDB(
      creator=pymysql,  # 使用链接数据库的模块
      maxconnections=6,  # 连接池允许的最大连接数，0和None表示不限制连接数。注意这里说的是允许最大连接数，而不是当前连接数。 # 6个线程
      mincached=2,  # 初始化时，链接池中至少创建的空闲的链接，0表示不创建
      blocking=True,# 连接池中如果没有可用连接后，是否阻塞等待。True，等待；False，不等待然后报错
      #了解一个ping参数
      ping=0,# ping MySQL服务端，检查是否服务可用。
      host='127.0.0.1',
      port=3306,
      user='root',
      password='123456',
      database='lib_book',
      charset='utf8'
  )
  
  # 去数据库中获取一个链接
  conn = POOL.connection()
  # 创建游标对象，帮助执行SQL语句
  cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
  # 执行sql语句
  cursor.execute("select * from users")
  # 获取执行数据
  reslut = cursor.fetchall()
  # 关闭游标对象
  cursor.close()
  # 关闭链接 —— 实际是将链接放回到连接池中
  conn.close()
  # 打印结果
  print(reslut)
  ```

  倘若想要模拟多个链接线程进行测试

  ```python
  import pymysql
  from DBUtils.PooledDB import PooledDB
  from threading import Thread
  
  # 创建数据库连接池
  POOL = PooledDB(
      creator=pymysql,  # 使用链接数据库的模块
      maxconnections=6,  # 连接池允许的最大连接数，0和None表示不限制连接数。注意这里说的是允许最大连接数，而不是当前连接数。 # 6个线程
      mincached=2,  # 初始化时，链接池中至少创建的空闲的链接，0表示不创建
      blocking=True,# 连接池中如果没有可用连接后，是否阻塞等待。True，等待；False，不等待然后报错
      #了解一个ping参数
      ping=0,# ping MySQL服务端，检查是否服务可用。
      host='127.0.0.1',
      port=3306,
      user='root',
      password='123456',
      database='lib_book',
      charset='utf8'
  )
  
  def task(num):
      # 去数据库中获取一个链接
      conn = POOL.connection()
      # 创建游标对象，帮助执行SQL语句
      cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
      # 执行sql语句
      cursor.execute("select * from users")
      # 获取执行数据
      reslut = cursor.fetchall()
      # 关闭游标对象
      cursor.close()
      # 关闭链接 —— 实际是将链接放回到连接池中
      conn.close()
      # 打印结果
      print(num,'-------->',reslut)
  
  for i in range(10):
      t = Thread(target=task, args=(i,))
      t.start()
  ```

  

  

#### 3.3、基于函数实现sqlhelper

sqlhlper文件

```python
import pymysql
from DBUtils.PooledDB import PooledDB
from threading import Thread

# 创建数据库连接池
POOL = PooledDB(
    creator=pymysql,  # 使用链接数据库的模块
    maxconnections=6,  # 连接池允许的最大连接数，0和None表示不限制连接数。注意这里说的是允许最大连接数，而不是当前连接数。 # 6个线程
    mincached=2,  # 初始化时，链接池中至少创建的空闲的链接，0表示不创建
    blocking=True,# 连接池中如果没有可用连接后，是否阻塞等待。True，等待；False，不等待然后报错
    #了解一个ping参数
    ping=0,# ping MySQL服务端，检查是否服务可用。
    host='127.0.0.1',
    port=3306,
    user='root',
    password='123456',
    database='lib_book',
    charset='utf8'
)


def def_fetchall(sql,*args):
    '''
    获取所有数据
    :return: result
    '''
    # 去数据库中获取一个链接
    conn = POOL.connection()
    # 创建游标对象，帮助执行SQL语句
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    # 执行sql语句
    cursor.execute(sql,args)
    # 获取执行数据
    reslut = cursor.fetchall()
    # 关闭游标对象
    cursor.close()
    # 关闭链接 —— 实际是将链接放回到连接池中
    conn.close()
    # 返回结果
    return reslut

def def_fetchone(sql,*args):
    '''
    获取单条数据
    :return:
    '''
    # 去数据库中获取一个链接
    conn = POOL.connection()
    # 创建游标对象，帮助执行SQL语句
    cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
    # 执行sql语句
    cursor.execute(sql, args)
    # 获取执行的单条数据
    reslut = cursor.fetchone()
    # 关闭游标对象
    cursor.close()
    # 关闭链接 —— 实际是将链接放回到连接池中
    conn.close()
    # 返回结果
    return reslut
```

使用到sqlhelper的文件

```python
from flask import Flask
import sqlhelper

# 创建Flask对象
app = Flask(__name__)




@app.route('/login')
def def_login():
    # 我欠缺一个堆*args的通俗理解
    # 注意这里的sql语句中的%s，是sql语句中的占位符，后面的参数，会依次替换掉%s。故而不用放着引号引起来
    result = sqlhelper.def_fetchall("select * from users where email=%s and password=%s", "yangzhi@ex.com","3333")
    print(result) # 打印出结果：[{'id': 3, 'firstName': 'zhi', 'lastName': 'yang', 'email': 'yangzhi@ex.com', 'password': '3333'}]
    return 'xxx——login'


@app.route('/index')
def def_index():
    result = sqlhelper.def_fetchall("select * from users")
    print(result) # 输出结果：[{'id': 1, 'firstName': 'John', 'lastName': 'Doe', 'email': 'john.doe@example.com', 'password': '1111'}, {'id': 2, 'firstName': 'Jane', 'lastName': 'Doe', 'email': 'jane.doe@example.com', 'password': '2222'}, {'id': 3, 'firstName': 'zhi', 'lastName': 'yang', 'email': 'yangzhi@ex.com', 'password': '3333'}]

    return 'xxx——index'


@app.route('/order')
def def_order():
    return 'xxx——order'

if __name__ == '__main__':
    # 启动Flask程序
    app.run(debug=True)
```



#### 3.4、基于类实现sqlhelper

这里用了一个叫做单例模式的东西。但是我并不是特别理解单例模式。

```python
from sqlhelper import PooledDB
import pymysql
class SqlHelper(object):
    # 实例化
    '''
    实例化的过程只是执行一遍。
    那么连接池只有一个
    '''
    def __init__(self):
        # 创建连接池
        self.__pool = PooledDB(
            creator=pymysql,  # 使用链接数据库的模块
            maxconnections=6,  # 连接池允许的最大连接数，0和None表示不限制连接数。注意这里说的是允许最大连接数，而不是当前连接数。 # 6个线程
            mincached=2,  # 初始化时，链接池中至少创建的空闲的链接，0表示不创建
            blocking=True,  # 连接池中如果没有可用连接后，是否阻塞等待。True，等待；False，不等待然后报错
            # 了解一个ping参数
            ping=0,  # ping MySQL服务端，检查是否服务可用。
            host='127.0.0.1',
            port=3306,
            user='root',
            password='123456',
            database='lib_book',
            charset='utf8'
        )
    def  def_fetchall(self,sql,*args):
        '''
        获取所有数据
        :return: result
        '''
        # 去数据库中获取一个链接
        conn = self.__pool.connection()
        # 创建游标对象，帮助执行SQL语句
        cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
        # 执行sql语句
        cursor.execute(sql,args)
        # 获取执行数据
        reslut = cursor.fetchall()
        # 关闭游标对象
        cursor.close()
        # 关闭链接 —— 实际是将链接放回到连接池中
        conn.close()
        # 返回结果
        return reslut

    
    def  def_fetchone(self,sql,*args):
        '''
        获取所有数据
        :return: result
        '''
        # 去数据库中获取一个链接
        conn = self.__pool.connection()
        # 创建游标对象，帮助执行SQL语句
        cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
        # 执行sql语句
        cursor.execute(sql,args)
        # 获取执行数据
        reslut = cursor.fetchone()
        # 关闭游标对象
        cursor.close()
        # 关闭链接 —— 实际是将链接放回到连接池中
        conn.close()
        # 返回结果
        return reslut

# 创建对象
db = SqlHelper()

```

假如觉得上述代码仍然冗余，可以再将公共部分提取出来，减少冗余：

```python
from sqlhelper import PooledDB
import pymysql
class SqlHelper(object):
    # 实例化
    '''
    实例化的过程只是执行一遍。
    那么连接池只有一个
    '''
    def __init__(self):
        # 创建连接池
        self.__pool = PooledDB(
            creator=pymysql,  # 使用链接数据库的模块
            maxconnections=6,  # 连接池允许的最大连接数，0和None表示不限制连接数。注意这里说的是允许最大连接数，而不是当前连接数。 # 6个线程
            mincached=2,  # 初始化时，链接池中至少创建的空闲的链接，0表示不创建
            blocking=True,  # 连接池中如果没有可用连接后，是否阻塞等待。True，等待；False，不等待然后报错
            # 了解一个ping参数
            ping=0,  # ping MySQL服务端，检查是否服务可用。
            host='127.0.0.1',
            port=3306,
            user='root',
            password='123456',
            database='lib_book',
            charset='utf8'
        )


    def open(self):
        # 去数据库中获取一个链接
        conn = self.__pool.connection()
        # 创建游标对象，帮助执行SQL语句
        cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)
        return conn,cursor

    def close(self,conn,cursor):
        # 关闭游标对象
        cursor.close()
        # 关闭链接 —— 实际是将链接放回到连接池中
        conn.close()

    def  def_fetchall(self,sql,*args):
        '''
        获取所有数据
        :return: result
        '''
        conn,cursor = self.open()
        # 执行sql语句
        cursor.execute(sql,args)
        # 获取执行数据
        reslut = cursor.fetchall()
        self.close(conn,cursor)
        # 返回结果
        return reslut


    def  def_fetchone(self,sql,*args):
        '''
        获取单条数据
        :return: result
        '''
        conn, cursor = self.open()
        # 执行sql语句
        cursor.execute(sql, args)
        # 获取执行数据
        reslut = cursor.fetchone()
        self.close(conn, cursor)
        # 返回结果
        return reslut

# 创建对象
db = SqlHelper()

```





#### 3.5、单独知识点——关于with的上下文管理

在`with`后跟一个对象的时候，会`自动执行`这个对象的`__enter__`方法，`__enter__`方法返回什么，`f`就是什么，没有返回就是`None`。再而执行`with xxx as yyy: `中的代码，在内部代码执行完毕之后，就执行这个对象内部的`__exit__`方法

```python
class Foo(object):
    def __enter__(self):
        return 12345

    def __exit__(self, exc_type, exc_val, exc_tb):
        pass
# 创建对象
obj = Foo()
with obj as f:
    print(f)

```



### 4、关于flask整体性认识

#### 4.1、wsgi & 找源码相关 —— 【可以反复观看，最后要用的】

>这块我暂时不深入涉及，但是我需要知道我曾经是这种见过类似的看源码方式，最后我需要自己会用。
>**盯着返回值找**



#### 4.2、创建flask对象

- 静态文件

  >这是暂时对我而言，是对flask比较深入的一次认识。

  这是Flask对象点进去后的`__init__`函数的东西

  ```python
   def __init__(
          self,
          import_name: str,
          static_url_path: str | None = None,
          static_folder: str | os.PathLike | None = "static",
          static_host: str | None = None,
          host_matching: bool = False,
          subdomain_matching: bool = False,
          template_folder: str | os.PathLike | None = "templates",
          instance_path: str | None = None,
          instance_relative_config: bool = False,
          root_path: str | None = None,
      ):
  # 重点盯着static_folder、static_url_path、template_folder
  ```

  ![1707113853835](E:\文档_Typora\关于怎么学会coding.assets\1707113853835.png)

  - 认准url:

  ![1707113991636](E:\文档_Typora\关于怎么学会coding.assets\1707113991636.png)

  

  **一般而言是默认的。**

  ```python
  app = Flask(__name__,template_folder='templates',static_folder='static',static_url_path='/static')
  ```

  - 关于静态文件的使用的规范建议

    >相当于是托管给Flask的`url_for`来渲染为网页展示的方式

    

    ```python
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>首页</title>
    </head>
    <body>
        <h1 align="center" style="color: blueviolet">首页</h1>
    <!--    引入图片-->
        <img src="/static/1.jpg"/>
    <!--    关于静态文件的使用规范整顿-->
        <img src="{{url_for('static',filename='1.jpg')}}"/>
        
    </body>
    </html>
    
    '''
    这段HTML代码是在使用Flask框架的url_for函数来生成静态文件的URL。
    url_for函数的第一个参数是端点名，这里的'static'表示静态文件的端点。filename='1.jpg'是url_for函数的关键字参数，表示要获取的静态文件的文件名。  所以，{{url_for('static',filename='1.jpg')}}会被Flask渲染为静态文件1.jpg的URL。然后，这个URL会被插入到<img>标签的src属性中，从而在网页上显示这个图片。
    '''
    
    ```

    **这么做的目的是便于批量修改：也就是当`static_url_path`变化了。下面这种渲染的方式仍然可以工作，而写死的，就得逐个修改了（~~似乎可以批量修改~~）**

    > `filename`中是还可以再指定路径的。例如：
    >
    >  <img src="{{url_for('static',filename='/xx/yy/1.jpg')}}"/>

- 模板

#### 4.3、配置文件相关的

- **基于全局变量的** —— `localsetings`

  >flask加载配置文件最多的方式是如下：
  >
  >`app.config.from_object()`
  >
  >那么这行代码如何理解了？
  >
  >`app.config.from_object('settings')`
  >
  >也就是运行这个py文件，就会在这个py文件所在的目录下去找==settings==文件。
  >
  >`app.config.from_object('config.settings')`
  >
  >这个的意思就是去config目录下找settings.py文件。
  >
  >![1709302622090](E:\文档_Typora\1-关于怎么学会coding.assets\1709302622090.png)
  >
  >这种就把配置文件调用了。注意配置的信息一定要用`大写`。调用的时候，用键值对的方式来搞。
  >
  >![1709302733118](E:\文档_Typora\1-关于怎么学会coding.assets\1709302733118.png)
  >
  >应用领域主要是在搞`数据库链接`的时候。以后链接数据库就可以直接读配置。用于区分自己本地编写和扔到公司服务器上的配置信息。
  >
  >这种配置的玩法。也就普及出了大众对`settings`和`localsettings`来保证信息安全的做法
  >
  >![1709303433700](E:\文档_Typora\1-关于怎么学会coding.assets\1709303433700.png)
  >
  >

  

  

  

- **基于类的配置文件** 
  ![1709303887950](E:\文档_Typora\1-关于怎么学会coding.assets\1709303887950.png)

  flask中用基于类的多，Django中用基于全局的多。

  

- 待定



#### 4.4、路由系统

- **路由的应用【两种写法】：用装饰器（推荐）、也可用方法**

  >这里的核心应该是将url和函数名进行打包，放在Rule中，得到一个rule对象，再将rule对象放给map。

  **细节我没有听，假如确实需要，我再回来，我现在需要将东西磕磕碰碰的做出来。**了解原理，反正就两种写法。

  ```python
  # 第一种写法
  def index():
      return render_template('index.html')
  add.add_url_rule('/index','index',index) # 这几个参数分别是：url、endpoint、view_func
  
  # 第二个写法 —— 公司里一般用这种方式
  @app.route('/login')
  def login():
      return render_template('login.html')
  
  ```

  

- **路由加载的源码流程**

  >① 将url和函数打包成为rule对象
  >
  >② 将rule对象添加到map对象中
  >
  >③ 通过app.url_map可以获得map对象中的诸多rule对象

  

- **动态路由**

  ```python
  @app.route('/login')
  def login():
  	return render_template('login.html')
  
  # 动态路由中常用的两种类型
  @app.route('/login/<name>')
  def login(name):
  	print(type(name)) # 这里就是默认的字符串类型。这个动态的name可以作为参数扔到函数中
      return render_template('login.html')
  
  @app.route('/login/<int:name>')
  def login(name):
  	print(type(name)) # 此时就需要传入一个int类型的参数了，否则就会出现路由匹配不通过的问题。
      return render_template('login.html')
  
  ```

  其他的动态路由也是有的：

  ![1709365084098](E:\文档_Typora\1-关于怎么学会coding.assets\1709365084098.png)

  

#### 4.5、视图



- **FBV**
  我当前学习到的编写方式就是FBV

  ```python
  # 第一种写法
  def index():
      return render_template('index.html')
  add.add_url_rule('/index','index',index) # 这几个参数分别是：url、endpoint、view_func
  
  # 第二个写法 —— 公司里一般用这种方式
  @app.route('/login')
  def login():
      return render_template('login.html')
  
  ```

- **CBV**
  这里有个装饰器感觉不太能绕过来。

  当前的代码如下：

  ```python
  from flask import Flask,render_template,views
  
  # 创建Flask对象
  app = Flask(__name__)
  
  # 编写嵌套的测试函数1
  def test1(func):
      def inner(*args,**kwargs):
          print('before1')
          result =  func(*args,**kwargs)
          print('after1')
          return result
      return inner
  
  def test2(func):
      def inner(*args,**kwargs):
          print('before2')
          result = func(*args,**kwargs)
          print('after2')
          return result
      return inner
  
  # 创建一个UserView的类，继承自views.MethodViews
  class UserView(views.MethodView):
      # 在这里可以通过methods来实现请求方式的限制
      methods = ['GET','POST','PUT','DELETE']
  
      decorators = [test1,test2]
  
      '''
      在你的代码中，test1和test2装饰器会被应用到UserView类的所有HTTP方法（如get、post等）上。
      这意味着，无论何时有一个HTTP请求到达/user这个URL，test1和test2装饰器都会被执行。  
      具体来说，当一个HTTP请求到达时，首先会执行test2装饰器（因为它是列表中的最后一个装饰器,那就是倒着取列表中的信息），
      然后是test1装饰器，
      最后才是UserView类中对应的HTTP方法。
      故而输出结果是：
      before2
      before1
      进入get方法
      after1
      after2
      你可以把装饰器看作是一种AOP（面向切面编程）的实现方式，它可以在不修改原有代码的情况下，为类或函数添加新的功能。
      
      
      其作用：在每个装饰器中，你都可以添加一些预处理或后处理的逻辑，比如打印日志、检查用户权限等。
      '''
  
      def get(self):
          print('进入get方法')
          return 'get请求'
      def post(self):
          print('进入post方法')
          return 'post请求'
      def put(self):
          return 'put请求'
      def delete(self):
          return 'delete请求'
  
  '''
  在Flask框架中，as_view()方法用于将类视图转换为视图函数，
  它接受一个参数，这个参数是视图函数的名称。在这里，'user'就是视图函数的名称。  
  
  当你使用app.add_url_rule('/user',view_func=UserView.as_view('user'))这行代码时，
  你实际上是在添加一个URL规则，当用户访问/user这个URL时，
  Flask会调用UserView类的相应方法（如GET、POST等）来处理请求。  
  这里的'user'参数，就是给这个视图函数命名，这个名称可以用于URL反向解析，
  也就是通过视图函数的名称来找到对应的URL。例如，你可以使用url_for('user')来获取到/user这个URL。
  '''
  # 添加路由
  app.add_url_rule('/user',view_func=UserView.as_view('user')) # view_func=UserView.as_view('user')相当于视图函数
  
  
  if __name__ == '__main__':
  # 启动Flask程序
      app.run(debug=True)
  ```

  最难理解的是这两个装饰器，以及装饰器的运行逻辑从而导致的输出结果。

  **我们先来理解我的两个闭包函数。装饰器是闭包的一种特殊化。**

  ```python
  def test2(func):
      def inner(*args,**kwargs):
          print('before2')
          result = func(*args,**kwargs)
          print('after2')
          return result
      return inner
  ```

  - **首先，什么装饰器？**

    

    >装饰器也是函数，它是一个特殊的函数，`能够修改其他函数的行为（例如增加原本函数不具备的功能）`

    ```python
    # 先从我原本最简单的闭包函数再开始
    def outer(x):
        def inner(y):
            return x+y
        return inner
    print(outer(6)(5))
    ```

    这个例子很清晰，在没有闭包之前，outer函数只能接受一个参数x，可能也会对其进行一定的处理。但是终归是有限的。于是加入inner函数，这个inner函数有自己的参数y，同时，因为它是在outer函数中，outer的参数x，它也可以使用，==故而使得功能得以增加。==最后返回给inner函数给outer函数，也就是inner函数中处理后的东西给outer。

    

    

  - **其次，它内部的执行逻辑是什么样的了**我们清楚了上面这个例子后，我们看看我们的代码：
    test2函数中有个参数`func`。后续会使用它，看完后续我们就知道，这个func就是我们想要装饰（即增加功能）的函数。

    内部我们写了一个inner函数，这个函数的参数我们给得随意，这里是了解。它这个参数的意思是，这个函数接受任意数量的`位置参数`和`关键字参数`，用==(*args,**kwargs)==表示。

    那么在这个例子里，inner函数做了什么了？其实做的简单，只是在==调用func函数之前==和调用只有输出一些内容。这是这个例子的功能增加。假如用`@test2`的形式去装饰某函数，这个被装饰函数就成为一个参数扔到inner中处理。

    

  - **最后，那为什么那个输出结果了？**

    输出结果如下：

    ```python
        before2
        before1
        进入get方法
        after1
        after2
    ```

    因为`decorators = [test1,test2]`的执行有点类似于栈，把数据放入列表，然后倒着取出来。这行代码是写在get请求的上面，也就是当请求到/user这个URL的时候。由于使用的了装饰器，会先执行装饰器中的东西，也就是先执行test2，输出before2；然后执行test1，输出before1。==也许你想问为什么不是直接把test2中的执行完再去执行test1。而是再按照相反顺序执行后半部分==。这个我也暂时解决不了。

    

#### 4.6、模板

##### 4.6.1、模板的基本用法

>目前感觉在传递参数的时候很好用。
>
>**使用起来很像python。比如这个列表，直接按照python中获取列表信息的方式就可以获得相应信息。**

```python
<body>
    <h1>{{nums[0]}}</h1>
</body>
</html>

######################下面是python代码，上面是部分HTML的#######################

from flask import Flask,render_template

# 创建Flask对象
app = Flask(__name__)

# 编写首页路由
@app.route('/md')
def index():
    nums = [11,22,33]
    return render_template('md.html',nums=nums)

if __name__ == '__main__':
# 启动Flask程序
    app.run(debug=True)
```

>**同样也可以使用模板的继承**

何谓继承，也就是我们编写一个HTML文件，其中写好相应的骨架：

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>模板继承的实例</title>
</head>
<body>
    <h1>头</h1>
    {%block content%} {%endblock%}
    <h1>底</h1>
</body>
</html>
```

在我们准备继承的HTML文件中，我们按照继承的模板编写好，然后在`block content`中编写内容。然后其中的内容就会传递到编写的模板中的{%block content%}与{%endblock%}之间。

```html
<!--<!DOCTYPE html>-->
<!--<html lang="en">-->
<!--<head>-->
<!--    <meta charset="UTF-8">-->
<!--    <title>模板基本用法</title>-->
<!--</head>-->
<!--<body>-->
<!--    <h1>{{nums[0]}}</h1>-->
<!--</body>-->
<!--</html>-->
<!--使用模板之后，上面的就可以推翻重新写了。直接继承我们编写的模板文件-->
<!--这里的写法和Django的是一样的-->
{%extends 'layout.html'%}
{%block content%}
    <h1>{{nums[0]}}</h1>
    <h1>mddddd</h1>
    {%include 'form_include_test.html'%}
<!--传递函数来了-->
    {{f("汪汪汪")}}
{%endblock%}
```

其效果（暂时忽略include和传递函数）

![1709445596714](E:\文档_Typora\1-关于怎么学会coding.assets\1709445596714.png)

>**同样可以使用`include`引入一些结构组件**

诸如编写一个负责输入的form表单：

```haxe
<form>
    <input type="text">
    <input type="text">
    <input type="text">
    <input type="text">
    <input type="text">
</form>
```

然后在我们需要展示的页面中编写相应的引入代码：

```html
<!--<!DOCTYPE html>-->
<!--<html lang="en">-->
<!--<head>-->
<!--    <meta charset="UTF-8">-->
<!--    <title>模板基本用法</title>-->
<!--</head>-->
<!--<body>-->
<!--    <h1>{{nums[0]}}</h1>-->
<!--</body>-->
<!--</html>-->
<!--使用模板之后，上面的就可以推翻重新写了。直接继承我们编写的模板文件-->
<!--这里的写法和Django的是一样的-->
{%extends 'layout.html'%}
{%block content%}
    <h1>{{nums[0]}}</h1>
    <h1>mddddd</h1>
    {%include 'form_include_test.html'%}
<!--传递函数来了-->
<!--    {{f("汪汪汪")}}-->
{%endblock%}
```

就可以实现引入：

![1709445713792](E:\文档_Typora\1-关于怎么学会coding.assets\1709445713792.png)

>**同样也可以传递函数，这是一个不错的功能**

在`python`文件中编写好相应的函数：

```python
from flask import Flask,render_template

# 创建Flask对象
app = Flask(__name__)

# 传字典传元组是基本操作了，flask可以传入函数
def func(args):
    return "你好呀，"+args

# 编写首页路由
@app.route('/md')
def index():
    nums = [11,22,33]
    return render_template('md.html',nums=nums,f=func) # 注意这里是f=xxx

if __name__ == '__main__':
# 启动Flask程序
    app.run(debug=True)
```

然后就可以在传递过去的md.html文件中引入这个函数了

```html

{%extends 'layout.html'%}
{%block content%}
    <h1>{{nums[0]}}</h1>
    <h1>mddddd</h1>
    {%include 'form_include_test.html'%}
<!--传递函数来了-->
    {{f("汪汪汪")}}
{%endblock%}
```

最终效果：

![1709445906464](E:\文档_Typora\1-关于怎么学会coding.assets\1709445906464.png)

>**`拓展`—— 关于{%%}和{{}}的使用区别**

**这两行代码都是使用了 Flask 的模板引擎 Jinja2 的语法。** 
{%include 'form_include_test.html'%}：==这行代码使用了 {% %} 格式，这是 Jinja2 的语句语法==。include 是一个指令，它的作用是将指定的模板文件（在这里是 'form_include_test.html'）插入到当前位置。`这种语法通常用于执行某些操作，如包含其他模板、设置变量、控制流等。`

  

{{f("汪汪汪")}}：==这行代码使用了 {{ }} 格式，这是 Jinja2 的表达式语法==。`它的作用是输出一个值，这个值可以是一个变量或者是一个函数的返回值`。在这里，f 是一个函数，"汪汪汪" 是传递给这个函数的参数，{{f("汪汪汪")}} 会被替换为函数 f 对参数 "汪汪汪" 调用的结果



##### 4.6.2、定义全局模板方法

>**为什么要用这个？**
>
>我们上面指出了可以引入函数，但是倘若有100个函数都需要引入同一个函数，对每个都进行传入实在有点子呆。因此使用`装饰器`来增加原本普普通通的函数，让它变成全局，使得我们能够不再手动录入。



用两个装饰器可以实现，异曲同工，只是调用的方式不同

**@app.template_global()**

****

```python
from flask import Flask,render_template

# 创建Flask对象
app = Flask(__name__)

@app.template_global() # 这个装饰器是全局的，可以在所有的模板中使用
# 调用方式: {{func("汪汪汪")}}
def func(args):
    return "海狗子是"+args


# 编写首页路由
@app.route('/md/hg')
def index():
    nums = [11,22,33]
    return render_template('md_hg.html',nums=nums)

if __name__ == '__main__':
# 启动Flask程序
    app.run(debug=True)
```

HTML中的代码

```html
<!--定义全局模板方法-->
{%extends 'layout.html'%}
{%block content%}
    <h1>{{nums[0]}}</h1>
    <h1>海狗子来咯</h1>
    {%include 'form_include_test.html'%}
<!--传递函数来了-->
    {{func("汪汪汪")}}
{%endblock%}
```

输出效果：

![1709447344325](E:\文档_Typora\1-关于怎么学会coding.assets\1709447344325.png)



**或者@app.template_filter()**

****

```python
from flask import Flask,render_template

# 创建Flask对象
app = Flask(__name__)

@app.template_global() # 这个装饰器是全局的，可以在所有的模板中使用
# 调用方式: {{func("汪汪汪")}}
def func(args):
    return "海狗子是"+args

@app.template_filter() # 这个装饰器是过滤器的，可以在所有的模板中使用
# 调用方法：{{"汪汪汪"|x1("小白")}}
def x1(args,name):
    return "海狗子2号"+args+name

# 编写首页路由
@app.route('/md/hg')
def index():
    nums = [11,22,33]
    return render_template('md_hg.html',nums=nums)

if __name__ == '__main__':
# 启动Flask程序
    app.run(debug=True)
```



HTML 中调用方式也要更改：

```html
<!--定义全局模板方法-->
{%extends 'layout.html'%}
{%block content%}
    <h1>{{nums[0]}}</h1>
    <h1>海狗子来咯</h1>
    {%include 'form_include_test.html'%}
<!--传递函数来了-->
    {{func("汪汪汪")}}
    <br>
    {{"汪汪汪"|x1("小白")}}
{%endblock%}
```



输出效果：

![1709447577119](E:\文档_Typora\1-关于怎么学会coding.assets\1709447577119.png)

>唯一需要注意的是，在蓝图注册的时候，这个全局只能在当前蓝图中全局。app肯定是整个都可以用，但是：
>
>比如蓝图是@bro1.template_global（）。那么就只能服务于bro1这个蓝图。





#### 4.7、特殊装饰器 

**————同Django中间件**

>**主要是通过：`@app.before_request`和`@app.after_request`**完成在请求之前和请求后的工作。
>
>这里有个返回值的问题需要特别注意：
>
>结论是：**before_request不能放返回值，但是after_request必须接受一个响应参数进去，并且返回这个响应**
>
>因为请求进来，先执行的是before_request，before_request这里没有返回值，然后执行视图函数，这里通过render_template会有一个返回值，最后页面要展示，就是展示的这个返回值，故而最后在after_request之后，这个返回一个响应response。
>
>此时执行结果：
>
>```
>f1函数被调用
>进入index函数
>f10函数被调用
>
>```
>
>
>
>即，最后的展示要一个返回，在before_request放返回值，满足页面需要的返回要求了，就不会返回后续的页面了。
>此时执行结果：
>
>```
>f1函数被调用
>f10函数被调用
>```
>
>



```
from flask import Flask,render_template

# 创建Flask对象
app = Flask(__name__)

@app.before_request
def f1():
    print('f1函数被调用')
    return '提前截胡'

@app.after_request
def f10(response):
    print('f10函数被调用')
    return response

# 编写首页路由
@app.route('/index')
def index():
    print('进入index函数')
    return render_template('index_special.html')

if __name__ == '__main__':
# 启动Flask程序
    app.run(debug=True)
```



>**假如有多个before_request和多个after_request了？**

```python
from flask import Flask,render_template

# 创建Flask对象
app = Flask(__name__)

@app.before_request
def f1():
    print('f1函数被调用')
    # return '提前截胡'

@app.before_request
def f2():
    print('f2函数被调用')
    # return '提前截胡'


@app.after_request
def f10(response):
    print('f10函数被调用')
    return response

@app.after_request
def f20(response):
    print('f20函数被调用')
    return response

# 编写首页路由
@app.route('/index')
def index():
    print('进入index函数')
    return render_template('index_special.html')

if __name__ == '__main__':
# 启动Flask程序
    app.run(debug=True)
```

执行结果知道就好。暂时不深入扒：

```
f1函数被调用
f2函数被调用
进入index函数
f20函数被调用
f10函数被调用
# 正着取before_request。倒着取after_request
```



>**关于蓝图的作用域问题**：
>
>before_request和after_request只能作用于本蓝图的视图呀、路由呀。



```python
from flask import  Blueprint

# 注册蓝图
x = Blueprint('x',__name__)

# 它们都是只能作用于@x下的相关作用域
@x.before_request
def f1():
    print('进入f1了')
    
@x.app_template_global
def func(args):
    return '哇呜哇呜,'+args   

@x.route('/index')
def index():
    return 'xxx'


@x.route('/index2')
def index2():
    return 'xxx2'

@x.route('/index3')
def index3():
    return 'xxx3'
```







#### 4.8 装饰器的小细节

咱们使用`@app.after_request`其实也就是把装饰器下面的函数放到`after_request`中取执行了【可以从源码看出来】，同样，我们可以手动给他放到`after_request`中，本质就是模拟源码的意思。



```pyhton
from flask import Flask,render_template

# 创建Flask对象
app = Flask(__name__)

@app.before_request
def f1():
    print('f1函数被调用')
    # return '提前截胡'

# 也可以手动加载函数进入装饰器

def hand_fun():
    print("手动加入")

app.before_request(hand_fun)


# 编写首页路由
@app.route('/index')
def index():
    print('进入index函数')
    return render_template('index_special.html')

if __name__ == '__main__':
# 启动Flask程序
    app.run(debug=True)
```



输出结果：

```
f1函数被调用
手动加入
进入index函数
```





>**截止此处，flask基础部分完成。**
>
>



#### 4.9、threading.local的运用

##### 4.9.1、基本的线程知识

现在倘若有一个变量num被甲乙丙丁都进行操作。

甲将其修改为0，乙将其修改为10，丙将其修改为20，丁将其修改为30。

最后输出结果是多少了？是按照最后一位修改的丁的数值而展示。

```python
import threading
import time

class Foo(object):
    # 初始化函数
    def __init__(self):
        self.nums = 999

# 创建对象
val = Foo()

# 创建完成线程任务的函数
def task(i):
    val.nums = i * 10
    time.sleep(1)
    print(val.nums)

for i in range(4):
    t = threading.Thread(target=task,args=(i,))
    t.start()
```

输出结果：

30
30
30
30



>**倘若使用threading.local。将会在内部通过线程ID为每一个线程开辟独立的空间，它们之间彼此不受其他线程的干扰。**



```python
import threading
import time

'''

class Foo(object):
    # 初始化函数
    def __init__(self):
        self.nums = 999

# 创建对象
val = Foo()
'''

# 同样创建对象
val = threading.local()

# 创建完成线程任务的函数
def task(i):
    val.nums = i
    time.sleep(1)
    print(val.nums)

for i in range(4):
    t = threading.Thread(target=task,args=(i,))
    t.start()
```

输出结果：

3
0
2
1

其运行逻辑是：当每一个线程执行val.xx = yyy时，会在内部为这个线程开辟一个空间，来存储这个val.xx。val.xx再到自己的线程内存地址去存储和操作xx。故而能够实现独立。





>**后面的内容是源码分析。我先跳过，后面再回来补吧，目前我需要做出东西出来。**





### 5、前端部分

#### 5.1、Vue初体验

和layui有点大同小异的感觉。都是交接页面出去托管了。但是layui有一个较为成熟的模板了哎

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vue的尝鲜</title>
<!--    step1:引入vue.js文件。直接使用本地引入的方式-->
    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>

</head>
<body>
<!--step2:指定区域，该区域的内容希望使用vue.js来接管-->

    <div id="app">
        <h1>Vue的入门测试</h1>
        <div>我的名字是{{name}}，微信号是{{wechat}}</div>

        <input type="button" value="请点击我" v-on:click="clickMe">
    </div>

</body>
<script>
    //step3:创建vue实例,并关联指定HTML区域
    var app = new Vue({
        el: '#app', //关联的区域
        data: {     //数据
            name: '张三',
            wechat: 'zhangsan'
        },
        methods: {
            clickMe: function () {
                // alert('你点击了我');
                this.name = '李四';
                this.wechat = 'lisi555'
            }
        }
    });
</script>
</html>
```





#### 5.2、Vue常见指令（也可以说是语法）

##### 1、插值表达式

>**`一般在显示文本内容的标签中使用 —— {{}}`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>插值表达式</title>
<!--    1、先引入vue.js-->
    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>

</head>
<body>
<!--    2、指定需要vue.js托管的区域-->
    <div id="app">
        <div>我的名字是{{name}},我喜欢{{hobby}},我的邮箱是{{dataInfo.email}}</div>
        <ul>
<!--            直接暴力填充字符串进去-->
            <li>{{'杨枝'}}</li>
<!--            字符串的拼接-->
            <li>{{'杨枝'+"甘露"}}</li>
<!--            调用data中的信息参与运算-->
            <li>{{base+1+1}}</li>
<!--            运算符搞运算-->
            <li>{{base === 1?"杨枝":"甘露"}}</li>
        </ul>
<!--        ul换一个-->
        <ul>
            <li>{{condition?"李白":"林清"}}</li>
        </ul>
        <input type="button" value="点击我" v-on:click="clickMe">
    </div>

</body>
<script>
    var app = new Vue({
        el: '#app',
        //data中的数据，可以在插值表达式中直接使用
        data: {
            name: '杨枝',
            hobby: '甘露',
            dataInfo: {
                email: 'yangzhi595753',
                phone: '123456789'
            },
            base: 1,
            condition: true
        },
        methods: {
            clickMe: function () {
                this.name = '汪汪汪';
                this.hobby = '大骨头';
                this.dataInfo.email = 'wangwangwang3327';
                this.dataInfo.phone = '987654321';
                this.base += 100;
                this.condition = !this.condition;
            }
        }
    }); //创建vue实例。也就是，这里整体而言是创建一个对象var app = new Vue();只是通过{}的方式再传入数据信息
</script>
</html>
```



##### 2、v-bind指令

>**一般对标签中的属性进行操作，操作什么了？让一些原本是定下来的东西使用变量表示，也就动起来了。那么我写一个修改变量的方法，这些变量数据一修改，整个页面就动态了。**

**先对单个值进行操作**

—— 下面的例子将img元素的`src`和`class`两个属性绑定到Vue实例的imageUrl和cls数据属性上。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-bind相关</title>
<!--    1、先引入vue.js-->
    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
    <div id="app">
        <img src="staitc/2-饮品.jpg" class="c1"/>

        <img alt="" v-bind:src="imageUrl" v-bind:class="cls">
    </div>

</body>
<script>
    //3、创建vue实例
    var app = new Vue({
        el: '#app',
        data: {
            imageUrl:'https://pic.imgdb.cn/item/65e9601a9f345e8d0396bbe0.jpg',
            cls:'igg'
        },
    });
</script>
</html>
```



—— 也可以绑定多个

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-bind相关</title>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<!--2、挂载需要vue托管的部分-->
    <div id="app">
        <img src="staitc/2-饮品.jpg" class="c1"/>

        <img alt="" v-bind:src="imageUrl" v-bind:class="cls">

<!--        这里就是绑定多个-->
        <h1 v-bind:class="{info: v1,danger: v2}">哇呜哇呜</h1>
        <h1 v-bind:class="clsDict">嗷呜嗷呜</h1>

<!--        注意一个是相当于传入字典，那么中间就用逗号分隔开-->
<!--        另个相当于传入独立的信息，也就是需要使用分号将不同的信息分隔开-->
        <h3 v-bind:style="{color:clr,fontSize:fs}">三号标题</h3>
        <h3 style="color: red;font-size: 19px">三号标题</h3>

        <input type="button" value="请点击我" v-on:click="clickMe">
    </div>

</body>
<script>
    //3、创建vue实例
    var app = new Vue({
        el: '#app',
        data: {
            imageUrl:'https://pic.imgdb.cn/item/65e9601a9f345e8d0396bbe0.jpg',
            cls:'igg',
            v1:true,
            v2:false,
            clsDict:{
                info_1:true,
                danger_1:false
            },
            clr:"red",
            fs:"19px"
        },
        methods:{
            clickMe:function () {
                this.imageUrl = 'https://pic.imgdb.cn/item/65e9601a9f345e8d0396bbe0.jpg';
                this.cls = 'igg';
                this.v1 = !this.v1;
                this.v2 = !this.v2;
                this.clsDict.info_1 = !this.clsDict.info_1;
                this.clsDict.danger_1 = !this.clsDict.danger_1;
                this.clr = "blue";
                this.fs = "25px";
            }
        }
    });
</script>
</html>
```



**v-bind的注意事项**

① 可以简写。简写格式是`:属性名=xxx`。

```html
<h1 v-bind:class="v1">
    标题一
</h1>
<h1 :class="v1">
    简写
</h1>
<img :src="xxx"/>
```



② v-bind是单项绑定。

也就是修改js中的东西可以影响到html中展示的内容，但是修改html中的，是不会影响到js中内容的

![1709812193596](E:\文档_Typora\1-关于怎么学会coding.assets\1709812193596.png)





##### 3、v-model指令

>**一般用于在交互的表中使用。例如：input、select、textarea等等。做的是`双向绑定`的事儿**

**用的登录展示一个实例：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-model相关内容</title>
<!--    1、引入vue.js文件-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<!--交代清楚需要vue接管的内容-->
<div id="app">
<!--    模拟登录的页面-->
    <div>
        用户名：<input type="text" v-model="user">
    </div>
    <div>
        密码：<input type="text" v-model="pwd">
    </div>

    <div>
        <input type="button" value="登录" v-on:click="login">
        <input type="button" value="重置" v-on:click="reSet">
    </div>
</div>

</body>
<script>
    //创建vue实例
    var app = new Vue({
        el: '#app',
        data: {
            user:"",
            pwd:"",
        },
        methods:{
            login:function () {
                console.log("用户名："+this.user+"密码："+this.pwd);
                alert("用户名："+this.user+"密码："+this.pwd);
            },
            reSet:function () {
                this.user = "";
                this.pwd = "";
            }
        }
    });
</script>
</html>
```



**更完整的实例：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-model相关内容</title>
<!--    1、引入vue.js文件-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<!--交代清楚需要vue接管的内容-->
<div id="app">
<!--    模拟登录的页面-->
    <div>
        用户名：<input type="text" v-model="user">
    </div>
    <div>
        密码：<input type="text" v-model="pwd">
    </div>
    <div>
        性别：
        <input type="radio" v-model="sex" value="1">男
        <input type="radio" v-model="sex" value="2">女

    </div>

    <div>
        爱好：
        <input type="checkbox" v-model="hobby" value="11">篮球
        <input type="checkbox" v-model="hobby" value="22">足球
        <input type="checkbox" v-model="hobby" value="33">排球
    </div>

    <div>
        城市：
        <select v-model="city">
            <option value="sz">深圳</option>
            <option value="gz">广州</option>
            <option value="bj">北京</option>
        </select>
    </div>

    <div>
        公司：
        <select v-model="company" multiple>
            <!--        技术，销售，运营可以多选-->
            <option value="js">技术</option>
            <option value="xs">销售</option>
            <option value="yy">运营</option>
        </select>
    </div>

    <div>
        其他：<textarea v-model="more"></textarea>
    </div>

    <div>
        <input type="button" value="注 册" v-on:click="clickMe">
    </div>
</div>

</body>
<script>
    //创建vue实例
    var app = new Vue({
        el: '#app',
        data: {
            //注意这里的数据都需要使用""引起来
            user:"",
            pwd:"",
            sex:"1",
            hobby:["22"],
            city:"sz",
            company:"xs",
            more:"..."
        },
        methods:{
            clickMe:function () {
                console.log("用户名："+this.user+"密码："+this.pwd+"性别："+this.sex+"爱好："+this.hobby+"城市："+this.city+"公司："+this.company+"其他："+this.more);
                alert("用户名："+this.user+"密码："+this.pwd+"性别："+this.sex+"爱好："+this.hobby+"城市："+this.city+"公司："+this.company+"其他："+this.more);
            },
        }
    });
</script>
</html>
```





##### 4、v-for指令

>**对用户数据进行循环展示**

下面通过五个实例来进行演示：

**示例一**：

单纯输出

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <h1>Vue的入门测试</h1>
    <div>
        <ul>
            <!--            v-for写在哪里，就对那个元素进行循环-->
            <li v-for="item in arr">{{item}}</li>
        </ul>
    </div>
</div>

</body>
<script>
    //实例化VUe
    var app = new Vue({
        el: '#app',
        data: {
            //定义一个数组
            arr: ['张三', '李四', '王五', '赵六']
        }
    });
</script>
</html>
```

输出结果：

![1709816658538](E:\文档_Typora\1-关于怎么学会coding.assets\1709816658538.png)

**示例二**：

输出数据并带下标

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <h1>Vue的入门测试</h1>
    <div>
        <ul>
<!--          其实不用管item和idx的顺序区别，交给Python考虑。读出来就行-->
            <li v-for="(item,idx) in arr">{{idx}} --> {{item}}</li>
            <li v-for="(idx,item) in arr">{{idx}} --> {{item}}</li>
        </ul>
    </div>
</div>

</body>
<script>
    //实例化VUe
    var app = new Vue({
        el: '#app',
        data: {
            //定义一个数组
            arr: ['张三', '李四', '王五', '赵六']
        }
    });
</script>
</html>
```



输出结果：

![1709816949757](E:\文档_Typora\1-关于怎么学会coding.assets\1709816949757.png)

**示例三：**

循环输出字典

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <h1>Vue的入门测试</h1>
    <div>
        <ul>
<!--            -->
            <li v-for="(key,value) in dataDict">{{key}} --> {{value}}</li>
            <li>颠倒一下获得字典的东西</li>
            <li v-for="(value,key) in dataDict">{{key}} --> {{value}}</li>
        </ul>
    </div>
</div>

</body>
<script>
    //实例化VUe
    var app = new Vue({
        el: '#app',
        data: {
            //定义一个字典
            dataDict: {
                id:1,
                name: '张三',
                age: 18,
            },
        }
    });
</script>
</html>
```



输出结果有趣了：

![1709817226174](E:\文档_Typora\1-关于怎么学会coding.assets\1709817226174.png)

`意思是，想要按照键值对的方式展示出来。要写成这种形式：(value,key)`。后续才能正常展示为键值对。然后列表那里的下标也是一个道理。得写成`(item,idx)`





**实例4：**

列表中嵌套字典。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <h1>Vue的入门测试</h1>
    <div>
        <ul>
            <!--            v-for写在哪里，就对那个元素进行循环-->
<!--            首先读出列表中的信息，再通过插值表达式读取字典中东西-->
            <li v-for="item in arr">id是：{{item.id}}；姓名是： {{item.name}}；年龄是： {{item.age}}</li>
<!--            也可以写成二重循环-->
            <li v-for="(item,idx) in arr">
<!--                读取内层信息-->
                <span v-for="(v,k) in item">键是{{k}} --> 值是{{v}}；</span>
            </li>
        </ul>
    </div>
</div>

</body>
<script>
    //实例化VUe
    var app = new Vue({
        el: '#app',
        data: {
            //列表中嵌套字典
            arr: [
                {id: 1, name: '张三', age: 18},
                {id: 2, name: '李四', age: 19},
                {id: 3, name: '王五', age: 20},
                {id: 4, name: '赵六', age: 21},
            ]
        }
    });
</script>
</html>
```



输出结果：

![1709818765883](E:\文档_Typora\1-关于怎么学会coding.assets\1709818765883.png)

整理一下，将循环输出的结果整理得漂亮一点。

整齐了：

![1709818851959](E:\文档_Typora\1-关于怎么学会coding.assets\1709818851959.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <h1>Vue的入门测试</h1>
    <div>
        <ul>
            <!--            v-for写在哪里，就对那个元素进行循环-->
<!--            首先读出列表中的信息，再通过插值表达式读取字典中东西-->
            <li v-for="item in arr">id是：{{item.id}}；name是： {{item.name}}；age是： {{item.age}}</li>
<!--            也可以写成二重循环-->
            <li v-for="(item,idx) in arr">
<!--                读取内层信息。item中有三个信息，故而每个内层循环中，span要输出三次-->
                <span v-for="(v,k) in item">{{k}}是：{{v}}；</span>
            </li>
        </ul>
    </div>
</div>

</body>
<script>
    //实例化VUe
    var app = new Vue({
        el: '#app',
        data: {
            //列表中嵌套字典
            arr: [
                {id: 1, name: '张三', age: 18},
                {id: 2, name: '李四', age: 19},
                {id: 3, name: '王五', age: 20},
                {id: 4, name: '赵六', age: 21},
            ]
        }
    });
</script>
</html>
```





##### 5、v-on指令

>**负责与事件有关的指令，例如：**
>
>v-on:click # 点击
>
>v-on:dblclick # 双击
>
>v-on:mouseover
>
>v-on:mouseout
>
>v-on:change
>
>v-on:focus
>
>...



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<div id="app">
    <ul>
        <li @click="clickMe">点击我</li>
        <li v-on:dblclick="dosomething('双击了我')">双击我</li>
        <li v-on:mouseover="dosomething('鼠标移入')" v-on:mouseout="dosomething('鼠标移开')">鼠标移入&鼠标移出</li>
    </ul>
</div>

</body>
<script>
    var app = new Vue({
        el: '#app',
        data: {
            //定义一个数组
            arr: ['张三', '李四', '王五', '赵六']
        },
        methods:{
            clickMe:function(){
                alert('你点击了我');
            },
            dosomething:function (msg) {
                console.log(msg)
                // alert(msg)
            }
        }
    });
</script>
</html>
```



可以将`v-on:`简写为`@`





##### 6、数据管理案例

>**数据的管理包括对数据的：展示、动态添加、删除、修改**

**数据列表展示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
    <style>
        .penal{
            background-color: #d9d9d9;
            border: 1px solid #dddddd;
            margin: 20px 0 0 0;
            padding: 10px;
            border-bottom: 0;
        }
        .table{
            width: 100%;
            border-collapse: collapse;
            border-spacing: 0;
        }

        /*一堆放在一起加一个样式*/
        .table > tbody >tr>td,
        .table > table >tr>th,
        .table > tfoot>tr>td,
        .table>tfoot>tr>th,
        .table > thead>tr>th
        .table > thead>tr>td{
            border: 1px solid #dddddd;
            padding: 8px;
            text-align: left;
            vertical-align: top;
        }
    </style>
</head>
<body>
<div id="app">
    <h3 class="penal">数据列表</h3>
    <table class="table">
        <thead>
            <td>姓名</td>
            <td>年龄</td>
        </thead>
        <tbody>
            <tr v-for="item in dataList">
                <td>{{item.name}}</td>
                <td>{{item.age}}</td>
            </tr>
        </tbody>
    </table>
</div>

</body>
<script>
    //实例化VUe
    var app = new Vue({
        el: '#app',
        data: {
            dataList: [
                {name: '张三', age: 18},
                {name: '李四', age: 19},
                {name: '王五', age: 20},
                {name: '赵六', age: 21},
            ]
        }
    });
</script>
</html>
```





**数据删除：**

传入参数进行删除

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
    <style>
        .penal{
            background-color: #d9d9d9;
            border: 1px solid #dddddd;
            margin: 20px 0 0 0;
            padding: 10px;
            border-bottom: 0;
        }
        .table{
            width: 100%;
            border-collapse: collapse;
            border-spacing: 0;
        }

        /*一堆放在一起加一个样式*/
        .table > tbody >tr>td,
        .table > table >tr>th,
        .table > tfoot>tr>td,
        .table>tfoot>tr>th,
        .table > thead>tr>th
        .table > thead>tr>td{
            border: 1px solid #dddddd;
            padding: 8px;
            text-align: left;
            vertical-align: top;
        }
    </style>
</head>
<body>
<div id="app">

    <h3 class="penal">表单区域</h3>
    <div>
<!--        通过v-model实现双向绑定了-->
        <label>姓名</label>
        <input type="text" v-model="user">
    </div>

    <div>
        <label>年龄</label>
        <input type="text" v-model="age">
        <input type="button" value="新建" v-on:click="addUser">
    </div>

    <h3 class="penal">数据列表</h3>
    <table class="table">
        <thead>
            <td>姓名</td>
            <td>年龄</td>
            <td>操作</td>
        </thead>
        <tbody>
            <tr v-for="(item,idx) in dataList">
                <td>{{item.name}}</td>
                <td>{{item.age}}</td>
                <td>
                    <input type="button" value="删除" @click="deleteRow(idx)">
                </td>
            </tr>
        </tbody>
    </table>
</div>

</body>
<script>
    //实例化VUe
    var app = new Vue({
        el: '#app',
        data: {
            user: "",
            age : "",
            dataList: [
                {name: '张三', age: 18},
                {name: '李四', age: 19},
                {name: '王五', age: 20},
                {name: '赵六', age: 21},
            ]
        },
        methods:{
            addUser:function () {
                // this.dataList.push({name:this.user,age:this.age});
                //也开始拆开写
                let obj = {name:this.user,age:this.age};
                this.dataList.push(obj)
                //重新清空输入区
                this.user = "";
                this.age = "";
            },
            //根据索引进行idx删除
            deleteRow:function (idx) {
                this.dataList.splice(idx,1) //从idx开始，删除一个数据
            }
        }
    });
</script>
</html>
```

拓展：

因为js会默认获得一个event的参数。我们可以从这里搞出一些花儿出来。

![1709825158626](E:\文档_Typora\1-关于怎么学会coding.assets\1709825158626.png)



```html
<td>
    <input type="button" value="删除" @click="deleteRow" v-bind:data-idxx="idx">
</td>
```

注意需要使用v-bind来绑定这个，`v-bind绑定的是属性，对某个属性进行绑定一个灵活的值`。我的idx是灵活的值，这个data-idxx是我自己写的属性，故而可以绑定在一起。这个idx写不写引号都不影响运行。

> 这里牵扯出HTML5和JavaScript对data-命名是有些区别的，在HTML5中。data-中不能出现大写的。但是JavaScript是接受大写的。故而，HTML5中的data-my-id在JavaScript中会被解析为驼峰式的data-myId。
> `为了保险，尽量上小写`

**编辑数据**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
    <style>
        .penal{
            background-color: #d9d9d9;
            border: 1px solid #dddddd;
            margin: 20px 0 0 0;
            padding: 10px;
            border-bottom: 0;
        }
        .table{
            width: 100%;
            border-collapse: collapse;
            border-spacing: 0;
        }

        /*一堆放在一起加一个样式*/
        .table > tbody >tr>td,
        .table > table >tr>th,
        .table > tfoot>tr>td,
        .table>tfoot>tr>th,
        .table > thead>tr>th
        .table > thead>tr>td{
            border: 1px solid #dddddd;
            padding: 8px;
            text-align: left;
            vertical-align: top;
        }
    </style>
</head>
<body>
<div id="app">

    <h3 class="penal">表单区域</h3>
    <div>
<!--        通过v-model实现双向绑定了-->
        <label>姓名</label>
        <input type="text" v-model="user">
    </div>

    <div>
        <label>年龄</label>
        <input type="text" v-model="age">
        <input type="button" :value="title" v-on:click="optionUser">

    </div>

    <h3 class="penal">数据列表</h3>
    <table class="table">
        <thead>
            <td>序号</td>
            <td>姓名</td>
            <td>年龄</td>
            <td>操作</td>
        </thead>
        <tbody>
<!--            <tr v-for="(item,idx) in dataList">-->
            <tr v-for="(item, idx) in dataList">
                <td>{{idx+1}}</td>
                <td>{{item.name}}</td>
                <td>{{item.age}}</td>
                <td>
<!--                    <input type="button" value="删除" @click="deleteRow(idx)" v-bind:data-myId="idx"/>-->
                    <input type="button" value="删除" @click="deleteRowFinal" v-bind:data-idxx="idx"/>
                    <input type="button" value="编辑" @click="editUser" v-bind:data-idxx="idx"/>
                </td>
            </tr>
        </tbody>
    </table>
</div>

</body>
<script>
    //实例化VUe
    var app = new Vue({
        el: '#app',
        data: {
            indexTag:undefined,
            user: "",
            age : "",
            title:"新建添加",
            dataList: [
                {name: '张三', age: 18},
                {name: '李四', age: 19},
                {name: '王五', age: 20},
                {name: '赵六', age: 21},
            ]
        },
        methods:{
            optionUser:function () {

                if (this.indexTag){
                    //编辑
                    this.dataList[this.indexTag].name = this.user;
                    this.dataList[this.indexTag].age = this.age;
                    this.title = "新建添加";

                }else {
                    //添加
                    // this.dataList.push({name:this.user,age:this.age});
                    //也开始拆开写
                    let obj = {name:this.user,age:this.age};
                    this.dataList.push(obj)
                }
                //无论是新建还是编辑，最后都要重新清空输入区
                this.user = "";
                this.age = "";
                this.indexTag = undefined;
            },
            //传入idx参数。根据索引进行idx删除
            // deleteRow:function (idx) {
            //     alert("数据展示"+idx+this.dataList[idx])
            //     //妖艳了，我都没有获取到idx。结果把信息删除了
            //     this.dataList.splice(idx,1) //从idx开始，删除一个数据
            // },
            //使用默认的event参数
            deleteRowTemp:function (event) {
                // this.dataList.splice(idx,1) //从idx开始，删除一个数据
                // console.log(event.srcElement.dataset.myId);
                // let idx = event.srcElement.dataset.myId
                //srcElement其实是被废止了，现在用target
                /*
                在你的代码中，
                你试图通过event.srcElement.dataset.myId
                和event.target.dataset.idx来获取索引值idx，
                但是这两个属性都是undefined。
                这是因为你在绑定数据时使用的是v-bind:data-myId="idx"，
                所以你应该使用event.target.dataset.myId来获取索引值
                * */
                let idx = event.currentTarget.dataset.idx
                this.dataList.splice(idx,1)
                alert("数据展示"+idx)
            },
            deleteRowFinal:function (event) {
                /*
                * 目前测试知道：我绑定的变量的名字修改，是不会影响到event抓数据。老老实实盯着data-xx来打就可以。只是要区分HTML的data-和JavaScript的data-的区别
                * 当我使用data-myId时，在下方使用dataset.myId就会输出数据展示NaN 当我使用data-my时候。在下方使用dataset-my就能够正常输出数据展示1。请问为什么
                * 这是因为HTML5的data-属性和JavaScript的dataset属性在处理属性名称时有一些特殊的规则。  在HTML5中，你可以使用任何data-后面跟着的名称作为自定义数据属性。这个名称可以包含任何小写字母，数字，或者破折号，但不能包含大写字母或者任何非ASCII字符。  然而，在JavaScript中，当你通过dataset属性访问这些自定义数据属性时，属性名称会被转换为驼峰式命名。这意味着所有的破折号都会被移除，破折号后面的第一个字母会被转换为大写。例如，data-my-id在JavaScript中会被转换为dataset.myId。  因此，当你在HTML中使用data-myId，你应该在JavaScript中使用dataset.myId来访问这个属性。但是，由于data-属性的名称不能包含大写字母，所以data-myId实际上是无效的。你应该使用data-my-id，然后在JavaScript中使用dataset.myId来访问这个属性。  同样，当你在HTML中使用data-my，你应该在JavaScript中使用dataset.my来访问这个属性。这是因为data-my和dataset.my都是有效的，并且它们的名称是匹配的。  总的来说，你需要确保你在HTML中使用的data-属性名称和你在JavaScript中使用的dataset属性名称是匹配的。你也需要确保你的data-属性名称只包含小写字母，数字，和破折号。
                * 以后都老老实实写小写吧
                * */
                console.log(event.currentTarget.dataset.idxx);
                let idx = parseInt(event.currentTarget.dataset.idxx)

                this.dataList.splice(idx,1)
                alert("数据展示"+idx)
            },
            editUser:function (event) {
                //点击编辑之后，需要将当前的数据填充到输入框中。至于数据的获取，可以使用类似python的解包，也可以逐个逐个的取
                // this.user = this.dataList[idx].name;
                // this.age = this.dataList[idx].age;
                //也可以写成
                let idxx = event.target.dataset.idxx
                // alert(idxx)
                //记得需要和得到的包中的数据名称一致
                let {name,age} = this.dataList[idxx];
                // alert(name+age)
                this.user = name;
                this.age = age;
                this.title = "编辑修改";
                this.indexTag = idxx;
            }
        }
    });
</script>
</html>
```





##### 7、v-if和v-else指令

>条件判断。这里和常规的
>
>```
>if
>if else
>else
>```
>
>的组合是相同的

目前不算卡顿了。这个文档这里的前端学完，也可以终止了。



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-bind相关</title>
<!--    1、先引入vue.js-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <h1>Vue的入门测试</h1>
    <div>
            <h1 v-if="v1">阿里无人区</h1>

            <h1 v-if="v2">去西藏</h1>
            <h1 v-else>去新疆</h1>

            <div v-if="v3 === '北京'">
                <h1>在天安门</h1>
            </div>
            <div v-else-if="v3 === '新疆'">
                <h1>在乌鲁木齐</h1>
            </div>

            <div v-else-if="v3 === '西藏'">
                <h1>在拉萨</h1>
            </div>

            <div v-else>
                <h1>在大理</h1>
            </div>

    </div>

</div>

</body>
<script>
    //3、创建vue实例
    var app = new Vue({
        el: '#app',
        data: {
            v1: true,
            v2: false,
            v3:'广州'
        },
        methods:{

        }
    });
</script>
</html>
```





##### 8、v-show指令

>v-show和v-if差不多，区别是，v-show中无论是不是true.都会渲染到页面。只是display与否的区别。然而v-if则得根据true与否来定是否要渲染

![1709866029029](E:\文档_Typora\1-关于怎么学会coding.assets\1709866029029.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-bind相关</title>
<!--    1、先引入vue.js-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <h1>Vue的入门测试</h1>
    <div>
            <h1 v-show="v1">阿里无人区</h1>
            <h1 v-show="!v1">去西藏</h1>

    </div>
</div>

</body>
<script>
    //3、创建vue实例
    var app = new Vue({
        el: '#app',
        data: {
            v1: true,
            v2: false,
            v3:'广州'
        },
        methods:{

        }
    });
</script>
</html>
```



##### 9、axios的简单认识

>他是一个HTTP库，在前后端分离中运用较多。可以发送HTTP请求

![1709866968807](E:\文档_Typora\1-关于怎么学会coding.assets\1709866968807.png)



##### 10、验证码和账号密码登录案例

先完成使用v-model完成双向绑定拿到信息

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-bind相关</title>
<!--    1、先引入vue.js-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <div>
        <input type="button" value="短信验证码登录" @click="isMsg=true">
        <input type="button" value="账 号密码登录" @click="isMsg=false">
<!--        默认展示账号密码登录-->
<!--        短信验证码-->
        <div v-show="isMsg">
            <p>
                <label>手机号</label>
<!--                当用户开始在输入框中输入内容时，placeholder的值会消失。如果输入框的内容被清空，placeholder的值会再次显示。-->
<!--                使用v-model完成双向绑定-->
                <input type="text" placeholder="手机号" v-model="msg.phone">

            </p>
            <p>
                <label>验证码</label>
                <input type="text" placeholder="请输入验证码" v-model="msg.code">
            </p>
        </div>

<!--        密码登录-->
        <div v-show="!isMsg">
            <p>
                <label>账号</label>
                <input type="text" placeholder="账号" v-model="info.username">

            </p>
            <p>
                <label>密码</label>
                <input type="password" placeholder="请输入密码" v-model="info.password">
            </p>
        </div>

        <input type="button" value="登录" @click="loginForm">

    </div>
</div>

</body>
<script>
    //3、创建vue实例
    var app = new Vue({
        el: '#app',
        data: {
            isMsg:false,
            //将账号密码以及手机号验证码等等信息双向绑定，存储的时候放在一包，后面方便取
            info:{
                username:"",
                password:""
            },
            msg:{
                phone:"",
                code:""
            }
        },
        methods:{
            loginForm:function () {
                //1、获取用户在其选择的模式下，输入的值
                //isMsg为真，则短信验证码登录，否则为账号密码
                let dataDict = this.isMsg?this.msg:this.info;
                //输出这个信息
                console.log(dataDict);
            }
        }
    });
</script>
</html>
```



再写axios校验

先附带一个Google调试的时候，使用顺序，以及怎么拿反馈

![1709869881453](E:\文档_Typora\1-关于怎么学会coding.assets\1709869881453.png)







最后的代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>v-bind相关</title>
<!--    1、先引入vue.js-->
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入axioscnd-->
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <div>
        <input type="button" value="短信验证码登录" @click="isMsg=true">
        <input type="button" value="账 号密码登录" @click="isMsg=false">
<!--        默认展示账号密码登录-->
<!--        短信验证码-->
        <div v-show="isMsg">
            <p>
                <label>手机号</label>
<!--                当用户开始在输入框中输入内容时，placeholder的值会消失。如果输入框的内容被清空，placeholder的值会再次显示。-->
<!--                使用v-model完成双向绑定-->
                <input type="text" placeholder="手机号" v-model="msg.phone">

            </p>
            <p>
                <label>验证码</label>
                <input type="text" placeholder="请输入验证码" v-model="msg.code">
            </p>
        </div>

<!--        密码登录-->
        <div v-show="!isMsg">
            <p>
                <label>账号</label>
                <input type="text" placeholder="账号" v-model="info.username">

            </p>
            <p>
                <label>密码</label>
                <input type="password" placeholder="请输入密码" v-model="info.password">
            </p>
        </div>

        <input type="button" value="登录" @click="loginForm">

    </div>
</div>

</body>
<script>
    //3、创建vue实例
    var app = new Vue({
        el: '#app',
        data: {
            isMsg:false,
            //将账号密码以及手机号验证码等等信息双向绑定，存储的时候放在一包，后面方便取
            info:{
                username:"",
                password:""
            },
            msg:{
                mobile:"",
                code:""
            }
        },
        methods:{
            loginForm:function () {
                //1、获取用户在其选择的模式下，输入的值
                //isMsg为真，则短信验证码登录，否则为账号密码
                let dataDict = this.isMsg?this.msg:this.info;
                //输出这个信息
                console.log(dataDict);

                //基于axios向某个地址发送请求
                //我理解为，直接将axios对象写在这里
                //使用账号密码的url:https://api.luffycity.com/api/v1/auth/password/login/?loginWay=password
                //遵循其Request payload的格式：{username: "13981562354", password: "1234321434"}
                //使用短信验证码的url:https://api.luffycity.com/api/v1/auth/mobile/login/?loginWay=mobile
                //遵循其Request payload的格式：{mobile: "13408975643", code: "321432"}
                //键值对格式要对应,名称也要对应
                let url;
                if(this.isMsg){
                    //走短信验证码登录
                    url="https://api.luffycity.com/api/v1/auth/mobile/login/?loginWay=mobile";
                }else{
                    //走账号密码的url
                    url="https://api.luffycity.com/api/v1/auth/password/login/?loginWay=password";
                }

                axios({
                    method:"post",
                    url:url,
                    data:dataDict,
                    headers:{
                        "Content-Type":"application/json"
                    },
                }).then(function (res) {
                    //res.data是返回的值
                    //console.log(res);
                    if(res.data.code === -1){
                        alert(res.data.msg);
                        return;
                    }else {
                        //正常登录成功就可以跳转了
                        window.location.href = "https://www.luffycity.com/"
                    }

                }).catch(function (error) {
                    console.log(error);
                })

            }
        }
    });
</script>
</html>
```



#### 5.3组件化开发

##### 5.3.1、局部组件

##### 5.3.2、全局组件

#### 6、vue-router组件















## End-关于提问以及解答



1、那么对于我这个项目而言，如何布置前台页面和后台页面的关系了？

>答：我零零散散的写吧。想看什么或者受到什么启发，就都写写。
>前台是上传用户的车辆数据文件，用户也可以下载一些格式化表格，暂时分析结果，前台只是给用户用，就像淘宝一样。
>
>后台主要是给公司用，用来干嘛呢，更替模型，修改一些UI界面，后台可以有一个审核用户提交的数据。



 2、我现在应该怎么学了？

>答：既然我搞清楚了前后台拿来干什么，我大节奏是实现这个前后台。为了实现前后台，我需要学习前后端的技术。



3、那么语言我应该有限制吗？

>答：对于完成毕设，你只能用python了。但是对于找工作，你还需要思考。



4、什么是前端、后端、前台、后台了？我需要前后台吗？

>台子给人看的，直接用的，没有编码；前端、后端是掉了内容，还有三个工程师的字省略了，也就是程序员用的技术。



5、那综合来看，我现在的主要任务是什么了？

>去github找一个前后端分离的web项目，什么语言都可以，硬怼，开始整。



6、虚拟机是用来干嘛的？它在开发中、模拟开发（学习）中的作用是什么了？

> —— 目前只是知道是一个模拟真实计算机的软件。



7、docker部署是什么东西了？



8、如何使用conda对python进行管理？

>答：下面我附了不错的链接



8、什么是WSGI？

>答：暂时知道名字：web服务网关接口。



9、GET、POST于开发中的区别是什么了？





10、常规HTML写一个form表单怎么写了？

>写好<form>标签，写好提交的method 和 提交的action就好



11、怎么集成不同的机器学习算法了？





12、我现在的主要矛盾是什么了？

>答：是把期中要的东西凑齐了，然后把期中划过去。因为我现在想要推翻重写是有难度的，也是大概率来不及的。那么我就围绕这个需要提交的表格，然后总结我未来要用到的东西，编上去。
>那么我现在就一个前后台编上去。VUE搭建前台 、 后台。
>不行，我现在就按照前后台不分离去做，先有交的，然后再自己改成前后台分离的。



13、上次的反馈是什么了？ —— 还需要解决的

>(1)、应该是自己上传数据信息之后，进行数据分析，并得到一个预测性的结果
>
>(2)、目前的机器学习有点老，需要融合和创新，不然体现不出工作量。
>
>(3)、于我自己而言，我需要区分出一个前后台。



14、我应该怎么将算法融入进来日常学习中了？权重应该放多少？方法应该是什么？





15、nnd，脱离到自己手上开始编码的时候，为什么这么难？









16、为什么浏览器检查出来的代码在原本的HTML代码中却又毫无踪影了？是因为layui框架的原因吗？

>比对起来，是中间红框中的代码对应浏览器中的代码：
>
>![1704771188191](E:\文档_Typora\关于怎么学会coding.assets\1704771188191.png)
>
>![1704771301630](E:\文档_Typora\关于怎么学会coding.assets\1704771301630.png)
>
>但是仍然没有懂为什么可以这种写，以及这块代码究竟是怎么搞出来的。



17、ORM工具：Object Relational Mapping(对象关系映射)具体是什么了？













## Reference——关于参考链接/文档/文章

Typora、Markdown笔记为文字添加颜色的快捷键设置_markdown 字体添加颜色快捷键-CSDN博客
https://blog.csdn.net/hshudoudou/article/details/126725897

什么是前端什么是后端？什么是前台后台_胖胖的小龙猫-华为云开发者联盟
https://huaweicloud.csdn.net/638f11f5dacf622b8df8e74b.html?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Eactivity-3-120709884-blog-130177207.235%5Ev40%5Epc_relevant_anti_t3_base&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Eactivity-3-120709884-blog-130177207.235%5Ev40%5Epc_relevant_anti_t3_base&utm_relevant_index=4

到底什么是前端、后端、后台啊？ - 知乎 —— 这篇不错，生动形象
https://www.zhihu.com/question/21923056

b1ackc4t/14Finger: 功能齐全的Web指纹识别和分享平台,基于vue3+django前后端分离的web架构，并集成了长亭出品的rad爬虫的功能，内置了一万多条互联网开源的指纹信息。 —— 感觉是一个比较顶的项目
https://github.com/b1ackc4t/14Finger

如何用Conda优雅的管理Python环境 | About_conda
https://ckfanzhe.github.io/About_conda/

imoyao/idealyard: 使用 Vue 和 Flask 搭建前后端分离的 RESTful 个人博客 —— 延展了关于flask的东西（七百多页的书，估计得伴随着走了） ———— 也是我主要需要部署和展开的了 ———— 但是似乎并不好部署。
https://github.com/imoyao/idealyard

Repository search results
https://github.com/search?q=%E5%89%8D%E5%90%8E%E7%AB%AF%E5%88%86%E7%A6%BB%20python&type=repositories

表格标签、tr、td、th、table_table tr td-CSDN博客 —— 表单扫盲
https://blog.csdn.net/QQQqq031110/article/details/126941375?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-5-126941375-blog-79400642.235^v40^pc_relevant_3m_sort_dl_base4&spm=1001.2101.3001.4242.4&utm_relevant_index=8

解决Pycharm挂代理后依旧插件下载慢_pycharm中文插件下载慢-CSDN博客 —— 处理插件搜索缓慢甚至搜索不出来
https://blog.csdn.net/qq_41620542/article/details/119465357

webstorm ctrl + 鼠标滚轮缩放字体_webstorm滚轮缩放后如何还原-CSDN博客
https://blog.csdn.net/qq_37338983/article/details/78674098#:~:text=%E6%89%93%E5%BC%80webstorm%2C%20File%2D%3Esetting,%E7%82%B9%E5%87%BBApply%E5%B0%B1%E5%8F%AF%E4%BB%A5%E4%BA%86%E3%80%82

pycharm配置anaconda环境时找不到python.exe_pycharm找不到anaconda的python-CSDN博客
https://blog.csdn.net/weixin_45413925/article/details/132838970?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-132838970-blog-134905816.235%5Ev40%5Epc_relevant_3m_sort_dl_base4&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-132838970-blog-134905816.235%5Ev40%5Epc_relevant_3m_sort_dl_base4&utm_relevant_index=2
![1704982739316](E:\文档_Typora\关于怎么学会coding.assets\1704982739316.png)

单步调试 step into/step out/step over 区别_stp into stpe over step out 的功能和区别-CSDN博客 
https://blog.csdn.net/huangfei711/article/details/51220382#:~:text=step,into%EF%BC%9A%E5%8D%95%E6%AD%A5%E6%89%A7%E8%A1%8C%EF%BC%8C%E9%81%87%E5%88%B0%E5%AD%90%E5%87%BD%E6%95%B0%E5%B0%B1%E8%BF%9B%E5%85%A5%E5%B9%B6%E4%B8%94%E7%BB%A7%E7%BB%AD%E5%8D%95%E6%AD%A5%E6%89%A7%E8%A1%8C%EF%BC%88%E7%AE%80%E8%80%8C%E8%A8%80%E4%B9%8B%EF%BC%8C%E8%BF%9B%E5%85%A5%E5%AD%90%E5%87%BD%E6%95%B0%EF%BC%89%EF%BC%9Bstep%20over%EF%BC%9A%E5%9C%A8%E5%8D%95%E6%AD%A5%E6%89%A7%E8%A1%8C%E6%97%B6%EF%BC%8C%E5%9C%A8%E5%87%BD%E6%95%B0%E5%86%85%E9%81%87%E5%88%B0%E5%AD%90%E5%87%BD%E6%95%B0%E6%97%B6%E4%B8%8D%E4%BC%9A%E8%BF%9B%E5%85%A5%E5%AD%90%E5%87%BD%E6%95%B0%E5%86%85%E5%8D%95%E6%AD%A5%E6%89%A7%E8%A1%8C%EF%BC%8C%E8%80%8C%E6%98%AF%E5%B0%86%E5%AD%90%E5%87%BD%E6%95%B0%E6%95%B4%E4%B8%AA%E6%89%A7%E8%A1%8C%E5%AE%8C%E5%86%8D%E5%81%9C%E6%AD%A2%EF%BC%8C%E4%B9%9F%E5%B0%B1%E6%98%AF%E6%8A%8A%E5%AD%90%E5%87%BD%E6%95%B0%E6%95%B4%E4%B8%AA%E4%BD%9C%E4%B8%BA%E4%B8%80%E6%AD%A5%E3%80%82

ModuleNotFoundError: No module named 'DBUtils' - 温泉镇谢步东 - 博客园 —— 关于安装默认的DButils了，但是用不了
https://www.cnblogs.com/fadedlemon/p/13794749.html



这个vue的教程挺完善的：

Vue.js 教程
https://learning.dcloud.io/#/?vid=1















## Thinking —— 关于犯错的反思

1、对于flask项目，我最容易犯错的一个点是忘记处理`return`的东西。从报错信息你可以读出是没有返回值，在我目前经验不足的情况下，排除缓慢一点。

2、对于flask项目在用的时候，一定是用路由，比如这种在框架里，仍然是找路由和函数来控制静态

![1705588527871](E:\文档_Typora\关于怎么学会coding.assets\1705588527871.png)

这种情况下，路由的链接是这种的：

![1705588683083](E:\文档_Typora\关于怎么学会coding.assets\1705588683083.png)

当按照规则调整好，就可以如下了：

![1705589224498](E:\文档_Typora\关于怎么学会coding.assets\1705589224498.png)

