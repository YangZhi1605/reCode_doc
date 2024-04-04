>**`Vue脚手架相关的东西，要结束开发自己的东西了`**

# Start

**在没有用脚手架之前，代码太冗余。Vue中，一切皆是组件。脚手架中也是这种思想**

Vue CLI启动【vue2】



# Body

## 一、Vue CLI脚手架

### 1.1、什么是CLI

>CLI（Command-Line Interface），即**命令行界面**，与之对应的是图形化用户界面，就是通过命令跟系统（软件）进行交互，例如Linux 和Windows的PowerShell。 软件的CLI安装，就是软件提供了一套自己的执行命，通过命令实现某些操作。 



### 1.2、什么是Vue CLI

基本命令还是要学的~

Vue CLI 是一个基于Vue.js进行快速开发的完整系统。使用Vue脚手架之后，我们开发的页面将是一个完整的系统或者说，完整的项目。`既然是完整的开发系统，其中也就有自己的项目系统结构`

### 1.3、Vue CLI优势

我目前是Vue最新版本的指令，那就跟着文档上的指令走吧。

- 通过 `@vue/cli` 实现的交互式的项目脚手架。 那么就像java的maven，像python的pip，可以用网络和指令来下载需要的依赖。
- 通过 `@vue/cli` + `@vue/cli-service-global` 实现的零配置原型开发。 也就原本Vue中的Vue.js、Router.js等等它配置好了。axios则可以一行命令搞定
- 它有一个运行依赖`@vue/cli-service`，该依赖了，
  - 可升级；==>（一条命令搞定）
  - 基于 webpack 构建，并带有合理的默认配置；==>（webpack是项目打包方式，像java的jar、war包），这种编译好的项目源码能够直接部署到服务器上直接使用。
  - 可以通过项目内的配置文件进行配置；==>默认配置文件可以通过简单修改就得到自己想要的
  - 可以通过插件进行扩展。
- 一个丰富的官方插件集合，集成了前端生态中最好的工具。 ==> 服务器用的Node.js（相当于纯java编写的tomcat，node就是纯js编写的服务器），前后端分离，Vue和Vue Router都有，打包方式webpack和yarn都行
- 一套完全图形化的创建和管理 Vue.js 项目的用户界面。 



### 1.4、Vue CLI的安装

#### 1.4.1、环境准备

##### 1.4.1.1、**Node.js的安装配置和检验**



![1710948392714](E:\文档_Typora\1-关于怎么学会coding5.assets\1710948392714.png)

##### 1.4.1.2、**npm相关内容**

tips:根据我终端打印的东西来看，我的npm下载位置是没有配置的

![1710949923705](E:\文档_Typora\1-关于怎么学会coding5.assets\1710949923705.png)







**npm介绍**

```markdown
	node package manager,是nodejs的包管理工具，现在也是前端主流技术，大多数也都使用npm进行统一管理
	相当于java的maven
	maven管理的是java后端的依赖，	其有一个远程仓库（中心仓库）		也有国内的阿里云镜像
	npm  管理的是前段系统的依赖，  具有一个远程仓库（中心仓库）	   也有国内的淘宝镜像
```

**配置淘宝镜像**

配置用：

```
npm config set registry https://registry.npmmirror.com
```

查看镜像使用状态用：

```
npm config get registry
```



还原回到官方的用：

```
npm config set registry https://registry.npmjs.org
```





![1710949958434](E:\文档_Typora\1-关于怎么学会coding5.assets\1710949958434.png)



**配置npm下载依赖位置**

它是一个缓存`cache`配合一个全局`global`一起使用的

验证nodejs环境配置：`npm config ls` 

配置cache:

```
npm config set cache "E:\java\nodejs\node_cache"
```

配置global

```
npm config set prefix "E:\java\nodejs\node_global"
```



配置完成

![1710951032940](E:\文档_Typora\1-关于怎么学会coding5.assets\1710951032940.png)



##### 1.4.1.3、**脚手架的安装**



**这玩意更新好快**

![1710984353321](E:\文档_Typora\1-关于怎么学会coding5.assets\1710984353321.png)



**如何安装？**通过一条命令~

我下方的指令应该是安装2.x版本的。目前已经是迭代到4.x版本了。我顺带学一下其他版本的安装和写在了

```
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```



安装2.x版本的【2.x和3.x不兼容】：

```
npm install -g vue-cli
```





**如何卸载其他版本的？**

```
npm uninstall -g @vue/cli //卸载3.x版本的脚手架
npm uninstall -g vue-cli  //卸载2.x版本脚手架
```



`很好，不出意外，出了意外。。。`

![1710985047071](E:\文档_Typora\1-关于怎么学会coding5.assets\1710985047071.png)

自己读报错，是权限的问题，再用root/Administrator执行，搞定

![1710985222699](E:\文档_Typora\1-关于怎么学会coding5.assets\1710985222699.png)



安装完成，先用2.x跟着操作，假如后续发现2.x确实不好用了，再卸载

##### 1.4.1.4、脚手架使用的小项目

**①使用vue脚手架(2.x)创建第一个项目**

注意要到自己放置项目的项目文件夹下，使用使用创建一个项目

```
vue init webpack 项目名
```

那么简单的cd指令等等是顺理成章需要的了。



![1710986905142](E:\文档_Typora\1-关于怎么学会coding5.assets\1710986905142.png)

我当前的项目位置应该没有问题，我就是想在`VueDemo`这个项目文件夹下创建本次案例

至于哪些该要，哪些不要，这个图现阶段可以作为参考

![1710987096884](E:\文档_Typora\1-关于怎么学会coding5.assets\1710987096884.png)

创建完成，它也告诉了怎么运行的了

![1710987139823](E:\文档_Typora\1-关于怎么学会coding5.assets\1710987139823.png)

以及其目录结构

```markdown
    build
    config
    src
    static
    .babelrc
    .editorconfig
    .gitignore
    .postcssrc.js
    index.html
    package.json
    README.md
```



**`关于一点问题的解决`：**

很奇怪。我刚才没有使用`npm install`之前，项目结构如上，是如下，视频中作者的如下：

![1710988529327](E:\文档_Typora\1-关于怎么学会coding5.assets\1710988529327.png)

也就是我使用`npm install`之后的目录内容

![1710988588703](E:\文档_Typora\1-关于怎么学会coding5.assets\1710988588703.png)



假如没有这步，就会频繁报错表示系统找不到`webpack-dev-server`命令 

![1710988701914](E:\文档_Typora\1-关于怎么学会coding5.assets\1710988701914.png)

**解决办法如下：**

1. `webpack-dev-server`没有全局安装在你的电脑上。
2. 项目的依赖没有被正确安装。

解决这个问题，你可以采取的步骤可能包括：

1. 全局安装webpack-dev-server。在你的控制台运行如下命令：

```
npm install -g webpack-dev-server
```

1. （推荐）在你的项目目录下安装所有依赖。在你的项目目录（在你的例子中是`E:\develops\workspace_webstorm_vue1\vueDemo\hellocli`）中运行如下命令：

```
npm install
```

这会根据你项目中的`package.json`文件安装所有的依赖。`webpack-dev-server`应该就在这些依赖之中。

>**关于webpack-dev-server**
>
>`webpack-dev-server` 是 `webpack` 提供的一个**小型的 Node.js Express 服务器**。它的主要作用是在开发过程中提供一个简单的 web 服务器(相当于Tomcat)，**并具备热重新加载的能力**。这使得开发过程中可以实时看到代码改变后网页的效果，极大地提高了开发效率。
>
> 
>
>以下是 `webpack-dev-server` 的一些主要特点：
>
>1. 提供了一个 Web 服务器：你可以打开浏览器并访问你的网页，而不必为每个项目搭建一个完整的后端服务。
>2. 热重载能力（Hot Module Replacement）：这意味着当你修改了代码并保存后，页面会自动刷新来展示新的效果。这比传统的完全重载页面的方式更高效。
>3. 支持模块替换：在一些情况下（比如修改样式），页面甚至不需要刷新就可以立即看到新的效果。
>4. 代理功能：通过配置，本地服务器可以将某些请求代理到对应的后端服务，这在处理跨域请求时很有帮助。
>5. 自定义配置：你可以根据你的项目和开发习惯对 `webpack-dev-server` 进行一系列的配置。
>6. 可以直接与Webpack配置和其它Webpack工具（如Webpack插件）配合使用，充分利用Webpack生态。
>
>因此，对于大多数基于Webpack的前端项目（包括Vue项目），`webpack-dev-server` 都是一个很常用的开发工具。

**解决，启动成功**

![1710988977753](E:\文档_Typora\1-关于怎么学会coding5.assets\1710988977753.png)





**Vue cli项目结构剖析**

> **`脚手架的重点也就是这个项目结构了：`**
>
> ![1710990277817](E:\文档_Typora\1-关于怎么学会coding5.assets\1710990277817.png)







**Vue cli中项目开发方式**

>**在Vue中，一切皆组件。**
>
>那么，一个组件中包含什么了？js代码+HTML代码+CSS样式

那么，记得理解：

- Vuecli开发方式是在项目中开发一个一个组件对应一个一个业务功能模块，日后可以将多个组件组合到一起形成一个前端系统。
- 日后在使用Vue cli进行开发时不再书写HTML，编写的是一个一个组件（组件是后缀为.Vue结尾的文件），日后打包时，Vue cli会将组件编译成运行的html文件





### 1.4.2、实际运用上手

##### 1.4.2.1、回顾组件和路由



注意理解我上面说的话，Vue中，一切皆是组件对象。

我们最初开发组件是怎么样的？

>声明好组件对象，然后写好这个组件负责什么样的静态页面模板，以及后面的注册到vue实例和直接使用组件名字调用。

`写模板的时候记得，需要使用<div></div>包裹`

```html
<div id="app">
<!--    此时，这里常规调用-->
    <login></login>
</div>

<template id="loginTemplate">
    <div><h1>登录管理呜哇</h1></div>
</template>

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



后来？我们交给路由来管理组件了。

>还是老老实实将组件对象声明好，模板是什么样的写好。挂载了？变化了，不再直接挂载给vue实例，而是挂载给Router对象，再将Router交给Vue管理。
>
>最后通过`<router-view></router-view>`来展示挂载的组件。

```html
<div id="app">
    <h1>你好，路由</h1>
    <a href="#/login">进入登录</a>
    <a href="#/register">进入注册</a>
    <!-- 路由出口 -->
    <!-- 路由匹配到的组件将渲染在这里 -->
    <router-view></router-view>
</div>

<script>
    //②
    const login = {
      template:'<div><h1>登录</h1></div>',
    };

    const register = {
        template:'<div><h1>注册</h1></div>',
    };

    //③
    const router = new VueRouter({
        routes:[
            {path:'/login',component:login},
            {path:'/register',component:register},
        ]
    });
    //3、创建vue实例
    const app = new Vue({
        el: '#app',
        data: {},
        methods: {},
        //生命周期相关的函数
        components: {},
        //注册路由 (同样也可以简写为router,因为ES6的语法)
        router:router,
    });
</script>
```



后面咱就是认识到啊，这个组件，也是一个缩小版的vue实例了，麻雀虽小五脏俱全，也是有data，有methods，有生命周期函数等等

```js
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
```





##### 1.4.2.2、看看我们的Vue

**它的`main.js`相当于我们之前`<script></script>`中干事儿**

![1711000166783](E:\文档_Typora\1-关于怎么学会coding5.assets\1711000166783.png)

`./`是当前文件夹。`../`是上层中的同级文件夹

**至于App.vue相当于一个主组件，组组件中写好<router-view/>也就负责展示好哪些挂载在Router()上的信息了**

组件是在哪里写的？`<script></script>`标签中。

只是使用脚手架后，要加在一个暴露对象`export default`中

![1711000592244](E:\文档_Typora\1-关于怎么学会coding5.assets\1711000592244.png)

还有，它们只是组件化了，来帮助开发，底层还是执行的vue的语法，别把Vue语法扔了。

>**以后咱们App.vue就拿来作为入口了，以后就让App.vue中干净一点**



**那么其他子组件了？** ----> **常规写好（写其他组件的时候，记得首字母大写），然后去注册，去确定好访问逻辑**

![1711000844251](E:\文档_Typora\1-关于怎么学会coding5.assets\1711000844251.png)





主组件中就写一点跳转，其他的工作，交给子组件去干

![1711002952956](E:\文档_Typora\1-关于怎么学会coding5.assets\1711002952956.png)



**组件的复用演示**

这种就是没有交给路由管理的普通组件了。



比如写一个页脚组件：

```vue
<script setup>
  export default {
  name:'Footer',
}
</script>

<template>
  <div>
    <h4>底部组件Footer,@copyright 杨枝</h4>
  </div>
</template>

<style scoped>

</style>

```



然后在`Home`组件中复用





##  二、脚手架实际的前后端分离项目

### 2.1、构建基本的Vue项目

使用如下指令进行项目初始化

```
vue init webpack 项目名
```

在管理员权限下的控制台中，进入这个项目，安装npm

```
npm install
```



启动项目

```
npm run start
```

然后把基本的架子搭建一下。

```js
import Vue from 'vue'
import Router from 'vue-router'
import Home from "../components/Home.vue";
import User from "../components/User.vue";
import Student from "../components/Student.vue";

Vue.use(Router)

export default new Router({
  routes: [
    {path: '/', redirect: '/home'},
    {path: '/home', component: Home},
    {path: '/user', component: User},
    {path: '/student', component: Student},
  ]
})

```

![1711064481968](E:\文档_Typora\1-关于怎么学会coding5.assets\1711064481968.png)







后面我我先停一下，我直接先把ElementUI搞定了，再回溯回来，其业务应该和之前的差不多，只是目前是交托给脚手架管理，有个发动请求的疑惑（怎么导入axios），其他的应该好解决，先把UI学了，再搞定这个，然后直接怼我自己的毕设了。





## 三、使用的问题汇总

> **·1、vue指令不能使用。**

突然有一天使用的时候，发现出现了：使用vue2脚手架时候出现了问题。我已经使用`npm install -g vue-cli`安装了脚手架，并且安装了node.js，也可以npm工具。但是当我在WebStorm的控制台中使用`vue init webpack element_sys`时，出现如下报错：

```
PS E:\develops\workspace_webstorm_vue1\vueDemo> vue init webpack element_sys
vue : 无法将“vue”项识别为 cmdlet、函数、脚本文件或可运行程序的名称。请检查名称的拼写，如果包括路径，请确保路径正确，然    
后再试一次。
所在位置 行:1 字符: 1
+ vue init webpack element_sys
+ ~~~
    + CategoryInfo          : ObjectNotFound: (vue:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

**怎么解决？**

这个问题可能是由于vue-cli没有被正确地添加到你的系统路径中。你可以尝试以下步骤来解决这个问题：  

- 首先，**你需要确认vue-cli是否已经被正确地安装**。你可以通过运行`npm list -g --depth=0`来查看全局安装的npm包。如果vue-cli在列表中，那么它已经被正确地安装。  
  ![1711182629839](E:\文档_Typora\1-关于怎么学会coding5-vue脚手架.assets\1711182629839.png)

- 如果vue-cli已经被正确地安装，**那么问题可能是它没有被添加到你的系统路径中【确实是之间的环境变量被我删除了（因为换了node_global的文件夹）】**。你可以通过运行`npm bin -g`来查看全局npm包的安装路径，然后将这个路径添加到你的系统环境变量中。  
  ![1711182708071](E:\文档_Typora\1-关于怎么学会coding5-vue脚手架.assets\1711182708071.png)

  **尝试去添加系统环境变量：**

  - 首先，复制你得到的路径E:\java\npmreps\global。  
    然后，右键点击电脑左下角的Windows图标，选择"系统"。  
    在新打开的窗口中，选择"关于"，然后点击"系统信息"。  
    在新打开的窗口中，选择"高级系统设置"。  
    在新打开的窗口中，选择"环境变量"。  
    在新打开的窗口中，找到系统变量中的"Path"，然后点击"编辑"。  
    在新打开的窗口中，点击"新建"，然后粘贴你之前复制的路径。  
    点击"确定"保存你的更改

- 如果以上步骤都不能解决问题，**你可以尝试重新安装vue-cli。首先，运行npm uninstall -g vue-cli来卸载vue-cli，然后运行npm install -g vue-cli来重新安装。** 

- 为什么需要添加环境变量？为什么要添加系统环境变量？
  环境变量是操作系统用来指定运行环境信息的一种参数。
  在这个问题中，我们需要将vue-cli的安装路径添加到环境变量中，这样当你在命令行中输入vue命令时，系统就能知道去哪个路径下找到这个命令并执行。  
  当你在命令行中输入一个命令时，系统会在环境变量Path指定的路径中寻找对应的命令。如果系统在这些路径中找不到对应的命令，就会返回一个错误，告诉你它无法识别这个命令。
  这就是你在运行vue init webpack element_sys时遇到的问题。  
  通过将vue-cli的安装路径添加到环境变量中，你就告诉了系统在哪里可以找到vue命令，从而可以在命令行中使用vue-cli











# Question













# Reference

介绍 | Vue CLI
https://cli.vuejs.org/zh/guide/

npm. 配置淘宝镜像方法 - 大雷小屋 - 博客园
https://www.cnblogs.com/bigron/p/17486819.html

06-npm下载依赖存放位置修改 - 猎奇游渔 - 博客园
https://www.cnblogs.com/haoqiyouyu/p/14728261.html

Windows命令行cmd之cd命令用法_cmd cd-CSDN博客
https://blog.csdn.net/zdy219727/article/details/98605287

用vue-cli搭建的vue项目怎么更改端口_vue-cli创建的项目在哪改端口-CSDN博客
https://blog.csdn.net/wys997/article/details/106491377

WebStorm创建Vue的template(模板) - 兔老大
https://www.r2coding.vip/articles/2022/04/30/1651248851007.html

cmd 如何查询vue版本和vue-cil（脚手架）版本_cmd查看vue版本-CSDN博客
https://blog.csdn.net/AdamMaoKkk/article/details/109355731

