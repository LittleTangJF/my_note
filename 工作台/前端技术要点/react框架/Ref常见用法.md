## forwardRef

### 语法
>React.forwardRef(render(props, ref))

使用场景

1. 转发ref到组件内部的DOM节点上
2. 在高阶组件中转发ref

```jsx
// Foo.jsx
import React from 'react'; 
const Foo = React.forwardRef((props, myRef) => { 
  return ( <div> <p>....一些其他节点</p> 
   <input type="text" defaultValue='ref 成功转发到 Foo 组件内部的 input节点上' ref={myRef}/> 
   <p>....一些其他节点</p>
   <p>....一些其他节点</p> 
  </div> ); }); 
export default Foo;
```

### 注意

在高阶组件中，ref会挂载在外层的组件上，而不是在传入的包裹的组件，不会跟着 props 一起透传下去

所以解决如下
```jsx
// 最终形态
import React from 'react';

export default function logProps(WrappedComponent) {
  
  class LogProps extends React.Component {
    // 2
    constructor(props) {
      super(props);
      this.state = {
        message: '这是LogProps'
      }
    }
    componentDidUpdate(prevProps) {
      console.log('Previous props: ', prevProps);
      console.log('Current props: ', this.props);
    }
    render() {
      // 3
      const {customRef, ...props} = this.props;
      // 3.5 return <WrappedComponent {...this.props}/>;
      return <WrappedComponent {...props} ref={customRef} />;
    }
  }
  // return LogProps; 注意：**一定要转发到自定义属性**
  return React.forwardRef((props, ref) => (
    // 1
    <LogProps {...props} customRef={ref} />
  ))
  
}
```

## 保存变量

`ref` 具有可以 _穿透闭包_ 的能力，可以用来保存非state、props的值

## 保存函数组件实例的属性

```jsx
class Model {
    constructor() {
        console.log('创建 Model');
        this.data = [];
    }
}

function Counter() {
    const [count, setCount] = useState(0);
    //const countRef = useRef(new Model()); // 触发问题，多次执行，可以借助state的特性
     const [model] = useState(() => new Model());
    const countRef = useRef(model);

    return <p onClick={() => setCount(count + 1)}>clicked {count} times</p>;
}

```