# 开发文档

# 功能介绍

科创管理平台共有5个功能模块：系统管理、人员分组、项目管理、知识产权与成果管理、财务管理。

- 系统管理：配置用户权限、角色，新增或删除用户、配置菜单栏
- 人员分组：对系统内用户进行分组，便于新建项目时批量添加项目成员
- 项目管理：新建项目（项目名称、项目状态）、新建计划（里程碑、任务）、计划实施（参与项目的所有成员均可提交计划新增的进度，经项目管理员审核后项目进度才会改变）
- 知识产权与成果管理：添加和管理专利、论文、软著、国标，成果可与项目关联
- 财务管理：财务设置（新增和删除预算和支出选项）、预算管理、支出管理

# 技术路线

前端使用`html`、`css`、 `js`( 即 `javascript` ) 语言，结合 `vue` 框架、`uniCloud-admin` 框架和 `element-ui` 组件库进行开发。

后端也使用 `javascript` 语言，使用 `uniCloud` 框架进行开发。服务器实际为阿里云服务器，`uniCloud`提供技术支持。

# 文件结构

参考[uniCloud-admin的文件结构](https://uniapp.dcloud.io/uniCloud/admin?id=%e7%9b%ae%e5%bd%95%e7%bb%93%e6%9e%84)

其中主要需要了解的是`pages` 目录和`components` 目录

`pages`目录下的文件是主要的视图文件，应用中的每一个页面都对应`pages`目录下的一个`.vue` 文件

对于需要复用的视图元素，封装为组件，放在`components` 目录下，比如`components/achieve-form/gb-form.vue` 是新建国标、编辑国标时都需要使用的表单，为了减少重复代码，将其封装为组件（`components`）来使用。

- uniCloud 阿里云空间相关文件
    - database 数据库配置文件（数据库表）
        - admin-achieve-gb.schema 国家标准
        - admin-achieve-paper.schema 论文
        - admin-achieve-patent.schema 专利
        - admin-achieve-software.schema 软著
        - admin-fund-budget.schema 预算
        - admin-fund-expense.schema 支出
        - admin-fund-expense-user.schema 每项支出-人员 关系表
        - admin-fund-project-budget.schema 项目-预算 关系表
        - admin-fund-project-expense.schema 项目-支出 关系表
        - admin-group.schema 分组
        - admin-group-user.schema 分组-组员 关系表
        - admin-plan-log.schema 工作日志
        - admin-plan-status.schema 计划
        - admin-project-approval.schema 项目批复材料
        - admin-project-conclusion.schema 项目结题材料
        - admin-project-draft.schema 项目策划材料
        - admin-project-establish.schema 项目立项材料
        - admin-project-group.schema 项目-分组 关系表 （已不再使用）
        - admin-project-leader.schema 项目-负责人 关系表
        - admin-project-member.schema 项目-成员 关系表
        - admin-project-stage.schema 项目
- common 公用 css 样式
    - uni.css 主要放置全局 css 样式
    - uni-icons.css 不用管
- components 放置所有自定义的组件，便于视图页面调用
    - achieve-form 成果管理表单文件夹，内含4种成果的表单（专利、论文、软著、国标）
    - download-excel 将变量导出为 excel 的组件
    - expense-progress 支出进度可视化组件
    - plan-form 计划表单
    - plan-gantt 任务实施甘特图
    - project-form 项目表单
    - project-selector 筛选项目组件，决定哪些项目显示在列表中
    - project-stage-selector 选择项目阶段组件，可通过属性`prop`配置是否显示“全部项目”
    - user-selector 选择人员组件
- js_sdk 存放部分js代码，用于页面配置，减少单页面的代码
    - option 各种选项和数值对应关系的配置文件，打开文件代码内容就明白了
        - gb.js 国标
        - paper.js 论文
        - patent.js 专利
        - plan-log.js 实施管理中的工作日志
- pages 视图页面代码存放于此

    所有文件夹的末级目录均含 `add.vue` `edit.vue` `list.vue` 三个文件，分别属于`新增`、`编辑`和`查看列表`功能的代码，对于没有编辑权限的用户，`编辑`页面有时也用作`查看详情`功能。

    - achievement 成果管理
        - gb 国家标准
        - paper 论文
        - patent 专利
        - software 软件著作权
    - fund 财务管理
        - budget 预算管理
        - expense 支出管理
        - settings 财务设置
    - group 人员分组
    - index 首页

        系统登录后展示的第一个页面

    - project 项目管理
        - do 实施管理
        - plan 计划管理
        - procedure 流程管理
    - system 系统管理

        这部分页面为`uniCloud-admin` 框架自带的页面

# 快速开始

## 获取源代码权限

源代码托管在codechina平台，属于私有项目，需要通过以下邀请链接经审核后获取权限。（需要提前注册 csdn 账户）

```python
https://codechina.csdn.net/invite_link?invite_code=G4HRL5oeT2sS1dMzyGmz
```

## 获取数据库权限

数据库使用 `uniCloud`，需前往 [https://unicloud.dcloud.net.cn/](https://unicloud.dcloud.net.cn/) 注册账户，然后联系数据库拥有者新增项目成员

## 安装 node 环境

node 环境中的 npm 用于管理项目所依赖的包

1. 去 [https://nodejs.org/en/](https://nodejs.org/en/) 下载安装包并安装，安装 LTS 版本即可
2. 检查是否安装成功：打开 cmd，用以下命令查看node版本

```
node -v
```

如果显示了版本号，则安装成功

## 安装 HBuilderX

HBuilderX 用作代码编辑器，安装 app 开发版的 HBuilderX 比较省事，网址：

[https://www.dcloud.io/hbuilderx.html](https://www.dcloud.io/hbuilderx.html)

安装完成后，打开 HBuilderX，工具-插件安装，安装新插件，点击 git 插件旁边的安装按钮。

## 导入源代码

1. 打开codechina平台的项目，点击“克隆”，复制“通过https克隆项目”的链接
2. 打开`HBuilderX` ，`文件`-`导入`-`从git导入`，粘贴刚才的链接，点击导入，根据提示使用自己的code china 账户导入。
3. 如果提示需要安装插件，则根据提示安装即可。
4. 导入成功后，可以在`HBuilderX`左侧看到项目文件夹。如果文件夹内容为空，则是导入失败，需要重新导入。

## 安装依赖

本项目使用了一些外部依赖，需要通过`npm`安装。打开项目根文件夹，在文件资源管理器中输入cmd然后回车可以在当前目录下打开cmd

[本项目使用的外部依赖及其官网如下](https://www.notion.so/bbdb46e1de754c338cb376f628c6d627)

本项目使用的外部依赖及其官网如下

| 依赖名称     | 网址                                                    | 功能               |
| ------------ | ------------------------------------------------------- | ------------------ |
| v-charts     | http://woolen.gitee.io/v-charts/#/                      | 绘制各种图表       |
| VueClipboard | https://github.com/Inndy/vue-clipboard2                 | 将变量复制到剪切板 |
| element-ui   | https://element.eleme.cn/#/zh-CN/component/installation | 组件库             |

安装外部依赖时，根据各依赖官网的介绍输入命令即可，需要在项目的根文件夹(`cmci-tech-admin-v2`文件夹里)打开cmd窗口，或者在其它地方打开 cmd 再修改路径。

```python
npm i v-charts echarts -S
npm install --save vue-clipboard2
npm i element-ui -S
```

## 运行项目

打开`HBuilderX`，然后任意打开项目中的一个文件，点击 `HBuilderX` 顶部的运行-运行到浏览器，选择自己电脑拥有的浏览器，即可开始编译，编译结束后会打开浏览器窗口显示项目运行结果。（或者也可以选择运行到内部浏览器，编译结束后将窗口分离出来，见下图，然后双击分离出来的窗口顶部即可放大，然后选择`PC模式`查看效果）

![Untitled](%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3%20c3e8fcef87a4454eaa236e5c95f9e960/Untitled.png)

![Untitled](%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3%20c3e8fcef87a4454eaa236e5c95f9e960/Untitled%201.png)

在程序运行期间可以自由修改代码，代码保存后程序会自动重新加载（称为“热重载”），重载后会显示修改后的结果。一般来说修改 `vue` 和 `js` 文件后都可以重载成功，如果遇到修改代码后重载后的效果没变的情况，可以重新运行程序。编译过程中底部跳出来的窗口右上角可以重新运行和停止运行。

## 安装 electron 用于打包

使用`npm`进行安装，需要安装`electron`和`electron-packager`

```python
npm install electron -g
npm install electron-packager -g
```

## 项目打包app

[参考链接](https://ext.dcloud.net.cn/plugin?id=2905)

1. 在 `HBuilderX` 中，打开项目下的 `manifest.json` 文件，选择`h5配置` 
2. 将`运行的基础路径`设置为 `./`，并去掉`启用https协议`

    ![Untitled](%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3%20c3e8fcef87a4454eaa236e5c95f9e960/Untitled%202.png)

3. 点击`发行` -`网站-PC web或手机h5`，弹出来的窗口直接点击`发行`即可
4. 发行完成后，在项目文件夹里找到 `unpackage\dist\build\h5` 目录，创建以下两个文件并复制到`h5`文件夹里。

    1 文件名 `main.js`

    内容：

    ```jsx
    const { app, BrowserWindow, Menu } = require('electron')
    const path = require('path')
    const url = require('url')

    // Keep a global reference of the window object, if you don't, the window will
    // be closed automatically when the JavaScript object is garbage collected.
    let win

    function createWindow() {
      // Create the browser window.
      // win = new BrowserWindow({width: 800, height: 600})

      // 默认全屏
      // win = new BrowserWindow({ fullscreen: true })

      // 默认最大化
      win = new BrowserWindow({ show: false })
      win.maximize()
      win.show()
      // 取消顶部窗体菜单栏
      Menu.setApplicationMenu(null)

      // and load the index.html of the app.
      win.loadURL(url.format({
        pathname: path.join(__dirname, 'index.html'),
        protocol: 'file:',
        slashes: true
      }))

      // Open the DevTools.
      // win.webContents.openDevTools()

      // Emitted when the window is closed.
      win.on('closed', () => {
        // Dereference the window object, usually you would store windows
        // in an array if your app supports multi windows, this is the time
        // when you should delete the corresponding element.
        win = null
      })
    }

    // This method will be called when Electron has finished
    // initialization and is ready to create browser windows.
    // Some APIs can only be used after this event occurs.
    app.on('ready', createWindow)

    // Quit when all windows are closed.
    app.on('window-all-closed', () => {
      // On macOS it is common for applications and their menu bar
      // to stay active until the user quits explicitly with Cmd + Q
      if (process.platform !== 'darwin') {
        app.quit()
      }
    })

    app.on('activate', () => {
      // On macOS it's common to re-create a window in the app when the
      // dock icon is clicked and there are no other windows open.
      if (win === null) {
        createWindow()
      }
    })

    ```

    2 文件名：package.json

    内容：

    ```jsx
    {
      "name"    : "app-name",
      "version" : "0.1.0",
      "main"    : "main.js"
    }
    ```

    ![Untitled](%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3%20c3e8fcef87a4454eaa236e5c95f9e960/Untitled%203.png)

5. 使用 `cmd` 运行下面的命令，开始打包

    ```bash
    electron-packager . 科创管理平台 --win --out 科创管理平台 --arch=x64 --electron-version 13.1.8 --overwrite --ignore=node_modules
    ```

6. 打包完成后，`h5` 目录下会新增一个文件夹，打开后，里面的`科创管理平台.exe`即为可运行的应用

    ![Untitled](%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3%20c3e8fcef87a4454eaa236e5c95f9e960/Untitled%204.png)

# 如何学习

## 前端基础

网页主要由文字、图像和超链接等元素构成。当然，除了这些元素，网页中还可以包含音频、视频以及Flash等。浏览器是网页显示、运行的平台，常用的浏览器有IE、火狐、谷歌、Safari、Edge等。

互联网 web 开发分为前端和后端两部分。前端的任务是向后端发送用户请求，用户请求被后端处理后返回给前端数据，前端再把这些数据通过浏览器网页美观地展示给用户。后端的任务是接收前端发来的请求，对数据库进行增删改查以及数据处理，把得到的数据传给前端。

Web 标准主要包括结构（Structure）、表现（Presentation）和行为（Behavior）三个方面。分别对应 `html`、`css`和`Javascript` 。也就是说， `html` 用于展现网页的结构，`css` 用于美化样式，`Javascript` 用于和用户交互。

### HTML

HTML 指的是超文本标记语言 (**H**yper **T**ext **M**arkup **L**anguage)是用来描述网页的一种语言。HTML 不是一种编程语言，而是一种标记语言 (markup language)。网页是由网页元素组成的 ， 这些元素是利用html标签描述出来，然后通过浏览器解析，就可以显示给用户了。

HTML骨架标签：

```html
<html>
	<head>
		<title>页面标题</title>
	</head>
	<body>
		页面主体
	</body>
</html>
```

将上面的代码复制到一个空的 `txt` 文档中，将文件拓展名改为`.html`，用浏览器打开可看到页面。

**HTML常用标签**

| 标签名                       | 定义       | 说明                                  |
| ---------------------------- | :--------- | :------------------------------------ |
| ```<hx></hx> x为1~6的数字``` | 标题标签   | 作为标题使用，并且依据重要性递减      |
| ```<p></p>```                | 段落标签   | 可以把 HTML 文档分割为若干段落        |
| ```<hr />```                 | 水平线标签 | 就是一条线                            |
| ```<br />```                 | 换行标签   |                                       |
| ```<div></div>```            | div标签    | 用来布局的，但是现在一行只能放一个div |
| ```<span></span>```          | span标签   | 用来布局的，一行上可以放好多个span    |

主要知道`div`和`span`即可，`div`在一行只能显示一个，`span`可以显示多个。标签可以嵌套。标签大多数都是`<>` 和 `</>`两两成对出现，少数标签可以自己闭合 `</>`。

```css
/* 成对出现 */
<div>1111</div>
<span>2222</span>
/* 自己闭合 */
<img src="图像URL" />
```

简单示例：

```html
<html>

<head>
  <title>页面标题</title>
</head>

<body>
  <div>1111</div>
  <span>2222</span>
  <span>3333</span>
  <span>4444</span>
  <div>
    <span>11</span>
    <span>22</span>
  </div>
  <div>
    <span>33</span>
    <span>44</span>
  </div>
</body>

</html>
```

效果：

![Untitled](%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3%20c3e8fcef87a4454eaa236e5c95f9e960/Untitled%205.png)

标签也可以有**属性** 

```html
图像标签 img 的属性 src 中填写图像的url，可以是本地图片也可以是网络链接
<img src="图像URL" />
如果填本地路径，则：
./ 表示当前文件所在的当前目录
../ 表示上一级目录
<img src="./baidu.jpg" /> baidu.jpg 与本文件处于同一个文件夹
<img src="../baidu.jpg" /> baidu.jpg 位于本文件夹的外部
<img src="../../baidu.jpg" /> baidu.jpg 位于本文件夹的上两级目录
<img src="./imgs/baidu.jpg" /> baidu.jpg 位于本文件夹中的 imgs 文件夹中

网络图片
<img src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/7c946930-bcf2-11ea-b997-9918a5dda011.png" width="160">
```

### CSS

**概念**：CSS(Cascading Style Sheets) ，通常称为CSS样式表或层叠样式表（级联样式表）

**作用**：

- 主要用于**设置** HTML页面中的文本内容（字体、大小、对齐方式等）、图片的外形（宽高、边框样式、边距等）以及**版面的布局和外观显示样式。**
- CSS以HTML为基础，提供了丰富的功能，如字体、颜色、背景的控制及整体排版等，而且还可以针对不同的浏览器设置不同的样式。

**书写位置**：

CSS可以写在标签里，作为标签的 style **属性**

```html
<div style="color: red; font-size: 12px;">文字内容</div>
```

也可以写在`html`的头部的`style`标签中

```html
<head>
  <title>页面标题</title>
  <style>
    .red {
      color: red;
    }
		
    div {
      font-size: 18px;
      font-weight: 700;
    }
  </style>
</head>

注释：这里的div表示选择当前页面中所有的 div 标签，赋予 color、font-size属性
见下述“常用CSS选择器”
.red 表示选择所有调用 red **类**的元素，赋予这些属性，调用该类时，需要在标签中写上 class="red"
```

**常用CSS选择器**

| 选择器       | 作用                          | 缺点                     | 使用情况   | 用法                 |
| ------------ | ----------------------------- | ------------------------ | ---------- | -------------------- |
| 标签选择器   | 可以选出所有相同的标签，比如p | 不能差异化选择           | 较多       | p { color：red;}     |
| 类选择器     | 可以选出1个或者多个标签       | 可以根据需求选择         | 非常多     | .nav { color: red; } |
| id选择器     | 一次只能选择器1个标签         | 只能使用一次             | 不推荐使用 | #nav {color: red;}   |
| 通配符选择器 | 选择所有的标签                | 选择的太多，有部分不需要 | 不推荐使用 | * {color: red;}      |

举例：

```html
<html>

<head>
  <title>页面标题</title>
  <style>
    .red {
      color: red;
    }
		/* 浏览器默认字体大小为16px */
    .big-font {
      font-size: 18px;
      font-weight: 700;
    }
  </style>
</head>

<body>
  <div class="big-font">1111</div>
  <span>2222</span>
  <span>3333</span>
  <span>4444</span>
  <div class="red">
    <span>11</span>
    <span>22</span>
  </div>
  <div class="red big-font">
		<!-- 子标签会自动继承父标签的样式 -->
    <span>33</span>
    <span>44</span>
  </div>
</body>

</html>
```

![Untitled](%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3%20c3e8fcef87a4454eaa236e5c95f9e960/Untitled%206.png)

**CSS 复合选择器**

```css
/* 后代选择器：选择该元素的所有后代 */
父级 子级 {属性:属性值;属性:属性值;}
.class h3 {color:red;font-size:16px;}
/* 子代选择器：只选择该元素的第一级后代 */
父级 > 子级 {属性:属性值;属性:属性值;}
.class>h3 {color:red;font-size:14px;}
/* 交集选择器 */
两个选择器之间不能有空格
h3.class {color:red;font-size:14px;}
/* 并集选择器:如果某些选择器定义的相同样式，就可以利用并集选择器，可以让代码更简洁。*/
比如  .one, p , #test {color: #F00;}  
表示   .one 和 p  和 #test 这三个选择器都会执行颜色为红色。 
通常用于集体声明。
```

**常用CSS属性**：

```css
/* 字体属性（类名仅作示意） */
.font {
  color: #f6f6f6; /* 字体颜色 */
  font-size: 16px; /* 字体大小 */
  font-weight: 700; /* 加粗 */
}
/* 外边距 */
.margin {
  margin: 10px 10px 10px 10px; /* 四个数值依次表示上、右、下、左外边距 */
  margin-top: 10px; /* 上边距 */
  margin-right: 10px;
  margin-bottom: 10px;
  margin-left: 10px;
}
/* 内边距 */
.padding {
  padding: 10px 10px 10px 10px; /* 四个数值依次表示上、右、下、左内边距 */
  padding-top: 10px;
}
/* 边框 */
.border {
	border: 1px solid red; /* 边框综合设置 粗细 样式 颜色 */
	border-ridus: 5px; /* 边框圆角半径 */
}
/* flex 布局 */
.flex {
  display: flex; /* 启用 flex 布局，[参考链接](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html) */
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
/* position 属性 及 CSS定位方法 */
/* 参考链接：[https://www.w3school.com.cn/css/css_positioning.asp](https://www.w3school.com.cn/css/css_positioning.asp) */

```

flex 布局参考链接[点击此处](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

CSS定位方法参考链接[点击此处](https://www.w3school.com.cn/css/css_positioning.asp)

**CSS 优先级问题：**

定义CSS样式时，经常出现两个或更多规则应用在同一元素上，此时，

- 选择器相同，则执行层叠性（代码中位于后边的属性覆盖前边的属性）
- 选择器不同，就会出现优先级的问题，仅显示权重高的属性。

**CSS权重计算公式**：

| 标签选择器             | 计算权重公式 |
| ---------------------- | ------------ |
| 继承或者 *             | 0,0,0,0      |
| 每个元素（标签选择器） | 0,0,0,1      |
| 每个类，伪类           | 0,0,1,0      |
| 每个ID                 | 0,1,0,0      |
| 每个行内样式 style=""  | 1,0,0,0      |
| 每个!important  重要的 | ∞ 无穷大     |

值从左到右，左面的最大，一级大于一级，权重可叠加，数位之间没有进制，级别之间不可超越。

举例：

```html
<html>

<head>
  <title>页面标题</title>
  <style>
    .red {
      color: red;
    }

    /* 后代选择器 */
    div .grey {
      color: #666666;
    }

    .pink {
      color: pink;
    }

    .big-font {
      font-size: 18px;
      font-weight: 700 !important; /* !important 这样写 */
    }
  </style>
</head>

<body>
  <div class="big-font">1111</div>
  <span>2222</span>
  <span>3333</span>
  <span>4444</span>
  <div class="red">
		<!--11： .red 自动继承，但 .grey 权重更大。（因为继承的权重是0） -->
    <span class="grey">11</span>
		<!--22： .red 自动继承，没有其它属性来层叠 -->
    <span>22</span>
  </div>
  <div class="red">
		<!--33： div .grey 权重 0,0,1,1 -->
		<!--33： .red 权重 0,0,1,0 小于 div .grey ，所以会显示灰色-->
    <span class="grey red big-font">33</span>
    <span>44</span>
  </div>
</body>

</html>
```

![Untitled](%E5%BC%80%E5%8F%91%E6%96%87%E6%A1%A3%20c3e8fcef87a4454eaa236e5c95f9e960/Untitled%207.png)

### JS

项目在浏览器中运行时，按下`F12`键打开控制台

一个比较全面的中文教程，[点击这里](https://zh.javascript.info/)，主要了解“JavaScript 基础知识”、“Object（对象）：基础知识”、“数据类型”、“错误处理”、“Promise，async/await”这几章即可，快速过一遍，然后能看懂项目中`script` 标签中的代码即可。注意：单看教程对程序的提升不是很快，所以快速过一遍教程即可，在真实项目中去看代码，遇到不懂的回到教程中来看，这样是最快速的。

项目中大量用到的 `try...catch` 和 `async await` 分别属于 `“错误处理”`、`“Promise，async/await”`这两章的内容。

## Vue框架

使用 `html` + `css` + `js` 写的网页无需像python等编程语言那样，需要编译之后才能运行，而是直接用浏览器打开就能显示页面，这一点和其它编程语言不同。

然而，使用 `html` + `css` + `js` 一般只适合写小型的、静态的网页，遇到数据量大或数据频繁变动的项目时，需要通过`js`来频繁操作`DOM`结构来改变显示内容，对开发和运维都是巨大的考验，因此，出现了一些前端框架，让前端写得更优雅、简洁、易于维护。前端三大开源框架：`vue`、`react`、`angular` 。其中，`vue`框架是国人写的。

Vue的官网如下，本项目使用的是2.x版本：

[Vue.js](https://cn.vuejs.org/)

官网中的教程大部分是在`html`页面引入`vue`进行使用，但是以**单文件组件**的方式使用`vue`更常用，此时我们写的文件不再是`html`文件，而是扩展名为`.vue`的文件，页面结构也有所不同。而且写完的代码需要经过编译转化为`html`文件才能被浏览器读取。

使用`vue`框架需要有一定的`html`和`javascript`基础，一般看完前边的教程和参考资料就足够了。以**单文件组件**的方式使用 `vue` 的教程参考链接：[点击这里](https://uniapp.dcloud.io/vue-basics?id=%e4%bb%8b%e7%bb%8d)，这也是`uni-app`官网的`vue`教程。

## element-ui 组件

`element-ui`是一套基于`vue`框架的组件库，非常适用于`pc`端，尤其是管理系统。官网如下：

[Element - The world's most popular Vue UI framework](https://element.eleme.cn/#/zh-CN/component/installation)

学完 `vue` 之后，就可以从`element-ui` 中挑选合适的组件进行使用，只需阅读各组件对应的文档即可。

## UniCloud

本项目使用 `uniCloud` 作为后端，原因是只需要 `js` 语言即可编写后端。而 `js` 语言一般在学习前端时已经学过，这样就降低了前端人员学习后端的成本。

uniCloud官网如下：

[uni-app官网](https://uniapp.dcloud.io/uniCloud/README)

官网给出了详细的文档和视频教程，我们只需学习首页的[视频教程](https://uniapp.dcloud.io/uniCloud/README?id=%e7%9c%8b%e8%a7%86%e9%a2%91%ef%bc%8c%e5%8f%aa%e9%9c%8025%e5%88%86%e9%92%9f%ef%bc%8c%e5%bf%ab%e9%80%9f%e5%85%a5%e9%97%a8unicloud)，文档的`“基本概念”`部分和`“云数据库”`部分里的`“前端操作数据库的 API 和 JQL 语法”`即可。