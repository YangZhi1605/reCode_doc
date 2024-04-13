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
    # 将单行的电压比率列表加入到结果列表
    all_voltage_ratios.append(voltage_ratios)

# 打印或返回结果
print(all_voltage_ratios)
```











#### 2.5、维修信息日志

这里的设计思想是：在当前组件中，用户点击`健康状态分析`按钮后，会记录一个日志信息，其中包括`用户名`，`分析时间`，`分析结果文本`，`用户处理文本`。将这个日志信息传递给后端，后端需要存储到数据库中。

用户点击跳转到维修信息日志页面时，读取数据库中的信息，然后展示，进而可以实现增删改查以及对用户处理标记进行输入。

先把前台做了，后面再去做后端的业务接口。









## 后台

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

| 编号 | 测试功能           | 预期结果                                                     | 测试结果 |
| ---- | ------------------ | ------------------------------------------------------------ | -------- |
| 1    | 文章发布功能       | 用户登录系统后，可以编写文章进行发布，编辑完成后点击发布按钮进行文章发布，文章进入审核流程。 | 符合预期 |
| 2    | 文章保存为草稿功能 | 未编辑完的文章可以暂时储存为草稿之后再进行编辑，如果文章被管理员下架或者审核不通过，也将存放至草稿箱。 | 符合预期 |
| 3    | 文章修改和删除功能 | 已发布的文章的作者有权限对文章进行修改和删除。               | 符合预期 |
| 4    | 文章点赞功能       | 用户浏览完文章后，可以通过点赞给作者一些鼓励，点赞信息记载文章的点赞总数。 | 符合预期 |
| 5    | 文章管理功能       | 登录的用户若是管理员，则具有权限进入后台进行文章管理，包括审核文章、下架文章、设置文章的标签。 | 符合预期 |

暂时放一下测试模块



我现在有一个prompt。请帮助我完成我的需求： 



我将提供给你我每个模块的详细设计，请你结合我的详细设计帮我生成每个功能点的测试表格，其中测试结果均填写符合预期。表头为编号、测试功能、预期结果、测试结果。 各模块功能介绍如下： 

（1）    用户登录模块：。 

（2）    文章保存为草稿：未编辑完的文章可以暂时储存为草稿之后再进行编辑，如图4.x所示。用户还可以对文章以及草稿进行修改与删除。草稿功能还用于存放被管理员下架或者审核不通过的文章。 

（3）    文章修改与删除：已经发布的文章，作者有权限对文章进行修改和删除。作者点击自己的文章，系统会根据权限判断当前登录用户是否具有修改和删除权限，如果有才会显示编辑按钮。作者可以点击编辑，进入文章发布的页面。当前页面和发布文章是的页面是同一个页面，但是区别在于发布文章时输入框中的内容均为空白，而编辑文章时输入框中的内容为当前所编辑文章的内容，这一功能的实现得益于Vue的模块复用设计。在编辑完成后，同样能够将文章暂时保存为草稿。 

（4）    点赞：当用户浏览完文章后，觉得文章有所帮助，可以通过点赞给作者一些鼓励。点赞功能的实现通常涉及到存储用户的点赞信息以及计算文章的点赞总数。使用Redis作为后端存储是一种常见的选择，因为Redis是一个高性能的内存数据库，适合处理类似计数和缓存的任务，对于读取频繁的操作可以提供高性能的缓存。将热门数据存储在Redis中，可以减轻数据库的负担，提高访问速度。Redis的原子性操作使得计数非常高效。在点赞场景中，使用Redis可以方便地实现对文章点赞总数的实时更新。引入Redis后还需要考虑Redis和数据库数据同步问题，在本系统中采用定时更新到数据库的方案解决。 

（5）    文章管理功能：登录的用户若是管理员，则具有权限进入后台进行文章管理。用户可以在后台审核文章、下架文章、设置文章的标签。其中审批功能中，系统引入自动审核与人工审核相结合的方式，自动审核利用腾讯云文本审核功能，对文章进行初步审核。对于通过自动审核但仍存在疑似违规的文章，管理员将进行人工审核，确保文章内容的合规性和规范性。管理员在后台可以随时查看已发布的文章，对违规、不当或不符合平台规范的文章进行下架处理。这一功能保障了平台内容的质量，维护了用户的良好体验。管理员有权限对文章的标签进行设置和调整。标签与话题结合，有助于对文章进行更精准的分类。管理员可以创建、编辑和删除标签，同时关联标签至平台的话题，以引导平台的话题走向，确保平台内容更有层次和组织性。 ``` 





**等级得分表**

>最后附带一个等级得分表



#### 2.3、信息管理页面

这里继续上一个页面的监测结果。对维护信息进行日志统计



#### 2.4、订单页面

这里用户可以在本网址购买一些零件

















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

Vue项目中添加 页面 标签页 的 小图标_vue 标签的小图标-CSDN博客 —— 有三个位置要改。
https://blog.csdn.net/qq_41709082/article/details/98855528



