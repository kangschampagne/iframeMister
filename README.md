# iframeMister

## What
解决在同一个页面下，主页面和 iframe 中的通信，基于 postMessage 提出一套通信的解决方案。


## 几个点
1.只有在同源的情况下，主窗口才能创建一个 `<script>` 标签插入 `<iframe>` 的 `<body>` 中并执行。  
2.在不同源的情况下，不能使用 (1) 中的方法，只能在 `<iframe>` 对应的原页面中插入js文件。  

## 解决思路
几个不同的状态：  
0: init  
1: ready  
2: send  

log的形式：  
[iframeMister][who? HostSir : IframeSir][event][description]  

message形式：  
```javascript
{
  header: {
    messageType: 'application/x-iframe-mister-v1+json'
  },
  id: '[HostSir-{index}]',
  type: 'ready',
  content: {
    type: 'ADD_SOMETHING',
    value: { something: 5 }
  }
}
```

1.同源情况下，主窗口加载完毕时(onload)，创建一个已有js文件的 `<script src="./iframeSir.js" />` 标签，并插入到 `<iframe>` 的 `<body>` 中。  
非同源的情况下，将js文件手动引入到 iframe 所在的页面。  
*此时 iframe 是否加载成功？是否影响到 (1) 的操作？是否插入成功?  

2.iframe 加载完毕，获取父级 `window` 对象，并使用 `parentWindow.postMessage()` 告诉父级窗口，此 iframe 已经处于 ready 状态。

3.主窗口接收到 iframe 的 ready 状态，更改自身状态 为 ready 状态。  

(1)(2)(3) 完成之后两个窗口通信成功。  



