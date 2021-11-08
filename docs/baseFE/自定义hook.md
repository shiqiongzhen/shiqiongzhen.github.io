## 重用状态逻辑的三种方式：
1. render props
2. 高阶组件

优点：
不影响内层组件的状态，降低了耦合度

缺点：
- 不能访问内层组件的状态, 导致无法过滤掉不必要的更新（React 在支持 ES6 Class 之后提供了React.PureComponent来解决这个问题）
- 组件的传参可能会被高阶组件的值覆盖，它无法清晰地标识数据的来源

3. 自定义 hook（遵循 hook 原则的 JavaScript 函数）

优点
- 简洁：嵌套问题解决
- 解耦：把 UI 和状态分离
- 组合：Hooks + hooks
- 函数友好：解决了类组件的几个问题
  - this 指向易错（类组件可以通过箭头函数和绑定this解决，使得this指向类实例）
  - 分割生命周期导致代码不易维护
  - 代码复用成本高
缺点
- 破坏了PureComponent、React.memo浅比较的性能优化效果（为了取最新的props和state，每次render()都要重新创建事件处函数）
- 写法上有限制（不能出现在条件、循环中），并且写法限制增加了重构成本
- React.memo并不能完全替代shouldComponentUpdate（因为拿不到 state change，只针对 props change）

### hook 使用规则
1. 只能在函数最外层调用 Hook。不要在循环、条件判断或者子函数中调用
2. 只能在 React 的函数组件中调用 Hook。不要在其他 JavaScript 函数中调用。（还有一个地方可以调用 Hook —— 就是自定义的 Hook 中，我们稍后会学习到。）


## 常见的自定义hook
1. useMemo：可以帮我们将变量缓存起来

问题场景：有的 state 不需要设置

2. useCallback：可以缓存回调函数，它们的第二个参数和useEffect一样，是一个依赖项数组，通过配置依赖项数组来决定是否更新。

```
import { useState, useCallback } from 'react';

const useCounter = (step) => {
  const [counter, setCounter] = useState(0);
  const increment = useCallback(() => setCounter(counter + step), [counter, step]);
  const decrement = useCallback(() => setCounter(counter - step), [counter, step]);
  const reset = useCallback(() => setCounter(0), []);
  
  return {counter, increment, decrement, reset};
}

export default useCounter;
```

3. useRef ?

```
const useDidUpdate = (callback, inputs) => {
  const initial = useRef(true);

  useEffect(() => {
    if (initial.current) {
      initial.current = false;
      return;
    }
    callback?.();
  }, inputs);
};
```

问题场景：

> 参考文献

1. [https://time.geekbang.org/column/article/381423](https://time.geekbang.org/column/article/381423)
2. [Hooks API 规范](https://ahooks.js.org/zh-CN/docs/api)
3. [aHooks 自定义库](https://ahooks.js.org/zh-CN/hooks/async)