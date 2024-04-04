>**`ElementUI相关的内容`**

# Start





# Body



## 一、ElementUI 引言

>Element：网站快速成型工具和基于 Vue 2.0 的桌面端组件库 。
>
>即，它就是基于Vue的UI框架，该框架提供了基于Vue开发的组件（看文档，找组件，完成需求），方便我们快速开发页面。



## 二、ElementUI安装

### 2.1、通过Vue脚手架创建项目

初始化项目

```
vue init webpack element
```

到项目目录中

```
npm install
```



启动项目

```
npm start
```

### 2.2、在Vue脚手架中安装ElementUI

**1、通过指令将ElementUI的依赖安装下来：**

```
npm i element-ui -S
```



nnd，我这个Node.js问题有点子大啊，只能在管理员权限下才可以npm 安装东西

先记录一下：

```
> y@1.0.0 start
> npm run dev


> y@1.0.0 dev
> webpack-dev-server --inline --progress --config build/webpack.dev.conf.js

(node:10040) [DEP0111] DeprecationWarning: Access to process.binding('http_parser') is deprecated.
(Use `node --trace-deprecation ...` to show where the warning was created)
 12% building modules 24/28 modules 4 active ...torm_vue1\vueDemo\element\src\App.vue{ parser: "babylon" } is deprecated; we now treat it as { parser: "babel" }.
 95% emitting                                                                        

 DONE  Compiled successfully in 2171ms                                                                            08:17:43

 I  Your application is running here: http://localhost:8081
Terminate batch job (Y/N)? y
PS E:\develops\workspace_webstorm_vue1\vueDemo\element> npm i element-ui -S
Active code page: 65001
npm ERR! code EPERM
npm ERR! syscall open
npm ERR! path E:\java\nodejs\node_cache\_cacache\tmp\9f6856ad
npm ERR! errno -4048
npm ERR! Error: EPERM: operation not permitted, open 'E:\java\nodejs\node_cache\_cacache\tmp\9f6856ad'
npm ERR!  [Error: EPERM: operation not permitted, open 'E:\java\nodejs\node_cache\_cacache\tmp\9f6856ad'] {
npm ERR!   errno: -4048,
npm ERR!   code: 'EPERM',
npm ERR!   syscall: 'open',
npm ERR!   path: 'E:\\java\\nodejs\\node_cache\\_cacache\\tmp\\9f6856ad'
npm ERR! }
npm ERR!
npm ERR! The operation was rejected by your operating system.
npm ERR! It's possible that the file was already in use (by a text editor or antivirus),
npm ERR! or that you lack permissions to access it.
npm ERR!
npm ERR! If you believe this might be a permissions issue, please double-check the
npm ERR! permissions of the file and its containing directories, or try running
npm ERR! the command again as root/Administrator.

npm ERR! Log files were not written due to an error writing to the directory: E:\java\nodejs\node_cache\_logs
npm ERR! You can rerun the command with `--loglevel=verbose` to see the logs in your terminal

```

**破案了，就是缓存惹得错**

删除`.nmprc`文件和控制台指令都试试

但是这个得配置被清了

![1711068480024](E:\文档_Typora\1-关于怎么学会coding6.assets\1711068480024.png)

感觉了一盘，原生npm的速度，太可爱了。

配置重新装了一下，舒服了。







**2、指定当前项目使用ElementUI**

>在main.js中

```js
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```



其实主要就是引入两句话，并将ElementUI交给Vue

```js
//引入样式和组件
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
```

注册进去

```js
Vue.use(ElementUI);
```



然后去文档扒拉自己组要的组件代码



## 三、ElementUI中组件的详细使用

>**`这里主要是在学如何看文档，通过文档来学习`**

### 3.1、按钮组件的详细使用

`日后视同element ui`的相关组件时需要注意的是：`所有组件爱你都是el-组件名`的形式

#### 3.1.1、创建按钮组件

```vue
 <el-button>默认按钮</el-button>
```

### 3.1.2、看文档，根据下面的属性列表写自己需要的东西

```vue
    使用按钮组件，直接去扒拉组件-->
    <el-button type="success">默认按钮</el-button>
    <el-button type="danger" size="small" plain=true icon="el-icon-s-goods">另一个按钮</el-button>
```

`可见，所有属性全部写在组件标签上的，并且使用的是`属性名=属性值`的方式直接写上。`

### 3.1.3、组合按钮的使用

这个在文档中有

```vue
    <el-button-group>
      <el-button type="primary" icon="el-icon-arrow-left">上一页</el-button>
      <el-button type="primary">下一页</el-button>
    </el-button-group>
```



### 3.2、文字链接组件

#### 3.2.1、使用流程：

也是官网上看文档，先创建默认的组件样式，然后看属性，调整出自己需要的属性状态。



### 3.2、布局组件

#### 3.2.1、创建Layout组件

`通过基础的 24 分栏，迅速简便地创建布局。 `。先划分为行row，再划分为24列/栏，通过 row 和 col 组件，并通过 col 组件的 `span` 属性我们就可以自由地组合布局，相当于之前的栅格。

即，在一个布局组件中，是有row和col组合而来的。

那么，在使用时要区分`row属性`和`col属性`。

```vue
  <div>
    <h1>布局组件</h1>
    <el-row>
      <el-col :span="8"><div style="border: 1px crimson solid">占有成8份</div></el-col>
      <el-col :span="8"><div style="border: 1px crimson solid">占有成8份</div></el-col>
      <el-col :span="8"><div style="border: 1px crimson solid">占有成8份</div></el-col>
    </el-row>
    <br>
    <el-row>
      <el-col :span="3"><div style="border: 1px coral solid">占有3份</div></el-col>
      <el-col :span="4"><div style="border: 1px coral solid">占有4份</div></el-col>
      <el-col :span="8"><div style="border: 1px coral solid">占有8份</div></el-col>
      <el-col :span="9"><div style="border: 1px coral solid">占有9份</div></el-col>
    </el-row>
  </div>
```

我主要想说一下通过`span`标签配合`v-bind：`绑定的事儿，因为直接传入单纯的数字`span=9`也可以，总之是通过`span`属性在管理，但是传入的是字符串的时候，就得绑定了。



#### 3.2.2、Layout组件的相关属性

![1711156034462](E:\文档_Typora\1-关于怎么学会coding6.assets\1711156034462.png)

![1711156055546](E:\文档_Typora\1-关于怎么学会coding6.assets\1711156055546.png)



### 3.3、布局容器组件

即，一般先划分容器，再到容器中累组件。

>在我们的系统重，一般是划分为头，左侧，中心，底部四个部分【模仿了】



![1711156624181](E:\文档_Typora\1-关于怎么学会coding6.assets\1711156624181.png)

>可以理解为一个容器是一行

![1711159273929](E:\文档_Typora\1-关于怎么学会coding6.assets\1711159273929.png)



#### 3.3.1、创建布局容器

```vue
    <el-container>
      <h2>我是容器组件</h2>
    </el-container>
```



#### 3.3.2、容器组件中包含子元素

>`<el-container>`：外层容器。当子元素中包含 `<el-header>` 或 `<el-footer>` 时，全部子元素会**垂直上下排列**，否则会水平左右排列。
>
>`<el-header>`：顶栏容器。
>
>`<el-aside>`：侧边栏容器。
>
>`<el-main>`：主要区域容器。
>
>`<el-footer>`：底栏容器。





#### 3.3.3、容器中的嵌套使用

>总之嵌套归嵌套，样式是需要自己一点一点的去调整的。

```vue
<template>
  <div>
    <el-container>
      <h2>我是容器组件</h2>
    </el-container>

    <br>
    <el-container>
      <el-header>
          <div><h3>标题</h3></div>
      </el-header>
<!--      这里的左侧菜单和中间主体就融合在一行了-->
      <el-container>
        <el-aside><div><h3>左侧菜单</h3></div></el-aside>
        <el-main><div><h3>主体内容</h3></div></el-main>
      </el-container>
    </el-container>

<!--    底部容器-->
    <el-container>
      <el-footer>
        <div><h3>底部</h3></div>
      </el-footer>
    </el-container>
  </div>
</template>

```

#### 3.3.3、容器的属性

### 3.4、Form相关组件

#### 3.4.1、Radio单选按钮

##### 3.4.1.1、创建单选按钮

**这里有个小细节：`在使用Radio单选按钮的时候，至少加入v-model和label属性。`**

```vue
<template>
  <div>
    <h2>单选按钮</h2>
    <el-radio v-model="label" label="男">男</el-radio>
    <el-radio v-model="label" label="女">女</el-radio>
  </div>
</template>
 data() {
    // 这里存放数据
    return {
      label:"男",
    }
  },
```



##### 3.4.1.2、Radio属性的使用

这里和之前的类似，也是`属性名=属性值`

##### 3.4.1.3、Radio事件的使用

>新东西来了

事件的绑定，我们在`vue`中最初学习的时候就是用的`v-on:事件名=“xxx事件函数”`或者`@`代替`v-on:`，例如`v-on:click="clickMe"`或者`@click="clickMe"`

这里也是类似。

- 事件的使用和属性的使用一致，都是直接卸载对应的组件标签上
- 事件在使用时，必须使用Vue中绑定时间方式进行使用，即`@事件名=事件处理函数（绑定在Vue组件中对应的函数）`



**到目前为止，先停一下。**



### 3.4.2、复选框组件

这里整体我觉得比较简答

### 3.4.3、input组件





## 四、ElementUI配合Vue综合案例

### 一、前台

#### 1、整体布局的搭建

搭建的目标：

![1711183989287](E:\文档_Typora\1-关于怎么学会coding6-ElementUI.assets\1711183989287.png)

**①划分基础的模块**

>**前台其实可以分为模块的，比如`用户模块`,`权限模块`、`订单模块`,每个模块创建对应的文件夹。在模块中又累加组件。**

即：

![1711187021940](E:\文档_Typora\1-关于怎么学会coding6-ElementUI.assets\1711187021940.png)



**②完成基本的骨架搭建**

去ELementUI偷代码了。

![1711187756801](E:\文档_Typora\1-关于怎么学会coding6-ElementUI.assets\1711187756801.png)

**③该思考点击这些菜单项之后，如何实现路由切换的问题了【需要借助点击事件了】**

官网上说了，`el-menu-item`中的属性中，`index`是唯一标识，通过console输出知道`键`是每一项的索引。

| index | 唯一标志 | string/null | —    | null |
| ----- | -------- | ----------- | ---- | ---- |
|       |          |             |      |      |

```js
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    }
  },
```

![1711188057326](E:\文档_Typora\1-关于怎么学会coding6-ElementUI.assets\1711188057326.png)

因此可以将路由作为参数传递进去，再切换。调整好：

![1711196736952](E:\文档_Typora\1-关于怎么学会coding6-ElementUI.assets\1711196736952.png)



#### 2、完成首页模块的组件开发

使用轮播图来展示图片。

**收获到一个细节：自己导入东西是在<script>标签中，但是在`expert defualt`之外**



#### 3、用户列表展示列表的开发

同样，找自己需要的样式，然后一点点调整。先把列表页面用假数据做好，再去根据这个页面写数据库的表以及写后端接口。务必先去测试能够拿到数据，再去开发控制器。

![1711200195637](E:\文档_Typora\1-关于怎么学会coding6-ElementUI.assets\1711200195637.png)

**后端开发好之间，就得前台发送axios请求了，vue-cli中得安装它了**

然后得引用

![1711201368808](E:\文档_Typora\1-关于怎么学会coding6-ElementUI.assets\1711201368808.png)



仍旧是在created()函数中使用，也就是在组件创建的时候就把这些数据请求发送了

![1711201318694](E:\文档_Typora\1-关于怎么学会coding6-ElementUI.assets\1711201318694.png)





### 二、后台

老规矩，去写后端接口，作为服务器，这里从控制持久层的模型到service层，再到视图层。











# Question











# Reference

npm install 报错（npm ERR! errno -4048，Error: EPERM: operation not permitted） - Letyo - 博客园
https://www.cnblogs.com/yaohe/p/11912547.html

组件 | Element —— link组件
https://element.eleme.cn/#/zh-CN/component/link

组件 | Element —— layout布局组件
https://element.eleme.cn/2.13/#/zh-CN/component/layout



​	