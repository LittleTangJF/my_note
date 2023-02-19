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

## 三、渐变更新

### 3.0 ## startTransition

场景：比如输入框，下面是联想展示数据，我们可以将联想的内容优先度降低，避免抢占用户操作

```jsx
// 仅仅只是将 setKeywords 用 startTransition 包裹一层，即可启用渐变更新
+        getList().then(res => startTransition(() => setKeywords(res)));
```


### 3.1 ## useDeferredValue

场景：将更新数据包裹，

`useDeferredValue` 相当于是 `startTransition(() => setState(xxx))` 的语法糖，在内部会调用一次 `setState`，但是此更新的优先级更低

### 3.2 ## useTransition

场景： 当页面相应快，loading过渡出现闪烁，可以使用它来包裹数据，等待内容加载，同时还允许将数据返回较慢的推迟随后渲染
### 概念

-   `useTransition` 允许组件再切换到下一个界面之前等待内容加载，从而避免出现不必要的加载状态
    
-   允许组件将速度较慢的数据获取更新推迟到随后渲染（低优先级更新），以便能够立即渲染更重要的更新
    
-   `useTransition` 返回包含两个元素的数组：
    
    -   `isPending: Boolean`，通知我们是否正在等待过渡效果的完成
    -   `startTransition: Function`，用它来包裹需要延迟更新的状态
