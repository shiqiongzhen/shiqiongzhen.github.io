> 为什么需要 React-router，为了满足更多的单页面路由场景，如嵌套路由，动态路由(/:id)

> Router 和 Route 的关系

- Router: 完整的路由解决方案

  - 定义：React Router 保持 UI 与 URL 同步。它拥有简单的 API 与强大的功能例如代码缓冲加载、动态路由匹配、以及建立正确的位置过渡处理。
  - 配置方式：JSX & 对象
  - 分类: Router 包括 HashRouter、BrowserRouter、createMemoryHistory，它主要定义了 Router 的模式

- Route: 路由 

    Switch/Route 一般和 Link

- 应用：React Router 知道如何为我们搭建嵌套的 UI，因此我们不用手动找出需要渲染哪些 <Child> 组件。

```
// JSX 配置方式
  <Router>
    <Route path="/" component={App}>
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox} />
    </Route>
  </Router>
```

> react-router-dom 和 react-router 包有什么区别

```
import { HashRouter, BrowserRouter, Route, Link, Switch } from 'react-router-dom';
import { Router, Route, Link } from 'react-router'
```

> react-router 基于 window.history 做了什么？

... 

> 参考文献

1. [https://react-guide.github.io/react-router-cn/docs/Introduction.html](https://react-guide.github.io/react-router-cn/docs/Introduction.html)

