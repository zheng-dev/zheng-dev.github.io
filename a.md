# 介绍
- 👋 Hi, I’m @zheng-dev

### 测试1
**测试**一下效果
### 测试2
>- kkskdjf
>- kkkk
>kkkk
>sss

| 维度 | `window.onload` | `$(document).ready()` |
|:--------| :---------:|--------:|
| 执行时机 | 必须等网页全部载完毕（包括图片等），然后才执行 |只需要等网页中的DOM结构加载完毕，就执行|
| 执行次数 |只能执行一次，重复执行会覆盖之前的 |可以执行多次，不会覆盖|
| 简写方案 | 无 | `$(function(){});` |


- 1
- 2
- 3

# 开源协议的选择
[参考博文](http://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html "来源")

![参考图](http://www.ruanyifeng.com/blogimg/asset/201105/free_software_licenses.png "引用图")

## 创建ssh
```markdown
ssh-keygen -t ed25519 -C "Gitee SSH Key"
type C:\Users\xxx\.ssh\id_ed25519.pub

git@github.com:zheng-dev/zheng-dev.github.io.git

git config --global user.name "xxx"
git config --global user.email xx@x.com
```