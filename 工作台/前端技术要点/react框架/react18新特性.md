## 一、自动批量更新

18以前，react提供了手动批量更新

>语法：reactDOM.unstable_batchedUpdates

18以后，使用了新的 `API`： `ReactDOM.createRoot(root).render(jsx)`实现自动批量更新

## 二、Suspense用法

早在react16时，可以用react.lazy 配合Suspense来做懒加载

```jsx
import React from "react";
import ReactDOM from "react-dom";

const User = React.lazy(() => import("./User"));

const App = () => {
    return (
        <>
            <React.Suspense fallback={<div>Loading...</div>}>
                <User id={1} />
            </React.Suspense>
        </>
    );
};

ReactDOM.createRoot(document.getElementById("root")).render(<App />);
```

但是美中不足的地方，用户看到的仅仅是组件加载完成，想要看的真实数据还没有处理完成

### 内部流程

1. Suspense让子组件在渲染前进行等待，并现实设置的fallback的内容
2. Suspense让内的组件子树，比组件树的其他部分拥有更低的优先级

### SuspenseList

```jsx
 <React.SuspenseList revealOrder="forwards" tail="collapsed">
            <React.Suspense fallback={<div>Loading...</div>}>
                <User id={1} />
            </React.Suspense>
            <React.Suspense fallback={<div>Loading...</div>}>
                <User id={3} />
            </React.Suspense>
            <React.Suspense fallback={<div>Loading...</div>}>
                <User id={5} />
            </React.Suspense>
        </React.SuspenseList>
    );
```