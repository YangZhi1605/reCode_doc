>**`九转轮回，可算回来了,启动`**

# Start



# Body

## 通识性认知

**前端和后端一般是指代码上技术上的区别；前台和后台一般是指展现形式的区别。** 

![1703751292091](E:\文档_Typora\关于怎么学会coding_任务规划篇.assets\1703751292091.png)

比如之前的学习中，我们对博客进行编辑的那些就是后台，既能够操纵数据，再交给前台展示处理的地方。

前台呢，直接拿给用户看的，后台了，是为了服务好拿给前台看的东西而进行工作的地方。经过后台的操作后，前台的东西就变了。前后台是只有`操作`而言的，是没有代码编辑这么一说的。代码编辑是在前端、后端这里的。人们省略了几个字，应该是前端工程师：写代码给浏览器‘吃’；后端工程师：写代码给服务器'吃'。



绝大多数情况下，互联网就是这样运行的——发东西给服务器，服务器再发回些什么东西。 

------

为了防止这两种不同的攻城狮工作内容串杂在一起，双方约定，定下一个发送请求的地址，和请求的格式，至此老死不相往来。这种请求的地址和其相应的格式，又被称为API（接口）。至此，做好API文档后，前端和后端终于可以老死不相往来，各自调试各自的代码。这一不相往来的概念，也被称为**前后端分离**。





## 前台

### 一、整体骨架的基本搭建

>也就是我要有哪些功能，然后根据这么功能去扒拉组件。



#### 1.1、开发环境的安装

**安装vuecli2的脚手架**

```
vue init webpack front_environ
```

进入这个文件目录，启动它：

```
  cd front_environ
  npm run dev 或者 npm start
```



**安装ELementUI**

```
npm i element-ui -S
```

在`main,js`中使用ELementUI

```
// 引入ElementUI
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'

//注册ElementUI
Vue.use(ElementUI)
```



**发送异步请求的axios的安装**

这里不通过`npm`搞（会报好多错），直接在`assets`目录下创建一个`dist`，然后把`axios.min,js`放进去

```
//引入axios
import axios from './assets/dist/axios.min'
//添加axios到Vue的原型中，这样在其他组件中就可以直接使用this.$axios
Vue.prototype.$axios = axios
```



#### 1.2、收获

>axios 提供了 `axios.min.js`，这是一个预编译的版本，不需要 Babel 转译就可以在 ES5 环境中运行。你可以直接将其导入到你的项目中。 



>`webpack.base.conf.js` 这个文件是你的基本的webpack配置，修改这个文件会影响到开发环境和生产环境的配置，因此你只需要修改这一个地方。







### 二、写每个页面在静态死数据下的页面



>**我目前的想法是：我能想出什么功能就写什么功能，能够设计是最好，假如实在不能设计，那就到处抄一下组件**



#### 2.1、首页写好，重定向写好



#### 2.2、抄Container 布局容器+导航条



![1711932295632](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1711932295632.png)

写各个页面下的展示内容的组件，这里就涉及到功能模块的问题了：

**我到底有些什么功能了？我是这个网站的用户，我想有些什么功能了？**

>——excel数据的上传，整理，可视化
>
>——excel数据的机器学习数据分析结果的展示
>
>



#### 2.3、首页展示可视化信息+附带分析结果

这里先把死的图片写了卡上。然后再通过后台传递数据，将真的数据更新进去。

**安装Echarts**

```
npm install echarts --save
```



**然后，您可以在需要使用的组件中导入Echarts：**

```
import * as echarts from 'echarts';
```

**在`mounted()`函数中，初始化Echarts实例** 

```
mounted() {
  this.chart = echarts.init(document.getElementById('graph'));
}
```

以上代码假定您的模板中有一个id为'graph'的元素作为图表的容器。 所以需要用到ELementUI的布局容器。

**根据官方文档，配合`setOption函数`来将实例化的结果展示出来：**

```
this.chart.setOption({
    title: {
      text: '示例图表'
    },
    tooltip: {},
    legend: {
      data:['销量']
    },
    xAxis: {
      data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
    },
    yAxis: {},
    series: [{
      name: '销量',
      type: 'bar',
      data: [5, 20, 36, 10, 10, 20]
    }]
  });
```

![1712130651137](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712130651137.png)

至于这里展示的数据，是需要经过分析之后，看怎么通过JSON传递回来。更新就好，即，**此部分的前台已经写好了**









#### 2.4、工作台拿给用户下载数据模板+用户上传数据+点击整理数据

我的想法是，为了不让页面看起来特别单调，让页面中展示一个图表，告诉用户，自己的数据格式如下面的图表：

![1712135625458](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712135625458.png)



>**我此时的设想是，我点击上传数据后，跳转到另一个页面中。此页面先展示综合性分析（先上结论）再是各种图的分析，首页那个就写一些炫酷的图，告诉用户，自己这个系统是拿来干嘛的。**

+

>**做一个页面负责设备维修信息日志**

+

>**可以点击购买自己需要的一些零件，自行维修。或者显示附近临近的修理店**



**`到目前为止，可以写后台的东西了。`**









## 后台

### 一、开发环境的搭建+跨域问题的解决

先按照自己的骨架，将后端开发出来吧。

![1712191762140](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712191762140.png)



### 二、将上面每个写死的页面写活起来

#### 2.1、首页

首页干什么？仿照这个排版，中间放置默认的数据进行动态展示（后续用户更新数据后，这里会随着更新）。周边放小的图+介绍这个系统在干嘛。

![1712136784215](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712136784215.png)

##### 2.1.1、动态折线图的研究处理思路

**需要安装JQuery：**

以通过npm的方式在基于Vue CLI 2搭建的项目中安装jQuery。要安装jQuery，您只需在项目的根目录下运行以下命令：

```
npm install jquery --save
```

一旦安装后，您可以在Vue组件中通过`import`语法引入jQuery： 

```
import $ from 'jquery';
```

**处理思路：**

```js
//官网源码
import * as echarts from 'echarts';

var ROOT_PATH = 'https://echarts.apache.org/examples';

var chartDom = document.getElementById('main');
var myChart = echarts.init(chartDom);
var option;

$.get(
  ROOT_PATH + '/data/asset/data/life-expectancy-table.json',
  function (_rawData) {
    run(_rawData);
  }
);
function run(_rawData) {
  // var countries = ['Australia', 'Canada', 'China', 'Cuba', 'Finland', 'France', 'Germany', 'Iceland', 'India', 'Japan', 'North Korea', 'South Korea', 'New Zealand', 'Norway', 'Poland', 'Russia', 'Turkey', 'United Kingdom', 'United States'];
  const countries = [
    'Finland',
    'France',
    'Germany',
    'Iceland',
    'Norway',
    'Poland',
    'Russia',
    'United Kingdom'
  ];
  const datasetWithFilters = [];
  const seriesList = [];
  echarts.util.each(countries, function (country) {
    var datasetId = 'dataset_' + country;
    datasetWithFilters.push({
      id: datasetId,
      fromDatasetId: 'dataset_raw',
      transform: {
        type: 'filter',
        config: {
          and: [
            { dimension: 'Year', gte: 1950 },
            { dimension: 'Country', '=': country }
          ]
        }
      }
    });
    seriesList.push({
      type: 'line',
      datasetId: datasetId,
      showSymbol: false,
      name: country,
      endLabel: {
        show: true,
        formatter: function (params) {
          return params.value[3] + ': ' + params.value[0];
        }
      },
      labelLayout: {
        moveOverlap: 'shiftY'
      },
      emphasis: {
        focus: 'series'
      },
      encode: {
        x: 'Year',
        y: 'Income',
        label: ['Country', 'Income'],
        itemName: 'Year',
        tooltip: ['Income']
      }
    });
  });
  option = {
    animationDuration: 10000,
    dataset: [
      {
        id: 'dataset_raw',
        source: _rawData
      },
      ...datasetWithFilters
    ],
    title: {
      text: 'Income of Germany and France since 1950'
    },
    tooltip: {
      order: 'valueDesc',
      trigger: 'axis'
    },
    xAxis: {
      type: 'category',
      nameLocation: 'middle'
    },
    yAxis: {
      name: 'Income'
    },
    grid: {
      right: 140
    },
    series: seriesList
  };
  myChart.setOption(option);
}

option && myChart.setOption(option);

```



根据您提供的官网实例代码，要将您现有的`chart1`替换为动态折线图，您需要进行以下步骤的更改：

1. 引入ECharts并获取数据。
2. 定义`run`函数，该函数将处理数据并生成ECharts的配置选项。
3. 在Vue组件的`mounted`生命周期钩子中初始化`chart1`。
4. 使用官网提供的配置设置`chart1`。

下面是您的Vue组件代码中内嵌动态折线图逻辑的方式，只是一个简化的示例，您会需要根据您的项目结构进行适当的修改：

```vue
<template>
  <div id="graph1" style="width: 600px;height:400px;"></div>
  <!-- 确保这里的ID与下面的getElementById一致 -->
</template>

<script>
import * as echarts from 'echarts';
import $ from 'jquery'; // 确保已经安装了jQuery

export default {
  mounted() {
    var self = this;
    var chartDom = document.getElementById('graph1');
    self.chart1 = echarts.init(chartDom);
    var option;

    $.get('https://echarts.apache.org/examples/data/asset/data/life-expectancy-table.json', function (_rawData) {
      run(self.chart1, _rawData);
    });

    function run(chart, _rawData) {
      // ... 这里是您复制的run函数内容，比如countries定义、datasetWithFilters、seriesList等 ...
    
      option = {
        animationDuration: 10000,
        // ... 这里是您复制的option配置内容 ...
      };
      
      chart.setOption(option);
    }
  }
};
</script>
```

注意：请确保在您的项目中已经安装了jQuery，因为官网示例中使用了`$.get()`。

还需要注意的是，原始的数据请求地址`ROOT_PATH`需要根据实际情况调整，确保数据能够正确加载。另外，确保`echarts`已正确安装，并且您的项目能够识别ES6的import语法。

发送GET请求嘛，那FLask的后台跑不脱了。写吧，不然就是跨域到Echarts的服务器了。

![1712201081094](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712201081094.png)

**写好了，准备推送到github上托管一下，再考虑让数据一直动态更新的事儿**



##### 2.1.2、Github托管

暂时不在软件中托管。直接使用的Bash界面进行的托管。



##### 2.1.3、编写循环动态展示 —— 未实现

并未实现循环播放，但是我想想，只要我的数据足够多，按照那种JSON排列出来，在我演示的时候一直是跑着的，动态获取的，那就是实时获取。

```vue
mounted() {
  var _this = this; // 将Vue实例的this赋值给_this变量，以便在函数回调中使用。
  var chartDom = document.getElementById('graph1'); // 根据ID获取DOM元素，该元素是要初始化图表的容器。
  _this.chart1 = echarts.init(chartDom); // 初始化echarts实例，将它赋值给Vue实例的chart1属性。

  // 初始请求数据并且创建图表
  _this.fetchDataAndUpdateChart();

  // 设置定时器每隔一段时间更新图表数据
  _this.interval = setInterval(() => {
    _this.fetchDataAndUpdateChart();
  }, 3000);  // 这里的3000是更新数据的时间间隔，单位毫秒
},

// 在Vue实例的methods中添加数据获取和图表更新的方法
methods: {
  fetchDataAndUpdateChart() {
    $.get('http://127.0.0.1:5000/lineRace', (rawData) => {
      this.run(this.chart1, rawData); 
    });
  },
  run(chart, rawData){
    // 省略具体的图表配置和数据处理...
    chart.setOption({
      // 您的 ECharts 配置对象
    });
  }
},

beforeDestroy() {
  // 清除定时器
  clearInterval(this.interval);
}
```



##### 2.1.4、写用户在前台下载后台的数据模板

`send_file` 不是需要单独安装的模块，它是 Flask 框架内置的一个函数。这个函数归属于 `flask` 模块，主要用于在 Flask 应用中发送文件到客户端。

**`搞定，既然是用户下载，那么可以搞一个数据表，统一用户的下载次数` —— 后端的功能又增加了**

![1712215862093](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712215862093.png)





##### 2.1.5、写用户在前台上传数据到后台，后台得到之后，进行持久化

这里得使用数据库连接池了，应该。



















# Question

> 1、首先需要思考的问题是：我的考虑需要不需要提升到vue3？

我是学的Vue2的脚手架，但是现在应用更多的是Vue3的脚手架。

老项目大多数是Vue2，新的项目，比如我今天看到的，几乎都是Vue3的东西。

那么，Vue2和Vue3在使用上有什么区别了？



>Node和npm的关系是什么了？

npm应该是node下的一个管理工具，之后后面被普及化了。



>nvm/nodejs/npm/npx区别是什么？

**`nodejs`**是js的运行环境,能将js代码编译成计算机能识别的代码,在没有nodejs前,这个过程是浏览器完成的,nodejs把js从浏览器中解放出来,使js不仅能在浏览器中执行,也能在任何装有nodejs环境中去执行,nodejs使得我们能够使用js开发web服务端

 **`nvm`**是node version management,是node版本管理工具,nodejs更新较快,nvm把不同版本的nodejs都安装到本地,然后根据项目中使用到的不同版本的nodejs去切换版本 

**`npm`**是node package management是nodejs中第三方插件的管理工具 

**`npx`**是npm5.6之后自带的一个命令,npm会把依赖下载到本地,形成一个node_modules文件,执行npx命令时,会先到项目文件夹中去找,没有的话再下载到内存里,执行完命令后就会马上删除掉依赖,不会侵入源代码 











# Reference

AugustLYH1998/VUE2-vuecli2-ElementUI-ECharts: VUE2+vuecli2+ElementUI+ECharts后端管理系统 —— 这个demo蛮详细的，vue2
https://github.com/AugustLYH1998/VUE2-vuecli2-ElementUI-ECharts#%E4%B8%80%E9%A1%B9%E7%9B%AE%E5%88%9D%E5%A7%8B%E5%8C%96

前端项目不要再问用的是Vue2还是Vue3了，不重要且显得特别小白_哔哩哔哩_bilibili —— 大部分公司还是用的vue2
https://www.bilibili.com/video/BV133411S76P/?spm_id_from=333.337.search-card.all.click&vd_source=be8081cb351e616080452087e4f6f6b3

配置SumatraPDF快捷键实现Pdf阅读快速标注 - 知乎 —— 这个拿来高亮批注PDF挺不错的。
https://zhuanlan.zhihu.com/p/613119812

如何用sklearn对随机森林调参? - 知乎
https://zhuanlan.zhihu.com/p/126288078

【一图】看懂 nvm/nodejs/npm/npx 的联系和区别！_哔哩哔哩_bilibili
https://www.bilibili.com/video/BV13Q4y1K7dD/?spm_id_from=333.337.search-card.all.click&vd_source=be8081cb351e616080452087e4f6f6b3

什么是前台？什么是中台？什么是后台？_什么是后台?-CSDN博客
https://blog.csdn.net/weixin_42826672/article/details/103406132

前端，后台，后端，前台他们区别是什么？ - 小辣椒樱桃 - 博客园
https://www.cnblogs.com/aaaazzzz/p/13023372.html

如何 将不同机器学习算法集成 - Google Search —— 对集成学习的汇总。
https://www.google.com/search?q=%E5%A6%82%E4%BD%95+%E5%B0%86%E4%B8%8D%E5%90%8C%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0%E7%AE%97%E6%B3%95%E9%9B%86%E6%88%90&oq=%E5%A6%82%E4%BD%95+%E5%B0%86%E4%B8%8D%E5%90%8C%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0%E7%AE%97%E6%B3%95%E9%9B%86%E6%88%90&gs_lcrp=EgZjaHJvbWUyBggAEEUYOdIBCjc5MzAzajBqMTWoAgCwAgA&sourceid=chrome&ie=UTF-8#ip=1

机器学习 | 基础通俗讲解集成学习算法！ - 知乎
https://zhuanlan.zhihu.com/p/150457320

Examples - Apache ECharts——动态折线图
https://echarts.apache.org/examples/zh/editor.html?c=line-race

