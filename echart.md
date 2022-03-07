### echarts源码分析

1. 实例

```javascript
const container = document.getElementById('container');
const instance = echarts.init(container);
instance.setOption(options, true)
```

2. 调用栈

```javascript
echarts.init(container);

l: 30187: var chart = new ECharts(dom, theme, opts);
```

