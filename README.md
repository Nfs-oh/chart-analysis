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

l: 30160: function init$1(dom, theme, opts)
l: 30187: var chart = new ECharts(dom, theme, opts);
l: 28133: var Echarts = (function (_super){
  	  // 30096
  	  // Eventful是一个订阅器模型
	})(Eventful)

// 调用setOptions开始绘制图表
instance.setOption(options)

l: 28289: ECharts.prototype.setOption = function (option, notMerge, lazyUpdate)

// 核心语句
l: 28346:
prepare(this);
updateMethods.update.call(this, null, updateParams);
```
```javascript
prepare(this);
l: 29038:
  prepare = function (ecIns) {
    var scheduler = ecIns._scheduler;
    scheduler.restorePipelines(ecIns._model);
    scheduler.prepareStageTasks();
    prepareView(ecIns, true);
    prepareView(ecIns, false);
    scheduler.plan();
  };
```

```javascript
l:28348
// 该变量的赋值在 ECharts.internalField 的立即执行函数里面
updateMethods.update.call(this, null, updateParams);

l: 29222: updateMethods = {}
l: 29232: updateMethods.update = function (payload, updateParams){}

l: 29265: 
render(this, ecModel, api, payload, updateParams) {
  allocateZlevels(ecModel);
  renderComponents(ecIns, ecModel, api, payload, updateParams);
  each(ecIns._chartsViews, function (chart) {
    chart.__alive = false;
  });
  renderSeries(ecIns, ecModel, api, payload, updateParams);
  each(ecIns._chartsViews, function (chart) {
    if (!chart.__alive) {
      chart.remove(ecModel, api);
    }
  });
}

l: 29707: renderSeries = function (ecIns, ecModel, api, payload, updateParams, dirtyMap) {}


```

