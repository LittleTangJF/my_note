## 关键词

Chromium、Node、二进制、Fiddle、**Electron 进程**、**分发**、渲染器进程、应用的生命周期、执行特殊操作、预加载脚本、进程间通信 (IPC) 模组、__dirname、Electron Forge、**代码签名**、autoUpdater 

- `webPreferences.preload` 传入脚本的路径，脚本附在渲染进程
- IPC：ipcMain和ipcRenderer进行进程间通信
- invoke：函数来触发该处理程序（handler）
- Forge： 打包分发

## 一、主进程 定义：

每个 Electron 应用都有一个单一的主进程，作为应用程序的入口点。 主进程在 Node.js 环境中运行，这意味着它具有 `require` 模块和使用所有 Node.js API 的能力

主进程的主要目的是使用 [`BrowserWindow`](https://www.electronjs.org/zh/docs/latest/api/browser-window) 模块创建和管理应用程序窗口


### 1.1 应用程序生命周期

[`app`](https://www.electronjs.org/zh/docs/latest/api/app) 模块来控制您应用程序的生命周期
- ready
- will-finish-launching
- window-all-closed
-  before-quit
- will-quit
- 
- 
- 

### 1.2 主进程模块

- 托盘模块 -- tray
- 菜单模块 --- 原生不好用，自定义菜单
- 异步处理模块 -- crashReporter
### 1.3原生 API

主进程也添加了自定义的 API 来与用户的作业系统进行交互。 Electron 有着多种控制原生桌面功能的模块，例如菜单、对话框以及托盘图标。

## 二、渲染器进程

每个 Electron 应用都会为每个打开的 `BrowserWindow` ( 与每个网页嵌入 ) 生成一个单独的渲染器进程。

### 2.1 渲染进程模块£

- 静态资源--- cdn资源 、 本地获取
- 数据储存  ----- Electron-store第三方库
- 打包---注意要调整请求API代码， 因为本地资源，API前缀要区分本地和应用环境


## 三、Preload 脚本

这些脚本虽运行于渲染器的环境中，却因能访问 Node.js API 而拥有了更多的权限
- 预加载脚本可以在 `BrowserWindow` 构造方法中的 `webPreferences` 选项里被附加到主进程。

	上下文隔离是什么？
	确保您的 `预加载`脚本 和 Electron的内部逻辑 运行在所加载的 [`webcontent`](https://www.electronjs.org/zh/docs/latest/api/web-contents)网页 之外的另一个独立的上下文环境里。

## 四、IPC

- [`ipcMain`](https://www.electronjs.org/zh/docs/latest/api/ipc-main)
- [`ipcRenderer`](https://www.electronjs.org/zh/docs/latest/api/ipc-renderer)
这些通道是 **任意** （您可以随意命名它们）和 **双向** （您可以在两个模块中使用相同的通道名称）的。
![[Pasted image 20230318174804.png]]
### 4.1 同步和异步

- 【异步】渲染进程->发送->主进程 --> send
- 【同步】渲染进程->发送->主进程---> sendSync


## 五、技术挑战™

### 5.1 安全性问题

- xss攻击、---electron主进程的nodeIntegration属性以及DOM Based-XSS和RCE攻击
- 用户信息泄露、
- 本地缓存明文读取问题

### 5.2 发布构建流程

### 5.3 应用更新问题

- 全量更新
- 增量更新

#### 5.3.1 全量更新

1. 打开app，请求json文件
2. 本地和远程版本比较
3. 不一致询问用户下载，是的话下载到指定文件夹，双击安装

缺陷：只适用于更新频率慢的场景


#### 5.3.2 增量更新

electron-updater：**依赖新旧版本blockmap文件的对比来实现增量更新**，下载blockmap和本地作对比

- 强更新--强制--不更新退出应用--下载完成才能关闭窗口
- 弱更新--用户自主选择 --- 若更新可以最小化窗口

##### 5.3.2.1 文件替换（热更新）

- 版本号下载到本地，判断远程和本地版本号
- 有更新，下载解压资源
- http.get()获取js资源--有错误就出错回调
- 以二进制形式在成功回调中返回
- 写入压缩文件--失败（权限、资源占用）就更新失败提醒
- 解压资源到指定目录，更新完成

## 六、遇到问题
- 硬件加速功能---判断是不是win7---app.disableHardwareAcceleration ()
- 降低内存--disable-http-cache、reloadIgnoreCache、clearCodeCaches、资源禁止缓存
