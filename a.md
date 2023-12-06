## 测试1
**测试**一下效果
## 测试2


| 维度     |                `window.onload`                 |                   `$(document).ready()` |
| :------- | :--------------------------------------------: | --------------------------------------: |
| 执行时机 | 必须等网页全部载完毕（包括图片等），然后才执行 | 只需要等网页中的DOM结构加载完毕，就执行 |
| 执行次数 |       只能执行一次，重复执行会覆盖之前的       |                  可以执行多次，不会覆盖 |
| 简写方案 |                       无                       |                      `$(function(){});` |




# 开源协议的选择
[参考博文](http://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html "来源")

![参考图](http://www.ruanyifeng.com/blogimg/asset/201105/free_software_licenses.png "引用图")

## 创建ssh
```bash
ssh-keygen -t ed25519 -C "Gitee SSH Key"
type C:\Users\xxx\.ssh\id_ed25519.pub

git@github.com:zheng-dev/zheng-dev.github.io.git

git config --global user.name "xxx"
git config --global user.email xx@x.com

#cdn
https://az764295.vo.msecnd.net/stable/1a5daa3a0231a0fbba4f14db7ec463cf99d7768e/VSCodeUserSetup-x64-1.84.2.exe
vscode.cdn.azure.cn/stable/1a5daa3a0231a0fbba4f14db7ec463cf99d7768e/VSCodeUserSetup-x64-1.84.2.exe
```

## git同时向两个远端库上传
```bash
[remote "gitee"]
	url = git@gitee.com:koo66/erlang_server.git
	fetch = +refs/heads/*:refs/remotes/gitee/*
	url = git@github.com:zzc16707826/my_all_test0.git
```

```mermaid
graph LR
eq("effector_queue")--"调用"-->eTxt1("【内容/包装】效果器")--"调用"-->eTxt2("内容效果器2")--"调用"-->eTxt3("内容效果器N")
```