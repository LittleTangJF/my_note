## 一、通信

### 通信方式1： port.postMesssage 

Node.js 的 `worker_threads` 模块中进行线程间通信的示例。`worker_threads` 允许你在 Node.js 中创建多线程，从而在不阻塞主线程的情况下执行一些耗时的任务。

```js
import { parentPort } from 'worker_threads'
parentPort.postMessage({
    method: type,
    arg: {
      snParams,
      SN: sn,
      totalCount: getTotalCount(project?.inferType, snParams || []),
      project,
      inferType: project?.inferType || 'dianyuan-bofenghan', // 默认走模板推理流程
    }
  })
```

在接收处监听

```js
import createInferWorker from '../../workers/watch/index?nodeWorker';
const watchWorker = createInferWorker({ workerData: { isPackaged: app.isPackaged } });
watchWorker.on('message', (msg) => {
  const { method, arg } = msg;
  const _method = WORKER_FN_MAP.get(method);
  _method && _method(arg);
})
```

### 通信方式2：主-渲染线程通信

1. 渲染进程---> 主进程

```ts
// 渲染页面
ipcRenderer.sendMessage('createInferWindow', [projects]);
// 主进程
ipcMain.on('createInferWindow', async (_event: any, arg: any) => {})
```

2. 主进程---> 渲染进程

```ts
// 渲染进程通过 ipcRenderer.on 封装了hooks useRefIpcRender

useRefIpcRender({
    eventName: 'service-stopped',
    deps: [],
    callback: (curProject) => {
      if (curProject) {
        message.error({
          content: (
            <>
              <span style={{ marginRight: 24 }}>
                AI检测功能已停止，复判台无法接收到新的AI检测图片
              </span>
            </>
          ),
          key: 'service-msg',
          duration: 0,
        });
      }
    },
  });
// 主线程发送信息 // 创建mainWindow
global.mainWindow.webContents.send('download-template', [templateName, project]);

```