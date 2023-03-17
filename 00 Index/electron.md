## 关键词

Chromium、Node、二进制、Fiddle、**Electron 进程**、**分发**、渲染器进程、应用的生命周期、执行特殊操作、预加载脚本、进程间通信 (IPC) 模组、__dirname、Electron Forge、**代码签名**、autoUpdater 

- `webPreferences.preload` 传入脚本的路径，脚本附在渲染进程
- IPC：ipcMain和ipcRenderer进行进程间通信
- invoke：函数来触发该处理程序（handler）
- Forge： 打包分发

## 主进程 定义：

每个 Electron 应用都有一个单一的主进程，作为应用程序的入口点。 主进程在 Node.js 环境中运行，这意味着它具有 `require` 模块和使用所有 Node.js API 的能力

主进程的主要目的是使用 [`BrowserWindow`](https://www.electronjs.org/zh/docs/latest/api/browser-window) 模块创建和管理应用程序窗口


### 应用程序生命周期

[`app`](https://www.electronjs.org/zh/docs/latest/api/app) 模块来控制您应用程序的生命周期
- ready
- will-finish-launching
- window-all-closed
-  before-quit
- will-quit
- 
- 
- 
- 
### 原生 API

主进程也添加了自定义的 API 来与用户的作业系统进行交互。 Electron 有着多种控制原生桌面功能的模块，例如菜单、对话框以及托盘图标。

## 渲染器进程

每个 Electron 应用都会为每个打开的 `BrowserWindow` ( 与每个网页嵌入 ) 生成一个单独的渲染器进程。


## Preload 脚本

这些脚本虽运行于渲染器的环境中，却因能访问 Node.js API 而拥有了更多的权限
- 预加载脚本可以在 `BrowserWindow` 构造方法中的 `webPreferences` 选项里被附加到主进程。

## 上下文隔离是什么？

确保您的 `预加载`脚本 和 Electron的内部逻辑 运行在所加载的 [`webcontent`](https://www.electronjs.org/zh/docs/latest/api/web-contents)网页 之外的另一个独立的上下文环境里。

## IPC

- [`ipcMain`](https://www.electronjs.org/zh/docs/latest/api/ipc-main)
- [`ipcRenderer`](https://www.electronjs.org/zh/docs/latest/api/ipc-renderer)
这些通道是 **任意** （您可以随意命名它们）和 **双向** （您可以在两个模块中使用相同的通道名称）的。

