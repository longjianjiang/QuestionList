# 2020-11-12

问题：  

一个cell中加载一个离线包页面，用了一个通用的webViewController去加载，这个时候在`didFinish navigation`中执行`document.documentElement.scrollHeight`获取webview的内容高度一直是初始设置的高度约束值。

但是如果将这个容器View单独加在View上，可以正常获取。

暂时的解决方案是，定义一个bridge让前端进行告知实际的高度。
