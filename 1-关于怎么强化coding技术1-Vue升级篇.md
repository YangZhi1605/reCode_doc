>**强化卷开启——本卷聚焦Vue相关内容**

## Start —— vue强化



## Body



## Question



>路由管理这儿你觉得有哪些让你觉得恍然大悟的参考资料了？

B站那个



>这种写法是按照什么原理导入的了？ ``` import transition from '@/components/layout/transition'; ``` 

这种写法是在使用 ES6 的 `import` 语句来导入模块。在这里，`import transition from '@/components/layout/transition';` 这条语句的原理和含义如下：

- `import` 关键字是用来导入由另一个模块导出的绑定（可以是函数、对象、原始类型等）。
- `transition` 是你定义的名称，表示导入的 `@/components/layout/transition` 模块的默认导出。你可以在代码中使用这个名称来访问模块导出的内容。
- `from` 关键字后面跟着的是一个字符串，表示导入模块的路径。
- `'@/components/layout/transition'` 是一个路径别名。在 Vue CLI 项目中，`@` 符号通常被配置为指向 `src` 目录，这是一种快捷方式，使得开发者无需写相对路径就能轻松地引用 `src` 目录下的文件或模块。

因此，这条导入语句的含义是：从项目的 `src/components/layout/transition` 目录下导入 `transition` 模块，并将它的默认导出绑定到名字为 `transition` 的本地变量。这种方式在组织大型 Vue 项目时尤其有用，因为它简化了文件引用的路径，使得开发者更容易维护和管理项目代码。



>项目的整理中遇到的问题——我github上拉取下来的项目和仿小米商城之间的区别是什么了？



>`<router-link>`这个组件是vue自带的吗？我通过npm list查看当前项目按照的依赖，并没有<router-link> ?

`<router-link>` 是 Vue Router 库中提供的组件，并不是 Vue.js 核心库的一部分。Vue Router 是 Vue.js 的官方路由库，为在 Vue.js 应用程序中创建单页应用提供路由功能的插件。如果你想要在你的 Vue.js 项目中使用 `<router-link>` 组件，你需要确保你已经安装并使用了 Vue Router。 

如果项目中尚未安装 Vue Router，你可以通过运行 `npm install vue-router` 来添加它。安装完成后，你需要在项目中配置并插入 Vue Router，通常这是在项目的入口文件（如 `main.js` 或 `app.js`）中完成的 



> `node-sass`无法编译 怎么解决？ —— 废除 —— **学到一个清除npm缓存和删除node_module文件夹**
>
> 此错误信息表明您在尝试编译`node-sass`时遇到了问题，这通常是由`node-gyp`需要Python环境而未能找到导致的。`node-gyp`是一个用于编译本地addon模块的工具，它需要Python（2.7版本，不支持Python 3.x）和一个C/C++编译器。 

**6、清理npm缓存和node-modules**： ——==不起作用==
清理`npm`缓存和`node_modules`文件夹，然后重新运行npm install尝试：

```
npm cache clean --force
Remove-Item node_modules -Recurse -Force
```



> `node-sass`和`Node.js`的的区别是什么了？**不再使用node-sass了，与nodejs16不兼容**

`node-sass`是一个库，它允许你在Node.js环境中将SASS (Syntactically Awesome Style Sheets) 文件编译成CSS。SASS是一种预处理器脚本语言，它会被编译成Cascading Style Sheets (CSS)。SASS让开发者使用变量、嵌套规则、混合 (mixins)、继承等特性来编写更加动态和管理起来更加容易的样式表。

`nodejs`则是一个基于Chrome V8引擎的JavaScript运行时环境，它让开发者可以在服务器端运行JavaScript代码。Node.js采用了事件驱动、非阻塞I/O模型，使其轻量又高效，非常适合处理大量并发的数据密集型操作。

**它们之间的关系可以这样理解：**

- **Node.js** 提供了一个平台，使得JavaScript可以脱离浏览器运行，这包括了文件系统的操作、网络请求等服务器端功能。
- **node-sass** 则是一个第三方库，它依赖于Node.js，提供了SASS到CSS的转换功能，让开发者在Node.js的环境中更加高效地编写和维护样式表。

在构建现代网站和应用程序的过程中，特别是当使用了一些构建工具（如Webpack）和框架（例如React、Vue或Angular）时，`node-sass`作为构建链的一部分可以自动编译`.scss`或`.sass`文件为浏览器可以理解的`.css`文件。

需要注意的是，`node-sass`是依赖于一个名为`libsass`的C/C++库的，后者负责实际的编译过程。因此，在安装`node-sass`时，它会使用`node-gyp`编译`libsass`的二进制绑定到Node.js环境中。这一过程可能需要你在系统上安装额外的工具链，比如Python或是C/C++编译器。



>**首先在这里暂时把sass和scss统一看成sass** 
>
>**关系链：**vue中欲想使用sass，需要下载sass-loader，sass-loader需要依托于node-sass运行，node-sass的运行环境是node，所以说需要下载sass-loader和node-sass两个包，同时node-sass要兼容node版本。





> **关于vue-cli2下的package.json认识是什么了？**
>
> 对于一个vue-cli2的项目，其需要的所有依赖都是写在package.json文件中的吗？因此可以使用npm insatll 去安装需要的库。

是的，对于一个使用vue-cli 2创建的Vue.js项目，所有的依赖通常都会列在`package.json`文件的`dependencies`和`devDependencies`中。`dependencies`部分包含了项目运行时必须的库，而`devDependencies`则包含了开发过程中需要的工具和库，比如测试框架、代码压缩工具等。

运行`npm install`命令会根据`package.json`中列出的依赖，安装所有需要的库到`node_modules`文件夹中。这样确保了任何有相同`package.json`文件的开发环境都可以安装相同版本的依赖，从而有助于避免因不同的依赖版本而引起的问题。

在执行`npm install`前，确认你的Node.js和npm是最新版或是符合项目需求的版本，这样可以减少不必要的兼容性问题。此外，如果项目比较早之前初始化的，那么还可能需要运行一些特定的命令来更新全局或局部的CLI工具。

记住，任何时候，当你克隆了一个新的Vue项目或者在不同的环境中设置相同的项目时，首先应该运行`npm install`，以便安装项目依赖的所有库。



>**Vue-cli2和Vue-cli3有什么区别了？**

vue-cli2和vue-cli3在脚手架开发中确实存在一些区别，同时，它们的项目目录结构也有一些不同。

**vue-cli2:return {**
初始化过程比较繁琐，需要手动进行一系列的配置；
所有的配置信息全都暴露给开发者；
配置文件主要是在项目目录中的`config`和`build`文件夹中；
具备E2E和单元测试；
支持服务端渲染。

其目录结构如下：

```bash
.
├── build/                      # webpack config files
│   └── ...
├── config/
│   ├── index.js                # main project config
│   └── ...
├── src/
│   ├── main.js                 # app entry file
│   ├── App.vue                 # main app component
│   └── ...
├── static/                     # pure static assets (directly copied)
├── test/
│   └── unit/                   # unit tests
├── .babelrc                    # babel config
├── .postcssrc.js               # postcss config
└── .gitignore
└── ...
```

**vue-cli3:return {** 

脱离了webpack模板，提供了一种新的扩展方式； 默认隐藏了所有的webpack配置，减少项目的配置文件，使得结构更简洁； 具有强大的图形化界面，集成了检查和报错等功能； 更人性化的提示信息，帮助开发者对问题进行定位； 

```ba
.
├── public/                     # pure static assets (directly copied)
│   └── ...
├── src/
│   ├── main.js                 # app entry file
│   ├── App.vue                 # main app component
│   └── ...
├── tests/
│   └── unit/                   # unit tests
├── .browserslistrc             # browserslist config
├── .eslintrc.js                # eslint config
├── .gitignore                  # specifies intentionally untracked files to ignore
└── ...
```



>假如我使用webstorm软件开发Vue项目的项目。可以即创建运行vue-cli2的项目，又可以创建运行vue-cli3的项目吗？ 

是的，你完全可以在Webstorm这个IDE中创建和运行使用vue-cli2和vue-cli3初始化的项目。

这两个版本的脚手架工具都可以创建可运行的Vue项目，在Webstorm中运行这些项目没有问题。**只需记住，在使用任何脚手架工具时，都必须确认你的系统已经安装了这个工具。如果你的系统中已经安装了vue-cli2和vue-cli3**，你就可以在Webstorm中创建和运行由这两个工具创建的项目。



>一台电脑系统重可以即安装vue-cli2工具又安装vue-cli3工具吗。即使可以，那么应该如何区分这两个工具了？ 

对于安装vue-cli2和vue-cli3在同一台电脑上，有一些需要注意的地方。

一般来说，它们是不能同时存在的，因为它们都会安装一个名为`vue`的全局命令。换句话说，如果你先安装了vue-cli2，然后再安装vue-cli3，`vue`命令将被vue-cli3覆盖。

但是，vue-cli3给出了一个解决方案，也就是提供了一个新的命令，名为`vue-cli-service`，它是在每个用vue-cli3创建的项目中局部安装的。换句话说，即使你全局安装的是vue-cli2，你仍然可以在vue-cli3的项目中使用`vue-cli-service`命令。

所以，如果你希望装有两个版本的脚手架工具，你可以通过以下步骤进行：

1.首先，全局安装vue-cli2，使用以下命令：

```bash
npm install -g vue-cli
```

此时你可以使用 `vue` 命令来创建和维护vue-cli2的项目。

2.当你需要创建vue-cli3的项目时，你不需要全局安装vue-cli3。相反，你可以用npx（npm5.2+自带的工具）来暂时安装并使用vue-cli3，创建项目的命令如下：

```bash
npx @vue/cli create my-project
```

时的`my-project`是你的项目名称，你可以更换成你自己想要的项目名。项目创建完成后，你可以进入项目文件夹，用`npm run serve`命令来运行vue-cli3的项目。 



>那么。假如我是全局安装的vue-cli2，我从github上录取了vue-cli3的项目，我应该如何按照这个vue-cli3脚手架下的依赖了？仍然使用`npm install`吗？

是的，不论你是使用vue-cli2还是vue-cli3创建的项目，用来安装项目所需依赖的命令都是`npm install`。

当你从GitHub下载下来一个使用vue-cli3创建的项目后，你应该在项目的根目录下运行`npm install`来安装项目所需的依赖。这个命令会根据项目的`package.json`文件中的描述，从npm仓库下载所需的所有依赖包到项目的`node_modules`文件夹中。

值得注意的是，即使你是全局安装的vue-cli2，但是这并不影响你使用vue-cli3项目。因为每个由vue-cli（无论是2还是3）创建的项目，都会自动在项目中安装一个名为`vue-cli-service`的命令行工具，这个工具封装了webpack的所有配置，无需我们手动进行配置。在你运行`npm run serve`（或者其他npm scripts）的时候，事实上是用的这个`vue-cli-service`工具。

所以，在你全局安装了vue-cli2的情况下，你仍然可以下载、安装依赖、运行使用vue-cli3创建的项目。





>我运行上通过Vue-cli3创建的项目了。那么我应该如何修改端口号了？不太理解vue-cli3的目录结构 

这里有点子深。

端口被写到npm install后的`node_modules`文件夹下的`@vue`文件夹下的`cli-service`文件夹下的`lib`文件夹下的`serve.js`文件中

![1713251407752](E:\文档_Typora\1-关于怎么强化coding技术1-Vue升级篇.assets\1713251407752.png)





>在用`node-gyp`工具编译`node-sass`时出错了 怎么解决了？ 

```bash
E:\develops\workspace_webstorm_vue2_vuecli3\vuecli3_repository\MiMall\node_modules\node-sass        
npm ERR! gyp ERR! node -v v16.18.1
npm ERR! gyp ERR! node-gyp -v v3.8.0
npm ERR! gyp ERR! not ok
npm ERR! Build failed with error code: 1
```

核心大致就是上面这种。罗列出各个版本。

 `node-sass` 在构建时需要使用 `node-gyp`。你的 `node-gyp` 版本是 `3.8.0` 而你的 Node.js 版本是 `16.18.1` ，此时就版本不兼容了。

怎么解决？

**将原本依赖中的node-sass和sass-loader卸载，然后 “npm install -D sass-loader@^10 sass”，即可启动项目(但是是在vue-cli3搭建的项目中)** 

```bash
npm uninstall node-sass
npm uninstall sass-loader
npm install -D sass-loader@^10 sass
```

当然，node16确实也有点问题。也有将node降回14的。

对于vue-cli2的项目，

```
npm install --save-dev sass
```

不然应该是webpack版本不兼容





>这个指令`npm install --global --production windows-build-tools`可以在Windows终端执行吗？ 
>
>—— 废除

是的，你可以在Windows命令行工具（如cmd或者PowerShell）中执行指令`npm install --global --production windows-build-tools`。这条指令将会全局安装windows-build-tools，这个npm包含有在Windows系统中构建本地addon的所有必需工具，包括Python、MSBuild和C++ Build Tools。这通常可以解决大部分的本地编译问题，尤其是对于需要编译的依赖，如`node-sass`。 

**但是一阵子折腾后得知：**

此外，现在已经不建议使用Python 2.7了，因为Python 2.7已经在2020年1月停止了支持。对于新的项目，推荐使用Python 3.

另外，`windows-build-tools`这个npm包已经被废弃，因为Node.js现在已经自带了构建工具。建议你看一下这个库的官方描述：<https://github.com/felixrieseberg/windows-build-tools> ，可能你并不需要这个工具。



>webpack和vue-cli之间的关系是什么？ 

Webpack 是一个现代 JavaScript 应用程序的静态模块打包器。它会根据应用程序的文件和模块的依赖图，生成一个或多个 bundle。它可以处理各种资源，比如 JavaScript，CSS，和图片等，通过使用 loader 转换这些资源，使得它们可以在打包中被添加。

Vue CLI 是一个官方发布的脚手架，用于快速生成 Vue.js 项目的结构。Vue CLI 在内部使用 webpack 作为其构建工具。基本上，当你通过 Vue CLI 创建一个新项目时，它会提供一个预先配置好的 webpack 配置文件（以及许多其他的工程化配置），这样你就不需要从头开始设置 webpack。

总结来说，vue-cli 是为了简化 webpack 的配置和项目的初始化流程，给予开发者一个开箱即用的 Vue.js 开发环境。WEBPACK 本身是构建工具的核心，Vue CLI 是在 Webpack 基础上提供了高层次的抽象，简化了项目的创建和配置工作。



>如何查看vue-cli2构建的项目中webpack的版本？ 

在使用 Vue CLI 2 创建的项目中，你可以通过几种方法来检查 Webpack 的版本：

**查看package.json文件**:
打开项目根目录下的`package.json`文件，然后查看`devDependencies`和`dependencies`部分，找到`webpack`条目。版本号应该标在名称后面。

**使用npm或yarn命令**:
打开终端或命令行工具，导航到你的项目目录，然后运行如下命令：

```bash
npm list --depth=0 webpack
```

这会列出项目中安装的 webpack 及其版本。 —— 我毕设的vue-cli2的版本：` webpack@3.12.0`

**检查项目的node_modules目录**:
你也可以直接去到项目的`node_modules/webpack`目录中，然后查看里面的`package.json`文件，其中会包含该 webpack 包的版本信息。

 

由于 Vue CLI 2 自身搭载了一定的 webpack 版本，即使你在项目的`package.json`中没有明确看到 webpack 的版本，CLI 工具也依赖于特定的 webpack 版本。要查看这一信息，你需要查看全局安装的 Vue CLI 2 的依赖，方法如下：

 全局查看 Vue CLI 2 的 webpack 版本：

```bash
  npm list -g --depth=0 @vue/cli npm list -g --depth=0 @vue/cli
```

 在列出的包中找到对 webpack 的引用，来确定 Vue CLI 2 使用的 webpack 版本。

请注意，Vue CLI 2 默认使用 webpack 3，在大多数官方模板中都是这样配置的。





>**我现在的node.js的版本是16。用vue-cli2构建的项目中webpack版本是3.12.0。我此时需要使用sass和scss。但是与node.js适配的node-sass版本是6.0+。但是webpack是3的版本，只能支持6.*的node-sass。我并不想舍弃项目，我此时应该怎么样才可使用sass?** 

首先，需要明确一点，`node-sass` 是依赖于 Node.js 的版本来编译的，而 `webpack` 使用的是 `sass-loader` 来作为 `node-sass` 或 `sass` (Dart Sass) 的桥梁。因此，问题在于 `sass-loader` 及其依赖的 `node-sass` 版本与你的 Node.js 版本是否兼容。 

==也就是，sass的使用需要嗲用Node.js，因此这里有一个版本适配；然后，webpack又使用sass-loader来调用node-sass或者sass，因此又出现了sass-loader与node-sass或者sass的适配，以及，webpack与sass-loader的适配==

第一组适配：

![1713271935576](E:\文档_Typora\1-关于怎么强化coding技术1-Vue升级篇.assets\1713271935576.png)

第二组适配（这张图有点错误）

![1713271870654](E:\文档_Typora\1-关于怎么强化coding技术1-Vue升级篇.assets\1713271870654.png)

第三组适配：

![1713272005024](E:\文档_Typora\1-关于怎么强化coding技术1-Vue升级篇.assets\1713272005024.png)

我现在是`Node.js16`，也就是需要`node-sass6.0+`，然后`webpack3`需要`sass-loader6.0*`。最后，`node-sass6.0+`需要`sass-loader10.0.1`相关的。==因此我这里使用node-sass是死局==

>如何获取sass-loader的所有发行版本？

```bash
npm view sass-loader versions --json
```



>那么，我现在需要使用sass或者scss应该怎么办？

升级webpack可能可以解决这种。高版本之间适配会好一些。但是我不能，我升级了项目可能就西内了。

**①**`webpack@3.12.0` ==> 先去把能够驱动node-sass或者scss的，`sass-loader`版本安装好。【`npm install sass-loader@7 --save-dev`（`sass-loader@7.0.0`支持`webpack` 3和4）。】

```bash
npm install sass-loader@7 --save-dev
```



**②**安装`sass`驱动Node.js。不使用`node-sass`来驱动Node.js，此时就不用考虑sass与Node.js的版本问题了。

```bash
npm install --save-dev sass
```

然后运行 `npm install --save-dev sass` 或者 `yarn add --dev sass` 来安装 Dart Sass。完成这些操作后，sass-loader 将会优先使用 Dart Sass 来解析 .scss 或 .sass 文件。 

最后结果：

![1713276613053](E:\文档_Typora\1-关于怎么强化coding技术1-Vue升级篇.assets\1713276613053.png)

**`老子，tmd，改了一天，我rtw`**

**③** **更新webpack配置** 

你需要在`webpack`的配置文件(`webpack.config.js`)中，向`module.rules`添加一条新的rule来处理`.sass/.scss`文件。在这个规则中，你需要指定`sass-loader`，`css-loader`和`style-loader`来处理文件 

```js
// webpack.config.js
module.exports = {
  // ...
  module: {
    rules: [
      //...
      {
        test: /\.s[ac]ss$/i, // 用于匹配 .sass 或 .scss 文件
        use: [
          // 将 JS 字符串生成为 style 节点
          'style-loader',
          // 将 CSS 转化成 CommonJS 模块
          'css-loader',
          // 将 Sass 编译成 CSS
          'sass-loader'
        ],
      },
      // ...
    ],
  },
  // ...
};
   }
```



**④** **安装css-loader和style-loader** 

如果你的项目中还没有安装`css-loader`和`style-loader`，你需要安装它们： 

```bash
   npm install --save-dev css-loader style-loader
```

![1713277723351](E:\文档_Typora\1-关于怎么强化coding技术1-Vue升级篇.assets\1713277723351.png)



如果你开发的是Vue.js项目，并使用了Vue的单文件组件，建议使用`vue-style-loader`。在`vue-cli`搭建的项目中，默认配置就是使用`vue-style-loader`来处理`.vue`文件中的样式。那么，我不需要安装了。

如果你不使用Vue.js或者不需要HMR，那么`style-loader`是更适合你需要的。在Vue项目中也可以使用`style-loader`，但是你将无法充分利用Vue提供的HMR功能。



>无论是安装dart-sass，还是node-sass，更新webpack配置是一样的吗？ 

是的，无论是`dart-sass`还是`node-sass`，更新`webpack`配置文件(`webpack.config.js`)的方式是一样的。这是因为`sass-loader`作为连接`webpack`和Sass编译器（即，dart-sass或者node-sass）之间的桥梁，能够处理来自两者的输入。 

不管是`dart-sass`或`node-sass`，这两个Sass编译器对于`webpack`来说是透明的。`sass-loader` 会自动使用你在项目中安装的Sass编译器来处理`.sass/.scss`文件。如果两者都未安装，`sass-loader`将会报错。 

如果你刚开始使用Sass，并且你使用的是较新的环境，推荐使用`dart-sass`，因为`node-sass`已经过时，`dart-sass`是官方推荐的Sass实现，并且是持续更新支持的。 





>Node.js和npm的关系是什么？

`Node.js`是`JavaScript`的一种运行环境，是对Google V8引擎进行的封装。是一个服务器端的`JavaScript`的解释器。 

包含关系，`Node.js`中含有`npm`，比如说你安装好`Node.js`，你打开`cmd`输入`npm -v`会发现`npm`的版本号，说明`npm`已经安装好。

`npm`是`Node Package Manager`的缩写，它是`Node.js`的包管理和分发工具，用于管理`JavaScript`的包，包括安装、卸载、管理依赖等。





>npm是Node Package Manager的缩写，它是Node.js的包管理和分发工具，用于管理JavaScript的包，包括安装、卸载、管理依赖。那么，不同版本的Node.js就应该被管理不同的依赖，对吧？ 

是的，不同版本的Node.js可能依赖于或兼容于特定版本的npm包。这是因为随着时间的发展，Node.js和npm包都会更新，与之相关的API和功能也可能会发生变化。这些变化可能包括新功能的加入、旧功能的弃用或者是对性能的提升。由于这些更新，某个npm包的新版本可能会要求依赖更高版本的Node.js。

为了更好地管理这些依赖，npm提供了一些机制和工具，例如`package.json`文件，它允许包的开发者指定项目所依赖的包的版本范围。例如，如果某个包需要至少Node.js版本8.10.0，那么它可以在`package.json`文件中这样指定：

```json
"engines": {
  "node": ">=8.10.0"
}
```

 

这就确保了使用该包的开发者必须至少有这个版本的Node.js，从而避免了因版本不匹配造成的功能缺失或者运行错误。

开发者还可以使用版本管理工具如`nvm`（Node Version Manager）在同一台机器上安装并维护不同版本的Node.js。这样，就可以根据需要选择和切换到适当的Node.js版本，以保证所有依赖都得到正确的支持。

此外，并不是所有包都会随Node.js的每个新版本发布时更新其依赖要求。在许多情况下，npm包可以跨多个Node.js版本工作，特别是当这些版本的变化不太大的时候。因此，npm的语义版本控制（SemVer）就显得尤为重要，它允许包作者和用户理解版本号的变化对包的兼容性所产生的影响。



>那么，无论我的电脑安装的是Node.js16，还是Node.js14或者Node.js8。都是使用npm指令来管理。只是不同的版本中应该有不同的依赖包，对吧？ 

对的，无论你安装的是Node.js 16，Node.js 14，还是Node.js 8，都会用npm这个命令行工具来进行包管理。npm作为Node.js的包管理工具，负责安装、更新、卸载和管理Node.js项目的依赖包。

每个Node.js版本通常会捆绑一定版本的npm，以确保兼容性。尽管npm的基本命令（如`npm install`, `npm update`, `npm uninstall`等）在不同的Node.js版本下使用方式基本一致，依赖包的具体版本则由项目的`package.json`文件中指定的版本范围和实际的兼容性决定。

 例如，在一个Node.js项目里，你可能有如下的`package.json`：

```json
{
  "name": "my-awesome-project",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.17.1",
    "lodash": "^4.17.20"
  }
}
```

 

上述的`^4.17.1`意味着你可以安装`express` 4.17.1 及以上的版本，直到下一个主要版本（不包括5.0.0）。这样的版本控制限制使得开发者在新版本Node.js发布后不需要马上更新依赖包，但是有责任确保自己的代码与正在使用的所有依赖包的版本兼容。

因此，不同Node.js项目可能依赖不同版本的同一个包，这取决于`package.json`文件中指明的版本信息以及开发者对项目依赖进行更新和维护的情况。

总而言之，npm提供了一致的界面来处理不同Node.js版本的包管理问题，而具体的依赖版本管理则通过项目中的配置文件来具体控制。





>倘若我安装了sass-loader之后。我可以使用scss了。但是我项目原本使用的css样式会被破坏吗？ 

安装`sass-loader`后，你确实可以在项目中使用SCSS（Sassy CSS）了，这是一种CSS的预处理语言，它在CSS的基础上增加了变量、嵌套、混入（mixins）、继承等高级功能，使得样式表更加强大和易于维护。

但是，安装`sass-loader`本身不会影响到你项目原有的CSS样式。因为`sass-loader`只是一个webpack的加载器（loader），它允许你将`.scss`文件编译为CSS，进而被浏览器解析。这个过程是在构建或开发阶段发生的，不会修改已有的`.css`文件。

你可以在项目中同时使用`.scss`和`.css`文件。当你开始使用SCSS编写样式时，`sass-loader`会处理`.scss`文件，将它们转换为普通的CSS，并且将转换后的CSS注入到构建的最终输出中。现有的`.css`文件仍然会照常被处理。



>
>
>这种写法：
>```
>import axios from 'axios'
>import VueAxios from 'vue-axios'
>Vue.use(VueAxios,axios);
>```
>和我的写法：
>```
>import axios from './assets/dist/axios.min'
>import VueAxios from 'vue-axios'
>Vue.prototype.$axios = axios
>```
>有什么区别了？
>
>

这两种写法都是将`axios`库绑定到Vue的原型上，使得在Vue的任何组件中都能够通过`this.$axios`使用`axios`的功能。但是，两者使用的方式略有不同。

- 使用Vue插件`vue-axios`：

```
    import axios from 'axios'
    import VueAxios from 'vue-axios'
    Vue.use(VueAxios,axios);
```

```
这段代码先导入`axios`库和`vue-axios`插件，然后通过`Vue.use`方法使用`vue-axios`插件，并将`axios`实例传入作为参数。`vue-axios`插件的作用是将`axios`绑定到`Vue`的原型链上，使得在任何Vue组件中，都可以通过`this.axios`或`this.$http`访问`axios`。
```

 

- 直接在原型链上添加`axios`：

 

```
    import axios from './assets/dist/axios.min'
    Vue.prototype.$axios = axios
```

```
这段代码直接将`axios`库导入，并手动地将它添加到Vue的原型链上，也就是直接在`Vue.prototype`对象上添加了一个名为`$axios`的属性，值为`axios`库的实例。这样一来，在任何Vue组件中，也可以通过`this.$axios`访问`axios`。
```

总的来说，两种方式都能实现将`axios`添加到Vue原型链上的目的，只不过方式略有不同。`vue-axios`是一个第三方插件，它为将`axios`实例添加到Vue原型链上提供了一个更“Vue式”的方式，即采用了`Vue.use()`的方式。而直接在原型链上添加`axios`的方式更直接，不需要引入额外的插件，但需要你手动地操作原型链。

在选择使用哪种方式时，你可以根据自己的需要和项目的情况来决定，例如考虑到是否需要引入额外的依赖，以及是否希望采用更符合Vue习惯的方式来操作等。







## Reference

npm ERR! reason: certificate has expired（淘宝镜像过期）_2.4.tgz failed, reason: certificate has expired-CSDN博客
https://blog.csdn.net/qq_49907632/article/details/135974644

前端报错 request to https://registry.npm.taobao.org/yorkie/download/yorkie-2.0.0.tgz failed, reason: certificate has expired - 朱呀朱~ - 博客园
https://www.cnblogs.com/zhu-ya-zhu/p/18091292

npm i 报一堆版本问题_yorkie-2.0.0.tgz failed, reason: certificate has e-CSDN博客
https://blog.csdn.net/m0_70752874/article/details/135763875

node版本升级到16，sass-loader兼容报错问题_node升级为16后,saaa-loader报错-CSDN博客 ——**wc，恩人。终于nm跑动了**
https://blog.csdn.net/weixin_44218698/article/details/123069769

升级 node16 后 vue 项目中 sass 报错踩坑记录 - 简书
https://www.jianshu.com/p/33e4cec41bd6

node.js16.13.1版本与node-sass4.7.2版本不兼容问题的解决 - 蔡地像徐坤 - 博客园
https://www.cnblogs.com/LEPENGYANG/p/15929780.html

vue使用sass以及如何选择版本 - 掘金 —— **讲清楚了scss和node-sass以及node、node-loader之间的关系**
https://juejin.cn/post/7047378050270363662#heading-2

sass-loader和vue版本对应_sass-loader对应vue版本-CSDN博客
https://blog.csdn.net/quhan6686/article/details/124949606

vue使用scss-CSDN博客—— node-sass与sass-loader的适配
https://blog.csdn.net/qq_42129143/article/details/129692221?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-3-129692221-blog-124949606.235%5Ev43%5Epc_blog_bottom_relevance_base4&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-3-129692221-blog-124949606.235%5Ev43%5Epc_blog_bottom_relevance_base4&utm_relevant_index=6

Node.js和npm的关系 - 踏步 - 博客园
https://www.cnblogs.com/mjtabu/p/14363424.html

Vue-cli 项目中 src 目录每个文件夹和文件的用法？ - 掘金
https://juejin.cn/post/7031892686579695629

