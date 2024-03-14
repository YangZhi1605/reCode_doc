# 关于怎么学会coding2

## Start

>**好事是清晰的内容更多了，当然，也有坏事，需要内化的，需要实际动刀的也更多了**









## Body

### 一、关于接口文档

仍旧是区分两个东西，后台和后端。后台是我们写好的，看得见摸得着的了，而后端则是形容某些实现后台的技术。按照那个up展示的效果，那么我的编写，**应该是从后端开始写，确定好接口，然后写前端。先展示，再调优，调整漂亮**



因此，在目前清晰了vue的一些语法后。准备进军接口文档这块的编写，这儿确定好，那么整个毕设的衔接几乎是没有问题了。

>**此处目前是没有搞定的**



### 二、关于前端开发之脚手架开发和组件

![1709888425850](E:\文档_Typora\1-关于怎么学会coding2.assets\1709888425850.png)
![宏观操作](https://github.com/YangZhi1605/reCode_doc/blob/main/1-%E5%85%B3%E4%BA%8E%E6%80%8E%E4%B9%88%E5%AD%A6%E4%BC%9Acoding2.assets/1709888425850.png?raw=true)



#### Vue深化

##### 1、Vue引言

![1709890047887](E:\文档_Typora\1-关于怎么学会coding2.assets\1709890047887.png)

##### 2、Vue入门

>**宏观来看，和我昨天学的差不多，选择性记忆笔记。**



###### 2.1、下载vue

###### 2.2、Vue的第一个例子

>**新的收获是：插值表达式中是可以调用函数，搞运算符的；**
>
>**vue推荐用id选择器进行绑定，其他的也是可以的**



![1709891121679](E:\文档_Typora\1-关于怎么学会coding2.assets\1709891121679.png)



**关于v-text**

![1709891563998](E:\文档_Typora\1-关于怎么学会coding2.assets\1709891563998.png)

注意覆盖原有数据的事儿，现在用插值表达式较多了。但是网络较差的时候，推荐使用v-text



**关于v-html**

![1709891739429](E:\文档_Typora\1-关于怎么学会coding2.assets\1709891739429.png)

**`tips`:这位老师讲一个板块互动一个板块这儿感觉挺好的（于我而言）。让课堂有节奏感和清晰，并且有交互**



**关于v-on，事件绑定**

>**这里之前自己是学过的**

- v-on的基本使用方式：

![1709900568490](E:\文档_Typora\1-关于怎么学会coding2.assets\1709900568490.png)

- v-on的简化写法 —— 用`@`来简化

- vue事件函数的两种写法
  ![1709901248986](E:\文档_Typora\1-关于怎么学会coding2.assets\1709901248986.png)

  

- vue事件的参数传递
  ![1709901419769](E:\文档_Typora\1-关于怎么学会coding2.assets\1709901419769.png)



**v-show和v-if和v-bind**

![1710115543135](E:\文档_Typora\1-关于怎么学会coding2.assets\1710115543135.png)





**v-for**

>**对对象进行遍历**



`拓展：`

关于自定义模板：

![1710115850818](E:\文档_Typora\1-关于怎么学会coding2.assets\1710115850818.png)





```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>${NAME}$</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">

</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<script>
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods:{},
        components:{},
    });
</script>
</html>
```



![1710116395486](E:\文档_Typora\1-关于怎么学会coding2.assets\1710116395486.png)



![1710117945247](E:\文档_Typora\1-关于怎么学会coding2.assets\1710117945247.png)

![1710118107483](E:\文档_Typora\1-关于怎么学会coding2.assets\1710118107483.png)

———— 源自Vue官方文档

**v-model双向绑定**

![1710118189866](E:\文档_Typora\1-关于怎么学会coding2.assets\1710118189866.png)

![1710118417160](E:\文档_Typora\1-关于怎么学会coding2.assets\1710118417160.png)

这个MVVM架构是Vue特有的











#####  3、巩固性的小案例

>**主要完成一个对页面中的记事本实现增删改查等基础操作**



###### 3.1、先写基础的固态页面后再逐个的动态化

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>11-记事本案例$</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <input type="text" v-model="msg"> <input type="button" value="添加到记事本" v-on:click="addInfo">
    <br>
    <ul>
        <li v-for="(item,index) in lists">
<!--            先使用href="javascript:;"阻止超链接默认的行为-->
            {{index+1}}{{item}} <a href="javascript:;" @click="delInfo(index)">删除</a>
        </li>

    </ul>
    <br>
    <span>当前总数据量：{{lists.length}}条</span> <input type="button" v-show="lists.length != 0" value="删除所有" @click="delAll">
</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<script>
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {
            lists:["吃饭","睡觉","混日子"],
            msg:"",
        },
        methods: {
            addInfo:function () {
                this.lists.push(this.msg);
                this.msg="";
            },
            //根据传递的索引值删除对应的数据
            delInfo:function (index) {
                this.lists.splice(index,1);
            },
            //删除所有数据，即将lists数组清空
            delAll:function () {
                this.lists=[];
            }
        },
        components: {},
    });
</script>
</html>
```





##### 4、事件修饰符

事件处理 — Vue.js官方文档
https://v2.cn.vuejs.org/v2/guide/events.html#%E4%BA%8B%E4%BB%B6%E4%BF%AE%E9%A5%B0%E7%AC%A6

![1710121116613](E:\文档_Typora\1-关于怎么学会coding2.assets\1710121116613.png)



**.stop事件修饰符:主要用于阻止事件冒泡**

vue中是这种执行逻辑，事件倘若内层外层都有，当触发了内层事件后，会向外层去冒泡着执行。

诸如：

![1710121773091](E:\文档_Typora\1-关于怎么学会coding2.assets\1710121773091.png)



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>12-事件修饰符</title>
    <style>
        .aa{
            background: aquamarine;
            height: 300px;
            width: 600px;
        }
    </style>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <div class="aa" @click="divClick">
<!--        用.stop阻止向外的冒泡-->
        <input type="button" value="这是一个十分可爱的按钮" @click.stop="btnClick">
    </div>
</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<script>
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {
            btnClick(){
               alert('按钮被点击了');
            },
            divClick(){
                alert('div被点击了');
            }
        },
        components: {},
    });
</script>
</html>
```



在使用`.stop`后，就不会出现这种了：

![1710121837894](E:\文档_Typora\1-关于怎么学会coding2.assets\1710121837894.png)









**prevent事件修饰符**

用于阻止默认行为的。

![1710122062805](E:\文档_Typora\1-关于怎么学会coding2.assets\1710122062805.png)

此时就不会执行默认的跳转了。





**self事件修饰符**

![1710122410165](E:\文档_Typora\1-关于怎么学会coding2.assets\1710122410165.png)

**once事件修饰符**

![1710122515830](E:\文档_Typora\1-关于怎么学会coding2.assets\1710122515830.png)



##### 5、按键修饰符

事件处理 — Vue.js
https://v2.cn.vuejs.org/v2/guide/events.html#%E6%8C%89%E9%94%AE%E4%BF%AE%E9%A5%B0%E7%AC%A6

9.按键修饰符_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1SE411H7CY/?p=9&spm_id_from=pageDriver&vd_source=be8081cb351e616080452087e4f6f6b3



![1710122677227](E:\文档_Typora\1-关于怎么学会coding2.assets\1710122677227.png)

**enter按键修饰符**

在执行回车之后触发的事件。这个其实蛮常用的，比如我们经常用的回车搜索。





##### 6、**Axios**基本使用

>**这玩意就是拿来异步请求的，前后端分离的时候好用，上手也快。稍微正统点的说法就是：其核心作用是用来在页面中发送异步请求，并获取对应数据在页面中渲染。即，以前的Ajax局部更新技术**

###### 6.1、Axios 的第一个程序

其中文网站：

起步 | Axios中文文档 | Axios中文网 https://www.axios-http.cn/docs/intro

axios中文文档|axios中文网 | axios http://www.axios-js.com/zh-cn/docs/



其安装的cnd:

```js
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
```







**Axios的GET请求演示**

基础的信息前后台交互：

前台拿后台传递的数据：

```js
// axios.get('https://api.apiopen.top/getJoke?page=1&count=2&type=video')
    axios.get('http://127.0.0.1:5000/admin/dataget')
        .then(function (response) {
            console.log(response);
        })
        .catch(function (error) {
            console.log(error);
        });
```



后台代码：

```python
from flask import Blueprint,render_template,request
from flask_cors import CORS  # 导入 CORS 扩展

# 注册蓝图
axios = Blueprint('axios',__name__)
CORS(axios)  # 在蓝图上启用 CORS

@axios.route('/findAll', methods=['GET'])
def find_all_users():
    name = request.args.get('name')

    # 打印参数 name
    print("Received name:", name)
    
    # 创建用户列表
    users = [
        UserInfo(id="21", username="陈艳男", email="609937647egg.com", age=23, phone="13244556789"),
        UserInfo(id="22", username="汪汪汪", email="609937445@qq.com", age=24, phone="13212349078"),
        UserInfo(id="23", username="三儿呀", email="609937445@qq.com", age=25, phone="13290782354")
    ]

    # 转换用户列表为 JSON 格式并返回
    return jsonify([user.__dict__ for user in users])
```



这里注意：`CORS(axios)  # 在蓝图上启用 CORS`

因为

>通常由浏览器的同源策略引起。**浏览器限制**页面中的 JavaScript 代码通过 XMLHttpRequest 或 Fetch API 向不同源的服务器发起 HTTP 请求。在您的情况下，您的前端代码位于 `http://localhost:xxxx`，而后端代码在 `http://127.0.0.1:5000`，因此属于不同的源。
>
>要解决这个问题，您需要在后端代码中添加 CORS（跨源资源共享）头部，允许来自前端代码的跨源请求

假如前台需要向后台传递数据，就直接传入参数即可：

```js
// axios.get('https://api.apiopen.top/getJoke?page=1&count=2&type=video')
    axios.get('http://127.0.0.1:5000/admin/findAll?name=xiaochen')
        .then(function (response) {
            console.log(response);
        })
        .catch(function (error) {
            console.log(error);
        });
```

后台中，python则是直接使用request库来接收。



**Axios的POST请求**

```java
 //发送POST方式请求
    axios.post('http://127.0.0.1:5000/admin/save', {
        id:"1",
        username: 'yangzhi',
        age: 18,
        email:"3324595753@qq.com",
        phone:"133678890078"
    })
        .then(function (response) {
            console.log(response);
        })
        .catch(function (error) {
            console.log(error);
        });
```

后台代码：

```python
from flask import Blueprint, render_template, request, jsonify
from flask_cors import CORS  # 导入 CORS 扩展
from dataclasses import dataclass

# 注册蓝图
axios = Blueprint('axios',__name__)
CORS(axios)  # 在蓝图上启用 CORS

# 用户实体类。用的是装饰器的形式配合python的datacalsses库
@dataclass
class User:
    id: str
    username: str
    email: str
    age: int
    phone: str


# 保存数据路由
@axios.route('/save', methods=['POST'])
def save_user():
    # 获取请求体中的 JSON 数据
    request_data = request.json

    # 使用请求体中的数据创建用户对象
    user = User(
        id=request_data.get('id'),
        username=request_data.get('username'),
        email=request_data.get('email'),
        age=request_data.get('age'),
        phone=request_data.get('phone')
    )

    # 打印用户信息
    print("User =", user)

    # 返回响应
    return jsonify({"success": True})

```







**Axios并发请求**

>**`并发请求：`将多个请求在同一时刻发送到后端服务接口，最后再集中处理每个请求的响应结果**



也就是这种，多个请求都可以各司其职。

![1710152643714](E:\文档_Typora\1-关于怎么学会coding2.assets\1710152643714.png)



这里是前台代码：

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>15-axios3-并发请求</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">

</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    //既然是并发请求，那么就是同时发送多个请求

    //1、创建一个查询后台信息的方法。并传递参数
    function findAll(){
        return axios.get('http://127.0.0.1:5000/admin/findAll?name=xiaochen');
    }

    //2、创建一个保存信息的方法。
    function saveInfo(){
        return axios.post('http://127.0.0.1:5000/admin/save',{
            id:"1",
            username: 'yangzhi',
            age: 18,
            email:"3324595753@qq.com",
            phone:"133678890078"
        });
    }
    //3、调用axios中处理并发执行的函数
    axios.all([findAll(),saveInfo()])
        .then(axios.spread(function (findAll,saveInfo) {
            console.log(findAll);
            console.log(saveInfo);
        }))
        .catch(function (error) {
            console.log(error);
        });
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        components: {},
    });
</script>
</html>
```



后台代码就用的上面的。

>**算是正式接触到前后台数据交互了。小突破。这个基础的小案例自己再独立写写，然后把有价值的收获总结出来。**



###### 6.2、Vue结合Axios完成天气查询的综合案例

>**顺带也延展一下，基本的小的项目怎么做**

**`step1：`先把静态页面设计出来**

*tmmd*，原来之前上的课还是有用的。直接把自己想搞的功能，最呆板的，死的静态页面写出来。~~后面再一点一点给它动起来~~



```html
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <input type="text" value="请输入"> <input type="button" value="搜索"><br>

    <a href="">北京</a><br>
    <a href="">上海</a><br>
    <a href="">广州</a><br>
    <a href="">深圳</a><br>

    <hr>
    <span>北京,今天的天气是：晴转多云，空气质量良好</span>

</div>
```

![1710155525465](E:\文档_Typora\1-关于怎么学会coding2.assets\1710155525465.png)



即功能效果为，搜索框搜索后，得把响应城市的天气查出来。

在点击下面链接之后，也要把相应的天气情况展示出来。





**`step2:`去把与后台拿数据的接口，接口下的方法写了**

~~想起了我的接口文档怎么写也要学学。~~

需要拿什么数据，就去写它对应的接口和函数。测试好函数确实可以拿到，再把接口放给Vue

​                  



**Tips:启动后端来传递参数进行试验的时候，URL传递需要指定自己传的是个什么参数：**

>http://127.0.0.1:5000/admin/find?name=北京



我后端代码：

```python
from flask import Blueprint, request, jsonify
from flask_cors import CORS  # 导入 CORS 扩展

# 注册蓝图
city_bp = Blueprint('city', __name__)
CORS(city_bp)  # 在蓝图上启用 CORS 解决跨域的问题


# 获取城市天气函数
def get_weather_by_city(name):
    weathers = {
        "北京": "晴转多云，空气清新！",
        "上海": "多云转晴，空气质量不错！",
        "深圳": "中到暴雨，空气也很好！",
        "广州": "局部地区大风，空气也算不错！",
        "天津": "离北京比较近，和北京差不过"
    }
    return weathers.get(name, "未知城市！")


# 创建路由
@city_bp.route('/find', methods=['GET'])
def find_weather_by_city():
    # 获取前端传递的参数 name
    # name = request.args.get('name', type=str, default=None)
    name = request.args.get('name')

    # 如果没有提供 name 参数或参数为空，则返回错误信息
    if name is None or name.strip() == "":
        return jsonify({"error": "请输入正确的城市名"})

    # 获取城市天气信息
    weather = get_weather_by_city(name)

    # 构建返回的 JSON 数据
    result = {name: weather}

    # 返回 JSON 格式的响应
    return jsonify(result)

```

可以看到，request库中查找是通过`name`来进行get的。故而需要再URL中指定。name=xxx



**`step3:`接口写好之后，一点一点回来前台的静态页面中完成把静态的改成动态的：**

小细节：注意this到底指代的是什么。

![1710211918130](E:\文档_Typora\1-关于怎么学会coding2.assets\1710211918130.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>17-vue和Axios的天气查询综合案例</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <input type="text" v-model="name" @keyup.delete="Showfunc" @keyup.enter="searchCity"> <input type="button" value="搜索" @click="searchCity"><br>

<!--    遍历hotCity-->
<!--    用@keyup.prevent阻止原本超链接的默认跳转行为，改为我们的操作-->
<!--    注意是@click中的prevent方法，而不是@keyup中的。确实不阻止原本的超链接行为，我们自己写的方法就不得有响应-->
    <span v-for="city in hotCitys">
        <a href="" @click.prevent="searchCityA(city)">{{city}}</a><br>
    </span>

    <hr>
    <span v-show="isShow">{{name}},今天的天气是：{{message}}</span>

</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {
            name:"",
            hotCitys: ["北京","上海","广州","深圳"],
            message:"",
            isShow:false,
        },
        methods: {
            searchCity:function () {
                //1、获取用户输入的城市
                let _this = this;
                console.log(_this.name);
                //注意Vue的this和axios的this不一样，所以需要将Vue的this赋值给一个变量
                //2、Axios发送请求
                axios.get('http://127.0.0.1:5000/admin/find?name='+_this.name).then(function (response) {
                    console.log(response.data);
                    //3、将返回的数据赋值给message
                    //Object { "北京": "晴转多云，空气清新！" }我输入北京时候，就是字符串了
                    _this.message = response.data[_this.name];
                    //显示搜索结果
                    _this.isShow = true;
                }).catch(function (error) {
                    console.log(error);
                });
        },
            //配合超链接中的searchCityA
            searchCityA:function (name) {
                //因为我们有city名字这个参数，则可以获取传递的参数,并把其修改到this.name。
                //再调用我们上面的searchCity方法
                this.name = name;
                this.searchCity();
            },
            //按删除键之后，清空输入框
            Showfunc(){
                this.isShow = false;
            }

    }
    });
</script>
</html>
```







###### 6.3、Vue结合Axios再梳理

>**`① Axios中GET请求和POST请求`在背后逻辑以及使用方法上的区别？**

答：

**GET请求**：通常用于从服务器检索数据。 由于参数直接附加在URL上，因此**GET请求**==适合传输少量数据或查询字符串。==

 **POST请求**：通常用于向服务器发送数据，例如提交表单或上传文件。 由于参数通过**请求**体传递，因此**POST请求**==更适合传输大量数据或复杂结构的数据。==



至于写法上的区别了。GET直接就URL中传递参数了，POST则是以一个对象的方式，单独包装了再扔过去。

`GET带参数请求样例：`

```js
// 为给定 ID 的 user 创建请求
axios.get('/user?ID=12345')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// 上面的请求也可以这样做
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```



至于Python后台中，只能说暂时在模仿业务代码，我业务能力总是薄弱。



>**`②关于跨域的问题`**

```python
from flask import Blueprint, render_template
from flask_cors import CORS  # 导入 CORS 扩展

# 注册蓝图
axios = Blueprint('axios', __name__)
CORS(axios)  # 在蓝图上启用 CORS
```

在前后端分离的项目中，前端代码位于`http：//localhost:xxx`，而后端代码在`http://127.0.0.1:5000`，是属于不用的源。浏览器会限制那种控制异步请求的js代码向 不同发送请求，故而出现各个框架下的跨源请求问题的解决。



>**`③POST`案例**

这里我上面说了，主要是其传递的信息多，故而用一个对象的形式封装起来传递了，注意写成JSON形式

```js
<!--    模仿一个前台传递一个用户信息到后台。后台进行save的过程。注意传递过去是以JSON的形式传递的-->
    axios.post('http://127.0.0.1:5000/admin/saveuser',{
        id:"1",
        username: 'yangzhi',
        age: 18,
        email:"3324678945@qq.com",
        phone:12356789012}).then(function (response) {
            console.log(response)
    }).catch(function (error) {
        console.log(error)
    });
```



只用python后端的代码，这种拿对象来保存的方式，在登录验证哪里应该可以用到：

```python
# 保存前台传递的信息的路由
@newaxios.route('/saveuser',methods=['POST'])
def saveInfo():
    # 获取请求体中的 JSON 数据
    request_data = request.json
    print("前台传递的参数是：",request_data)
    # 使用请求体中的数据创建用户对象
    user = UserInfomation(
        id=request_data.get('id'),
        username=request_data.get('username'),
        email=request_data.get('email'),
        age=request_data.get('age'),
        phone=request_data.get('phone')
    )

    # 打印用户信息的具体内容
    # 如果你想打印对象的内容，你可以使用__dict__属性，它会返回一个字典，字典中包含了对象的所有属性和它们的值
    print("User =", user.__dict__)
    # 返回响应
    return jsonify({"success": True})
```



>**`④ 执行多个并发请求`**

这里主要是记住Axios中掌管并发请求的方法，模拟就同时GET和POST一起上吧。

**需要注意的是，各自的函数中没有必要再写回调函数和catch了。交给all那里统一执行**



````js
<script>
    //并发请求是各自写各自的方法，然后最后把请求的方法放到all函数中执行
    function GetfindInfomation() {
        return axios.get('http://127.0.0.1:5000/admin/finduser?username=哇哇哇');
    }

    function PostSaveInfomation() {
        return axios.post('http://127.0.0.1:5000/admin/saveuser',{
            id:"1",
            username: 'yangzhi',
            age: 18,
            email:"3324678945@qq.com",
            phone:12356789012});
    }

    //统一调用
    axios.all([GetfindInfomation(),PostSaveInfomation()])
        .then(axios.spread(function (GetfindInfomation,PostSaveInfomation) {
            console.log(GetfindInfomation);
            console.log(PostSaveInfomation);
        }))
        .catch(function (error) {
            console.log(error);
        });
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        components: {},
    });
</script>
````





>**`⑤关于小案例`**

老规划，先把最呆板的静态页面设计出来

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>21-Vue和Axios综合性案例</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <input type="text" value="请输入"> <input type="button" value="搜索">

    <hr>

    <span>
        <a href="">北京</a><br>
        <a href="">上海</a><br>
        <a href="">广州</a><br>
        <a href="">深圳</a><br>
    </span>

    <hr>

    <span>北京今天的天气是：天气阴沉</span>
</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        components: {},
    });
</script>
</html>
```



至于后台，自己测一下，能否拿到数据

![1710235170842](E:\文档_Typora\1-关于怎么学会coding2.assets\1710235170842.png)

````python
from flask import Blueprint, request, jsonify
from flask_cors import CORS  # 导入 CORS 扩展

# 注册蓝图
weathernew = Blueprint('weathernew', __name__)

CORS(weathernew)  # 在蓝图上启用 CORS 解决跨域的问题

# 编写北京、上海、深圳、广州、天津五个城市的天气信息的函数，返回天气信息，用于查询前台传递的search信息
def get_weather_by_city(name):
    weathers = {
        "北京": "晴转多云，空气清新！",
        "上海": "多云转晴，空气质量不错！",
        "深圳": "中到暴雨，空气也很好！",
        "广州": "局部地区大风，空气也算不错！",
        "天津": "离北京比较近，和北京差不过"
    }
    return weathers.get(name, "未知城市！")

# 编写根据城市名查询天气的路由
@weathernew.route('/findweather', methods=['GET'])
def find_weather_by_city():
    # 获得前台传递的参数 name
    name = request.args.get('name')
    # 根据此参数调用函数进行查询
    weather = get_weather_by_city(name)

    # 注意是JSON格式的数据
    # 构建返回的 JSON 数据
    result = {name: weather}

    # 返回 JSON 格式的响应
    return jsonify(result)



````



然后把这些静态的数据，一点一点的活起来，交互起来。

交互这里注意有时候拿到的数据是`null`时候，有没有区分`Vue`和`Window`的this区别



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>21-Vue和Axios综合性案例</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
<!--    开始双向绑定了-->
    <input type="text" v-model="cityname" @keyup.enter="searchCity" @keyup.delete="delInfo"> <input type="button" value="搜索" @click="searchCity">

    <hr>

    <span v-for="city in cityList">
<!--        点击链接之后，需要得到一个跳转效果。此时需要阻止默认的超链接行为-->
        <a href="" @click.prevent="toCityByURL(city)">{{city}}</a><br>
    </span>

    <hr>

    <span v-show="isShow">{{cityname}},今天的天气是：{{message}}</span>
</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {
            cityname:"",
            isShow:false,
            cityList: ["北京","上海","广州","深圳"],
            message:""
        },
        methods: {
            searchCity:function () {
                //1、获取用户输入的城市
                let _this = this;
                console.log(_this.cityname); //输出没问题
                //注意Vue的this和axios的this不一样，所以需要将Vue的this赋值给一个变量
                //2、Axios发送请求
                axios.get('http://127.0.0.1:5000/admin/findweather?name='+_this.cityname).then(function (response) {
                    console.log(response.data);
                    //最后要修改的是Vue的data中的message
                    _this.message = response.data[_this.cityname];
                    _this.isShow=true;

                }).catch(function (error) {
                    console.log(error);
                });
            },
            //点击删除按钮，清空信息,隐藏下方状态结果
            delInfo(){
               this.isShow = false;
            },
            toCityByURL(city){
                this.cityname = city;
                //调用写好的searchCity方法。上面已经修改了cityname
                this.searchCity();
            }
        },
        components: {},
    });
</script>
</html>
```



>**其次是有个原则，就是自己看着要看的过去，假如自己的都看不过去，那就更ex了。先完成，再完美。**







##### 7、Vue的生命周期

>`生命周期钩子 `==`Vue生命周期函数`

主要是要理解一张图：



![](E:\文档_Typora\1-关于怎么学会coding2.assets/Vue生命周期.png)

视频讲解得很清楚。我看看后面有没有人写过类似的博文，没有的话，我再总结：

12.vue的生命周期钩子_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1SE411H7CY/?p=12&spm_id_from=333.880.my_history.page.click&vd_source=be8081cb351e616080452087e4f6f6b3



![1710245012306](E:\文档_Typora\1-关于怎么学会coding2.assets\1710245012306.png)





## Question





## Reference

【编程不良人】适用于后端编程人员的Vue实战教程,整合SpringBoot项目案例、已完结!_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV1SE411H7CY/?spm_id_from=333.999.0.0&vd_source=be8081cb351e616080452087e4f6f6b3

axios中GET、POST请求传参区别及使用方法-百度开发者中心
https://developer.baidu.com/article/details/2823079

在试用了 100+ WebExtension 扩展后，我挑选了这 30 个[下] - 知乎
https://zhuanlan.zhihu.com/p/27854433

