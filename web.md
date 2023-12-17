# web建站

#### 问题记录


#### *promise*的问题
###### 测试代码如下20231208
```javascript
    //异步函数
    async function mer_html(code, num) {
      let promiseRet = mermaid.render('mermaid-svg-' + num++, code);
      let ret = await promiseRet.then(ret => {
        console.log("test1", ret.svg)
        return ret.svg;
      });
      console.log('test2', ret);
      return ret;
    }
    //同步函数
    function test(code, num) {
      let ret2;
      let a1 = mer_html(code, num).then(ret => ret2 = ret);
      console.log('test0', a1, ret2);
    }
```
的打印顺序如下：
1. `test0 Promise {<pending>} undefined`
2. `test1 <svg ar...`
3. `test2 <svg ar...`

结论：
`async`函数返回的是*Promise*对象；`await`只能在`async`的函数体中，所以在同步函数体中不能*wait*函数的结果。如果在下面的场景下，就是不行的：如有这样一个调用链a调用b，b调用c。但a和c都是第3方提供的函数。如果b是 非`async`的函数，而c是`async`的函数，但b需要c的返回结果处理逻辑,那就是不行的。
###### 关于浏览器dom、线程及EventLoop扩展
渲染层的*DOM*为了避免多线程异步的复杂操作，所以设计**js是单线程**+**EventLoop**的模式。对于`async`函数都是进入了任务队列，在当前js栈执行完成后就去从队列取一个头任务执行。
浏览器线程大体有：
1. GUI渲染
2. JS引擎：执行宏任务+微任务
3. 事件触发
4. 定时器触发
5. http请求

###### JS引擎+GUI流程

```mermaid
graph LR
js("JS当前栈开始")-->js_end("JS当前栈结束")--"调用"-->que("【宏任务/微任务】任务队列")-->que_c{"队列空"}--"是"-->g("GUI渲染")
que_c--"否"-->js
```

###### js异步任务分类
```mermaid
graph TD
macro("宏任务")-->s1("script块")
macro-->timeout("定时器")
macro-->ajax("ajax")
micro("微任务")-->pt("Pormise.Then")
async("异步")-->macro
async-->micro

```


###### 浏览器runtime的Worker
* 主进程


```javascript
//创建Worker,可以是独立js文档或一个html不认识的标签内容
let worker = new Worker(workJsFileURI);
//注册一个接收消息的函数
worker.onmessage = function (e) {
    var data = e.data;
};
//给Worker发送消息内容，可以是任务结构
worker.postMessage({"k":333});
```

* *workJsFile*独立文件的内容


```javascript
//接收主进程发来的消息数据
self.onmessage = function(msg) {    
    // todo 处理逻辑
    //构造返回的数据
    var workerResult = {};
    //用消息的形式发送给主进程
    postMessage(workerResult);
}
```
这种有些像erlang的进程消息方式。只是js主进程鉴于浏览器是单线程的，所以只能注册回调func，不能支持像erlang的`receive`阻塞同步等消息回来的方案。
[firefox参考文档](https://developer.mozilla.org/zh-CN/docs/Web/API/HTML_DOM_API/Microtask_guide "文档")


#### 网页加载完成时机

| 维度     |                `window.onload`                 |                   `$(document).ready()` |
| :------- | :--------------------------------------------: | --------------------------------------: |
| 执行时机 | 必须等网页全部载完毕（包括图片等），然后才执行 | 只需要等网页中的DOM结构加载完毕，就执行 |
| 执行次数 |       只能执行一次，重复执行会覆盖之前的       |                  可以执行多次，不会覆盖 |
| 简写方案 |                       无                       |                      `$(function(){});` |




# 开源协议的维度比较

| 修改源码后                           | LGPL许可证 | Mozilla许可证 | GPL许可证 | BSD许可证 | MIT许可证 | Apache许可证 |
| :----------------------------------- | :--------: | :-----------: | :-------: | :-------: | :-------: | -----------: |
| 可以闭源                             |     否     |      否       |    否     |    是     |    是     |           是 |
| 必须采用同样的许可                   |     否     |      否       |    是     |   未知    |   未知    |         未知 |
| 对修改处提供说明文档                 |     否     |      是       |   未知    |   未知    |   未知    |         未知 |
| 改动文件必须放置版权说明             |    未知    |     未知      |   未知    |    否     |    否     |           是 |
| 衍生软件的广告是否可以用你的名字促销 |    未知    |     未知      |   未知    |    否     |    是     |         未知 |

# git相关

#### git配置
```bash
#生成key
ssh-keygen -t ed25519 -C "Git my SSH Key"
#查看内容，上传到github
type C:\Users\xxx\.ssh\id_ed25519.pub

git@github.com:zheng-dev/zheng-dev.github.io.git
#配置上传看到的名称
git config --global user.name "xxx"
git config --global user.email xx@x.com

```

#### git同时向两个远端库上传
```editorconfig
[remote "gitee"]
	url = git@gitee.com:koo66/erlang_server.git
	fetch = +refs/heads/*:refs/remotes/gitee/*
	url = git@github.com:zzc16707826/my_all_test0.git
```

