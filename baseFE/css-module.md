> .module.scss 和 .scss 的区别

- .module.scss

会被编译成哈希字符串，会隔离不同的组件

- .scss

不会被编译成哈希字符串，为全局样式

局部作用域语法:local(.className)
全局规则语法:global(.className)

参考文献
[http://www.ruanyifeng.com/blog/2016/06/css_modules.html](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)