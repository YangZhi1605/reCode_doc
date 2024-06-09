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





根据路由出口调整了前台的页面展示：

![1714620834334](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1714620834334.png)





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



#### 2.3-1、首页优化整顿

>首页我想模仿ELementUI的首页界面。



![1712803719569](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712803719569.png)

![1712803794751](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712803794751.png)

也就是这种，有大字介绍，有引导。

**优化完毕**

![1712817182325](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712817182325.png)







#### 2.3-2、首页数据写活

只是把中间的动态播报图写活，其他的保持死的，做一个装饰即可。以及我差一个说明查看的内容。

它的数据格式是这种的：

相同的`year`下有20个国家的数据。

```
[
    [——①
        "Income",
        "Life Expectancy",
        "Population",
        "Country",
        "Year"
    ],
    [——②
        815,
        34.05,
        351014,
        "Australia",
        1800
    ],
    [——③
        1314,
        39,
        645526,
        "Canada",
        1800
    ],
    [——④
        985,
        32,
        321675013,
        "China",
        1800
    ],
    [——⑤
        864,
        32.2,
        345043,
        "Cuba",
        1800
    ],
    [——⑥
        1244,
        36.5731262,
        977662,
        "Finland",
        1800
    ],
    [——⑦
        1803,
        33.96717024,
        29355111,
        "France",
        1800
    ],
    [——⑧
        1639,
        38.37,
        22886919,
        "Germany",
        1800
    ],
    [——⑨
        926,
        42.84559912,
        61428,
        "Iceland",
        1800
    ],
    [——⑩
        1052,
        25.4424,
        168574895,
        "India",
        1800
    ],
    [——11
        1050,
        36.4,
        30294378,
        "Japan",
        1800
    ],
    [——12
        579,
        26,
        4345000,
        "North Korea",
        1800
    ],
    [——13
        576,
        25.8,
        9395000,
        "South Korea",
        1800
    ],
    [——14
        658,
        34.05,
        100000,
        "New Zealand",
        1800
    ],
    [——15
        1278,
        37.91620899,
        868570,
        "Norway",
        1800
    ],
    [——16
        1213,
        35.9,
        9508747,
        "Poland",
        1800
    ],
    [——17
        1430,
        29.5734572,
        31088398,
        "Russia",
        1800
    ],
    [——18
        1221,
        35,
        9773456,
        "Turkey",
        1800
    ],
    [——19
        3431,
        38.6497603,
        12327466,
        "United Kingdom",
        1800
    ],
    [——20
        2128,
        39.41,
        6801854,
        "United States",
        1800
    ],
    [
        834,
        34.05,
        342440,
        "Australia",
        1810
    ],
    [
        1400,
        39.01496774,
        727603,
        "Canada",
        1810
    ],
    [
        985,
        32,
        350542958,
        "China",
        1810
    ],
    [
        970,
        33.64,
        470176,
        "Cuba",
        1810
    ],
    [
        1267,
        36.9473378,
        1070625,
        "Finland",
        1810
    ],
    [
        1839,
        37.4,
        30293172,
        "France",
        1810
    ],
    [
        1759,
        38.37,
        23882461,
        "Germany",
        1810
    ],
    [
        928,
        43.13915533,
        61428,
        "Iceland",
        1810
    ],
    [
        1051,
        25.4424,
        171940819,
        "India",
        1810
    ],
    [
        1064,
        36.40397538,
        30645903,
        "Japan",
        1810
    ],
    [
        573,
        26,
        4345000,
        "North Korea",
        1810
    ],
    [
        570,
        25.8,
        9395000,
        "South Korea",
        1810
    ],
    [
        659,
        34.05,
        100000,
        "New Zealand",
        1810
    ],
    [
        1299,
        36.47500606,
        918398,
        "Norway",
        1810
    ],
    [
        1260,
        35.9,
        9960687,
        "Poland",
        1810
    ],
    [
        1447,
        29.5734572,
        31088398,
        "Russia",
        1810
    ],
    [
        1223,
        35,
        9923007,
        "Turkey",
        1810
    ],
    [
        3575,
        38.34738144,
        14106058,
        "United Kingdom",
        1810
    ],
    [
        2283,
        39.41,
        8294928,
        "United States",
        1810
    ],
]
```



代码解读：

```vue
mounted(){
    var _this = this; // 将Vue实例的this赋值给_this变量，以便在函数回调中使用。
    var chartDom = document.getElementById('graph1'); // 根据ID获取DOM元素，该元素是要初始化图表的容器。
    _this.chart1 = echarts.init(chartDom); // 初始化echarts实例，将它赋值给Vue实例的chart1属性。
    var option; // 声明一个变量option，后面会用来存储echarts的配置项。

    // 初始请求数据并且创建图表
    _this.fetchDataAndUpdateChart();
}
methods: {
    //编写获取数据和图表更新的方法
    fetchDataAndUpdateChart() {
      $.get('http://127.0.0.1:5000//api/lineRace', (rawData) => {
        this.run(this.chart1, rawData);
      });
    },
    //编写其调用的run方法
    run(chart, rawData) {
      //这里吧啦吧啦的写自己需要定义的数据
      //写自己需要跑的数据
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

      echarts.util.each(countries,function (country) {
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

      //option配置
      const option = {
        animationDuration: 10000,
        dataset: [
          {
            id: 'dataset_raw',
            source: rawData
          },
          ...datasetWithFilters
        ],
        title: {
          text: '电路信息实时播报'
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
          name: '电压'
        },
        grid: {
          right: 140
        },
        series: seriesList
      };

      chart.setOption(option);
    },
  },
```



大致搞懂了，它的JSON数据很负责，但是它只是选了其中8个国家的收入作为展示，展示的时候，挂载了时间轴，时间数据是从1800到2015.但是它设定的Get起点是1950.

>**那么，我只用把我八条电路的输入电流数据展示出来。按照批次来，从1开始，每一批都是它们八个，然后从10000批。**

```
[
        "VoltageVal",
        "VoltageName",
        "num"
    ],
    [
        388.47,
        "circuit1",
        1
    ],
     [
       	364.95,
        "circuit2",
        1
    ],
     [
       	388.54,
        "circuit3",
        1
    ],
    [
       	385.38,
        "circuit4",
        1
    ],
    [
       	389.17,
        "circuit5",
        1
    ],
    [
       	343.38,
        "circuit6",
        1
    ],
    [
       	370.35,
        "circuit7",
        1
    ],
    [
       	398.6,
        "circuit8",
        1
    ],
    [
       	363.77,
        "circuit1",
        2
    ],
     [
       	392.98,
        "circuit2",
        2
    ],
     [
       	390.63,
        "circuit3",
        2
    ],
     [
       	355.45,
        "circuit4",
        2
    ],
     [
       367.37,
        "circuit5",
        2
    ],
     [
       	342.16,
        "circuit6",
        2
    ],
     [
       	386.37,
        "circuit7",
        2
    ],
     [
       	364.77,
        "circuit8",
        2
    ],
    
 ]
```

完成需求的函数：

```
def format_voltages(voltages):
    # 存储格式化后的电压
    formatted_voltages = []
    # 创建表头信息
    header = ["VoltageVal", "VoltageName", "num"]
    # 将表头信息加入结果列表
    formatted_voltages.append(header)
    
    # 批次的编号
    batch_num = 1
    
    for voltage_tuple in voltages:
        for index, voltage in enumerate(voltage_tuple):
            # 创建电压列表，并将它们添加到结果列表中
            circuit_name = f"circuit{index + 1}"
            # 忽略零值的电压（如果电压实际可以为0，删除此行）
            if voltage != 0:
                formatted_voltages.append([voltage, circuit_name, batch_num])
        # 更新设备编号
        batch_num += 1
    
    return formatted_voltages

# 使用get_odd_voltages类方法获取数据
voltages = Device.get_odd_voltages()
# 调用格式化函数
formatted_voltages_dict = format_voltages(voltages)
# 使用Flask jsonify来转换为JSON格式
from flask import jsonify
json_response = jsonify(formatted_voltages_dict)
```



**现在拿到指定的JSON数据了，需要修改动态折线图的信息，然后展示我需要展示的列。——完成**



**对使用建议进行逐字输出：**

```
<template>
  <div>{{ typewriterText }}</div>
</template>

<script>
export default {
  data() {
    return {
      text: 'Hello, this is a typewriter effect in Vue!',
      typewriterText: '',
      delay: 150, // 控制每个字符的输出速度
    };
  },
  mounted() {
    this.runTypewriter();
  },
  methods: {
    runTypewriter() {
      let i = 0;
      const typing = () => {
        if (i < this.text.length) {
          this.typewriterText += this.text.charAt(i);
          i++;
          setTimeout(typing, this.delay);
        }
      };
      typing();
    }
  }
};
</script>
```





写后端嘛，

也就是`Model`层创建模型，并写好对应的类方法。

>使用SQLAlchemy，记得设置好配置文件。并在初始化文件中，加载配置文件



>写好模型，需要写操作数据库数据的类方法。这里需要用到测试的东西了【又忘记了】



`servicec`层了，配合SQLAlchemy的模型，实现xx功能。

`controller`层再调用`service`层，实现业务需求，响应接口、





#### 2.4、下载数据模板+用户上传数据+点击整理数据

我的想法是，为了不让页面看起来特别单调，让页面中展示一个图表，告诉用户，自己的数据格式如下面的图表：

![1712135625458](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712135625458.png)



>**我此时的设想是，我点击上传数据后，跳转到另一个页面中。此页面先展示综合性分析（先上结论）再是各种图的分析，首页那个就写一些炫酷的图，告诉用户，自己这个系统是拿来干嘛的。【搞定】**

+

>**做一个页面负责设备维修信息日志**

+

>**可以点击购买自己需要的一些零件，自行维修。或者显示附近临近的修理店**



**`到目前为止，可以写后台的东西了。`**

#### 2.4-1、将用户上传数据界面写漂亮

**首先是对数据表的内容展示。在点击整理表格信息后，将数据库中的存储的信息展示出来。在整理文件的POST请求中，再发送一次GET请求，然后再处理一次回调函数，在回调函数中拿到需要的数据。**

```
this.$axios.post('http://127.0.0.1:5000/api/organizeExcel', { filename: file.name })
  .then(response => {
    // 第一个请求成功，接下来发起第二个请求
    this.$message.success('第一个请求成功，文件整理中！');
    // 发起第二个请求
    return this.$axios.get('http://127.0.0.1:5000/api/someOtherEndpoint');
  })
  .then(response => {
    // 第二个请求也成功了
    this.$message.success('第二个请求成功，文件整理完成！');
  })
  .catch(error => {
    // 捕获第一个或第二个请求中的任何错误
    this.$message.error('请求失败！');
    console.error('Error:', error);
  });
```

![1712842296545](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712842296545.png)

使用组件进行绑定，都不用使用vue的双向绑定了。

>当`el-table`元素中注入`data`对象数组后，在`el-table-column`中用`prop`属性来对应对象中的键名即可填入数据，用`label`属性来定义表格的列名。可以使用`width`属性来定义列宽。 

![1712843934968](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712843934968.png)

**目前是后端数据显示成功了：**

![1712843954794](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712843954794.png)





**尝试分页展示：**





此时是需要对这些数据进行**增删改查**。

>**调整一下用户上传后存储数据的数据库和对应数据表，统一到graduate数据库中。数据库连接池，以及SQLAlchemy的配置文件中，全部指向graduate数据库**



**`先写删除`**

```
from flask import jsonify, Blueprint
from your_service_module import User_Upload_Service

# 假设这是您的蓝图对象，您需要确保在您的应用中正确地进行了定义和注册
api_data_op = Blueprint('data_operation', __name__)

# 创建 User_Upload_Service 类的实例
upload_service = User_Upload_Service(data_dao_instance)

# 视图控制层函数 —— 这里用的DELETE，不太熟悉
@api_data_op.route('/api/deleteData/<int:item_id>', methods=['DELETE'])
def delete_item(item_id):
    try:
        # 使用服务层方法来执行删除操作
        upload_service.delete_info(item_id)
        # 如果没有异常被抛出，则认为删除成功
        return jsonify({'message': 'Data deleted successfully', 'id': item_id}), 200
    except Exception as e:
        # 发生任何异常时返回错误信息和500内部服务器错误状态码
        return jsonify({'message': 'Deletion failed', 'error': str(e)}), 500
```







​	**`写搜索功能`**

>**根据DeviceName和电压进行搜索**

**完成**



**`写编辑功能`**

可以跳转到相应组件，也可以写对话框来实现。直接用组件，因为可以多几个页面了...

实现将点击编辑后的行元素传递过来，并且展示出来了

![1712892705238](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712892705238.png)

下面我需要做的是，传递ID到后端，实现更新数据。

![1712899066716](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712899066716.png)

**更新成功。**

以及点击返回页面，重新加载展示数据库中的信息，这里需要有一个标记，如果是经过提交数据后，返回才读取，不然是相当于点进来看看，返回到数据上传页面是没有数据整理的，所以不读取。



>为了实现这个需求，我需要用到生命周期函数，也就是在TableCom组件创建时候，看看有没有经过update过的数据，倘若有工作台3返回过来的数据，就展示。



gpt提供了如下回复：

是的，当你从 `wrben/wrben3` 路由通过 `this.$router.push()` 方法跳转回 `wrben/wrben1` 路由时，并不会导致 `TableCom` 组件重新创建，因为它已经在之前被创建过。然而，Vue 提供了一个叫做 `watch` 的选项，可以用来监听路由的变化。

如果你想在路由变化时做一些操作，比如刷新表格数据，你可以在 `TableCom` 组件中添加一个 `watcher` 来监听 `$route` 对象，当检测到路由变化时执行相应的方法：

>**按照他说的，我并没有实现，我换一种逻辑，每次进入这个页面，并且上传文件被点击过，那么就显示**



我放弃了，写一个刷新按钮，更新之后刷新一下。

**写分页功能**

```

export default {
  name: 'TableCom',
  // import 引入的组件需要注入到对象中才能使用
  components: {},
  props: {},
  data() {
    return {
      tableData: [],
      fileList: [], // 用于维护上传文件列表的数组
      logInfo:{}, //用于维护日志信息
      searchVal:'',//搜索框输入的内容
      isShowTable:false,//标记'上传文件'是否被上传过了
      isShow:true,
      currentPage: 1, // 当前页码
      pageSize: 10, // 每页显示条数
    }
  },
    computed: {
    getPagedTableData() {
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.tableData.slice(start, end);
    }
  },
      //分页功能
    //挂载在size-change事件上，当pageSize改变时候，改变每一页显示条目个数
    handleSizeChange(newSize) {
      this.pageSize = newSize;
      // 当 pageSize 变化时，可能需要重新加载数据
    },
    //挂载在current-change事件上，当currentPage改变时候，改变当前页码
    handleCurrentChange(newPage) {
      this.currentPage = newPage;
      // 当当前页码变化时，可能需要重新加载数据
    },
}
```



#### 2.4-2、完成数据处理板块。对ELementUI的分页功能着重理解

> **首先明白一般的表格怎么展示的了？**

也就是将我们需要展示的数据`tableData`直接挂载在表头的`:data=xxx`处。然后通过`prop`指定传递数值的字段名，这里一定要和`tableData`中字段名一致。

```
<template>
  <div>
<!--    这里写一个表格组件，先展示假数据，当用户下载自己数据模板，将数据填进去，上传之后，再进行更新展示部分-->
    <el-row>
      <el-col :span="24">
        <el-table
          :data="tableData"
          border
          stripe
          style="width: 100%">
          <el-table-column
            fixed
            prop="ID"
            label="ID"
            width="150">
          </el-table-column>
         //其他类似
        </el-table>
        <!-- 分页组件 -->
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[10]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="tableData.length">
        </el-pagination>
      </el-col>
    </el-row>

  </div>
</template>
```



> **当然，这也就导致了，假如有10000条，整个页面全部都是这些数据，为了实现精美的展示，我们开始使用分页组件。**

```js
<el-pagination
    @size-change="handleSizeChange"
    @current-change="handleCurrentChange"
    :current-page="currentPage"
    :page-sizes="[10,20,30,40]"
    :page-size="pageSize"
    layout="total, sizes, prev, pager, next, jumper"
    :total="tableData.length">
</el-pagination>

  data() {
    return {
      tableData: [],
      fileList: [], // 用于维护上传文件列表的数组
      logInfo:{}, //用于维护日志信息
      searchVal:'',//搜索框输入的内容
      isShowTable:false,//标记'上传文件'是否被上传过了
      isShow:true,
      currentPage: 1, // 当前页码
      pageSize: 10, // 每页显示条数
    }
  },
```

这个组件直接放到放到表格下方就可以了。

分页组件我觉得比较让人头大的是它的属性和事件相对比较多。

上面代码片段中的。

layout是分页组件展示的一些信息，不用管。

total则是计算数据的总数。不用管

`currentPage`和`pageSize`是通过v-bind绑定到data中的数据了。这里可以自己定义当前起点是哪一页，每一页默认的多少数量，比如默认是10，当然，ELementUI比较灵性，这个10建议是`page-size`数组中的一部分，这种就可以跟换展示范围了。

**其他的，关心这两个事件函数。**

```js
export default {
  // ...
  methods: {
    // 当 pageSize 变化时触发此方法
    handleSizeChange(newSize) {
      this.pageSize = newSize;
      this.currentPage = 1; // 更改每页大小时重置当前页码到第一页
    },
    // 当 currentPage 变化时触发此方法
    handleCurrentChange(newPage) {
      this.currentPage = newPage;
    },
    // ... 其他方法
  },
  // ...
}
```



实际上，`@size-change`和`@current-change`事件处理器确实会从分页组件接收参数。

`el-pagination`组件的`size-change`事件将传递新的`pageSize`作为参数，而`current-change`事件将传递新的`currentPage`作为参数。

 

示例是正确的。这些参数并不需要你在模板里显式地写出来，它们是由组件内部自动传递的。

当你在模板中使用`@size-change="handleSizeChange"`时，实际上是在指定当分页组件中的页面大小变化时，调用名为`handleSizeChange`的方法，并传递新的页面大小作为参数给这个方法。

同样，`@current-change="handleCurrentChange"`会在分页组件的当前页发生变化时调用`handleCurrentChange`方法，并传递新的`currentPage`作为参数。

 

在 Vue.js 中使用事件处理器时，如果事件将参数传递给方法，无需在模板中指定参数。这是因为 Vue 会自动将事件的参数传递给方法。



**剩下就是一个核心函数了**

```js
computed: {
    // 计算当前页显示的数据
    /*
    * 这里的 getPagedTableData 是一个计算属性，
    * 它会根据当前页 currentPage 和每页大小 pageSize 来
    * 动态计算当前页所要显示的表格数据切片。
    * 当页码或每页条数发生变化时，el-pagination 组件将会
    * 触发 handleSizeChange 或 handleCurrentChange 方法，
    * 并且你可以在这些方法中处理页码变化*/
    getPagedTableData() {
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.tableData.slice(start, end);
    }
  },
```

这个切片函数需要替代原本的`tableData`，才能将切片结果也就是分页展示出来。





**表格这里有一个提交是空，我没有处理**



#### 2.4-3、美化表格+处理最初序号的问题

先处理序列号的问题。

我当前的表格中，我的序号是根据读取数据库后，得到的tableData对象中的ID属性，展示相应的值，是数据表的主键ID。因为它是自增长逐渐，所以读取出来的数据不是联系的1、2、3、4的形式。我该如何如何调整才能够实现无视数据表的主键ID，在进行随意删除之后。表格仍然是升序排列？

**——> 处理方式是专门写一个用来生成序号的事件函数。然后我的删除是根据数据库对象的ID进行的。这里不会影响到ID。**



**至于美化，就这种了。**



#### 2.4-4、数据可视化数据写活

##### ① AQI折线图

>随机切割6000条数据出来，然后怎么嵌套到这个范围中了？这个范围表示一危险的指数，那么我预测分析的结果，怎么扣合这个分析结果了？一条一条的拿给模型分析吗？按照：完美、健康、中等、轻微严重、十分严重来划分区间，划分之后，在每个区间中取随机数。
>
>然后都暂时不用机器学习，直接用统计分析，看那个阶段的多。



**`先研究实例代码的数据格式`**

==tips:顺带搞定了github不能存储前台代码的原因，因为是我之前拉取的其他项目中设置了不用`git add`。根据提示删除那个`VueAdmin`后搞定了。==

**一、研究数据格式**

目前的数据格式是这种的：

```
[
    [
        "2000-06-05",
        116
    ],
    [
        "2000-06-06",
        129
    ],
    [
        "2000-06-07",
        135
    ],
        [
        "2015-02-22",
        158
    ],
    [
        "2015-02-23",
        86
    ],
    [
        "2015-02-24",
        207
    ]
]
```

即从2000-06-05开始到2015-02-24结束

![1712975980496](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712975980496.png)

其自己指定的轴是从`2014-06-01`开始zoom的开始。

那么，我的数据，我需要做的是对电压进行健康状态分析【判断健康的标准从数据库中读取】，将健康状态分为：`：完美、健康、中等、轻微严重、十分严重`五档，在五档内容中生存随机数，x轴了？我的x轴怎么设置。

我的一行数据，综合来看8条路的权重，每条最后可以得到一个健康与否的分析。那么我就有多少条，我就展示多少吧。

那么具体怎么算？

看看已有的采集数据，就知道怎么分析每一批采集和该批采集中的8条电路健康状态了。

| 输入电压 | 输出电压 | 电压差 | 电压比率（电压差/输入电压*100%） |
| -------- | -------- | ------ | -------------------------------- |
| 4.67     | 4.82     | 0.15   | 3.21%                            |
| 4        | 4.12     | 012    | 3.00%                            |

根据我的计算。在正常情况下，电压比率应该是`3.38%`。

因此，对于每条电路，都计算电压比率。然后再根据8条电路的权重，计算加权平均数，得到最后的综合性结果。

**完美：3.3%~3.4%;**

**健康：3.1%~3.5%;**

**正常：3.0%~3.6%;**

**轻微严重：2.8%~3.0%以及， 3.6%~3.85%；**

**十分严重：≤2.8%或者≥3.9%**

**`如果输入电压高于输出电压，直接定义为十分严重，都不用展开计算了。`**

那么，我每条路都是可以得到得到一个计算结果。再根据【权限数据库】，计算这一行的加权平均数结果，比如是3.2%。那么就可以定标到健康，并生成一个该范围内的随机数，存储到相应数据库中。

**二、搞出我自己的适配的数据格式**

==现在就是，计算每行数据的8条电路电压比率。然后再调用数据库中的权重，计算最后的电压比率。==

```
# 假设 data 是从数据库取出的数据列表
data = [
    # ... 您的数据库信息 ...
]

# 结果列表，将包含每行数据的所有电压比率
all_voltage_ratios = []

# 为每行数据计算电压比率
for item in data:
    # 存储单行数据的电压比率
    voltage_ratios = []
    # 按对计算电压比率，从Voltage1/Voltage2 到 Voltage15/Voltage16
    for i in range(1, 16, 2):
        Vin = item[f'Voltage{i}']
        Vout = item[f'Voltage{i+1}']
        ratio = cal_voltage_ratio(Vin, Vout)
        voltage_ratios.append(ratio)
     # 遍历电路权重数据表，将电路权重乘以电压比率
        for item in data_weight:
          # 如果数据表中的IsSet为1，表示该行数据有效，则进行加权计算
            if item['IsSet'] == 1:
                # 从Circuit1到Circuit8
                for i in range(1, 9):
                    # 拿voltage_ratios列表中的信息，计算加权后的电压比率
                    voltage_ratios[i - 1] *= item[f'Circuit{i}']
                    # 结果保留四位小数
                    voltage_ratios[i - 1] = round(voltage_ratios[i - 1], 4)
    # 将单行的电压比率列表加入到结果列表
    all_voltage_ratios.append(voltage_ratios)

# 打印或返回结果
print(all_voltage_ratios)
```

加权平均数计算成功。生成对应范围的随机数成功。数据格式整理成功。返回前台展示成功。

**数据重新注入完毕了。现在需要管理权限**

| 名称 | 权重 |
| ---- | ---- |
| 1路  | 0.2  |
| 2路  | 0.2  |
| 3路  | 0.15 |
| 4路  | 0.1  |
| 5路  | 0.05 |
| 6路  | 0.1  |
| 7路  | 0.12 |
| 8路  | 0.08 |

**三、检验成果**

![1713061442416](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713061442416.png)

终于tm对了，加权平均数计算错了，nnd。这里最后就输出哪个阶段的评分最多即可。

**`加权平均数：将各数值乘以相应的权数，然后加总求和得到总体值，再除以总单位数`**。 





##### ② 写饼状图

**一、研究当前的数据格式**

```
pieData:[
        { value: 1048, name: 'Terminal-1' },
        { value: 735, name: 'Terminal-2' },
        { value: 580, name: 'Terminal-5' },
        { value: 484, name: 'Terminal-6' },
        { value: 900, name: 'Terminal-8' }
      ],
```

似乎这里的数据格式简单。统计出条磨损最为严重的电路即可。

回到我的本职工作：定义怎么计算磨损

>电池接线柱磨损之后，其实是传送电流的能力下降了。
>
>那么。也就是传输电流出去的能力下降了。
>
>比如Voltage1，一般而言，它们两次电流输出的结果应该在某个范围内浮动。但是当某两次输出结果出现了异常浮动。那么这异常浮动就值得注意了，统计这个异常浮动的次数，就是饼状图的磨损信息了。
>
>我现在需要看看，我的数据在哪些范围内的比较的多。然后框定数值。

**二、搞出我自己的数据格式**

```
def get_top_five_values(formatted_data):
    # 根据'value'键值对列表进行排序，设置reverse=True表示降序排列
    sorted_data = sorted(formatted_data, key=lambda x: x['value'], reverse=True)
    # 获取排序后的前五个元素，即'value'最大的五个元素
    top_five = sorted_data[:5]
    return top_five

# 假定formatted_data是前面函数的返回值
# 使用新函数筛选出'value'最大的五个元素
top_five_results = get_top_five_values(formatted_results)

# 打印结果
for item in top_five_results:
    print('得到的top 5结果：', item)
```

**三、完成**

![1713086877531](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713086877531.png)

**完成。这里最后就输出哪个接线柱的磨损最大，提醒用户去检修。**

##### tips:心得体会

今天写的逐步处理后端数据库的数据信息到自己想要的结果：

① 当出现高耦合的时候，注释写好，传入参数是什么，返回值什么。

② 当嵌套调用的时候，函数返回的结果最后不要乱写，因为容易分不清这个数据到底是干嘛的。就按照返回值命名，同时，返回值取名字的时候，取清晰一点，写长一点都不影响，一定得读了之后就知道在干嘛。

##### ③ 写堆叠图

**一、先研究当前有的数据格式**

它的数据简单：

```
 series: [
 {
      data: [140, 232, 101, 264, 90, 340, 250]
 }
 ]
```

> 它的数据格式简单，难在我想要通过这些数据展示什么信息出来？
>
> **电压均值（※）:** ==表示统计对象的一般水平，容易受到极端值的影响==
>
> **电压众数（※）：** ==在统计分布上具有明显集中趋势点的数值，代表数据的一般水平==
>
> **电压峰度：**==这里要和正态分布一起用，待定==`pass`
>
> **电压偏度：**==这里也是和正态分布一起用，待定==`pass`
>
> **电压方差或者变异系数** （※）：** ==是[标准差](https://www.bananaspace.org/wiki/%E6%A0%87%E5%87%86%E5%B7%AE)的平方. 方差越小, 就表明该随机变量越倾向于取值在其[期望](https://www.bananaspace.org/wiki/%E6%9C%9F%E6%9C%9B)附近; 方差越大, 就表明该随机变量越倾向于在大范围内波动==
>
> **电压中位数（※）：**==它可以提供中心趋势的另一种度量，不受异常值的影响==
>
> **异常值** （※）：==我自己选择一点幸运观众作为异常值或者极端情况==

想起来一个点，几个数据都是需要==标准化==再用。不然就是自己在机器学习中犯错的毛病一致了。

好的，五个需要展示的结果现在搞定了。现在就在一列数据中去研究。饼图研究的是输入数据的，那么我这里研究输出数据。

**二、搞我的数据并研究标准化的问题**

```
from sklearn.preprocessing import MinMaxScaler

def standardize_statistics_func(statistics):
    # 创建Scaler对象
    scaler = MinMaxScaler()
    # 对于每个统计量进行标准化
    for key in statistics:
        # 转换为二维数组以符合scaler的输入要求
        data = [[x] for x in statistics[key]]
        # 使用Scaler进行标准化操作
        scaled_data = scaler.fit_transform(data)
        # 更新标准化后的数据，保留三位小数
        statistics[key] = [round(x[0], 3) for x in scaled_data]
    
    # 返回更新后的统计数据
    return statistics

# 你已有的统计结果
statistics = {
    'mean': [393.66, 404.61, 400.91, 403.49, 401.07, 398.86, 402.2, 404.41],
    'mode': [...], # ....
    # 其他统计数据
    ...
}

# 调用标准化函数
standardized_statistics = standardize_statistics_func(statistics)
print(standardized_statistics)
```

出现零值是`MinMaxScaler`的正常行为，因为该方法会将数据缩放到0~1的范围内。这意味着，在每个特征列中最小的值会被缩放到0，最大的值会被缩放到1。如果你的列中有多个相同的最小（或最大）值，这些值标准化后也会是0（或1）。

如果你想避免零值，一种可能的做法是添加一个非常小的常数到所有的值中，但这可能会改变数据的分布，这不是一个标准的方法。

**三、完成**

![1713137789946](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713137789946.png)



##### ④ 写动态柱状图

**一、研究数据以及我想通过数据表达什么？**

想表达什么？

当初是决定了判定每条数据中的警报数量。

![1713139732834](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713139732834.png)

最后这两个图待定。

先试试更新数据库，前三个信息能够更新不。假如可以，最后这两个最后写，放两批假数据去骗一下。







#### 2.5、维修信息日志

这里的设计思想是：在当前组件中，用户点击`健康状态分析`按钮后，会记录一个日志信息，其中包括`用户名`，`分析时间`，`分析结果文本`，`用户处理文本`。将这个日志信息传递给后端，后端需要存储到数据库中。

用户点击跳转到维修信息日志页面时，读取数据库中的信息，然后展示，进而可以实现增删改查以及对用户处理标记进行输入。

先把前台做了，后面再去做后端的业务接口。

>这里的表单可以模仿后台中权限管理的做法。表单可以换风格，但是设计思想不能改变了。

>**表单是小事。**
>
>**现在出现两个问题：**
>
>**①点击分析处理后，需要将log日志页面中除了是否检修的标记之外的内容存储；**
>
>**②检修建议是应该是机器学习版本以及数据可视化分析的结果。这里并没有写逻辑进行存储;**
>
>归纳起来是一个问题，我需要将判断结果写出来，且存储起来了。
>
>==> 每个可视化处理自己的，然后自己调库去存储。一次点击即是对一次判断结果的存储，依次调用，依次追加。

**先处理五档健康状态图的结果分析，将其存储起来。——完成**





##### 2.5.1、写日志表格信息的编辑

完成，根据ID主键进行更新，同样将新数据作为参数传入。

##### 2.5.2、收获更新——关于日期时间选择器

- 这里是ELementUI中的组件。使用的时候记得把样例中data函数的内容带上，不能只写`<el-date-picker>`



##### 2.5.3、收获更新——关于时间日期格式

**从`dao`到`service`到`controller`层，然后JSON化给前端的时候，时间格式发生了什么变化了？**

> **① **在mysql数据库中存储的时间，例如：`2024-04-01 12:18:10`是按照ISO 8601存储的。对吧。 ``



```markdown
MySQL数据库中datetime字段的默认格式并非ISO 8601标准，而是'YYYY-MM-DD HH:MM:SS'。
即，日期和时间部分之间以空格（' '）而非字符T来分隔，并且没有时区信息。
例如，一个MySQL datetime字段的样例值可能是2024-04-01 12:18:10。
	ISO 8601标准包含了更多的元素，它规定日期和时间部分之间以字符T分隔，并且在字符串结束处添加了Z来表示协调世界时（UTC），或者添加一个时区偏移来表示非UTC时间。
	例如，一个符合ISO 8601标准的日期时间样例可以是2024-04-01T12:18:10Z（表示协调世界时）或2024-04-01T12:18:10+08:00（表示东8区时间）。
	在处理跨时区问题时，ISO 8601标准可以提供较好的解决方案。
然而，由于MySQL datetime字段的默认格式，并不直接兼容ISO 8601标准，这就需要我们在处理日期时间字符串时，进行适当的格式转换。
```

>**②**对于flask项目而言，当读取数据库中的信息反馈给前端的时候。我们使用的json数据，因此需要使用jsonify函数。但是它无法转换datetime对象，因此我们需要自己定义将对象转换为字典的函数。如下例，其中对MaintenanceDate的转换，即是将它从对象同等转换到mysql数据库存储时间的'YYYY-MM-DD HH:MM:SS'格式，对吧 ？

```python
​```
    def to_dict(self):
        return {
            'DeviceNodeID': self.DeviceNodeID,
            'MaintenanceDate': self.MaintenanceDate.strftime('%Y-%m-%d %H:%M:%S'),
            'MaintenanceUser': self.MaintenanceUser,
            'MaintenanceRport': self.MaintenanceRport,
            'MaintenanceTage': self.MaintenanceTage
        }

​```
```



```markdown
是的，由于 jsonify 函数不能直接序列化 datetime 对象，因此我们需要自己将 datetime 对象转换为一个能够被 jsonify 序列化的格式。
在你提供的 to_dict 方法中，使用了 strftime('%Y-%m-%d %H:%M:%S') 方法来将 MaintenanceDate 的 datetime 对象格式化为一个字符串，
其格式为 'YYYY-MM-DD HH:MM:SS'。这种格式是一个标准的日期时间格式，由于是字符串形式的，它能被 jsonify 正常处理，并能被大多数前端应用所理解。
```





**那么。从ELementUI通过`<el-date-picker>`进行时间选择，反馈给后端的时候，时间又方式了什么变化了？**

>**③**下来，我看到我的项目中，我使用了`<el-date-picker>`组件实现时间和日期的选择。我看到我后端拿到的数据内容有：`"MaintenanceDate":"2024-04-01T12:18:10.000Z"`。我没有对前台的时间进行任何格式化处理，那么，这个组件默认确定数据的格式是ISO 8601，对吧 ？

```markdown
是的，你说的对。
<el-date-picker> 是 Element UI 提供的日期选择器组件。
当你在这个组件上选择日期和时间后，组件会按照 ISO 8601 格式生成一个代表所选时刻的字符串。
对于日期和时间来说，这个格式通常是 'YYYY-MM-DDTHH:mm:ss.sssZ'。其中，T 是日期和时间的分隔符，.sss 是毫秒部分，Z 表示这个时间是以协调世界时（UTC）表示的。
所以你见到的 '2024-04-01T12:18:10.000Z' 是由 <el-date-picker> 组件生成的标准 ISO 8601 时间字符串，它代表 UTC 时间 2024 年 4 月 1 日 12 点 18 分 10 秒。
当你的后端接收到这样的字符串时，你可能需要将这个字符串转换为 MySQL 可接受的日期时间格式，否则会出现前面讨论过的错误。
```

因此出现了我代码中的格式转换：

```python
# 编写获取前台id和数据进行更新的接口
@api_data_op_maintaininfo.route('/api/update_info',methods=['POST'])
def update_info():
    # 获取前台传来的数据
    data = request.get_data()
    print('前台反馈的数据',data)
    # 将前台传来的数据转换为字典
    data_dict = json.loads(data)
    # 获取id并将id转换为int类型
    id = int(data_dict['id'])
    # 获取新数据
    new_data = data_dict['new_data']
    # 假定new_data中的MaintenanceDate格式为 'yyyy-mm-ddTHH:MM:SS.sssZ'
    # 需要转换为MySQL接受的格式 'yyyy-mm-dd HH:MM:SS'
    # 首先移除毫秒和'Z'
    formatted_date = new_data['MaintenanceDate'].split('.')[0]
    # 接着去除'T'
    formatted_date = formatted_date.replace('T', ' ')
    # 将格式化后的时间字符串赋值回new_data
    new_data['MaintenanceDate'] = formatted_date
    # 调用服务层的更新方法
    repair_log_service.update_info(id,new_data)
    # 返回JSON数据
    return jsonify({'msg':'success'})
```



```
{
"DeviceNodeID":1,
"MaintenanceDate":"2024-04-01T12:18:10.000Z",
"MaintenanceRport":这是apiRun中的测试",
"MaintenanceTage":"未处理",
"MaintenanceUser":"杨枝YYDS"
}
```





##### 2.5.4、写日志表格信息的删除

**完成**



##### 2.4.5、写日志表格信息的查询

**完成**

![1713189800570](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713189800570.png)

##### 2.4.6、写日志表格信息的添加

**添加是在点击`健康分析`之后的调用函数，将信息注入数据库。**

我再去向假数据平台注入部分数据。从现在开始，项目所有数据集中在`device_upload`。制造假数据和假展示放到`device_fk`中。

>在用户点击`整理文件`的时候，用户数据已经存储到数据库中，故而可以进行数据分析了。
>
>那么，我在点击`健康状态分析`的时候。可以直接调用一个数据注入函数，这个函数向后端发送请求，将所有的评测信息拿到，存储到数据库中。

![1713192298353](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713192298353.png)

##### 2.4.7-表格添加的异步学习



**这里遇到了异步调用的问题。post在get没有执行完的时候就执行了**



md。终于存储上了。明天看看AI说的内容，这个异步请求到底是个什么鬼。

我之前不加异步的时候，

```
存储给后端的日志信息： 
Object { MaintenanceDate: Getter & Setter, MaintenanceRport: Getter & Setter, MaintenanceTage: Getter & Setter, MaintenanceUser: Getter & Setter, … }
```

这个数据是等待整个页面加载完成再出现的。现在异步请求之后，终于正常了。

以及，自己别tmd傻逼，总把键值对的键写错。



**对于我最初的代码：**

```js

    get_log_info(){
        this.$axios.get('http://127.0.0.1:5000/api/create_logInfo')
            .then(response => {

            this.log_info_create = response.data;
            console.log('日志信息：',this.log_info_create);
        })
            .catch(error => {
            console.error('Error:', error);
        });
    },

    //跳转到工作台2，准备实现可视化分析
    analysisFile() {
        //调用get_log_info函数，获得本次日志信息
         this.get_log_info();
        //await this.get_log_info();
        //检查this.log_info_create确保其不是空对象
        console.log('准备发送给后端的日志信息：', this.log_info_create);
        if (Object.keys(this.log_info_create).length > 0) {
            this.$axios.post('http://127.0.0.1:5000/api/add_info', this.log_info_create)
                .then(response => {
                this.$message.success('日志信息已发送！');
                console.log('存储给后端的日志信息：', this.log_info_create);
            })
                .catch(error => {
                console.log(error);
            });
        } else {
            console.log('日志信息为空，无法发送！');
        }

        this.$router.push('/wrben/wrben2');
    },
```



JavaScript的异步执行特性。当你在`analysisFile`方法中调用`this.get_log_info()`时，它发起了一个异步的GET请求。由于GET请求是异步的，`this.$axios.post`会立即执行，而不会等待GET请求完成。由于GET请求尚未完成，此时`this.log_info_create`可能仍然是一个空对象`{}`，因此POST请求发送了一个空对象到后端。 



**故而得进行异步调整。调整到等待get_log_info先完成**

如果`get_log_info`是异步的，你应该使用异步处理方式（例如，使用`async`和`await`关键字或者`.then`方法）来确保数据完全加载后再执行后续操作。 

通过使用`async`声明`analysisFile`方法并在`this.get_log_info()`调用前使用`await`关键字，可以确保在`this.get_log_info()`的异步操作完成之前不会执行任何后续代码。 

若`get_log_info`函数是异步的，但是并没有将它声明为Promise，因此在你的`analysisFile`函数中使用`await`并不能等待它完成。你需要使用`new Promise()`将`get_log_info`函数改写成Promise形式，这样在其他部分的代码中就能正确地使用`await` 

也就有了最后的代码：

```js
    // get_log_info函数应该返回一个Promise
    get_log_info(){
      return new Promise((resolve, reject) => {
        this.$axios.get('http://127.0.0.1:5000/api/create_logInfo')
          .then(response => {
            this.log_info_create = response.data;
            console.log('日志信息：', this.log_info_create);
            resolve();  // 当方得到你需要的数据后，调用resolve告诉函数它已经完成了
          })
          .catch(error => {
            console.error('Error:', error);
            reject(error);  // 如果有错误，调用reject将错误传递出去
          });
      });
    },
        
    async analysisFile() {
        //等待get_log_info函数的异步操作完成
        await this.get_log_info();

        //检查this.log_info_create确保其不是空对象
        console.log('准备发送给后端的日志信息：', this.log_info_create);

        //只有当this.log_info_create不是空对象时，才执行POST请求
        if (Object.keys(this.log_info_create).length > 0) {
            this.$axios.post('http://127.0.0.1:5000/api/add_info', this.log_info_create)
                .then(response => {
                this.$message.success('日志信息已发送！');
                console.log('存储给后端的日志信息：', this.log_info_create);
            })
                .catch(error => {
                console.log(error);
            });
        } else {
            console.log('日志信息为空，无法发送！');
        }

        this.$router.push('/wrben/wrben2');
    }
```



#### 2.6、零件仓库

模仿小米商场

##### 2.6.1、Swiper的使用

**它用到了一个Swiper的东西**

**1、安装Swiper和Vue兼容库** 

```
 npm install swiper@5.3.6
 npm install vue-awesome-swiper@4.1.0
```

**2、在你的Vue项目中全局或局部注册Swiper组件** 

**全局注册**

在你的主入口文件（通常是`main.js`或`main.ts`）中全局注册`swiper`组

```js
     import Vue from 'vue'
     import VueAwesomeSwiper from 'vue-awesome-swiper'
     
     // 导入swiper的样式文件
     import 'swiper/css/swiper.css'
     
     Vue.use(VueAwesomeSwiper)
```



**3、使用Swiper组件**

确保你在模板中使用的是已经注册的Swiper组件名。如果你是全局注册，组件名称应该与`vue-awesome-swiper`提供的一致；如果是局部注册，请确保与你导入的组件名称一致。



以及它导入了一点其他的东西需要安装。—— 不属于swiper

```bash
 npm install --save vue-axios vue-cookie vue-lazyload
```

换一下版本：

```
npm i vue-lazyload@1.3.3 -S
```



##### 2.6.2、把基本的页面样式调整好

搞定了。



##### 2.6.3、编辑点击图片进入零件信息的页面

① 点击零件信息，会进行一次跳转，带着参数id跳转到指定的页面。

完成了，之前路由管理确实太乱了。

![1713448109230](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713448109230.png)

这个零件详细信息页面，是点击图片之后，通过`router-link`带着这个参数，在当前这层中寻找这个路由

```vue
      <div class="ads-box">
        <router-link v-for="(item, id) in adsList" :key="id" :to="{ name: 'ToTest', params: { id: item.id }}" @click.native="logRoute(item.id)">
          <img v-lazy="item.img" alt />
        </router-link>
      </div>
```

然后路由管理就开始找了，倘若在同层中找到这个路由，就在这层的顶层的路由展示`<router-view/>`中展示。

我这里确实找到了：

![1713448293922](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713448293922.png)

那么就在顶层中展示：

![1713448308726](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713448308726.png)

看看是否符合我的顶层代码？

![1713448408017](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713448408017.png)

暂时把跳转写好。然后我得去写后台管理了，一边训练模型一边写其他功能。



**个人理解的路由管理就是，注册的路由中，以大括号作为一个对象信息，并列的对象信息在一个路由出口出来。至于那种有children的，就在它的父亲中写路由出口。**



#### 2.7、前台登录注册

先写最简单和简陋的登录注册，然后再试着调整优美。

**登录是根据邮箱和密码登录**

****

**注册则是需要把数据库中的信息除了修改时间，全部处理完成**

**完成，但是没有怎么美化**



#### 2.8、前台零件仓库管理

###### 2.8.1、获取所有零件信息

这里选择将商品的图片按照路径存储。vue-cli2中，浏览器是到static目录下找内容

展示零件商品信息完成

##### 2.8.2、写点击零件商品之后，跳转到商品信息页面的具体内容展示



完成

##### 2.8.3、对购物车的数量修改+下单状态修改

完成

 

#### 2.9订单确认页面

##### 2.9.1、获取购物车中确认的订单

##### 2.9.2、获取收货地址列表

##### 2.9.3、对收货地址进行增、删、改

其中，为了实现编辑收货地址：

要从开源库如`chinese_regions`获取全国省市数据，并将其赋值给`addressOptions`，您需要执行几个步骤。以下是使用Vue.js和Axios（假设您使用Axios来处理HTTP请求）进行操作的基本方法：

1. **安装Axios（如果尚未安装）**

   如果您的项目中还没有Axios，请先安装它。在终端或命令提示符中运行以下命令：



```bash
   npm install axios
```

 

1. **准备API或数据源**

   因为`chinese_regions`是一个Python库，直接在Vue项目中使用它可能不太方便。您需要找到提供JSON格式省市数据的API接口或者下载好的JSON文件。这里，我们假设您已经有了可以直接访问的URL或本地的JSON文件作为数据源。

2. **获取数据并赋值**

   在您的Vue组件中，使用`created`钩子函数来获取数据，并更新`addressOptions`。

   - **使用本地JSON文件（假设文件位于public目录）：**

     将数据文件放在`public`目录下，例如`public/china_regions.json`，然后在`created`钩子中加载这个文件。

 

javascript

```
   created() {
     axios.get('china_regions.json')
       .then(response => {
         this.addressOptions = response.data;
       })
       .catch(error => console.error("加载省市数据出错:", error));
   },
```

 

- **使用在线API：**

  如果您有在线API的URL，情况类似，只是URL会是一个完整的HTTP路径。

 

javascript

```
   created() {
     axios.get('https://example.com/api/china_regions')
       .then(response => {
         this.addressOptions = response.data;
       })
       .catch(error => console.error("加载省市数据出错:", error));
   },
```

 

1. **在<el-cascader>组件中使用addressOptions**

   确保您的`<el-cascader>`绑定的`options`属性是`addressOptions`。这样，一旦`addressOptions`被赋值，下拉列表就会自动填充省市数据。

 

请注意，获取数据的操作取决于您的数据源格式，您可能需要根据实际数据结构调整代码。同时，请确保您的跨域请求（如果使用在线API）没有遇到CORS政策限制





**增加和修改完成**

**生成订单信息完成**

**清空已经购买的购物车完成**



#### 2.10、前台的订单信息展示列表

这里我只做一个事儿，展示购买的零件订单。



好的。前台完工。





















## **后台**

我决定把后台也单独领出来。flask只是作为一个服务器，处理各种api的请求。

![1712663509343](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712663509343.png)

后台找好了，开始疯狂改

### 一、电路支路权重管理

我在上面加功能的时候的，指出管理员需要对一定的支路权限进行权限编辑。

让ID主键不同，主要通过**名称**来区分。可以新建任意的权限分配规格。那么，也同时得加上，**是否使用的标记**。

前台读取的时候，找到被标记为可以使用的来进行使用。

**对系统管理的`系统环境变量`页面展开改造**

![1712999086176](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712999086176.png)

**先整理表格成为我需要的——整理好了**

**再把数据交互完成，拿到数据——完成了**

![1713006598421](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713006598421.png)



**`写编辑`**

>在他的设计思想里，是把编辑和添加用在一个弹窗，使用一个标记决定谁展示。因**为我的编辑需要填充原本的数据，所有我还是分开写。**——完成

>**写提交保存到后端的事件函数**

```
methods: {
  // ...其他方法...

  submitForm() {
    // 检查表单数据是否有效
    this.$refs.editForm.validate((valid) => {
      if (valid) {
        // 表单验证成功，开始发送请求
        this.loading = true; // 启用加载状态
        this.$axios.post('http://127.0.0.1:5000/api/edit_all_circuit_weight', {
          id: this.EditForm.ID, // 假设EditForm对象中包含ID
          ...this.EditForm // 展开EditForm对象作为其他数据
        }).then(response => {
          // 请求成功的处理
          this.loading = false; // 禁用加载状态
          this.editFormVisible = false; // 关闭对话框
          
          // 可以根据需要进行其他操作，例如更新视图或显示成功消息
          this.$message({
            message: '修改成功！',
            type: 'success'
          });
        }).catch(error => {
          // 请求失败的处理
          this.loading = false; // 禁用加载状态

          // 错误处理，可能会显示错误消息，或在控制台输出错误
          this.$message.error('修改失败：' + error.message);
          console.error('Edit error:', error);
        });
      } else {
        // 表单验证失败
        this.$message.error('表单数据有误，请检查后再提交！');
        return false;
      }
    });
  },
  // 打开编辑对话框的方法，这里需要传递所选行的数据
  editRow(rowData) {
    this.EditForm = { ...rowData }; // 填充表单数据
    this.editFormVisible = true; // 显示编辑对话框
  },
  // 关闭对话框的方法
  closeDialog() {
    this.editFormVisible = false;
    this.$refs.editForm.resetFields(); // 重置表单状态
  },
  // ...其他方法...
}
```



>**完成，处理v-model会自动把数据搞成字符串的问题**



**`写添加`**

**添加**和**编辑**有点异曲同工

页面布局确实是异曲同工。但是添加的逻辑不同，因为我给的页面中，没有要是否启动，反而要了时间。也正是因为时间模块，必须搞成MYSQL数据库的时间存储格式。



**`写搜索`**

![1713018341735](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713018341735.png)

**完成了，axios搞定好自己是什么请求，get还是post。注意get是从agrs中拿到参数**



**`写删除`**

删除比较好写，删除完成。



### 二、机器学习管理

我这个功能模块要干嘛？

**可以根据训练数据，选择对应的模型，进行数据训练。**

**对已有数据模型的管理：**

**增删改查+是否运用到本系统**



#### 2.1、管理已有的机器学习模型

##### 2.1.1、查询所有模型信息

完成

##### 2.1.2、删除当前模型信息

完成

##### 2.1.3、编辑当前模型的信息

显示弹出框没问题

![1713528185962](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713528185962.png)



**完成了**

##### 2.1.4、搜索当前模型的信息

不用了，直接使用过滤器

![1713533227069](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713533227069.png)

明天可以写模型训练了。



这里的分页功能也写好了，我还是用ElementUI的分页功能吧，别人的分页功能，我不一定能够吃下来。



### 三、写登录注册以及相应的用户管理

####  3.1、路由守卫的理解。

```js
router.beforeEach((to, from, next) => {
    if (to.matched.length != 0) {
        if (to.meta.requireAuth) { // 判断该路由是否需要登录权限
            if (Boolean(localStorage.getItem("userInfo"))) { // 通过vuex state获取当前的user是否存在
                next();
            } else {
                next({
                    path: '/login',
                    query: { redirect: to.fullPath } // 将跳转的路由path作为参数，登录成功后跳转到该路由
                })
            }
        } else {
            if (Boolean(localStorage.getItem("userInfo"))) { // 判断是否登录
                if (to.path != "/" && to.path != "/login") { //判断是否要跳到登录界面
                    next();
                } else {
                    /**
                     * 防刷新，如果登录，修改路由跳转到登录页面，修改路由为登录后的首页
                     */
                    next({
                        path: '/goods/Goods'
                    })
                }
            } else {
                next();
            }
        }
    } else {
        next({
            path: '/login',
            query: { redirect: to.fullPath } // 将跳转的路由path作为参数，登录成功后跳转到该路由
        })
    }
})

```

路由拦截器的代码中的 if-else 逻辑是用于控制页面的访问权限。下面我将详细解释代码中不同部分的功能和逻辑：

1. `router.beforeEach` 是Vue路由的全局前置守卫。它在路由发生变化之前的时候被调用，此时你可以决定是否允许或取消导航。
2. `if (to.matched.length != 0)` 检查即将跳转到的路由是否存在，`to.matched` 包含了所有匹配的路由记录。
3. `if (to.meta.requireAuth)` 根据路由元信息决定是否需要进行登录验证。如果 `requireAuth` 为真，代表这个路由需要登录后才能访问。
4. `if (Boolean(localStorage.getItem("userInfo")))` 通过查看 `localStorage` 中是否存储了用户信息来判断用户是否已经登录。
5. `next({ path: '/login', query: { redirect: to.fullPath } })` 如果用户没有登录，则重定向到登录页面，并附上一个查询参数 `redirect` ，这样登录成功后可以跳回至原先尝试访问的页面。
6. 如果 `to.meta.requireAuth` 为假，表示这个路由不需要登录即可访问。在这种情况下，还会再次检查用户是否已经登录。如果用户已登录，还会检查 `to.path` 是否指向根路径 `/` 或登录页 `/login`，如果是的话，将会重定向到一个默认的页面（在这个例子中是 `/goods/Goods`）。

总结起来就是:

- 如果用户未登录，试图访问需要登录的页面，会被重定向到登录页面。
- 如果用户已登录，并尝试访问根路径或登录页，则被重定向到一个默认的页面（比如“商品管理”页面）。
- 其他情况下（比如访问不需要登录的页面或者用户已经登录并访问其他页面），直接放行。

如果 `to.matched.length` 为 0，表示目标路由不存在，此时会强制重定向到登录页面。这通常用于捕捉无效的路由或者用户输入错误的URL。

此段代码确保了页面的访问权限得到控制，用户在没有登录的情况下只能访问不要求认证的页面，确保了应用的安全性。



在路由管控下进来了：

![1713755308076](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1713755308076.png)

#### 3.2、表单验证

不写表单验证了，可以登录注册就可以了。



#### 3.3、后端反馈数据的梳理

得反馈成功获取信息了，也就是账号密码正确与否。以及得返回一个token序列。

好的。磕磕盼盼的写完了，但是没得很大的收获，因为我在抗拒理解。









### 四、写系统用户的信息管理

#### 4.1、获取所有用户信息

完成

#### 4.2、删除用户信息并且发送邮件

当前的授权码：LQSGAYMZXFPPJKHW 

这里的积累是：

![1714523290034](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1714523290034.png)

```python
# 配置信息
    # 初始化邮件发送对象
    mail = Mail(app)
    # 邮件配置
    app.config['MAIL_SERVER'] = 'smtp.163.com'
    app.config['MAIL_PORT'] = 465  # 端口号，根据是否使用SSL/TLS选择端口
    app.config['MAIL_USE_TLS'] = False  # 网易邮箱中不使用TLS，根据邮箱服务提供商的要求设置
    app.config['MAIL_USE_SSL'] = True  # 网易邮箱使用了SSL，根据邮箱服务提供商的要求设置
    app.config['MAIL_USERNAME'] = 'yangzhi15791605@163.com'  # 将your_email@163.com替换为我的163邮箱地址
    app.config['MAIL_PASSWORD'] = 'LQSGAYMZXFPPJKHW'  # 将your_email_authorization_code替换为我的163邮箱授权码
    app.config['MAIL_DEFAULT_SENDER'] = 'yangzhi15791605@163.com'  # 发件人邮箱地址
    mail.init_app(app)

```

发送结果：

![1714523352575](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1714523352575.png)

![1714523389151](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1714523389151.png)

以及指定删除信息：

要添加一个步骤让操作者输入删除的原因并将其一起发送给后端，你需要使用Vue的`$prompt`方法来弹出一个输入框，提示用户输入删除原因 。

用了`this.$prompt()`来创建一个带有输入框的对话框，要求操作者输入删除原因，其中：

 

- `inputPattern: /\S+/` 确保输入内容不为空。
- `inputErrorMessage: '删除原因不能为空'` 定义了当输入不符合模式时显示的错误消息。

 

如果用户在输入框中输入了删除原因并点击确认，那么`value`就会包含这个删除原因，随后我们可以将这个原因作为一个新的字段`reason`添加到POST请求的数据对象中，并发送到后端。

![1714524089616](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1714524089616.png)



#### 4.3、搜索信息的功能

![1714525439999](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1714525439999.png)



#### 4.4、添加用户信息的功能

![1714527988258](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1714527988258.png)



#### 4.5、不要编辑框，直接上重置密码

完成。





### 五、零件商品信息管理

我写前台的时候发现，应该先把后台的零件商品信息写好，前台直接展示以及完成后续的加入购物车的操作即可。

#### 5.1、展示所有商品信息

完成+完成分页展示



#### 5.2、写商品的添加和编辑

添加完成，现在写编辑，完成

#### 5.3、写商品删除

完成



### 六、订单管理









## 后端

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



#### 2.2、工作台



##### 2.2.1、写用户在前台下载后台的数据模板

`send_file` 不是需要单独安装的模块，它是 Flask 框架内置的一个函数。这个函数归属于 `flask` 模块，主要用于在 Flask 应用中发送文件到客户端。

**`搞定，既然是用户下载，那么可以搞一个数据表，统一用户的下载次数` —— 后端的功能又增加了**

![1712215862093](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712215862093.png)





##### 2.2.2、写用户在前台上传数据到后台，后台得到之后，进行持久化

这里得使用数据库连接池了，应该。

不用，就像上传到服务器，指定一个存储的位置即可。



**初步完成将用户上传的excel表格存储到指定的位置：**

![1712541205400](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712541205400.png)



**初步完成列表展示用户的上传信息，并且完整对后端中数据的删除**

![1712545385168](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712545385168.png)

**准备完成对上传的数据进行格式整理。和进行可视化展示。**

`然后就可以着手开始写后台管理系统了`

整理这里先不动，不是那么好整理，我没有动过pandas，这里是到目前为止都有问题的。

```
from flask import Flask, request, jsonify
from werkzeug.utils import secure_filename
import os
import pandas as pd

# ... other code ...

@api_data_op.route('/api/organizeExcel', methods=['POST'])
def organize_excel():
    # ... other code ...
    
    if os.path.exists(file_path):
        try:
            # Specify `engine='openpyxl'` for xlsx files
            df = pd.read_excel(file_path, engine='openpyxl')

            # Your data processing logic goes here
            # df.fillna(方法或值)

            # When saving, also specify `engine='openpyxl'` for xlsx files
            df.to_excel(file_path, index=False, engine='openpyxl')

            return 'File organized successfully', 200
        except Exception as e:
            print('整理文件时出错:', str(e))
            return 'Error organizing file', 500
    else:
        return 'File does not exist', 404
```





##### 2.2.3、**搞数据可视化**

我的设计思想是，既然我已经通过前台放到服务器了，现在需要将这个数据持久化到数据库。后续的分析是调用MYSQL数据库进行分析。

**将excel数据存储到数据库中**

单条数据存储到数据库中成功：

![1712626115782](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712626115782.png)

存储数据是能够实现了。现在的问题是，这个可视化的数据，我应该如何伪造。

wc，tmd，以前造数据的代码不见了。

**我现在应该思考，我是先造数据再去可视化，还是先写可视化出来了再去补数据了？**

先直接把原本用起来的数据库搞来把可视化弄了。先有东西

###### 2.2.3.1、Echarts使用总结

>**汇总基本的使用Echarts的步骤**

① 把Echarts的图都导入【也可以根据需求导入】

```
import * as echarts from 'echarts';
```

② 基于准备好的dom，初始化echarts实例

此处即，自己在组件中写好栅格系统，自己确定好dom元素

```vue
<el-row>
    <el-col :span="12">
        <div id="graph_line" style="width:100%; height:500px;"></div>
    </el-col>
    <el-col :span="12">
        <div id="graph_bar" style="width:100%; height:500px;"></div>
    </el-col>
</el-row>
```

然后就可以在实例化中指定实例化的结果最后被放到哪个dom元素下。以及根据文档或者实例，写好自己需要展示的信息，通过自己注册的实例，调用`setOption`方法去完成对配置参数的加载

```js
mounted() {
    // 基于准备好的dom，初始化echarts实例
    var myChart = echarts.init(document.getElementById('graph_line'));
    // 指定图表的配置项和数据
    var option = {
      title: {
        text: 'ECharts 入门示例'
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
        type: 'line',
        data: [5, 20, 36, 10, 10, 20]
      }]
    };
    // 使用刚指定的配置项和数据显示图表。
    myChart.setOption(option);

    var myChart2 = echarts.init(document.getElementById('graph_bar'));
    var option2 = {
      title: {
        text: 'ECharts 入门示例'
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
    };
    myChart2.setOption(option2);
  },
```



###### 2.2.3.2、对各种数据可视化的理解

**对于折线图：**

>随机切割6000条数据出来，然后怎么嵌套到这个范围中了？这个范围表示一危险的指数，那么我预测分析的结果，怎么扣合这个分析结果了？一条一条的拿给模型分析吗？按照：完美、健康、中等、轻微严重、十分严重来划分，划分之后，在每个区间中取随机数。

![1712642551884](E:\文档_Typora\1-关于怎么学会coding9-本毕设.assets\1712642551884.png)





**对于饼状图**

>这里仍然是我之前做的，对磨损状态的统计。放到第一个页面的中



**堆叠图**

>放边缘，仍然是展示不同的结构计算值标准的堆叠



**对于柱状图：**

> 这里放置一个动态柱状图。300作为一批，分析每一批中，被预警支路的高低，机器学习最后反馈的时候，那个支路被预警最多，让它去检修。放到第二版的中间去

 



**等级得分表**

>最后附带一个等级得分表



#### 2.3、信息管理页面

这里继续上一个页面的监测结果。对维护信息进行日志统计



#### 2.4、订单页面

这里用户可以在本网址购买一些零件









## 机器学习

### 一、sklearn的安装

**使用pip包管理器**

`pip install -U scikit-learn`





### 二、脱离jupyter notebook写模型训练

主要将处理业务写在service层即可，jupyter是可以单步执行得到结果嘛，我这里就一块一块代码的执行了。

**目前将KNN的简单训练，训练后的模型保存，加载保存的模型进行预测的代码编写完毕。**

更新：额需要将模型的精度也存储到数据库中，为后续的动态仪表板分析做准备。





### 三、算法集成

> 集成的大致思路我是有了。目前需要解决一个超参数的调整问题。是应该我后端直接写死超参数还是在可视化图层中显示具体的信息传递给后端api来指定了？

**这个问题的本质应该是，看看我训练的模型是不是都是依赖依赖超参数的形式。**



例如训练支持向量机：

要将我的代码从训练随机森林模型迁移到训练支持向量机（SVM），您需要做的主要更改涉及到替换模型实例化部分，以及可能对预处理步骤和超参数搜索范围进行一些微调。支持向量机和随机森林在一些超参数方面是不同的，例如，SVM有`C`和`gamma`（对于RBF核的SVM）等特有的参数。 





**把cv的折数降低到三折，机器不是 **







# Question

>请解释我这段代码在做什么？

```vue
<div class="details-box">
  <router-link v-for="(item, id) in detailList" :key="id" :to="{ name: 'ToTest', params: { id: item.id }}" @click.native="logRoute(item.id)">
    <img :src="item.img" alt />
  </router-link>
</div>
```

这段代码主要是用来列出你的`detailList`数据数组中的所有项目，并创建每一个项目的路由链接和显示每个项目的图片。

详细来说：

1. `<router-link>` 是 Vue Router 提供的组件，用于在应用的不同部分之间导航。通过 `to` 属性，我们定义了点击链接后要向哪个路由跳转。`to` 中的 `name` 属性是你在 Vue Router 中预先定义好的路由名称，这个示例中是 `ToTest`。`params` 允许你向这个路由传递一些参数，这个示例中，你传递了 `item.id`。当你点击链接后，应用会跳转到 `ToTest` 路由，并且你可以在那个路由中访问到这个 `id` 参数。
2. `v-for="(item, id) in detailList"` 是 Vue 的列表/数组渲染指令。它遍历 `detailList` 数组，并给每一个元素生成一个新的 `<router-link>` 元素。在生成元素的过程中，你可以访问当前元素(`item`)和它的索引(`id`)。
3. `:key="id"` 是 Vue 索引。这个特性帮助 Vue 追踪每个节点的身份，是一个非常重要的机制。在数组发生变化时，比如添加、删除元素，Vue 会基于 `key` 的变化重新排序元素，使得差异化渲染变得更加准确快速。
4. `@click.native="logRoute(item.id)"` 添加了一个原生的点击事件监听器，当你点击链接时，`logRoute` 方法会被调用，`item.id` 会作为参数传递给它。
5. `<img :src="item.img" alt />` 是一个图片元素。`:src="item.img"` 是一个数据绑定，它把图片的 `src` 属性和当前元素的 `img` 属性绑定在一起，这样图片的源就会是你的数据对象中 `img` 的值。

 

总的来说，这段代码主要是在使用 Vue 和 Vue Router 的功能展示一个由链接和图片组成的列表。这个列表的数据来自 `detailList`，并且每个元素根据其 `id` 有一个到名为 `ToTest` 的路由的链接。这个列表很可能是一个产品列表，或者类似的东西。





>关于vue-cli2读取数据库中存储的图片路径并存储的认识有多少了？

在Vue CLI 2中，默认没有`public`文件夹这个概念，相对应的是`static`文件夹，用来存放静态资源。这意味着，对于使用Vue CLI 2构建的项目，应当将静态资源放置在`static`目录下，而非新建的`public`文件夹中。

根据你的项目结构，你已经有一个`static`文件夹。你应该将图片放在`static`文件夹或其子文件夹（例如`static/images`）中，而不是`public`文件夹中。这样，图片的路径应该基于`static`目录。当你的应用构建时，这些在`static`文件夹下的资源会被复制到输出目录（默认是`dist`），并保持原有的文件结构。

 

由于`static`文件夹的内容在构建时会被复制到根目录下，所以你的图片URL在后端返回时应该是这样的：

```json
{
  "desc": "这是马达",
  "editTime": "Fri, 03 May 2024 10:08:39 GMT",
  "editUser": "杨枝",
  "id": 2,
  "img": "/static/images/马达_out.jpg",
  "name": "马达",
  "number": 345,
  "price": 456.21,
  "productCompany": "奔驰公司的子公司丫丫吖"
}
```

 

注意，这里`img`的路径改成了`/static/images/马达_out.jpg`来反映图片实际存在于`static/images`目录下。

 

此时，你在Vue组件中引用图片的代码不需要改变，仍然是：

```html
<div class="details-box">
  <router-link v-for="(item, id) in detailList" :key="id" :to="{ name: 'ToTest', params: { id: item.id }}" @click.native="logRoute(item.id)">
    <img :src="item.img" alt />
  </router-link>
</div>
```



>我需要这个列表中`序号`这栏根据当前有的数据量来升序排列，即，即使我对数据库中id为4的删除了，数据库中id为5的为展示为序号4 

你可以在`el-table-column`设置`type`为`index`来自动生成序号，代码如下：

```vue
<el-table-column align="center" type="index" label="序号" width="50">
</el-table-column>
```

这样即使在你删除行的时候，序号依旧会依据当前数据进行更新，不会一直跟着id走。由于是自动生成的，序号是根据数据行在数据数组中的索引生成的，在进行排序或者过滤操作后，序号仍然会按照当前数据顺序进行排列。



>那么，我这个退出登录的logout函数应该如何编写了？这个localStorage和cookie的区别是什么了？ 

对于退出登录这个操作，基于现有的需求，我们只需要从本地存储中清除用户信息就行了：



```javascript
methods: {
  logout() {
    // 清除localStorage中的用户信息
    localStorage.removeItem('user');
    // 提示用户已退出
    this.$message.success('您已退出登录');
    //跳转到登录页面
    this.$router.push('/login');
  },
  ... // 其他methods
}
```

这样当用户点击退出时，用户信息就会被清除，导航栏就会显示‘登录’二字了。

对于你问到的localStorage和cookie的区别，这两者都是浏览器存储机制。这是他们的几点不同：

1. 存储大小：一个域名在cookie中只能保存4KB左右的信息，而localStorage能保存5MB。
2. 生命周期：cookie有有效期，达到有效期就会自动删除，而localStorage没有有效期，除非你自己去删除。
3. 数据随请求发送：cookie在HTTP请求中会自动携带，而localStorage不会。
4. API易用性：localStorage的API更易用，它有setItem，getItem，removeItem等方法，而操作cookie需要自己手动解析。

虽然localStorage看起来更优秀，当我们选择使用哪种技术时，需要对技术有深入理解和清楚的应用场景。例如，由于localStorage不能跨域，所以在需要跨域的场景下只能用cookie，这也是cookie依然广泛使用的原因之一。





>我想要获取前台传递的参数信息中加入一个邮箱信息，然后向这个邮箱发送一则为什么删除的信息提示，请问如何修改？ 

为了在现有的后端接口中添加额外的邮箱参数，并在删除用户信息时发送一封通知邮件，你需要修改后端接口的代码以接收和处理额外的邮箱参数。同时，你需要实现发送邮件的逻辑。下面是修改后的接口示例：

首先，你需要确保你的环境中安装了发送电子邮件所需的库，例如 `conda`，如果还没有，请先安装。



```python
from flask import Flask, request, jsonify
from flask_mail import Mail, Message

app = Flask(__name__)
mail = Mail(app)

# 邮件配置, 正式环境中请不要将配置信息硬编码在代码中。
app.config['MAIL_SERVER'] = 'your_mail_server'
app.config['MAIL_PORT'] = 587
app.config['MAIL_USE_TLS'] = True
app.config['MAIL_USERNAME'] = 'your_email@example.com'
app.config['MAIL_PASSWORD'] = 'your_password'
app.config['MAIL_DEFAULT_SENDER'] = 'your_email@example.com'

mail.init_app(app)

@api_data_op_userinfo_manage.route('/api/delete_front_user_info', methods=['POST'])
def delete_front_user_info():
    # 获取前台传递的id和email
    data = request.json
    user_id = int(data.get('id'))
    user_email = data.get('email')  # 获取传递过来的邮箱信息

    # 删除前台用户信息
    result = service_front_user_info.delete_info(user_id)

    # 如果删除成功并且提供了邮箱，则发送邮件通知用户
    if result['success'] and user_email:
        subject = "账号删除通知"
        body = f"您的账号已经被删除。\n删除原因: {result.get('reason', '无特定原因')}"
        send_mail(subject, body, [user_email])

    # 返回结果
    return jsonify(result)

def send_mail(subject, body, recipients):
    try:
        msg = Message(subject, recipients=recipients, body=body)
        mail.send(msg)
        print('邮件发送成功')
    except Exception as e:
        print('邮件发送失败', e)
```

 

在这个示例中，我们首先导入了必要的 Flask-Mail 类，实例化一个 `Mail` 对象，并通过一系列配置初始化了它。在 `delete_front_user_info` 函数中，我们新增了读取 `email` 参数的代码，并添加了条件判断，如果用户成功被删除并且提供了邮箱地址，就调用 `send_mail` 函数来发送邮件通知。

 

确保替换邮件配置中的占位符（如 'your_mail_server', 'your_email@example.com', 和 'your_password'）为实际工作中使用的邮件服务器设置。

 

这就是如何让你的后端接口接收一个额外的邮箱信息，并在删除用户时向该邮箱发送通知的方法。如果删除成功，`send_mail` 函数会发送一封邮件给用户告知他们账号被删除的原因。请注意，邮件发送的逻辑可能会根据实际的邮箱服务器设置有所变化。









>在我的支持向量机模型训练中，这段参数表示什么意思了？
>
> ``` # 设置参数 param_grid = { 'C': [0.1, 1, 10], 'gamma': ['scale', 'auto'], 'kernel': ['linear', 'rbf', 'poly'] } ```
>
> 我当前的`最佳结果: 0.821`,那么应该如何调整参数来调优 ?

在支持向量机模型中，`param_grid` 是用来定义网格搜索中会尝试的参数的值。这个字典中的每个键代表一个参数，而与键相关联的列表则是在模型训练过程中要尝试的各种不同的值。这里的参数意义如下：

 

- `C`：正则化参数。较小的`C`值会通过选择更大的间隔边界来增加错误分类的“容忍”，即允许更多的错误。较大的`C`值则会选择一个较小的间隔边界，通过惩罚分类错误来减少错误。
- `gamma`：核函数的参数。对于非线性核，`gamma`决定了单个训练样本影响的范围，较低的值表示‘far’，较高的值表示‘close’。`gamma`的`scale`和`auto`是两种不同的方式来设置这个参数。
- `kernel`：核函数类型。核函数可以是线性的，也可以是将输入空间映射到一个更高维度空间的函数。常见的核函数类型有`linear`, `rbf`和`poly`。

 

你当前的`最佳结果: 0.821`可能是指你在使用这个参数网格进行模型训练后得到的最高准确率。

 

为了进一步调优你的模型，你可以尝试以下方法：

 

1. 更细化的参数格网: 如果你的计算资源允许，可以在并行运算的帮助下扩大参数范围或增加更多的参数值，例如，在`C`中添加[0.001, 0.01, 0.5, 5, 50]。
2. 更改或添加参数: 如果你对SVM和你的数据集有足够的了解，可以思考是否需要在`param_grid`中添加新的参数，像是`degree`（针对`poly`核），或者移除不太重要的参数。
3. 交叉验证: 通过更多的交叉验证折数，你可以减少随机性的影响，并可能得到一个更精确的模型评估。但这会增加计算成本。
4. 使用随机搜索: 如果网格搜索的计算量太大，你可以尝试使用随机搜索，它在参数空间中随机选取组合，这通常更快，并且可以通过搜索更大的空间来提供相近或更好的结果。
5. 模型评估标准: 确保你使用正确的模型评估标准。例如，在不平衡的数据集中，精确度可能不是最佳的评价指标，而应该考虑f1分数或ROC曲线下面积等。

 

记住，在进行参数调整时，加大的仅是参数搜索的范围，这不一定会带来更好的结果，因为过度拟合问题可能会出现。确保有一个良好的交叉验证策略是至关重要的。 







>那么，我可以先分散的训练出15个不同的机器学习模型作为基学习器（比如支持向量机、随机森林，逻辑回归、梯度提升树），将这些模型存储到本地，再统一到一个方法中读取这些已经训练出来的模型，使用Voting或者Stacking进行集成吗？ 

当然可以。这是一个典型的集成学习工作流程，特别是在你想结合多个弱学习器的预测来构建一个更强大的集成模型的情况下。下面是详细的步骤说明：

**步骤 1: 训练和保存基学习器**

你可以独立地训练不同类型的机器学习模型，并使用各种库（比如scikit-learn的`joblib`）来将它们保存到磁盘上。例如：

 



```python
from joblib import dump, load

# 训练模型
svm_model = train_svm_procedure(...)   # 这是伪代码，替换为您的训练代码
rf_model = train_rf_procedure(...)
lr_model = train_lr_procedure(...)
gbt_model = train_gbt_procedure(...)

# 保存模型
dump(svm_model, 'svm_model.joblib')
dump(rf_model, 'rf_model.joblib')
dump(lr_model, 'lr_model.joblib')
dump(gbt_model, 'gbt_model.joblib')
```

 

 **步骤 2: 加载模型并进行集成**

 

当所有模型都训练并保存好之后，你可以编写一个新的方法来加载这些存储的模型文件，使用Voting或Stacking集成框架来结合它们的预测。以下是使用`scikit-learn`来实现的伪代码示例：

 



```python
from sklearn.ensemble import VotingClassifier, StackingClassifier
from joblib import load

# 加载模型
svm_model = load('svm_model.joblib')
rf_model = load('rf_model.joblib')
lr_model = load('lr_model.joblib')
gbt_model = load('gbt_model.joblib')

# 列出所有模型
models = [
    ('svm', svm_model),
    ('random_forest', rf_model),
    ('logistic_regression', lr_model),
    ('gradient_boosting', gbt_model),
    # ...其它模型
]

# Voting集成
voting_ensemble = VotingClassifier(estimators=models, voting='soft')
voting_ensemble.fit(X_train, y_train)

# 或者Stacking集成
stacking_ensemble = StackingClassifier(estimators=models, final_estimator=SomeMetaModel())
stacking_ensemble.fit(X_train, y_train)
```

 

在上面的代码中，`VotingClassifier`和`StackingClassifier`是`scikit-learn`中的集成模型，分别用于创建投票和叠加集成。记得替换`X_train`和`y_train`为你的训练数据和标签。

注意在集成之前，确保一点：所有模型都应该被训练和评估过，以确保它们各自有一个合理的性能水平，因为集成学习的目的是结合独立的模型来改善性能。一个非常弱的模型可能会降低整个集成的效果。此外，要灵活选择`final_estimator`（对于Stacking），这个模型将根据基学习器的预测来做最终决策。

完成这些步骤后，你将能够部署一个更准确、鲁棒性更好的集成学习模型，相比于单独的基学习器，它通常能提供更好的预测性能。





> 我的随机森林中选取训练集的特征是从Voltage1到Voltage16，那么，我在支持向量机中可以选取其中的任意部分特征来训练吗？这种训练出来的模型，后续可以使用Voting或者Stacking来集成吗？ 

在进行Voting或Stacking集成时，模型的多样性是一个关键因素。不同的特征集、模型参数或不同类型的模型可以增加集成的多样性，这通常能带来更好的性能。不过，要精细控制模型的复杂度和性能之间的平衡，以及组合模型的方式，以达到最优的预测效果。

最后，不要忘了评估组合后的模型性能，以验证集成学习方法是否真的比任何单个模型都要好。试验不同的集成策略、基模型的配置和元模型的选择，可以帮助找到最适合您特定数据集和任务的模型集成方案。





>那么，假如我此时训练出20个包含支持向量机、随机森林和逻辑回归的较高精准度的基学习器（SVMs1、SVMs2、...、RandomF1、RandomF2），我想要使用bagging的策略或者Voting的策略来集成，我应该如何编码了？ 

要使用Bagging或Voting策略对您提到的20个基学习器进行集成，您可以使用`scikit-learn`库中的`VotingClassifier`和`BaggingClassifier`。以下是您可能会使用的编码示例。

**1、准备基学习器列表**

首先，准备一个包含所有基学习器以及它们别名的列表。这假设已经有了预训练好的基学习器实例。

```python
from sklearn.ensemble import RandomForestClassifier, VotingClassifier
from sklearn.svm import SVC
from sklearn.linear_model import LogisticRegression

# 假设您已经有了预训练好的模型实例
models = [
    ('SVM1', trained_SVMs1),
    ('SVM2', trained_SVMs2),
    # ...
    ('RandomF1', trained_RandomF1),
    ('RandomF2', trained_RandomF2),
    # ...
    ('LogReg1', trained_LogReg1),
    # ...
]
```

 

**2、Voting集成策略**

对于Voting，您可以选择硬投票或软投票。硬投票是指每一个模型对于每一个样本投票选择一个类别，而软投票则是指每一个模型对于每个类别输出一个概率，然后进行加权求和，选概率最高的类别。

```python
# 实例化VotingClassifier
# 使用'hard'投票
voting_clf_hard = VotingClassifier(estimators=models, voting='hard')

# 使用'soft'投票，假设所有基学习器都有predict_proba方法
voting_clf_soft = VotingClassifier(estimators=models, voting='soft')

# 对模型进行训练
voting_clf_hard.fit(X_train, y_train)
voting_clf_soft.fit(X_train, y_train)

# 对模型进行评估
print(voting_clf_hard.score(X_test, y_test))
print(voting_clf_soft.score(X_test, y_test))
```

 

 **3、Bagging集成策略**

Bagging则通常是对单一模型进行多次训练，每次训练使用不同的数据子集。但如果您想对不同的模型实例使用Bagging，您需要分别对每种模型类型进行Bagging集成。下面以Random Forest模型为例实现Bagging。

```python
from sklearn.ensemble import BaggingClassifier

# 以Random Forest为例来创建Bagging策略
bagging_clf = BaggingClassifier(
    base_estimator=RandomForestClassifier(),
    n_estimators=20,
    max_samples=0.8,
    max_features=0.8
)

# 训练模型
bagging_clf.fit(X_train, y_train)

# 评估模型
print(bagging_clf.score(X_test, y_test))
```

注意，对于BaggingClassifier的`base_estimator`参数，您可以选择将其设置为你的随机森林或其他模型。`n_estimators`参数表示集成中基模型的数量。

确保在执行以上步骤之前，您已经完成了必要的数据预处理步骤，比如分割训练测试数据等 (`X_train`, `y_train`, `X_test`, `y_test`)，并正确导入所需的类和函数。

值得注意的是，Bagging通常是对同一个算法的不同实例进行集成，而Voting可以是不同算法的实例。如果您想同时对不同的算法实例进行集成，通常会使用Stacking或者Voting中的软投票（如果算法可以提供预测概率的话）。



>那么使用JWT 库生成我自己的token的如何写？ 

要使用JWT（JSON Web Tokens）库在Python中生成token，通常会用到`PyJWT`这个库，它是处理JWT的一种流行方式。以下是一个简单的例子，展示了如何使用`PyJWT`生成和验证JWT token。

首先，你需要安装`PyJWT`库。可以使用pip进行安装：

```
con
```

然后，你可以编写一个函数来生成JWT token。下面的代码示例中，我们创建了一个`generate_token`函数，它接受用户信息作为参数，并返回一个生成的token。

```
import jwt
import datetime

def generate_token(user_info):
    try:
        # 设置token的过期时间，这里设置为24小时后过期
        exp = datetime.datetime.utcnow() + datetime.timedelta(days=1)
        # 你的JWT密钥，用于签名token，应保持安全
        secret_key = "YOUR_SECRET_KEY"
        
        # 创建一个字典，包含你想要放入token的信息
        payload = {
            'exp': exp,
            'iat': datetime.datetime.utcnow(),  # token的发行时间
            'sub': user_info  # 用户信息，比如用户ID或用户名
        }
        
        # 使用HS256算法生成token
        token = jwt.encode(payload, secret_key, algorithm='HS256')
        
        return token
    except Exception as e:
        return str(e)

# 假设有个用户的信息是 'user_id_123'，生成token
token = generate_token(user_info='user_id_123')

print("Generated token:", token)
```

注意：这里的`YOUR_SECRET_KEY`应该被替换成你自己的密钥，这个密钥在JWT的签名过程中使用，并且在验证token时也必须知道。

此外，`generate_token`函数中的`user_info`应该是一个唯一确定用户身份的信息，比如用户ID或用户名等。你可以根据自己的需要添加更多的信息到token的payload中。

记住，token中的信息都是可以被解码查看的，所以不要在token中放入敏感信息，除非它们是加密的。

使用上述方法，你就可以在你的应用中生成JWT token了。在用户登录成功后，调用这个函数并返回生成的token给用户。然后用户在后续的请求中携带这个token，服务器可以验证这个token来确认用户的身份。





>TypeError: 'AdminInfoTable' object is not subscriptable

问题出现在尝试从 `result` 对象中读取 'token' 字段时。报错信息显示 `'AdminInfoTable' object is not subscriptable` 意味着 `result` 是一个 `AdminInfoTable` 类型的对象，而不是字典（dict），因此不能像字典一样用 `result['token']` 这样的语法去获取数据。

关于是否需要在数据表中加一个 `token` 字段，这实际上取决于你的业务逻辑。通常，登录逻辑包括验证用户的用户名和密码，验证成功后生成一个用于认证的 token（比如使用 JWT），然后将这个 token 发送给前端，前端随后用这个 token 来进行后续的请求验证。

你不必在 `admininfo_table` 数据表中直接存储 token。Token 通常是在用户登录时按需生成的，然后在一定时间后过期。可以在服务端维护一个映射，关联用户和生成的 token，或者使用 JWT 这样的机制，它允许你在 token 自身中安全地存储用户信息。

 

因此，你可能需要在 `result` 返回的对象中加入 token 的处理，但这个处理并不是直接将 token 存储到数据库中，而是生成 token 并在登录成功时返回给前端。例如：

 

```
from flask import jsonify
from your_jwt_module import generate_token  # 假设这是你用来生成 token 的函数

# 假设 result 是成功认证用户后的对象
if result is not None:
    # 生成 token
    token = generate_token(result)  # 传入用户信息或唯一标识，生成 token
    return jsonify({
        'success': True,
        'message': '登录成功',
        'data': {
            'token': token,  # 返回生成的 token
        }
    }), 200
else:
    return jsonify({
        'success': False,
        'message': '用户名或密码错误'
    }), 401
```

请注意，`generate_token` 函数需要你自己根据实际情况来实现，可能会使用到 JWT 库等。这里只是提供了一个概念性的示例。



>当前这段vue代码中，使用了scss进行编写样式，为什么有些需要加`.`运算符，有些不加？ 

```vue
<template>
  <div class="login-container_me">
<!--    建立两个表单-->
    <div class="form">
      <div class="title">欢迎 <b>回来</b></div>
      <div class="subtitle">登录你的账户</div>
      <div class="inputf">
        <input type="text" placeholder="用户名"/>
        <span class="label">用户名</span>
      </div>
      <div class="inputf">
        <input type="text" placeholder="密码"/>
        <span class="label">密码</span>
      </div>
      <button>登录</button>
    </div>

    <div class="form"></div>
  </div>
</template>
<style lang="scss">
.login-container_me {
  width: 100%;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: url("../assets/img/background_picture.jpg") no-repeat center center;
  background-size: cover;
  .form{
    width: 300px;
    height: 400px;
    background: rgba(17,25,40,0.75);
    backdrop-filter: blur(16px) saturate(0);
    border-radius: 10px;
    padding: 40px 60px;
    box-shadow: rgba(50,50,93,0.25) 50px 50px 100px -20px,
                rgba(0,0,93,0.5) 30px 30px 60px -30px,
                rgba(212,217,222,0.35) 2px -2px 6px 0px inset;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: flex-start;

    //标题样式
    .title{
      font-size: 18px;
      color: rgb(246,240,255);
      letter-spacing: 1px;
      font-weight: 300;

    }
    //副标题样式
    .subtitle{
      font-size: 11px;
      color: rgb(246,240,255);
      letter-spacing: 1px;
      margin-bottom: 35px;
    }
    //输入框这个整体结构的样式
    .inputf{
      width: 100%;
      position: relative;
      margin-bottom: 35px;
      input{
        width: 100%;
        height: 35px;
        border: none;
        outline: 1.5px solid rgb(200,200,220);
        background: transparent;
        border-radius: 8px;
        font-size: 12px;
        padding: 0 15px;
        color: rgb(246,249,255);
        &::placeholder{
          color: rgb(175,180,190);
        }
        //写鼠标聚焦效果
        &:focus{
          outline: 1.5px solid rgb(224,229,240);
          &::placeholder{
            opacity: 0;
          }
          & + .label{
            opacity: 1;
            top: -20px;
          }
        }
        //让上面的鼠标聚焦后，在输入文本到输入框之后，那个聚焦仍然在。
        &:not(:placeholder-shown)+.label{
          opacity: 1;
          top: -20px;
        }
      }
      .label{
        position: absolute;
        top: 0;
        left: 0;
        color: rgb(246,249,255);
        font-size: 11px;
        font-width: bold;
        transition: 0.25s ease-out;
        opacity: 0;
      }
    }
    button{
      width: 100%;
      height: 35px;
      background: rgb(36,217,127);
      color: #ffffff;
      border: none;
      outline: none;
      border-radius: 5px;
      font-weight: bold;
      font-size: 12px;
      cursor: pointer;
    }
  }
}
</style>
```

在提供的 Vue 组件中，使用了 SCSS 作为样式语言，这里涉及到了 SCSS 的嵌套语法。

在 SCSS 中，`.` 运算符用于表示类选择器。当你在 SCSS 中看到 `.className`，这意味着它选择所有具有 `className` 类的 HTML 元素。在你的代码中，`.login-container_me`、`.form`、`.title`、`.subtitle`、`.inputf` 和 `.label` 都是类选择器，用于应用特定样式到具有这些类的 HTML 元素。即，是类就加，不是类就不加。







>传递给守卫的参数· to、from 和 next各自代码什么意思？ 

在 Vue Router 的导航守卫中，`to`、`from` 和 `next` 是三个参数，它们具有特定的含义和作用：

- `to`: 这个参数代表==即将要进入的目标路由对象==。它包含了即将导航到的路由的信息，像是路径(`path`)、名称(`name`)、完整路径(`fullPath`)、hash、查询参数(`query`)和路由参数(`params`)等。此外，它还包含了之前提到的自定义 `meta` 字段。
- `from`: 这个参数代表==当前导航正要离开的路由对象==。其结构与 `to` 参数类似，包含了当前路由的相同集合的属性。使用 `from` 参数可以访问当前路由的信息，并根据这些信息执行诸如权限验证等逻辑。
- `next`: ==这是一个函数==，必须在全局前置守卫中调用它来解析这个钩子。执行 `next` 函数将会决定守卫钩子的行为。当调用：
  - `next()`：无参数时，表示放行，允许导航继续。
  - `next(false)`：中断当前的导航。如果浏览器的 URL 改变了（可能是用户手动或浏览器后退按钮），URL 地址会重置到 `from` 路由对应的地址。
  - `next('/path')` 或 `next({ path: '/path' })`：跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。
  - `next(error)`：如果传入任何参数且参数不是上述形式，导航会被终止并且该参数会传递给路由器的 `onError` 钩子。

这三个参数的配合使用可以让你对路由的访问进行全面控制，实现复杂的权限和重定向逻辑。



>如何在路由守卫中检查路由的 `meta` 字段？ 

在路由守卫中检查路由的 `meta` 字段非常简单。每次导航发生之前，全局前置守卫 `router.beforeEach` 会被调用，传递给守卫的参数 `to`、`from` 和 `next` 允许你对导航过程进行控制。

检查 `meta` 字段的步骤如下：

1. 在 `router.beforeEach` 的回调函数中，访问 `to` 对象（即将要进入的目标路由对象）。
2. 然后调用 `to.meta` 来获取目标路由的 `meta` 字段。
3. 通过 `to.meta` 下的属性（在你的例子中是 `requireAuth`）来决定是否需要进行某些操作，如重定向到登录页面、允许导航或取消导航。



实例：

```js
router.beforeEach((to, from, next) => {
  // 检查即将进入的路由配置中的meta字段的requireAuth属性
  if (to.meta.requireAuth) {
    // 根据情况做进一步处理
    // 比如：检查登录状态等
    if (用户已经登录) {
      next(); // 允许继续导航
    } else {
      next('/login'); // 重定向到登录页
    }
  } else {
    next(); // 如果不需要登录权限，直接允许导航
  }
});
```





>为什么要使用 `to.meta.requireAuth` 来判断路由是否需要登录权限？ 

使用 `to.meta.requireAuth` 来判断路由是否需要登录权限是因为在Vue Router中，每个路由记录可以带有一个 `meta` 字段，你可以在这个字段中设置自定义的路由元信息。`meta` 字段是一个可以存储任意值的对象，在路由记录中使用 `meta` 字段来定义额外的信息是一种常见的做法。

设置 `requireAuth` 属性是 Vue Router 的一种约定用法，用以说明访问该路由是否需要用户已登录。通过在路由元信息中标记 `requireAuth` 参数，可以让你的路由配置变得清晰和易于管理：

- 当 `requireAuth` 设置为true时，表示该路由需要登录才能访问。
- 当 `requireAuth` 设置为false或者没有设置时，表示该路由不需要登录就可以访问。

这种方式使得你可以轻松地判断某个路由是否受保护，而不需要在每次路由跳转的时候写复杂的逻辑。路由守卫（如 `beforeEach`）可以检查每个即将进入的路由的 `meta` 字段，来决定是否需要进行权限控制。





>当前在表头的这段代码的意思`:data="tableData.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))" `是什么？

将这一切放在一起，这段代码的含义是：如果 `search` 为空，就返回所有 `tableData`；如果 `search` 非空，那么仅返回 `name` 属性在忽略大小写的情况下包含 `search` 文本的数组元素。这常用于实现搜索框进行实时搜索过滤表格数据的功能。 

- `:data` 是一个 Vue 的动态属性绑定，它等价于 `v-bind:data`，用于绑定表格组件的 `data` 属性。
- `tableData` 应该是一个包含所有表格行数据的数组。
- `.filter(...)` 是 JavaScript 数组的一个方法，用于根据提供的测试函数创建一个新数组，该函数返回那些测试返回真值的元素。
- `data => ...` 是一个箭头函数，它接受数组中的每一个元素（这里表示为 `data`）并对其执行测试。
- `!search` 检查 `search` 变量是否不存在（空字符串、`null`、`undefined` 等），如果 `search` 为空，则表达式返回 `true`，意味着不进行过滤，所有 `tableData` 会被返回。
- `data.name.toLowerCase().includes(search.toLowerCase())` 是一个测试条件，它会把 `data` 元素的 `name` 属性转为小写字母，然后检查它是否包含（`includes`）转为小写的 `search` 字符串。如果包含，返回 `true`。
- `||` 是逻辑 OR 运算符，如果左边的表达式结果为 `true`，那么整个表达式结果为 `true`，否则计算右边的表达式。

注意：

在你的代码中，错误信息 "TypeError: data.name_val is undefined" 指出了问题所在：当你尝试访问数组中每个元素的 `name_val` 属性时，发生了错误。这个问题可能是因为在你的 `tableData` 数组中，至少有一个对象不包含 `name_val` 属性，或者该属性的值是 `undefined`。 

也就是，写在过滤中的`data`是绑定在此的对象`tableData`中的对象。==> 完成





>前台展示的时间信息中，将数据库中的存储格式转变为了方便JSON传递的格式：`  "Fri, 19 Apr 2024 12:28:54 GMT"`。请问我应该如何恢复数据库中的存储格式`2024-04-19 12:28:54`并展示在前台?

要将日期时间从 `Fri, 19 Apr 2024 12:28:54 GMT` 格式转换为 `2024-04-19 12:28:54` 格式并在前端展示，你可以使用JavaScript的 `Date` 对象和 `Intl.DateTimeFormat` API来实现这一格式转换。

以下是一个示例代码段，显示了如何在Vue.js组件中完成这个转换：

```vue
<el-table-column label="创建时间" prop="CreateTime">
  <template slot-scope="scope">
    <span>{{ formatDate(scope.row.CreateTime) }}</span>
  </template>
</el-table-column>
```

 

接下来在Vue组件的`methods`中添加`formatDate`方法：

```js
methods: {
  formatDate(dateString) {
    const date = new Date(dateString);
    const options = { year: 'numeric', month: '2-digit', day: '2-digit', hour: '2-digit', minute: '2-digit', second: '2-digit', hour12: false };
    // 根据需要调整locale，这里使用'zh-CN'表示中国大陆地区
    const formattedDate = new Intl.DateTimeFormat('zh-CN', options).format(date).replace(/\//g, '-');
    // Replace the commas added by Intl in some locales such as 'en-US'
    return formattedDate.replace(',', '');
  }
}
```

 

这个`formatDate`方法首先使用`Date`对象将传入的日期字符串转换为日期对象，然后使用`Intl.DateTimeFormat`与一个选项对象来定义输出的格式。在这个例子中，我们指定了数字年份(`numeric`), 两位数字月份和日期(`2-digit`)，以及24小时制的小时、分钟和秒。`hour12: false`确保使用的是24小时制而非12小时制。

注意，`replace(/\//g, '-')`用于将日期分隔符从斜杠(`/`)替换为短横线(`-`)，以符合目标格式 `YYYY-MM-DD HH:mm:ss`。

这个方法会返回一个按照 `2024-04-19 12:28:54` 格式转换后的字符串，可以直接在前端页面中显示。

请根据你的具体需求调整locale和格式化选项。例如，如果你的用户主要在其他地区，你可能需要根据那里的习惯调整日期和时间的格式化方式。





>我前台的代码中，对数据表中是否启用字段的展示如下： ``` <el-table-column label="是否启用" prop="IsUse"> </el-table-column> ``` 但是按照后端反馈的代码中。IsUse=true或者false。我应该如何编写，才能够在表格中展示 ?

在Vue.js 中，你可以使用自定义模板来定制 `el-table-column` 渲染单元格的方式。可以通过 `<template>` 与作用域插槽 `scope` 来实现这个目的。

在 `scope` 对象中有一个属性 `row`，它包含了当前行的数据。你可以使用这个属性来判断 `IsUse` 字段的值，并相应地显示 "启用" 或 "未启用"。

下面是实现这一功能的代码示例:

```vue
<el-table-column label="是否启用" prop="IsUse">
  <template slot-scope="scope">
    <span v-if="scope.row.IsUse">启用</span>
    <span v-else>未启用</span>
  </template>
</el-table-column>
```



在这个例子中，我们使用了 `v-if` 和 `v-else` 指令来基于 `IsUse` 字段的值条件渲染不同的文本。当 `IsUse` 为 true 时显示 "启用"，否则显示 "未启用"。

请确保在实际代码中`prop="IsUse"`所指向的属性与你后端发送的JSON对象中的对应属性名完全一致，大小写敏感。如果属性名正确，则上述代码应该按预期工作。







>我一个flask项目中只能有一个SQLAlchemy实例吗？ 

是的，在一个Flask应用程序中，通常情况下，你只应该创建并使用一个`SQLAlchemy`实例。这是因为`SQLAlchemy`实例负责管理数据库的连接和会话，多个实例可能会导致不可预测的行为，例如连接泄露、事务管理问题或者难以维护。 





>MYSQL数据库中可以存储庞大的机器学习训练后的模型吗，其是.pkl文件，有些模型文件可能高达数百MB ?

因此，针对这种情况，一种较好的做法是只在数据库中存储这些大型文件的路径，而实际的文件被保存在文件系统中。这样可以利用数据库快速查询文件路径的优点，同时避免了上述提到的一些问题。 





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

Vue项目中添加 页面 标签页 的 小图标_vue 标签的小图标-CSDN博客 —— 有三个位置要改。
https://blog.csdn.net/qq_41709082/article/details/98855528

Pycharm：鼠标滚动控制字体大小 - PamShao - 博客园
https://www.cnblogs.com/pam-sh/p/13173747.html

conda 查看python包版本-掘金
https://juejin.cn/s/conda%20%E6%9F%A5%E7%9C%8Bpython%E5%8C%85%E7%89%88%E6%9C%AC

安装scikit-learn-scikit-learn中文社区
https://scikit-learn.org.cn/lists/1.html

在vue2中，使用vue-awesome-swiper的坑 - 掘金
https://juejin.cn/post/7348247657284173874

vue2.0和vue3.0的Vue-Lazyload的使用_vue-lazyload版本-CSDN博客
https://blog.csdn.net/kkfake/article/details/128415360

图片懒加载v-lazy的使用 - 掘金
https://juejin.cn/post/7185065866592010301

强烈推荐7个国外图片资源网站 - 知乎
https://zhuanlan.zhihu.com/p/108643049

