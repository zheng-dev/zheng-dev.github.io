mermaid语法说明
---------------

//www.bootcdn.cn/mermaid/dist/mermaid.min.css
https://blog.csdn.net/cherrylovedog/article/details/100731294
https://mermaid.nodejs.cn/syntax/sequenceDiagram.html

md语法
------
https://markdown.com.cn/basic-syntax/images.html


随机数-线性同余
--------------

![线性同余](https://pic4.zhimg.com/v2-0ae6921256f2cd094ed2fa2bbb3f1627_r.jpg)

$N_{j+1}=(A \times N_j+B) \% M $



[线性同余等算法](https://oi-wiki.org/math/number-theory/linear-equation/)
[shell编程](https://c.biancheng.net/shell/base/)
[protobuf](https://protobuf.dev/programming-guides/proto3/)

[md数据公式](https://zhuanlan.zhihu.com/p/441454622)

vscode dbg,测试可用
-------------------

[dbg参考文章](https://learnku.com/rust/t/36706)
```json
//.vscode\launch.json
{
    "name": "dbg win",
    "type": "cppvsdbg",
    "request": "launch",
    "program": "${workspaceRoot}/target/debug/rusty-bomber.exe",
    "args": [],
    "stopAtEntry": false,
    "cwd": "${workspaceRoot}",
    "environment": [],
    "externalConsole": true
},
{
    "name": "dbg osx",
    "type": "lldb",
    "request": "launch",
    "program": "${workspaceRoot}/target/debug/rusty-bomber.exe",
    "args": [],
    "cwd": "${workspaceRoot}"
},

//.vscode\tasks.json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",
            "type": "shell",
            "command": "cargo run --example breakout ;echo ======done====",
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```
rust
-----
#### 1条件编译
```rust
//只有在 webp feature 被定义后，以下的 webp 模块才能被引入进来
#[cfg(feature = "webp")]
pub mod webp;
```

```toml
[features]
# 定义一个 feature : webp, 但它并没有启用其它 feature
webp = []
ico = ["bmp", "png"]
```
#### 2cargo.toml说明
[cargo.toml说明](https://course.rs/cargo/reference/manifest.html)   
#### 3派生特性trait
```rust
//被 derive 标记的对象会自动实现对应的默认特征代码，继承相应的功能
#[derive(Debug, PartialEq, Eq, Copy, Clone)]
enum Collision {
    Left,
    Right,
}
```

Rust网址
--------
[Rust语言中文社区](https://rustcc.cn/article?id=c6b9d6c4-02d0-44a4-adc2-20129166ebda)
