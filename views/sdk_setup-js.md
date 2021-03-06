{% import "views/_helper.njk" as docs %}
{% import "views/_parts.html" as include %}

# JavaScript SDK 安装指南

本指南按照应用的适用平台来介绍各自的安装与集成方式。

|[<img src="images/platforms/html5.svg" width="120"/>](#Web)|[<img src="images/platforms/node-js.svg"  width="120"/>](#Node.js)|[<img src="images/platforms/weapp.svg"  width="120"/>](#微信小程序)|[<img src="images/platforms/weapp-game.svg"  width="120"/>](#微信小游戏)|[<img src="images/platforms/cocos.png"  width="120"/>](#CocosCreator)|[<img src="images/platforms/laya.png"  width="120"/>](#LayaAir)|[<img src="images/platforms/egret.png"  width="120"/>](#Egret（白鹭引擎）)|[<img src="images/platforms/react-native.svg"  width="120"/>](#React-Native)|[<img src="images/platforms/electron.svg"  width="120"/>](#Electron)|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|Web|Node.js|微信小程序|微信小游戏|CocosCreator|LayaAir|Egret|React Native|Electron|



## Web

<a id="web" name="web"></a>适用于运行在浏览器、WebView 或其他应用内 HTML 平台上的应用。

### 安装与引用 SDK

#### npm
如果你的 Web 应用使用了 webpack 等前端打包工具，我们推荐使用包管理工具 npm 安装 SDK：

```bash
# 存储服务（包括推送）
$ npm install leancloud-storage --save
# 实时消息服务
$ npm install leancloud-realtime --save
```

如果因为网络原因无法通过官方的 npm 站点下载，推荐通过 taobao 镜像来下载，操作步骤如下：

```bash
# 存储服务（包括推送）
$ npm install leancloud-storage --save --registry=https://registry.npm.taobao.org
# 实时消息服务
$ npm install leancloud-realtime --save --registry=https://registry.npm.taobao.org
```

然后在代码中通过 require 获得 SDK 的引用：

```js
// 存储服务
var AV = require('leancloud-storage');
var { Query, User } = AV;
// 实时消息服务
var { Realtime, TextMessage } = require('leancloud-realtime');
```

如果需要使用存储服务的 [LiveQuery][livequery] 功能，需要按如下做法引入存储 SDK：

```js
var AV = require('leancloud-storage/live-query');
```

#### CDN

你也可以直接在页面中通过 script 标签引入我们的 SDK：

```html
<!-- 存储服务 -->
<script src="//cdn.jsdelivr.net/npm/leancloud-storage@{{jssdkversion}}/dist/av-min.js"></script>
<!-- 实时消息服务 -->
<script src="//cdn.jsdelivr.net/npm/leancloud-realtime@{{jsimsdkversion}}/dist/realtime.browser.min.js"></script>
```

如果需要使用存储服务的 [LiveQuery][livequery] 功能，需要按如下做法引入存储 SDK：

```html
<script src="//cdn.jsdelivr.net/npm/leancloud-storage@{{jssdkversion}}/dist/av-live-query-min.js"></script>
```

通过这种方式引入的 SDK 可以通过全局变量 `AV` 获得引用：

```js
// 存储服务
var { Query, User } = AV;
AV.init('appId', 'appKey');
// 实时消息服务
var { Realtime, TextMessage } = AV;
```

### 打开调试日志

在应用开发阶段，你可以选择开启 SDK 的调试日志（debug log）来方便追踪问题。调试日志开启后，SDK 会把网络请求、错误消息等信息输出到浏览器的 console 中。

要在 Web 平台中打开调试日志，请打开浏览器的控制台（console），运行以下命令：

```js
localStorage.setItem('debug', 'leancloud*,LC*');
```


## Node.js

<a id="node" name="node"></a>JavaScript SDK 也可以运行在 Node.js 运行环境中。如果希望在云引擎中访问我们的存储服务，请参照 [云引擎快速入门](leanengine_quickstart.html)，使用模板项目中提供的 `leanengine` 包接入存储服务。

### 安装与引用 SDK

Node.js 中 SDK 的安装与引用也是通过包管理工具 npm，请参考 [npm](#npm)。

### 打开调试日志

在 Node.js 平台中打开调试日志，需要设置环境变量 `DEBUG` 为 `leancloud*,LC*`。

你可以在启动某个命令之前设置环境变量。下面以本地启动云引擎调试的命令（`lean up`）为例：

```bash
# Unix
DEBUG=leancloud*,LC* lean up
# Windows cmd
set DEBUG=leancloud*,LC* lean up
```



## 微信小程序

### 手动导入文件

#### 存储服务

<a id="weapp" name="weapp"></a>前往 [存储 SDK 下载页](https://releases.leanapp.cn/#/leancloud/javascript-sdk/releases)，下载最新版本的 `av-weapp-min.js`，移动到 `libs` 目录。如果需要使用 [LiveQuery][livequery] 功能，需要下载 `av-weapp-live-query-min.js`。

在 `app.js` 中使用 `const AV = require('./libs/av-weapp-min.js');` 获得 `AV` 的引用。在其他文件中使用时请将路径替换成对应的相对路径。 

#### 实时消息服务

前往 [实时消息 SDK 下载页](https://releases.leanapp.cn/#/leancloud/js-realtime-sdk/releases)，下载最新版本的 `realtime.weapp.min.js`，移动到 `libs` 目录。

在 `app.js` 中使用 `const { Realtime, TextMessage } = require('./libs/realtime.weapp.min.js');` 获得 `Realtime` 等 SDK 暴露成员的引用。在其他文件中使用时请将路径替换成对应的相对路径。

### WePY

如果使用 [WePY](https://tencent.github.io/wepy/) 来开发小程序，可以直接通过 npm 安装和引用 SDK，具体操作步骤请参考 [npm](#npm)。

### mpvue

如果使用 [mpvue](http://mpvue.com/) 来开发小程序，可以直接通过 npm 安装和引用 SDK，具体操作步骤请参考 [npm](#npm)。

## 微信小游戏

<a id="weapp-game" name="weapp-game"></a>微信小游戏手动导入 SDK 的步骤与微信小程序一致，请参考 [微信小程序 · 手动导入文件](#手动导入文件)。

如果使用游戏引擎提供的开发工具开发微信小游戏，请参照对应的游戏引擎章节。


## CocosCreator

<a id="cocoscreator" name="cocoscreator"></a>CocosCreator 支持直接通过 npm 安装与引用 SDK，具体操作步骤请参考 [npm](#npm)。

{{ docs.note("CocosCreator 项目默认没有 `package.json` 文件，可以在安装 SDK 前通过 `npm init -y` 命令创建。") }}

如果你的 CocosCreator 项目需要发布为微信小程序，需要在构建发布到小程序之前修改 SDK 的引用路径：

```diff
  // 存储服务 SDK  路径变更为
- var AV = require('leancloud-storage');
+ var AV = require('leancloud-storage/dist/av-weapp-min.js');
  
  // 带 LiveQuery 功能的存储 SDK 路径变更为
- var AV = require('leancloud-storage/live-query');
+ var AV = require('leancloud-storage/dist/av-live-query-weapp-min.js');

  // 实时消息服务 SDK 路径变更为
- var { Realtime } = require('leancloud-realtime');
+ var { Realtime } = require('leancloud-realtime/dist/realtime.weapp.js');
```

请注意，此改动会导致其他平台的产出（包括浏览器与模拟器的预览功能）不能正常工作，因此应该只在构建发布到小程序之前临时修改，并在发布之后修改回来。

在改动之后，CocosCreator 的控制台可能会出现 load script error，但不影响构建发布小程序，并且构建产出在小程序开发工具中运行也不会有异常。

## LayaAir

<a id="layaair" name="layaair"></a>根据你创建的项目类型与需要使用的服务，下载对应的 SDK 文件，移动到 `bin/libs/` 目录：

||小程序项目|普通项目|
|--|:--:|:--:|
|存储服务|[leancloud-storage-weapp.min.js][]|[leancloud-storage.min.js][]|
|存储服务（LiveQuery）|[leancloud-storage-live-query-weapp.min.js][]|[leancloud-storage-live-query.min.js][]|
|实时消息服务|[leancloud-realtime-weapp.min.js][]|[leancloud-realtime.min.js][]|

[leancloud-storage-weapp.min.js]: https://cdn.jsdelivr.net/combine/gh/leancloud/laya-weapp-module-wrapper@0.1.1/start.js,npm/leancloud-storage@{{jssdkversion}}/dist/av-weapp-min.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/end.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/_/leancloud-storage-weapp.min.js
[leancloud-storage.min.js]: https://cdn.jsdelivr.net/combine/gh/leancloud/laya-weapp-module-wrapper@0.1.1/start.js,npm/leancloud-storage@{{jssdkversion}}/dist/av-min.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/end.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/_/leancloud-storage.min.js
[leancloud-storage-live-query-weapp.min.js]: https://cdn.jsdelivr.net/combine/gh/leancloud/laya-weapp-module-wrapper@0.1.1/start.js,npm/leancloud-storage@{{jssdkversion}}/dist/av-live-query-weapp-min.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/end.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/_/leancloud-storage-live-query-weapp.min.js
[leancloud-storage-live-query.min.js]: https://cdn.jsdelivr.net/combine/gh/leancloud/laya-weapp-module-wrapper@0.1.1/start.js,npm/leancloud-storage@{{jssdkversion}}/dist/av-live-query-min.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/end.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/_/leancloud-storage-live-query.min.js
[leancloud-realtime-weapp.min.js]: https://cdn.jsdelivr.net/combine/gh/leancloud/laya-weapp-module-wrapper@0.1.1/start.js,npm/leancloud-realtime@{{jsimsdkversion}}/dist/realtime.weapp.min.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/end.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/_/leancloud-realtime-weapp.min.js
[leancloud-realtime.min.js]: https://cdn.jsdelivr.net/combine/gh/leancloud/laya-weapp-module-wrapper@0.1.1/start.js,npm/leancloud-realtime@{{jsimsdkversion}}/dist/realtime.browser.min.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/end.js,gh/leancloud/laya-weapp-module-wrapper@0.1.1/_/leancloud-realtime.min.js

在 `bin/index.html` 中项目「IDE 生成的 UI 文件」之前引入刚下载的 SDK 文件：

```diff
	<!--提供了制作 UI 的各种组件实现-->
    <script type="text/javascript" src="libs/laya.ui.js"></script>
	<!--用户自定义顺序文件添加到这里-->
	<!--jsfile--Custom-->
+  	<!--LeanCloud 存储 SDK-->
+  	<script src="libs/leancloud-storage-live-query-weapp.min.js"></script>
+  	<!--LeanCloud 即时通讯 SDK-->
+  	<script src="libs/leancloud-realtime-weapp.min.js"></script>
	<!--jsfile--Custom-->
	<!--IDE 生成的 UI 文件-->
	<script src="../src/ui/layaUI.max.all.js"></script>
```

{{ docs.note("小程序项目与普通项目使用的 SDK 是不一样的，建议小程序项目在使用浏览器进行调试时切换到普通项目 SDK。") }}

此时在 `src` 目录下的代码中即可通过全局变量 `AV` 获得 SDK 的引用：

```js
// 存储服务
var { Query, User } = AV;
AV.init('appId', 'appKey');
// 实时消息服务
var { Realtime, TextMessage } = AV;
```

如果你创建的是 TypeScript 项目，或者希望得到 IDE 的自动提示能力，还需要下载 TypeScript 定义文件移动至 `libs` 目录。

- 存储服务：[storage.d.ts](https://cdn.jsdelivr.net/npm/leancloud-storage@3.7.2/storage.d.ts)
- 即时通讯服务：[realtime.d.ts](https://cdn.jsdelivr.net/gh/leancloud/js-realtime-sdk@ea3b7087809a9d76c237f9cf4548e06a94e2c33d/realtime.d.ts)

{{ docs.note("如果同时使用两个 SDK，因为 namespace 冲突的问题，需要下载 [leancloud-all.d.ts](https://cdn.jsdelivr.net/combine/npm/leancloud-storage@3.7.2/storage.d.ts,gh/leancloud/js-realtime-sdk@ea3b7087809a9d76c237f9cf4548e06a94e2c33d/realtime.d.ts)，然后手动删除最后一行 `export as namespace AV;`。") }}

你可以在 [这个示例项目](https://github.com/leancloud/laya-sdk-setup-sample/commit/533194407f127d412d4fa7e6c049ebe55bac4cbc) 中看到完整的改动。


## Egret（白鹭引擎）

<a id="egret" name="egret"></a>首先前往 <https://github.com/leancloud/egret-sdk>，下载对应的 SDK 目录（leancloud-storage），将其放置于你的 Egret 游戏项目同级目录下：

```
├── egret-game-project
│   ├── （其他目录与文件）
│   └── egretProperties.json
└── leancloud-storage
    ├── leancloud-storage.d.ts
    ├── leancloud-storage.js
    └── leancloud-storage.min.js
```

然后，编辑 `egret-game-project/egretProperties.json` 文件，在 `modules` 数组的最后添加 SDK：

```diff
{
  "engineVersion": "5.1.8",
  "compilerVersion": "5.1.8",
  "template": {},
  "target": {"current": "web"},
  "eui": {"exmlRoot": ["resource/eui_skins"],"themes": ["resource/default.thm.json"],"exmlPublishPolicy": "commonjs"},
  "modules": [
    {
      "name": "egret"
    },
    {
      "name": "eui"
    },
    {
      "name": "assetsmanager"
    },
    {
      "name": "tween"
    },
    {
      "name": "promise"
+   },
+   {
+     "name": "leancloud-storage",
+     "path": "../leancloud-storage"
    }
  ]
}
```

最后，在 `egret-game-project` 目录下运行 `egret build`，如果在 `egret-game-project/manifest.json` 中的 `initials` 数组中出现了 `"libs/modules/leancloud-storage/leancloud-storage.js"` 则意味着 SDK 安装成功了。

安装成功后，你可以在业务代码中通过全局变量 `AV` 获得 SDK 的引用：

```js
var { Query, User } = AV;
AV.init('appId', 'appKey');
```

{{ docs.note("目前在 Egret 平台上，我们只提供存储服务的 SDK（不含 LiveQuery 功能）。") }} 

## React Native

<a id="react-native" name="react-native"></a>React Native 直接通过 npm 安装与引用 SDK，具体操作步骤请参考 [#npm](#npm)。

[livequery]: livequery-guide.html

## Electron

<a id="electron" name="electron"></a>Electron 使用包管理工具 npm 管理依赖，你可以通过以下命令安装 SDK：

```bash
# 存储服务（包括推送）
$ npm install leancloud-storage --save
# 实时消息服务
$ npm install leancloud-realtime --save
```

### 作为浏览器脚本引入

在 index.html 中可以通过 script 标签引入 SDK：

```html
<!-- 存储服务 -->
<script src="./node_modules/leancloud-storage/dist/av-min.js"></script>
<!-- 实时消息服务 -->
<script src="./node_modules/leancloud-realtime/dist/realtime.browser.min.js"></script>
```

如果需要使用存储服务的 [LiveQuery][livequery] 功能，需要按如下路径引入存储 SDK：

```html
<script src="./node_modules/leancloud-storage/dist/av-live-query-min.js"></script>
```

### 作为 Node.js 模块引入

我们推荐使用 `script` 标签引入 SDK，该方式能满足绝大部分的需求。但是如果有以下的需求，SDK 也支持通过 `require('leancloud-storage')` 方法作为 Node.js 模块引入。

- 需要在 main process 中使用 SDK
- 需要使用 Node.js 的 `Buffer` 或 `Stream` 构造 `AV.File`

{{ docs.note("通过 Node.js `require` 方法引入的 SDK 与通过浏览器 `script` 标签引入的 SDK 是两个不同的 SDK，需要各自分别初始化，并且不能混用。") }}

## 初始化

首先进入 [控制台 > 设置 > 应用 Key](/app.html?appid={{appid}}#/key) 来获取 App ID 以及 App Key。

如果是在前端项目里面使用 LeanCloud JavaScript SDK，那么可以在页面加载的时候调用一下初始化的函数：

```javascript
var APP_ID = '{{appid}}';
var APP_KEY = '{{appkey}}';

AV.init({
  appId: APP_ID,
  appKey: APP_KEY
});
```
```nodejs
var APP_ID = '{{appid}}';
var APP_KEY = '{{appkey}}';
var AV = require('leancloud-storage');

AV.init({
  appId: APP_ID,
  appKey: APP_KEY
});
```

### 启用指定节点

SDK 的初始化方法默认使用**中国大陆节点**，如需切换到 [其他可用节点](#全球节点)，请参考如下用法：

```javascript
var APP_ID = '{{appid}}';
var APP_KEY = '{{appkey}}';
AV.init({
  appId: APP_ID,
  appKey: APP_KEY,
  {% if node != 'qcloud' -%}
  // 启用美国节点
  region: 'us'
  {% else -%}
  // 目前仅支持中国节点
  region: 'cn'
  {% endif %}
  
});
```

### 全球节点

- 中国大陆节点 **leancloud.cn**（SDK 初始化方法**默认**使用该节点）
- 北美节点 **us.leancloud.cn**（服务北美市场）

{{ docs.alert("各个节点彼此独立，开发者账号无法跨节点来创建应用或调用 API。") }}

## 验证

首先，确认本地网络环境是可以访问 LeanCloud 服务器的，可以执行以下命令行：

```shell
ping "{{host}}"
```
如果当前网路正常将会得到如下响应：

```shell
PING api-ucloud.leancloud.cn (123.59.41.31): 56 data bytes
64 bytes from 123.59.41.31: icmp_seq=0 ttl=51 time=9.032 ms
64 bytes from 123.59.41.31: icmp_seq=1 ttl=51 time=7.290 ms
64 bytes from 123.59.41.31: icmp_seq=2 ttl=51 time=8.131 ms
64 bytes from 123.59.41.31: icmp_seq=3 ttl=51 time=9.689 ms
64 bytes from 123.59.41.31: icmp_seq=4 ttl=51 time=6.559 ms
64 bytes from 123.59.41.31: icmp_seq=5 ttl=51 time=8.665 ms
64 bytes from 123.59.41.31: icmp_seq=6 ttl=51 time=8.041 ms
64 bytes from 123.59.41.31: icmp_seq=7 ttl=51 time=8.203 ms
64 bytes from 123.59.41.31: icmp_seq=8 ttl=51 time=6.288 ms
64 bytes from 123.59.41.31: icmp_seq=9 ttl=51 time=7.938 ms

--- api-ucloud.leancloud.cn ping statistics ---
10 packets transmitted, 10 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 6.288/7.984/9.689/0.997 ms
```

然后在项目中编写如下测试代码：

```javascript
var TestObject = AV.Object.extend('TestObject');
var testObject = new TestObject();
testObject.save({
  words: 'Hello World!'
}).then(function(object) {
  alert('LeanCloud Rocks!');
})
```

然后打开 [控制台 > 存储 > 数据 > TestObject](/data.html?appid={{appid}}#/TestObject)，如果看到如下内容，说明 SDK 已经正确地执行了上述代码，安装完毕。


![testobject_saved](images/testobject_saved.png)

如果控制台没有发现对应的数据，请参考 [问题排查](#问题排查)。

{{ include.sdkSetupFAQ() }}
