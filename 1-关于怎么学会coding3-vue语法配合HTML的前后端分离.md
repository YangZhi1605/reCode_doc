> **`关于怎么学会Coding3`**

# Start



算是第一个较为系统的前后端分离的项目。感觉Java的SpringBoot在业务上似乎是真的有板有眼，那么我此时的Flask就显得有点子呆了。

按照目前的说法是，使用Bootstrap的CSS样式，使用Vue的JS。他自己用的SpringBoot作为后台。

# Body

## 一、基础页面的编写

### 1.1、先把生产环境搭建了

Vue.js和Axios的js可以通过cnd引入，也可以使用下载js的方式。

对于Bootstrap，也是同样的道理，可以直接把它的CSS下载下来，也可以使用cdn来引入。



```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD" crossorigin="anonymous">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-/mhDoLbDldZc3qpsJHpLogda//BVZbgYuw6kof4u2FrCedxOtgRZDTHgHUhOCVim" crossorigin="anonymous"></script>
```



### 1.2、去Bootstrap官网粘贴自己需要的东西，然后调整

#### 1.2.1、写导航

![1710296273021](E:\文档_Typora\1-关于怎么学会coding3.assets\1710296273021.png)

====>删除调整好的样子

![1710297622718](E:\文档_Typora\1-关于怎么学会coding3.assets\1710297622718.png)

#### 1.2.2、写中心布局

本次中心布局想要写一个表格来自展示用户信息

第4节 网格系统-Bootstrap中文网
https://www.bootstrap.cn/doc/read/197.html

**用栅格的时候小心，col是在row的基础上才可以用的**



> 同样先把最基础的，死的表格写出来。把样式确定好，再慢慢附带数据进去。

![1710308169217](E:\文档_Typora\1-关于怎么学会coding3.assets\1710308169217.png)

按键是用的Bootstrap的样式。



>在确定样式看得过去后，将Vue带进来，暂时也是假数据，后面要从后台拿。



```html
<tbody>
    <tr v-for="user in userList">
        <td>{{user.id}}</td>
        <td>{{user.name}}</td>
        <td>{{user.age}}</td>
        <td>{{user.salary}}</td>
        <td>{{user.phone}}</td>
        <td><button>删除</button> &nbsp;&nbsp;<button>修改</button></td>
    </tr>
</tbody>
```

>写另一半栅格



>最后效果

![1710313738254](E:\文档_Typora\1-关于怎么学会coding3.assets\1710313738254.png)

## 二、写后端接口



**其一是理解后端拿数据并反馈给前台的流程：**

![1710314778257](E:\文档_Typora\1-关于怎么学会coding3.assets\1710314778257.png)



**其二是理解在Vue中，在哪个环节进行数据的拿取**

![1710376571600](E:\文档_Typora\1-关于怎么学会coding3.assets\1710376571600.png)



**然后就是写数据接口了**



### 2.1、根据页面建立数据表

>**收获一：写sql语句仍然有点创建对象的感觉，只是这个对象是得依据基础的SQL规定来。new对象一般用的（）。然后在对象中写好各个参数信息，逗号分隔**



>**收获二：DOUBLE 类型需要两个参数，第一个参数是总的位数，第二个参数是小数点后的位数。**



```sql
CREATE TABLE IF NOT EXISTS t_user(
 id VARCHAR(20) PRIMARY KEY,
 name VARCHAR(40),
 age int(3),
 salary DOUBLE(7,2),
 phoneCode VARCHAR(11)
);
```



### 2.2、搭建SpringBoot环境

于我而言，就是导入包了。

**它引入的依赖是这些，那么迁移到flask上，我应该做什么。**

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
<!--mysg1-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.38</version>
</dependency>
<!--mybatis-->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.1.0</version>
</dependency>
<!--1 ombok-->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.8</version>
    <scope>provided</scope>
</dependency>
<！--dcud-->
    <dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.19</version>
</dependency>
```

>目前ai反馈的结果：

Flask：这是基础的web框架，类似于Spring Boot的web模块。
Flask-SQLAlchemy：这是一个SQLAlchemy的Flask扩展，可以提供类似于MyBatis的ORM功能。
Flask-Migrate：这是一个Alembic的Flask扩展，用于数据库迁移，类似于Spring Boot的flyway或liquibase。
PyMySQL：这是一个Python的MySQL客户端，类似于mysql-connector-java。
pytest：这是一个Python的测试框架，类似于Spring Boot的test模块。
Flask-Testing：这是一个Flask的测试扩展，可以和pytest一起使用。
python-decouple：这是一个用于配置管理的库，类似于Spring Boot的配置管理。
你可以使用pip来安装这些包，如下所示：

```python
pip install flask
pip install flask-sqlalchemy
pip install flask-migrate
pip install pymysql
pip install pytest
pip install flask-testing
pip install python-decouple
```



注意，Python没有直接的替代品来替代Lombok和Druid。Python的属性和setter/getter方法通常直接公开，不需要像Java那样使用Lombok来自动生成。对于Druid，Python的数据库连接池通常由SQLAlchemy或其他ORM库处理。



大致的模仿springboot的编码逻辑，现在运行出我的了：



![1710380892568](E:\文档_Typora\1-关于怎么学会coding3.assets\1710380892568.png)

**关于SQLAlchemy和ORM映射**

在 Flask 项目中，`SQLAlchemy 是一个常用的 ORM（对象关系映射）工具`，它可以让你用 Pythonic 的方式来操作数据库，而不需要写 SQL 语句。

在你的项目中，User 模型是 SQLAlchemy 的一个映射类，它对应了数据库中的 t_user 表。  

当你需要对 t_user 表进行操作时，你可以通过 User 模型来进行。例如，你可以创建一个新的用户、查询用户、更新用户信息或删除用户。以下是一些示例：  创建一个新的用户：

```python
new_user = User(id='001', name='Tom', age=20, salary=5000.00, phoneCode='12345678901')
db.session.add(new_user)
db.session.commit()
```



查询用户：

```python
user = User.query.filter_by(name='Tom').first()
```



更新用户信息：

```python
user = User.query.filter_by(name='Tom').first()
user.age = 21
db.session.commit()
```

删除用户：

```python
user = User.query.filter_by(name='Tom').first()
db.session.delete(user)
db.session.commit()
```

这些操作都是通过 SQLAlchemy 的 API 来完成的，你不需要直接编写 SQL 语句。这样可以提高代码的可读性和可维护性，同时也可以减少 SQL 注入的风险。



### 2.3、SpringBoot是去写实体类和创建关系映射



```java
package com.baizhi.entity;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import lombok.Tostring;
import lombok.experimental.Accessors;
@Data
@AllArgsConstructor
@NoArgsConstructor
@Tostring
@Accessors(chain=true)
    public class User
    private String id;
    private String name;
    private Integer age;
    private Double salary;
    private String pohonecode;
}
```

在 Flask 项目中，你也需要创建类似于 Springboot 中的实体类。在 Flask 中，这些类通常被称为模型（Models）。这些模型类代表了你的数据库表，并且每个实例都对应表中的一行。  在 Flask 中，你可以使用 SQLAlchemy 这个库来创建模型。以下是一个例子，它创建了一个名为 User 的模型，这个模型有 id、name、age、salary 和 phoneCode 这几个字段，这些字段对应了数据库中 t_user 表的列：

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class User(db.Model):
    __tablename__ = 't_user'
    id = db.Column(db.String(20), primary_key=True)
    name = db.Column(db.String(40))
    age = db.Column(db.Integer)
    salary = db.Column(db.Float)
    phoneCode = db.Column(db.String(11))
```



### 2.4、编写DAO接口

`UserDAO`

 ```java
import java.util.List;
public interface t
UserDAO{
    //查询所有
    List<User>findAll();
}
 ```



`其对应接口`

```xml
<DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.baighi.dao.UserDAO">
    <!--查询所有功能-->
    <select id="findAll"resultType="User">
    select id,name,age,salary,phoneCode
    from t user
    </select>
</mapper>
```



`于我而言：`

在 Flask 项目中，你可以使用 SQLAlchemy ORM 来实现类似的功能。在 SQLAlchemy 中，你可以直接在模型类中定义方法来实现数据的查询、插入、更新和删除。  例如，你可以在 User 模型中定义一个 find_all 方法来查询所有用户：

```python
class User(db.Model):
    __tablename__ = 't_user'
    id = db.Column(db.String(20), primary_key=True)
    name = db.Column(db.String(40))
    age = db.Column(db.Integer)
    salary = db.Column(db.Float)
    phoneCode = db.Column(db.String(11))

    @classmethod
    def find_all(cls):
        return cls.query.all()
```

在这个例子中，find_all 方法使用了 SQLAlchemy 的 query.all() 方法来查询所有用户。

你可以在需要查询所有用户的地方调用 User.find_all() 来获取所有用户。  

注意，这里的 find_all 方法是一个类方法，它直接作用于 User 类，而不是 User 的实例。

这是因为我们在查询所有用户时，并不需要一个具体的用户实例。  

在 Flask 中，你不需要像在 MyBatis 中那样编写 XML 文件来定义 SQL 语句。你可以直接在 Python 代码中使用 SQLAlchemy 的 API 来操作数据库。这样可以让你的代码更加 Pythonic，同时也可以避免 SQL 注入的风险

### 2.5、写测试类查看是否实现数据的获取

这是springboot的逻辑：

```java
import com.baizhi.dao.UserDAO;
import org.junit.Test;
import org.junit.runner.Runwith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
eSpringBootTest(classes VueApplication.class)
@Runwith(SpringRunner.class)
public class TestUserDAO
eAutowired
private UserDAo userDAO;
@Test
public void testFindAll(){
	userDAO.findAll().forEach(user -System.out.println("user ="user));
}
```

在 Flask 项目中，你可以使用 Python 的 unittest 模块来编写测试。

**以下是一个例子，它测试了 User.find_all 方法：** 

 首先，你需要创建一个测试文件，例如 test_user.py。

在这个文件中，你可以定义一个测试类，这个类应该继承自 unittest.TestCase。

在这个类中，你可以定义一个或多个测试方法，这些方法应该以 test_ 开头。  

在每个测试方法中，你可以使用 assert 语句来检查你的代码的行为是否符合预期。

例如，你可以检查 User.find_all 方法返回的用户列表是否包含预期的用户。

  在测试开始前，你可能需要设置一些测试环境，例如创建一个测试数据库。

你可以在 setUp 方法中完成这些设置。

在测试结束后，你可能需要清理测试环境，例如删除测试数据库。你可以在 tearDown 方法中完成这些清理工作。

```python
import unittest
from BootVueDemo import create_app
from BootVueDemo.utils.models import db, User

class TestUser(unittest.TestCase):
    def setUp(self):
        self.app = create_app()
        self.app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///:memory:'
        self.app.config['TESTING'] = True
        self.client = self.app.test_client()
        with self.app.app_context():
            db.create_all()

    def tearDown(self):
        with self.app.app_context():
            db.session.remove()
            db.drop_all()

    def test_find_all(self):
        with self.app.app_context():
            user1 = User(id='001', name='Tom', age=20, salary=5000.00, phoneCode='12345678901')
            user2 = User(id='002', name='Jerry', age=22, salary=6000.00, phoneCode='09876543210')
            db.session.add(user1)
            db.session.add(user2)
            db.session.commit()

            users = User.find_all()
            self.assertEqual(len(users), 2)
            self.assertEqual(users[0].name, 'Tom')
            self.assertEqual(users[1].name, 'Jerry')

if __name__ == '__main__':
    unittest.main()
```

在这个例子中，setUp 方法创建了一个测试数据库，并在这个数据库中创建了所有的表。

tearDown 方法删除了所有的表，并关闭了数据库会话。  

test_find_all 方法首先在数据库中创建了两个用户，然后调用 User.find_all 方法来获取所有用户，最后检查返回的用户列表是否包含了预期的用户。  

你可以通过运行 python -m unittest test_user 来运行这个测试。

****

>**对flask工程流程的一个系统提炼**



## 三、小总结

`慢慢一步一步的还是把那个看似毫无头绪，十分困难的问题解决了`

### 3.1、前端页面

> **前端没得什么说的，先设计出最死板的固态页面，然后再逐步逐步改为动态，交互的。**

### 3.2 后端代码

>**重心在后端**

```markdown
	我当前的逻辑顺序是：
	①根据页面信息建立数据表 
	②搭建基本的开发环境 
	③ 完成ORM映射
	④编写DAO层（即操作数据库）
	⑤测试
```



我最初的项目结构是这种的：

![1710397352956](E:\文档_Typora\1-关于怎么学会coding3.assets\1710397352956.png)



现在升级为这种结构：

![1710397308768](E:\文档_Typora\1-关于怎么学会coding3.assets\1710397308768.png)



可以发现，现在整个生态是更加健全了。



#### 3.2.1、数据操作相关

这里可以就去Navicat中编写SQL语句或者使用图形化界面，或者在python里写sql语句，再配合之前学的数据库连接池版本的sqlhelper也能够实现：

>sqlhelper的两种写法

**常规版本**

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



**基于类的写法**

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



#### 3.2.2、环境搭建相关

我最初截屏的时候，已经展示了到时候各个文件夹应该怎么命名，其中的作用。我现在从上到下，逐个说明一下每个为什么要这种写。

```pyth
pip install flask

pip install flask-sqlalchemy

pip install flask-migrate

pip install pymysql

pip install pytest

pip install flask-testing

pip install python-decouple


```





##### ①配置文件相关

配置文件中，按照类来加载，细节是注意区分开发版本的类和测试版本的类。至于其中的信息，按照变量赋值的方式走就可以了。这里是相当于springboot的配置文件的处理了，主要的是数据库的配置处理嘛，并使用`app.config.from_object()`方法来从你的配置文件中加载配置

```python

class Config:
    SQLALCHEMY_DATABASE_URI = 'mysql+pymysql://root:123456@localhost:3306/bootvue?charset=utf8mb4'
    SQLALCHEMY_TRACK_MODIFICATIONS = False
    SQLALCHEMY_ECHO = True
    SQLALCHEMY_POOL_SIZE = 5

# 后续需要加载配置文件的时候，直接加载这个类就可以了
# app.config.from_object(Config)

# 测试环境中使用sqlite数据库。并指定链接,此链接是sqlite内存操控时候暂时的链接
class TestConfig(Config):
    SQLALCHEMY_DATABASE_URI = 'sqlite:///:memory:'

```





'sqlite:///:memory:' 表示使用 SQLite 数据库，并且数据库是在内存中，而不是在硬盘上。这种设置通常用于测试环境，因为在内存中的数据库可以快速创建和销毁，而且不会留下任何文件。

sqlite:///:memory:' 是 SQLite 数据库的一个特殊连接字符串，它表示创建一个在内存中的临时数据库，而不是在硬盘上的持久化数据库。这个内存数据库在程序结束时会自动销毁，不需要手动创建或删除。  

当你在测试环境中使用 SQLAlchemy 的 create_all 方法时，会自动在这个内存数据库中创建所有定义的表和字段，这些表和字段的定义来自你的 SQLAlchemy 模型。因此，你不需要手动在 SQLite 数据库中创建与 MySQL 数据库相同的表和字段。





##### ② 资源文件夹相关

这里就放着一些自己编写过程中的sql语句之类的吧，为假如后面推到github上，有人能够找到这些资源指令。



##### ③ static静态文件夹

这里还是老老实实放一点图片之类的。



##### ④ templates文件夹

仍然赋值rend_template返回文件引擎时候的需要



##### ⑤ utils文件夹

这里是今天学的最多的地方。这里其实是springboot的编写实体类和写mybatis映射。

>**一、ORM映射**

**Flask-SQLAlchemy可以帮助定义数据库模型**

**在 Flask 项目中，SQLAlchemy 是一个常用的 ORM（对象关系映射）工具，它可以让你用 Pythonic 的方式来操作数据库，而不需要写 SQL 语句**。

例如，在项目中，User 模型是 SQLAlchemy 的一个映射类，它对应了数据库中的 t_user 表。  当你需要对 t_user 表进行操作时，你可以通过 User 模型来进行。比如可以进行创建一个新的用户、查询用户、更新用户信息或删除用户等操作。

`需要注意的是：`

在 SQLAlchemy 中，**模型类**的名称默认会被转换为小写，并用作数据库表的名称。

所以，如果模型类名为 User，那么 SQLAlchemy 默认会将其映射到名为 user 的数据库表。

  如果你想要映射到一个不同的表，例如 t_user，你可以在模型类中设置 `__tablename__ `属性来**指定表名**。例如：

```python
# db是SQLAlchemy对象。
db = SQLAlchemy()
class User(db.Model):
    __tablename__ = 't_user'
    id = db.Column(db.String(20), primary_key=True)
    name = db.Column(db.String(40))
    age = db.Column(db.Integer)
    salary = db.Column(db.Float)
    phoneCode = db.Column(db.String(11))
```

此时User 模型会被映射到 t_user 表，而不是默认的 user 表。

在这么完成了数据表的映射之后，就可以较为方便的操作数据库了，例如：

**增加用户：**

```python
# 创建一个User对象，并将信息放入
new_user = User(id='001', name='Tom', age=20, salary=5000.00, phoneCode='12345678901')
db.session.add(new_user)
db.session.commit()
```



**查询用户：**

```python
user = User.query.filter_by(name='Tom').first()
```



**更改用户信息：**

```python
user = User.query.filter_by(name='Tom').first()
user.age = 21
db.session.commit()
```

**删除信息：**

```python
user = User.query.filter_by(name='Tom').first()
db.session.delete(user)
db.session.commit()
```

也就是不用编写SQL语句了，借助SQLAlchemy的API来实现功能。



**通过模型(Models)代表和挂接我们的数据库，并且我们是通过SQLAlchemy库来创建对象，与数据表的映射也完成了，SQL语句则可以借助API，故而不用再像springboot那种写一个entiy的实体类和写mapper以及在mapper中写SQL语句了。**



至于这个模型，模型是按照类来划分的，类里面的变量按照数据库字段来取名。

比如我目前是user类， User 模型中定义我数据库表的字段。

每个字段都应该是 db.Column 类的一个实例，你需要指定字段的类型，如 db.String、db.Integer 等。

如果字段是表的主键，你需要将 primary_key 参数设置为 True。

例如，如果我的用户表有 id、username 和 email 三个字段，你可以这样定义 User 模型：

```py
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(64), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)
```





>**二、DAO和mapper.xml在flask中是否必要？**

在 Flask 项目中，你可以使用 SQLAlchemy ORM 来实现类似的功能。

**在 SQLAlchemy 中，重心落在操作模型类。**

`可以直接在模型类中定义方法来实现数据的查询、插入、更新和删除`，mapper.xml中也就是编写sql语句实现业务。  

例如，你可以==在 User 模型中定义一个 find_all 方法==来查询所有用户:

```python
class User(db.Model):
    __tablename__ = 't_user'
    id = db.Column(db.String(20), primary_key=True)
    name = db.Column(db.String(40))
    age = db.Column(db.Integer)
    salary = db.Column(db.Float)
    phoneCode = db.Column(db.String(11))

    # 模型中满足业务需要而编写方法
    @classmethod
    def find_all(cls):
        return cls.query.all()
```

find_all 方法==使用了 SQLAlchemy 的 query.all() 方法==来查询所有用户

`注意，这里的 find_all 方法是一个类方法，它直接作用于 User 类，而不是 User 的实例。这是因为我们在查询所有用户时，并不需要一个具体的用户实例。  `

即，

```markdown
	find_all 是一个类方法，这意味着它是绑定到类而不是实例的。
	当你调用 User.find_all() 时，你实际上是在调用 find_all 方法并将 User 类作为参数传递给 cls。  

cls 是一个常用的约定，代表当前的类（在这个例子中，就是 User 类）。这就是为什么你可以在 find_all 方法中使用 cls.query.all()，它实际上等同于 User.query.all()。 

	因此，你不需要显式地将 User 类传递给 find_all 方法，因为当你使用 User.find_all() 调用它时，Python 会自动做这件事。
```



在 Flask 中，你不需要像在 MyBatis 中那样编写 XML 文件来定义 SQL 语句。你可以直接在 Python 代码中使用 SQLAlchemy 的 API 来操作数据库。这样可以让你的代码更加 Pythonic，同时也可以避免 SQL 注入的风险。





##### ⑥ views视图类

这里我进行了一定未调整，所有视图都注册在这里，即全部用蓝图，然后都在`__init__.py`中去注册蓝图。



##### ⑦整个BootVueDemo文件夹中的`__init__.py`

这个文件就拿来创建flask对象，加载配置文件，加载secret_key等等信息，最后返回app对象，用来服务mange.py这个启动文件





##### ⑧ 测试文件夹

这里我出来思路是模仿上面，完成开一个文件夹放测试的py文件。

>**三、这是今天收获第二大的地方。**





**第一：如何实现测试**

```markdown
在 Flask 项目中，你可以使用 Python 的 unittest 模块来编写测试。
	以下是一个例子，它测试了 User.find_all 方法：  
首先，你需要创建一个测试文件，例如 test_user.py。在这个文件中，你可以定义一个测试类，这个类应该继承自 unittest.TestCase。
	在这个类中，你可以定义一个或多个测试方法，这些方法应该以 test_ 开头。  在每个测试方法中，你可以使用 assert 语句来检查你的代码的行为是否符合预期。例如，你可以检查 User.find_all 方法返回的用户列表是否包含预期的用户.
在测试开始前，你可能需要设置一些测试环境，例如创建一个测试数据库。你可以在 setUp 方法中完成这些设置。在测试结束后，你可能需要清理测试环境，例如删除测试数据库。你可以在 tearDown 方法中完成这些清理工作。
```



```python
import sys
import os
# 将 BootVueDemoTest 目录添加到 Python 的模块搜索路径中。你可以在 test_user.py 文件的顶部添加以下代码
# sys.path.append(os.path.dirname(os.path.abspath(__file__)))
# 你可以在 test_user.py 文件的顶部添加以下代码
sys.path.append(os.path.dirname(os.path.abspath(__file__)))
import unittest
# 导入BootvueDemo包中的create_app函数，该函数在__init__.py文件中
from BootVueDemo import create_app
# 导入SQLAlchemy的db对象和User模型
from BootVueDemo.utils.models import db, User



# 创建一个测试类，继承自 unittest.TestCase
class TestUser(unittest.TestCase):

    # 在setUp方法中设置测试环境
    def setUp(self):
        # 创建一个app对象
        self.app = create_app()
        # 加载测试类的配置文件，测试类中设置 Flask 应用的 SQLAlchemy 数据库连接 URI
        self.app.config.from_object('BootVueDemo.config.setting.TestConfig')
        self.app.config['TESTING'] = True
        self.client = self.app.test_client()
        with self.app.app_context():
            db.create_all()
            # 删除所有的用户记录
            db.session.query(User).delete()
            db.session.commit()

    # tearDown 方法中完成这些清理工作
    def tearDown(self):
        with self.app.app_context():
            db.session.remove()
            db.drop_all()

    # 测试查询所有用户
    def test_find_all(self):
        with self.app.app_context():
            # 创建两个User对象
            user1 = User(id='001', name='Tom', age=20, salary=5000.00, phoneCode='12345678901')
            user2 = User(id='002', name='Jerry', age=22, salary=6000.00, phoneCode='09876543210')
            # 将两个User对象添加到数据库
            db.session.add(user1)
            db.session.add(user2)
            # 提交
            db.session.commit()

            # 查询所有的User对象
            users = User.find_all()
            # 断言: assert 语句来检查你的代码的行为是否符合预期
            self.assertEqual(len(users), 2)
            self.assertEqual(users[0].name, 'Tom')
            self.assertEqual(users[1].name, 'Jerry')


if __name__ == '__main__':
    unittest.main()
```



其实主要是三个环节:

1、按照现在数据库（比如mysql数据库）的逻辑，在sqlite内存中创建一个同样结构的，用来测试。

2、有创建就有销毁

3、实际编写自己想测试的方法，注意以`test_`开头。





>**四、创建环节中的上下文环境是如何理解的？**

`with self.app.app_context() `这行代码创建了一个 Flask 应用的上下文环境。

在 Flask 中，上下文环境是一种**临时的全局环境**，它使得你可以在没有直接引用应用或请求的情况下访问应用或请求的特定数据。  

在这个上下文环境中，你可以访问和修改 Flask 应用的配置，处理请求，以及访问请求特定的变量等。

**这个上下文环境在 with 语句结束时自动销毁**。  

db.create_all() 这行代码在当前的 Flask 应用上下文环境中创建所有的数据库表。这个方法会查找所有的 SQLAlchemy 模型，并为每个模型在数据库中创建一个对应的表。这个方法通常在应用启动时调用，以确保所有的数据库表都已经创建。 

 所以，with self.app.app_context(): db.create_all() 这两行代码的作用是在 Flask 应用的上下文环境中创建所有的数据库表。



>**五、怎么启动测试？**

要么用pycharm中自主集成的功能：

![1710401204438](E:\文档_Typora\1-关于怎么学会coding3.assets\1710401204438.png)

要么，就在Terminal中使用`PyCharm 的 Terminal 中手动运行 python -m unittest E:\develops\workspace_pycharm4_dev\BootVueDemo\BootVueDemoTest\test_user.py`

即指定到需要启动的py文件。

或者使用将 BootVueDemo 目录添加到 Python 的模块搜索路径中。：

```python
import sys
import os

sys.path.append(os.path.dirname(os.path.dirname(os.path.abspath(__file__))))
```



个人建议老老实实用人家软件写好的。

![1710401542140](E:\文档_Typora\1-关于怎么学会coding3.assets\1710401542140.png)

##### ⑨ manage.py

最后这个启动文件，主要就启动和配置一下端口了。





>**小总结完成，即Springboot的DAO完成，继续后面的开发**

## 四、开发业务

业务对于java而言，主要是一个接口(例如：`UserService`)配合一个实现类(例如：`UserServiceImpl`)

比如此时有：

接口：

```java
import com.baizhi.entity.User;
import java.util.List;
public interface userservice{
    //查询所有用户
List<User>findall();
}

```



其对应的实现类：

```java
import java.util.List;
@Service
@Transactional//控制事务
public class UserServiceImpl implements UserService{
    @Autowired
    private UserDAO userDAO;
    @override
    @Transactional(propagation Propagation.SUPPORTS)
    public List<User>findAll(){
    return userDAO.findAll();
    }
}

```



```markdown
1、将 Spring Boot 的 Controller 层迁移到 Flask 的路由和视图函数。在 Flask 中，我们使用装饰器来定义路由，并将路由映射到视图函数。  
2、将 Spring Boot 的 Service 层迁移到 Flask 的业务逻辑层。在 Flask 中，我们通常会创建一个或多个 Python 模块来封装业务逻辑。  
3、将 Spring Boot 的 Repository 层迁移到 Flask 的模型层。在 Flask 中，我们使用 SQLAlchemy 或其他 ORM 工具来定义数据模型和数据库操作。  
4、将 Spring Boot 的 DTO 迁移到 Flask 的表单验证和序列化。在 Flask 中，我们可以使用 WTForms 来处理表单验证，使用 Marshmallow 或 similar 库来处理序列化。  
5、将 Spring Boot 的全局异常处理迁移到 Flask 的错误处理。在 Flask 中，我们可以使用 @app.errorhandler 装饰器来定义全局错误处理函数。  
6、将 Spring Boot 的 AOP 迁移到 Flask 的 before_request 和 after_request 钩子函数。在 Flask 中，我们可以使用这些钩子函数来实现类似于 AOP 的功能。  
7、将 Spring Boot 的配置文件迁移到 Flask 的配置对象。在 Flask 中，我们通常会创建一个 Python 模块来存储配置信息，然后使用 app.config.from_object 方法来加载配置。  
8、将 Spring Boot 的测试迁移到 Flask 的测试。在 Flask 中，我们可以使用 unittest 或 pytest 来编写测试。 
```



大多数Python开发者在处理这种情况时，可能会选择使用Python的动态特性和鸭子类型，而不是创建接口和实现类。

他们可能会直接创建一个类，并在其中实现所需的方法。例如，对于你提供的Java代码，Python版本可能如下

```python
from typing import List
from your_project.models import User

class UserService:
    def __init__(self, user_dao):
        self.user_dao = user_dao

    def find_all(self) -> List[User]:
        return self.user_dao.find_all()
```

在这个例子中，UserService 类有一个 find_all 方法，该方法调用了 user_dao 的 find_all 方法。**user_dao 可以是任何具有 find_all 方法的对象**，这就是所谓的鸭子类型：如果它走起路来像鸭子，叫起来也像鸭子，那么它就是鸭子。  

这种方式的优点是简单、灵活，你可以轻松地替换 user_dao，只要新的 user_dao 有 find_all 方法即可。

这在写测试时特别有用，你可以用模拟对象或存根替换 user_dao。  这种方式的缺点是，如果 user_dao 没有 find_all 方法，你只有在运行时才会发现错误。

而在Java中，如果你试图实现一个接口，但没有提供接口中所有的方法，编译器会在编译时给出错误。



而至于这个类：

大多数Python开发者可能会将这种服务类放在一个名为 services 或 business_logic 的目录下。

这个目录通常位于项目的根目录下，**与 models、views 或 controllers 等其他目录平级**。

这样做的目的是为了保持代码的组织结构清晰，使得其他开发者能够更容易地理解和维护代码



综合出我的版本是：

```python
from typing import List
# 导入模型
from BootVueDemo.utils.models import User
# from your_project.models import User

class UserService:
    def __init__(self, user_dao):
        self.user_dao = user_dao
    
    # 配合SQLAlchemy的User模型，实现查询所有用户的功能
    def find_all(self) -> List[User]:
        return self.user_dao.find_all()
```





## 五、控制器开发

java里面要写控制器了，也就是我这儿的视图函数。

> **基于前后端分离的系统，其通讯方式主要是`JSON方式`**



```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import java.util.List;
@RestController
eRequestMapping("user")
    public class UserController{
        @Autowired
        private UserService userService;
        //查询所有方法
        @GetMapping("findAll")
        public List<User>findAll(){
            List<User>users userservice.findAll();
            return users;
        }
    }

```





对于我来说：

**我需要导入上面写好的Blueprint 类和 UserService 类。**

然后，可以创建一个 Blueprint 对象，并定义一个路由和视图函数，专门来负责网页的控制。

在视图函数中，你可以创建一个 UserService 对象，并调用其 find_all 方法来获取所有的 User 对象。

==最后，你将这些 User 对象转换为 JSON 格式，并返回==

这里需要注意，因为获得的是User对象：

```python
print(users)
print([user.to_dict() for user in users])


```



直接输出User模型查询数据库后的输出结果：

> [<User 1>, <User 2>, <User 3>]

通过自己写的`to_dict（）`方法去转为字典，现在正常了。

> [
>
> {'id': '1', 'name': '旺旺旺', 'age': 18, 'salary': 5000.3, 'phoneCode': '13408421910'},
>
>  {'id': '2', 'name': '杨枝', 'age': 20, 'salary': 9000.78, 'phoneCode': '13456781290'}, 
>
> {'id': '3', 'name': '小黑', 'age': 34, 'salary': 3900.89, 'phoneCode': '19978562354'}
>
> ]



**最后去写视图函数，即控制层**





>**Tips:关于JSON和python字典的再区分**

Flask 的 jsonify 函数可以将 Python 字典转换为 JSON 格式的数据。

这个函数不仅可以处理字典，还可以处理其他可以被转换为 JSON 格式的 Python 数据类型，如列表、元组等。例如：

```python
from flask import jsonify

data = {
    "name": "John",
    "age": 30,
    "city": "New York"
}

json_data = jsonify(data)
```



```markdown
	Python的字典和JSON格式的数据确实都是键值对的格式，但它们有一些重要的区别：  

数据类型：Python字典是Python的内置数据类型，而JSON是一种数据交换格式，它是一种纯文本格式，独立于任何语言。  

语法：Python字典的键和值可以是Python的任何数据类型，而JSON的键必须是字符串，值可以是字符串、数字、数组（类似于Python的列表）、另一个JSON对象、布尔值或null。  

使用场景：Python字典主要用于在Python程序内部存储和操作数据，而JSON主要用于在网络上传输数据，或者在不同的编程语言之间交换数据。  

可读性：Python字典在打印时会保留其结构，而JSON数据通常会被打印为单行字符串。  

转换：Python提供了json模块，可以使用json.dumps()函数将字典转换为JSON字符串，使用json.loads()函数将JSON字符串转换为字典。
```



关于本次的代码：

```python
	print(users)
    print([user.to_dict() for user in users])
    # return jsonify(users)
    print(jsonify([user.to_dict() for user in users]))
    return jsonify([user.to_dict() for user in users])

```



>`[user.to_dict() for user in users]`：这是一个列表推导式，它遍历 users 列表中的每个 User 对象，并调用每个对象的 to_dict 方法。这将每个 User 对象转换为一个字典，然后将这些字典放入一个新的列表中。  
>`jsonify([user.to_dict() for user in users])`：然后，jsonify 函数将这个列表转换为 JSON 格式的数据。  
>所以，这行代码的作用是将 users 列表中的每个 User 对象转换为字典，然后将这些字典放入一个列表中，最后将这个列表转换为 JSON 格式的数据。



当然，我直接输出`print(jsonify([user.to_dict() for user in users]))`得到的是一个响应`<Response 371 bytes [200 OK]>`



jsonify 函数的返回值是一个 Response 对象，而不是 JSON 格式的字符串。

这是因为 jsonify 不仅将数据转换为 JSON 格式，还创建了一个 Response 对象，该对象包含了 HTTP 响应的所有信息，如状态码、头部信息等。  

当你打印 Response 对象时，你看到的是其字符串表示形式，而不是其包含的 JSON 数据。

如果你想查看 Response 对象的 JSON 数据，你可以使用 get_json 方法：

```python
print(users)
print([user.to_dict() for user in users])
response = jsonify([user.to_dict() for user in users])
print(response.get_json())
return jsonify([user.to_dict() for user in users])
```

从输出结果来看，确实没有区别：

==[<User 1>, <User 2>, <User 3>]==
==[{'id': '1', 'name': '旺旺旺', 'age': 18, 'salary': 5000.3, 'phoneCode': '13408421910'}, {'id': '2', 'name': '杨枝', 'age': 20, 'salary': 9000.78, 'phoneCode': '13456781290'}, {'id': '3', 'name': '小黑', 'age': 34, 'salary': 3900.89, 'phoneCode': '19978562354'}]==
==[{'age': 18, 'id': '1', 'name': '旺旺旺', 'phoneCode': '13408421910', 'salary': 5000.3}, {'age': 20, 'id': '2', 'name': '杨枝', 'phoneCode': '13456781290', 'salary': 9000.78}, {'age': 34, 'id': '3', 'name': '小黑', 'phoneCode': '19978562354', 'salary': 3900.89}]==
json长相和字典确实像，只是确实不是一个东西。





## 六、前后端交互测试

加入跨域之后，通过`axios`发送请求。可以得到一个结果：

```
Array(3) [ {…}, {…}, {…} ]

0: Object { age: 18, id: "1", name: "旺旺旺", … }

1: Object { age: 20, id: "2", name: "杨枝", … }

2: Object { age: 34, id: "3", name: "小黑", … }
```

可以看到，得到的是一个数组。

>**到目前为止，第一版流程就这种执行完毕，先在实现其他功能。**





## 七、添加信息的功能

一样先把前台的信息交给`Vue`来管理。

数据？交给`v-model`实现双向绑定。怎么绑定？通过一个对象来绑定。

事件？交给`Vue`的方法和`axios`实现。

这里从前台写到后台，因为我们是前台数据要存储到后台嘛，先确定我们把信息绑定好了。



>**关于信息绑定**

是的，可以使用一个对象来承接这个数据。这个慢慢过渡出来。

其次，被默认事件教训了。主要就是这个刷新的动作，很奇怪，自己的控制台输出也不能输出信息。然后copilot指导说是`未阻止默认行为`

```markdown
 	另外，你的"提交"按钮的类型是submit，这意味着当你点击这个按钮时，表单会尝试提交。如果你没有阻止这个默认行为，页面会刷新，这可能会导致你的console.log(this.user);在页面刷新之前无法执行。
你可以尝试修改你的"提交"按钮的点击事件，添加.prevent修饰符来阻止表单的默认提交行为。这样，当你点击"提交"按钮时，页面就不会刷新，console.log(this.user);就可以正常执行了。
当然，我暴力一点，按钮就是按钮，类型直接改成button
```



```html
<div class="form-group">
    <div class="col-sm-offset-2 col-sm-10">
        <button type="button" class="btn btn-danger" v-on:click="saveUserInfo">提交</button>
        <button type="button" class="btn btn-default">重置</button>
    </div>
</div>
```

**此时控制台就能正常打印东西出来了**

![1710432979339](E:\文档_Typora\1-关于怎么学会coding3.assets\1710432979339.png)



**去使用axios向后端接口发送POST请求**

**现在去完成后端接口**

从我的DAO模型——>业务服务层——>视图函数控制层

dao模型和业务服务层都蛮好写的，重心在这个控制层的逻辑梳理：

```java
//保存用户方法
@PostMapping("save")
public Map<string,Object>save(@RequestBody User user){
    Map<String,object>map new HashMap<>();
    try{
        userservice.save(user);
        map.put("success",true);
    }catch (Exception e){
        map.put("success",false);
        map.put("message","用户保存失败！")：
    }
    return map;
}

```

可以看到，在java中，是将对接口进行请求的request处理为一个RequestBody了，然后其类型是User的。

在 Flask 中，可以使用 `request 对象`来获取请求体中的 JSON 数据，然后使用这些数据来创建一个新的 User 对象，后续传递给服务层和DAO层。你可以使用 try/except 语句来处理可能出现的异常，并在异常发生时返回一个包含错误信息的响应。



```python
from flask import request, jsonify

@user_controller.route('/save', methods=['POST'])
def save():
    response = {}
    try:
        # 获取请求体中的 JSON 数据
        data = request.get_json()
        # 使用这些数据来创建一个新的 User 对象
        user = User(id=data['id'], name=data['name'], age=data['age'], salary=data['salary'], phoneCode=data['phoneCode'])
        # 调用 UserService 的 save 方法来保存用户
        userService.save(user)
        response['success'] = True
    except Exception as e:
        response['success'] = False
        response['message'] = '用户保存失败！'
    return jsonify(response)
```





## 八、删除信息功能

先到Vue中去写对应事件函数，前端写好，然后去开发对应的后端接口。

也是模型——>service——>视图



## 九、修改信息功能

一样的，先到前台把事假函数写好，然后直接请求后端接口，再去开发后端接口。

后端接口开发完毕：能够查询到指定ID的数据

![1710487985398](E:\文档_Typora\1-关于怎么学会coding3.assets\1710487985398.png)



将查询到的信息添加到表单中。因为Vue双向绑定的机制，我们在表单中进行修改之后，那么，user对象的数据其实已经改了，现在需要更新这个id在数据表中的信息。



现在去完成后端接口，在这个视频中，接口还是之前保存信息的接口，之前加了if判断，判断id是否为空。id为空，说明数据库中没有，那么就进行保存新用户信息。id不为空，则进行更新操作。

我就写成两个不同的接口吧。





## 十、对姓名或者电话号码进行模糊查询

这里有一个动态SQL的学习，不知道python中有没有，但是本质都是模糊查询，只是将都输入，只是输入单个的情况进行动态的区分：

![1710493557344](E:\文档_Typora\1-关于怎么学会coding3.assets\1710493557344.png)



顺序一样的，先把前端的事件，需要的接口写好。然后再去后端写拿数据的接口，



前端这里有个链接通过`&`拼接，新接触。

```js
axios.get('http://127.0.0.1:5200/admin/findByNameOrPhone?name='+this.searchName+'&phoneCode='+this.searchPhone).then(function (response) {
                    console.log(response.data);
                    //将查询到的用户信息赋值给userList对象,vue的数据绑定会自动更新页面
                    _this.userList = response.data;
                }).catch(function (error) {
                    console.log(error);
                });
```

上面的动态SQL可以留意一下，以及这里最后是完成了需求

整个流程，从静态页面的设计到让静态页面活起来，再通过后端工程师开发的与数据库交互的接口来进行数据的交互。

于python而言，就是model层到service层，再到视图函数层。











# Question









# Reference

下载 Bootstrap · Bootstrap v5 中文文档 v5.3 | Bootstrap 中文网
https://v5.bootcss.com/docs/getting-started/download/