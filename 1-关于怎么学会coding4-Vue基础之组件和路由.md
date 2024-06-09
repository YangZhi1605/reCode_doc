>**`关于怎么学会coding4`**

# Start

本笔记主要有：

**Vue中的组件（Component）和管理组件的路由(Router)**



# Body

## 一、Vue中的组件（Component）

### 1.1、组件的作用

>用来减少Vue实例对象中代码量，日后在使用Vue开发过程中，可以根据不同业务功能，从而将页面划分为不同的多个组件，然后由多个组件去完成整个页面的布局，方便日后使用Vue进行开发时页面管理，方便开发人员维护。

### 1.2、如何使用组件

>**注意组件中，模板声明的时候，必须包裹在一个`<div></div>`中**

#### 1.2.1、全局组件的注册使用

**`全局组件注册给Vue实例，日后可以在任意Vue实例范围内使用该组件`**

**用过 `Vue.component` 来创建组件** 

其主要流程：
① 在`<script></script>`中开发组件

>Vue.component用来开发组件的时候，有参数：
>
>参数1：组件名 —— 拿来在实例中使用的时候直接调用
>
>参数2：组件配置对象{}
>
>​		其中有：template：在一个<div></div>的root元素中编写html代码。后续调用组件的的时候，就展示这部分html代码。
>
>

```js
<script>
    //4、创建全局组件
    Vue.component('login',{
        template:'<div><h1>登录管理</h1></div>'
    });

    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {},
    });


</script>
```



② 在Vue实例范围内使用组件

```html
<div id="app">
<!--    调用编写的全局组件-->

    <login></login>
</div>
```





③ 注意：vue绑定的时候慎重使用驼峰命名

同我前面写不通过参数传递进行删除的案例一样。需要注意JavaScript中接受驼峰命名，但是HTML中不接受，会将驼峰转为小写衔接-

![1710548823197](E:\文档_Typora\1-关于怎么学会coding4.assets\1710548823197.png)

例如此时：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>01-Vue全局组件的使用</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
<!--    调用编写的全局组件-->

    <userLogin></userLogin>
</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    //4、创建全局组件
    Vue.component('userLogin',{
        template:'<div><h1>登录管理</h1></div>'
    });

    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {},
    });


</script>
</html>
```

就报错了，找不到`userLogin`

![1710548904781](E:\文档_Typora\1-关于怎么学会coding4.assets\1710548904781.png)



将其中改成`-`衔接大写出现的驼峰，就能够正常

```html
<div id="app">
<!--    调用编写的全局组件-->

    <user-login></user-login>
</div>

```

![1710549148054](E:\文档_Typora\1-关于怎么学会coding4.assets\1710549148054.png)



#### 1.2.2、局部组件的注册使用

官网上也说了怎么用比较好。也就是将配置对象单独写出来，这种在vue实例的components中直接按照`组件名`:`组件对象`的方式就调用了。可以实现解耦

![1710549519124](E:\文档_Typora\1-关于怎么学会coding4.assets\1710549519124.png)



这种是稍微冗余的：

```html
<script>
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {
            login: {
                template: '<div><h1>登录管理丫丫</h1></div>'
            }
        },
    });
</script>


<div id="app">
    <login></login>
</div>

```



优雅的方式有：

- 写法一：将配置对象中的HTML代码，就写在`<script></script>`中

```html
<script>
    //单独将配置对象拿出来写
    let login = {
        template: '<div><h1>登录管理哇哇</h1></div>'
    };
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {
            login: login,
        },
    });
</script>

<div id="app">
    <login></login>
</div>

```

写法二：用Vue特有的`<template>标签配合id选择器实现`。注意在Vue作用范围外去声明`template`





```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>02-局部组件的使用2</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
<!--    此时，这里常规调用-->
    <login></login>
</div>

<!--通过模板标签去注册局部组件模板，记住在vue实例作用范围外声明-->
<template id="loginTemplate">
    <div><h1>登录管理呜哇</h1></div>
</template>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    let login = {
        template: '#loginTemplate'
    };
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {//用来注册局部组件
            login: login,//注册需要用的局部组件
        },
    });
</script>
</html>
```





>**即：仍然是四部曲：![1710550439513](E:\文档_Typora\1-关于怎么学会coding4.assets\1710550439513.png)**



以及，当注册的组件名和配置对象名字一样的时候，可以直接简写，不写成键值对的形式:

```html
<script>
    let login = {
        template: '#loginTemplate'
    };
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {//用来注册局部组件
            login,//注册需要用的局部组件
        },
    });
</script>
```





### 1.3、Prop的使用

>**用来为`组件`传递静态数据或者动态数据**



#### 1.3.1、通过在组件上声明静态数据传递给组件内部

> 论组件使用，仍旧是三部曲：
>
> ①声明组件（可以配合template标签以及使用id选择器把配置对象声明出来）；
>
> ```js
> //1、声明配置模板对象
> let login = {
>     template: '#loginTemplate',
>     //2、使用prop属性
>     props: ['userName','age'] //用来接受使用组件时标签中传递的参数
> };
> 
> <!--使用模板标签的方式声明-->
> <template id="loginTemplate">
>     <div>
>         <h1>欢迎：{{userName}}，它的年龄是{{age}}</h1>
>     </div>
> </template>
> ```
>
> ②在Vue对象的Components中注册组件；
>
> ```js
> //3、创建vue实例
> const app = new Vue({
>     el: '#app',
>     data: {},
>     methods: {},
>     //生命周期相关的函数
>     components: {
>         //用来注册局部组件
>         login,//注册需要用的局部组件
>     },
> });
> ```
>
> ③在Vue管辖的范围内声明并调用组件。
>
> ```html
> <!--    此时，这里常规调用-->
> <login user-name="小城" age="118"></login>
> ```

至于使用Prop传递数据。则是在第一步的`声明组件`的时候，在`props数组`中将需要挂载数据的变量名字指定好，然后在自己写的html模板中，使用`插值表达式`将数组中声明，且需要表达的变量扔到插值表达式中。最后在自己调用组件的地方，写好这些变量到底需要传递什么静态数据。



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>03-局部组件使用Prop</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <!--    此时，这里常规调用-->
    <login user-name="小城" age="118"></login>
</div>

<!--使用模板标签的方式声明-->
<template id="loginTemplate">
    <div>
        <h1>欢迎：{{userName}}，它的年龄是{{age}}</h1>
    </div>
</template>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    //1、声明配置模板对象
    let login = {
        template: '#loginTemplate',
        //2、使用prop属性
        props: ['userName','age'] //用来接受使用组件时标签中传递的参数
    };
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {
            //用来注册局部组件
            login,//注册需要用的局部组件
        },
    });
</script>
</html>
```





#### 1.3.2、通过在组件上声明动态数据传递给组件内部

**这里的核心就是通过`v-bind`将数据动态的绑定在`vue`实例的`data`数组中了**

>仍旧三部曲来把组件搞定。
>
>① 同样是声明组件对象。依据需要将需要展示的数据放到prop数组中：
>
>```html
>
><template id="loginTemplate">
>    <div>
>        <h1>欢迎：{{userName}}，它的年龄是{{age}}</h1>
>    </div>
></template>
>
><script>
> const login = {
>        template: '#loginTemplate',
>        //2、使用prop属性
>        props: ['userName','age'] //用来接受使用组件时标签中传递的参数
>    };
></script>
>```
>
>② 同样是在vue实例中注册
>
>③ 同样是在vue掌管的范围内使用这个标签。
>
>④ **不同的来了。之前写数据，在③中，直接将prop数据中的变量名应该赋值的数据赋好了，然后配合插值表达式来展示。现在，数据不直接绑定了，而是在vue实例中的data属性中，对某个数据赋值，再将这个数据通过v-bind，在标签中进行绑定，也就将原本写死的`"小城"`，变成动态的`:user-name='usernameYa'`，以后对usernameYa进行修改，即可修改到`user-name`的数据**
>
>```js
>//3、创建vue实例
>const app = new Vue({
>    el: '#app',
>    data: {
>        userNameYa: '小城',
>        ageYa: 118
>    },
>    methods: {},
>    //生命周期相关的函数
>    components: {
>        //用来注册局部组件
>        login,//注册需要用的局部组件
>    },
>});
>
>
>```
>
>使用的时候：
>
>```html
><div id="app">
>    <login v-bind:user-name="userNameYa" v-bind:age="ageYa"></login>
></div>
>```
>
>

并且整个传递数据的流程，和静态时候差别不大。只是静态的时候，数据写在调用的标签中，此时在调用的标签中使用v-bind属性绑定一个data中的动态值给声明在props中的变量名，从而实现把之前写死的东西变得动态了。



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>04-局部组件使用Prop传递动态数据</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <login v-bind:user-name="userNameYa" v-bind:age="ageYa"></login>
</div>

<template id="loginTemplate">
    <div>
        <h1>欢迎：{{userName}}，它的年龄是{{age}}</h1>
    </div>
</template>
</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    const login = {
        template: '#loginTemplate',
        //2、使用prop属性
        props: ['userName','age'] //用来接受使用组件时标签中传递的参数
    };
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {
            userNameYa: '小城',
            ageYa: 118
        },
        methods: {},
        //生命周期相关的函数
        components: {
            //用来注册局部组件
            login,//注册需要用的局部组件
        },
    });
</script>
</html>
```





#### 1.3.3、prop单向数据流【作为了解】

**所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。**

### 1.4 组件中定义自己的数据和事件



#### 1.4.1、组件中定义属于组件自己的data数据

>**主要变动是数据要放在一个`data`函数中，用对象的方式进行返回，其他的，数据如何赋值，如何调用，区别不大。**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>05-组件中定义属于组件自己的data数据</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <login></login>
</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    const login = {
        template: '<div><h1>它是{{cityName}},它已经{{age}}岁了</h1><ul><li v-for="item,index in lists">{{index}}+{{item}}</li></ul></div>',
        data(){
            return {
                cityName: '小城',
                age: 118,
                lists:['北京','广州','深圳']
            }
        }
    };
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {
            login,
        },
    });
</script>
</html>
```



#### 1.4.2、组件中事件的定义

和之前的常规情况其实差不多。也是在`methods`里面定义。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>06-组件中事件的定义</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
<!--    3、调用自己写的组件-->
    <login></login>
</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    //1、声明组件和组件中的数据以及事件
    const login={
        template:'<input type="button" value="点我撒" @click="clickMe">',
        data(){
            return {
                name:'我是一个姓名',
            };
        },
        methods:{
            clickMe(){
                alert(this.name);
                alert('点击了我');
            }
        },
    };
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {
            //2、用来注册局部组件
            login
        },
    });
</script>
</html>
```

这里还可以学到，在组件中，又有一个服务于该组件的`this`

![1710751596863](E:\文档_Typora\1-关于怎么学会coding4.assets\1710751596863.png)



#### 1.4.3、向子组件传递父组件的事件，并调用

其背后的意义和数据可以通过`v-bind`实现绑定，将父组件中的数据丢给子组件。

同理，可以通过`v-on`实现绑定，将父组件中的事件丢给子组件。

**那么先把`v-bind`梳理清楚**

![1710753534932](E:\文档_Typora\1-关于怎么学会coding4.assets\1710753534932.png)

- 首先清楚，子组件中的数据变量名都是放在`props:[]`中，这个每个数据变量名可以通过插值表达式`{{}}`在模板中调用，至于其展示的数据，可以通过在调用的时候静态赋值一个死的值进去，也可以通过`v-bind`将父组件中可以灵活变动数据的某一个变量绑定进去。比如父组件中`username=林清`，绑定到子组件上`:pname="username"`，那么，现在`pname`的值就是林清了，父组件中的username变动，pname变动。
  为了再灵活一点，子组件中也可以放置一个`data`函数，然后将父组件中的传递给子组件中的props中的变量，再放到data函数中，调用data函数中东西，可以更灵活一点。
- 至于传递事件，就是类似的了，在`methods`中编写好自己的子函数，子函数中可以调用父组件，当通过`v-on`绑定之后。绑定的语法有点特殊：`this.$emit('函数名')`。
  `注意`：不同于组件和 prop，事件名不存在任何自动化的大小写转换。而是触发的事件名需要完全匹配监听这个事件所用的名称，不同于组件和 prop，事件名不会被用作一个 JavaScript 变量名或 property 名，所以就没有理由使用 camelCase 或 PascalCase 了。**并且 `v-on` 事件监听器在 DOM 模板中会被自动转换为全小写 (因为 HTML 是大小写不敏感的)**，所以 `v-on:myEvent` 将会变成 `v-on:myevent`——导致 `myEvent` 不可能被监听到。

>**所以，绑定事件监听的时候，老老实实写小写就好**



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>07-子组件调用父组件中的方法</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">
    <login :proname="username" @faFunc="fatherFunction"></login>
</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    const login={
        template:'<div><h2>这是子组件,我用的proname,它绑定的父组件中的数据：{{proname}}</h2> <h2>这是子组件,我用的dataname,在data函数中，通过this指定到父组件传来的数据:{{dataname}}</h2><input type="button" value="请点击我" @click="clickMe"></div>',
        data(){
            return {
                dataname:this.proname,
            };
        },
        props:['proname'],
        methods: {
            clickMe:function () {
                // alert('我是子组件中的事件');
                // 上面绑定的时候写的大写，但是因为自动转换为小写，所以这里写的时候要小写
                this.$emit('fafunc');
            }
        },
    }
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {
            username:"我是父组件中的数据",
        },
        methods: {
            fatherFunction () {
                alert('我是父组件中的事件');
            }
        },
        //生命周期相关的函数
        components: {
            login,
        },
    });
</script>
</html>
```



>**`vue`中的组件是拿来满足SPA（single page application）单页面应用的，也就是在一张页面中完成多种功能。日后开发中，组件可是一把宝剑**

## 二、Vue中的路由（Router）

路由不算是基础Vue中的东西了，需要访问(Vue router官网)[https://router.vuejs.org/zh/introduction.html]

### 2.1、对路由的认识以及理解Vue的作用

`①什么是路由？`

用标致的话来说：

>路由会根据请求的路径按照一定的路由规则进行请求转发从而帮助我们实现统一请求的管理

用我的话说：

>路由是Vue中管理请求路径的家伙



`②路由的作用是什么？`

>路由是配合组件打组合拳实现SPA的。具体是用来在Vue中实现组件之间的动态切换



### 2.2、如何使用路由

这里也同样将使用路由规范化为步骤吧

#### 2.2.1、下载路由

可以使用cnd的形式，也可以下载为本地的js。但是总的原则是：`必须在已经引入vue之后才能引入vue router`

```html
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<!--引入路由-->
<script src="https://unpkg.com/vue-router@3/dist/vue-router.js "></script>
```

当引入路由之后，就可以创建路由对象`VueRouter`了。



#### 2.2.2、编写组件对象

路由是对模板的在操作。先把模板编写好，只是此时模板不用注册到Vue对象的components中了。

```html
const login = {
	template:'<div><h1>登录</h1></div>',
};

const register = {
	template:'<div><h1>注册</h1></div>',
};
```



#### 2.2.3、创建路由对象并定义路由对象中的路径等掌管规则

上面说了，引入vue-router之后，就可以得到一个VueRouter对象，现在就是创建这个对象，并对其进行一定的配置，使其管理我们的组件。**`注意:一个{}中一个路由的匹对。`**

```js
  const router = new VueRouter({
        routes:[
            {path:'/login',component:login},
            {path:'/register',component:register},
        ]
    });
```

其官网也有这种写法：

>将`routes`单独编写，然后再扔到VueRouter对象中，使用`routes: routes`调用。

```js
// 0. 如果使用模块化机制编程，导入Vue和VueRouter，要调用 Vue.use(VueRouter)

// 1. 定义 (路由) 组件。
// 可以从其他文件 import 进来
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. 定义路由
// 每个路由应该映射一个组件。 其中"component" 可以是
// 通过 Vue.extend() 创建的组件构造器，
// 或者，只是一个组件配置对象。
// 我们晚点再讨论嵌套路由。
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

// 3. 创建 router 实例，然后传 `routes` 配置
// 你还可以传别的配置参数, 不过先这么简单着吧。
const router = new VueRouter({
  routes // (缩写) 相当于 routes: routes
})

// 4. 创建和挂载根实例。
// 记得要通过 router 配置参数注入路由，
// 从而让整个应用都有路由功能
const app = new Vue({
  router
}).$mount('#app')

// 现在，应用已经启动了！

```

**可以看到，我们是在VueRouter对象中注册组件了，不用到Vue对象中注册了。**

#### 2.2.4、将路由对象注册到Vue实例中

```js
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {},
        //注册路由 (同样也可以简写为router,因为ES6的语法)
        router:router,
    });
```



#### 2.2.5、调用在页面中显示路由的组件

```html
<div id="app">
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
</div>
```

此时，在浏览器后加入`login`的请求，则可以进入登录页面。假如`register`的请求，就进入注册页面。

![1710813237264](E:\文档_Typora\1-关于怎么学会coding4.assets\1710813237264.png)





#### 2.2.6、根据链接切换路由

**这里的细节是，一定得加上哈希路由`#`**

```html
    <a href="#/login">进入登录</a>
    <a href="#/register">进入注册</a>
```











### 2.3、router-link的使用

router-link相当于替换掉了我们自己书写的a标签（默认情况下）。并且帮我们自动化了`#`，避免了我们手动书写。

![1710815370697](E:\文档_Typora\1-关于怎么学会coding4.assets\1710815370697.png)

```html
<div id="app">
    <h1>router-link</h1>
    <router-link to="/login">点击登录</router-link>
    <router-link to="/register">开始注册</router-link>

    <router-view></router-view>
</div>
```





更核心的说法是，`<router-link></router-link>`中自己挂载了一个点击事件，其还可以通过`tag`属性指定当前的到底是一个什么标签，`a`、`button`、`span`。。。等等都可以的。

![1710815578370](E:\文档_Typora\1-关于怎么学会coding4.assets\1710815578370.png)

```html
<div id="app">
    <h1>router-link</h1>
    <router-link to="/login" tag="button">点击登录</router-link>
    <router-link to="/register" tag="span">开始注册</router-link>

    <router-view></router-view>
</div>
```



### 2.4、默认路由

其实也就是在处理根路由`/`。让处于根路由的时候，页面不是空空如也。

![1710816156329](E:\文档_Typora\1-关于怎么学会coding4.assets\1710816156329.png)

```js
const router = new VueRouter({
        routes:[
            {path: '/',component: login},
            {path:'/login',component:login},
            {path:'/register',component:register},
        ]

    });



```

更推荐使用`redirect`

```js
const router = new VueRouter({
    routes:[
        // {path: '/',component: login},
        {path: '/',redirect: '/login'},
        {path:'/login',component:login},
        {path:'/register',component:register},
    ]

});
```



### 2.5、路由的参数传递

#### 2.5.1、在url中带参数传递

**`第一种方式——传统方式`**

即，`<router-link to="/login?id=21">我要登录</router-link>`在使用`router-link`进行访问的时候，将参数扔进去。这个扔进去的参数，在组件创建的时候`create（）`，即也跟着在组件中了。

>遇到个问题，现在不能获得this指代的Vue对象。



**目前遇到问题并没有解决**

我这里有一段代码，按照其执行逻辑来说，当点击`我要登录`按钮时，浏览器控制台应该执行代码`console.log(this)`输出一个`VueComponent`对象。但是控制台始终只是输出`Object`对象。请问为什么？

 —— **出案了。浏览器的问题**

在Chrome中能够输出VueComponent

![1710917099604](E:\文档_Typora\1-关于怎么学会coding4.assets\1710917099604.png)





**我编写的逻辑和他一致，但是并没有得到结果： `====>` 解决后的积累：有时候确认代码逻辑没有问题的时候，换个浏览器试试呢？**



![1710916549682](E:\文档_Typora\1-关于怎么学会coding4.assets\1710916549682.png)



**`第二种方式——restful`**

直接放到路径里，在params中

![1710916670691](E:\文档_Typora\1-关于怎么学会coding4.assets\1710916670691.png)



![1710917828862](E:\文档_Typora\1-关于怎么学会coding4.assets\1710917828862.png)



**整体代码：**



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>03-路由中的参数传递</title>

</head>
<body>
<!--2、挂载需要vue托管的部分-->
<div id="app">

    <router-link to="/login?id=12&name=羊羊羊" tag="button">我要登录</router-link>
    <router-link to="/register/56/林清">我要注册</router-link>

    <router-view></router-view>
</div>

</body>
<!--    1、先引入vue.js-->
<!--    <script src="vue.js" type="text/javascript" charset="UTF-8"></script>-->
<script src="https://cdn.jsdelivr.net/npm/vue@2.7.16/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router@3/dist/vue-router.js "></script>
<!--    引入Axios-->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    const login = {
        template:'<div><h1>登录{{this.$route.query.name}}</h1></div>',
        //麻雀虽小，五脏俱全
    //     回到url中对应的组件来获取参数
        data(){return {}},
        methods:{},
        created(){
            // console.log('=========>'+this.$route.query.id);
            // 我去,nnd，真是重启解决80%的问题。
            //这里在浏览器中怎么找到id，我并没有学会，但是确实是这么编写逻辑的
            console.log(this.$route.query.id+this.$route.query.name);
            console.log('这是create函数');
        },
    };

    const register = {
        template: '<div><h1>注册{{this.$route.params.username}}</h1></div>',
        created() {
            console.log(this);
            //通过restful的形式获取到参数
            // 这种拿到输出结果了，为什么上面的拿到的是一个undefined的结果了?
            console.log(this.$route.params.id+this.$route.params.username);
        }
    };

    var router = new VueRouter({
        routes: [
            {path: '/', redirect: '/login'},
            {path: '/login', component: login},
            // restful传递参数的格式是：+ 参数名称
            {path: '/register/:id/:username', component: register},

        ]
    });
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {},
        router
    });
</script>
</html>
```





### 2.6、嵌套路由

>**为什么要用嵌套路由？**
>
>比如我们先点击进入了`用户管理`页面，在此界面中，我们需要再进入这个页面下的`用户中心`、`管理设置`等等页面的时候，就需要Vue的嵌套路由了。



>切忌不可按照常规思维中的路由堆叠，这种的后果是可以实现跳转，但是是完全跳转到新页面，彻底覆盖之前的。因而，需要自己主动去使用嵌套路由所需要的语法`children`

即这种效果，跳转确实跳转了。但是跳转过去后是直接暴力的覆盖。



![](E:\文档_Typora\1-关于怎么学会coding4.assets/路由直接覆盖.gif)

**`那么正确的姿势，不会覆盖顶层的姿势是什么了`？**

![1710923813300](E:\文档_Typora\1-关于怎么学会coding4.assets\1710923813300.png)



**一、声明模板，确定好内层和外层，把需要展示的路由放着，待会声明路由对象的时候，也填充在路由对象中**

```html
<template id="title">
    <div>
        <h1>用户管理界面来了</h1>
<!--        直接按照常规逻辑来这里写附属的跳转点击-->
        <router-link to="/title/add">添加用户</router-link>
        <router-link to="/title/edit">编辑用户</router-link>
<!--        同样，写显示路由的组件-->
        <router-view></router-view>
    </div>
</template>
<script>
    //1、创建模板组件
    const title = {
        template:'#title',
    };
    //1.1、写大页面下的子组件
    const add = {
      template: '<h4>添加页面</h4>',
    };
    const edit = {
        template:'<h4>编辑页面</h4>'
    };
</script>
```

**二、使用`children`配合着创建一个含有嵌套路由的路由对象**



```js
   var router = new VueRouter({
        routes:[
            {
                path:'/title',
                component:title,
                children:[
                    {path: 'add',component: add},
                    {path: 'edit',component: edit}
                ],
            },
        ],
    });
```



我上面说了，将`{}`视为一个对象，在这个对象中，有`path`、`component`、`children`等等属性。这个`children`了，其中又可以在`/title`的情况下叠加路由`add`，并通过`{}`再此挂载`component`。





**三、常规注册路由对象**

```js
 const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {},
        //注册路由
        router:router,
    });
```



**四、常规使用路由**

把顶层显示起来就可以了，顶层中包含了子元素的。

```html
<div id="app">
<!--    编写掌控组件的跳转-->
    <router-link to="/title">到用户管理界面</router-link>
<!--    将组件的展示同样交给路由管理-->
    <router-view></router-view>
</div>

<template id="title">
    <div>
        <h1>用户管理界面来了</h1>
<!--        直接按照常规逻辑来这里写附属的跳转点击-->
        <router-link to="/title/add">添加用户</router-link>
        <router-link to="/title/edit">编辑用户</router-link>
<!--        同样，写显示路由的组件-->
        <router-view></router-view>
    </div>
</template>
```





## 三、使用组件和路由的综合性Demo

### 3.1、配合Bootstrap先把基本的静态页面写好

>**仍旧是使用Vue的js，和Bootstrap的CSS，目前定位在Bootstrap3**

#### 3.1.1、先把基本的页面写好

![1710937137195](E:\文档_Typora\1-关于怎么学会coding4.assets\1710937137195.png)



#### 3.1.2、再把每个页面下的组件写好以及托管给路由来管理

```js
//主页组件配置对象，当然，自己评估好自己项目中HTML代码的大小，假如比较多就拎出去写。
    const home = {
        template: '<h1>这是主页</h1>',
    };
    //用户管理组件配置对象
    const user = {
        template: '<h1>这是用户管理</h1>',
    };
    //学生管理组件配置对象
    const student = {
        template: '<h1>这是学生管理</h1>',
    };

    //通过路由挂载组件
    const router = new VueRouter({
        routes: [
            {path: '/',component: home},
            {path: '/home', component: home},
            {path: '/user', component: user},
            {path: '/student', component: student},
        ]
    });


//用超链接的时候，记得用好#
<div class="col-md-10 col-md-offset-4" style="margin-top: 70px">
    <ul class="nav nav-pills">
        <li role="presentation" class="active"><a href="#/home">主页</a></li>
            <li role="presentation"><a href="#/user">用户管理</a></li>
                <li role="presentation"><a href="#/student">学生管理</a></li>
                    </ul>
</div>
```



> **`class="active"`控制的是最初试进入网页，是那个页面被激活展示**





**`最最最容易忘记的是，自己既然交给路由管理，那么记得展示路由，每次都忘记`**

```html
<div class="row">
    <div class="col-md-10 col-md-offset-4" style="margin-top: 10px">
        <router-view></router-view>
    </div>
</div>
```





#### 3.1.3、向各个页面中填充自己需要放入的内容

写主页的东西

![1710939683496](E:\文档_Typora\1-关于怎么学会coding4.assets\1710939683496.png)

写第二页的表格

![1710940029586](E:\文档_Typora\1-关于怎么学会coding4.assets\1710940029586.png)



第三页信息还是写表格

![1710940127732](E:\文档_Typora\1-关于怎么学会coding4.assets\1710940127732.png)

其实目前可以发现，纯模板和组件开发，当HTML多了，还是容易乱的。





### 3.2、开发后台

**遵循：model到service到视图**。这是模仿的MVC，我现在只是简单的返回一点数据。直接视图上

```python
from flask import  request, jsonify, Blueprint
# 解决跨域请求
from flask_cors import CORS

# 声明蓝图
routerTry_controller = Blueprint('routerTry_controller', __name__)
# 解决跨域请求
CORS(routerTry_controller)

# 查询所有用户的路由，按照json的格式返回，自定义假数据，数据中有ID，姓名，年龄，生日
@routerTry_controller.route('/findInfoRouter',methods=['GET'])
def def_find():
    users = [
        {
            'id': 1,
            'name': '张三',
            'age': 18,
            'birthday': '2000-01-01'
        },
        {
            'id': 2,
            'name': '李四',
            'age': 19,
            'birthday': '2001-01-01'
        },
        {
            'id': 3,
            'name': '王五',
            'age': 20,
            'birthday': '2002-01-01'
        }
    ]
    return jsonify(users)

```



页面上拿到结果了

![1710942977848](E:\文档_Typora\1-关于怎么学会coding4.assets\1710942977848.png)



最后学学用vue来调整`active`激活



我们的`active`参数控制上面导航栏的状态，那么就调整它，最后结果就比较舒服了

![1710943360434](E:\文档_Typora\1-关于怎么学会coding4.assets\1710943360434.png)

其根本原理是，当点击到这个页面，就将这个页面的名字参数传递到点击函数中，使得 `showActive == 'home'?'active':' '`这种三元运算符发挥作用，为点击的那个导航赋值`active`



```html
<div class="col-md-10 col-md-offset-1" style="margin-top: 70px">
                <ul class="nav nav-pills nav-justified">
                    <li role="presentation" v-bind:class="showActive == 'home'?'active':' '" @click="change('home')"><a href="#/home">主页</a></li>
                    <li role="presentation" v-bind:class="showActive == 'user'?'active':' '" @click="change('user')"><a href="#/user">用户管理</a></li>
                    <li role="presentation" v-bind:class="showActive == 'student'?'active':' '" @click="change('student')"><a href="#/student">学生管理</a></li>
                </ul>
            </div>
```





>**`恭喜，Vue的基础环节到这里就结束了，下面准备进入脚手架`**







# Question





# Reference

组件注册 — Vue.js
https://v2.cn.vuejs.org/v2/guide/components-registration.html

Prop — Vue.js —— 单项数据流
https://v2.cn.vuejs.org/v2/guide/components-props.html#%E5%8D%95%E5%90%91%E6%95%B0%E6%8D%AE%E6%B5%81

自定义事件 — Vue.js
https://v2.cn.vuejs.org/v2/guide/components-custom-events.html



kebab-case是什么-掘金 也就是使用短横线来衔接
https://juejin.cn/s/kebab-case%E6%98%AF%E4%BB%80%E4%B9%88

Vue Router —— 3.x
https://v3.router.vuejs.org/zh/

介绍 | Vue Router —— 4.x
https://router.vuejs.org/zh/introduction.html

