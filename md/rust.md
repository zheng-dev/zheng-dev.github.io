# rust配置-需要链编工具
参考官网`https://www.rust-lang.org/zh-CN/learn/get-started`
#### 方式A windows(wsl)安装
`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
#### 方式B windows安装
###### 安装微软的c++
`vs_buildtools__b375a2a77f354184bb5ea71b15323f09.exe`
###### 安装rust
`rustup-init.exe`
#### cargo设置国内镜像
1. 设置环境变量(win下也支持)

`export RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static`
2. cargo太慢、改国内镜像
```bash
#C:\Users\Admin\.cargo目录下的config文件加如下内容

[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'ustc'
[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"
[source.rustcc]
registry = "https://code.aliyun.com/rustcc/crates.io-index"

```
#### rust环境确认及cmd操作
```bash
#可以编译成哪些目标文件
rustup target list
#查看toolchains
rustup show
#安装某toolchains
rustup toolchain install
#gnu链编
rustup toolchain install  stable-x86_64-pc-windows-gnu
#切换默认toolchain
rustup toolchain install  stable-x86_64-pc-windows-gnu

#建工程
cargo new RustDemo
#编译生成exe
rustc greeting\src\main.rs
#编译并 运行
cargo run
```



# idea安装
1. 安装rust插件
2. 安装toml插件

# 基础概念
1. 包（packages）: Cargo 的一个功能，它允许你构建、测试和分享 crate。
2. 箱(crates): 一个模块的树形结构，它形成了库或二进制项目
3. 模块(modules) 和 use:  允许你控制作用域和路径的私有性
4. 路径(path): 一个命名例如结构体、函数或模块等项的方式

模块文件拆分时，放到子目录要用到桥的rs来代理

#### 多线程
channel 其实是一个 multi-producer，single-consumer 的结构，也就是我们俗称的 MPSC