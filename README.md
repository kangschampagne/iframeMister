# iframeMister

## What
解决在同一个页面下，主页面和 iframe 中的通信，基于 postMessage 提出一套通信的解决方案。


## 几个点
1.只有在同源的情况下，主页面才能创建一个 `<script>` 标签插入 `<iframe>` 的 `body` 中并执行。  
2.在不同源的情况下，不能使用 (1) 中的方法，只能在 `<iframe>` 对应的原页面中插入js文件。  

## 几个应用场景
