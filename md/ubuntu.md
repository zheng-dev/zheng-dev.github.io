# ubuntu相关下的说明和指令备忘录

安装命令apt
-----------
1. `apt install ubuntu-gnome-desktop`安装指定包
2. `apt list --installed`查看安装了的包

`yum install python3.11 --nogpgcheck`可以不检查gpg,直接安装

文件查找
--------
`grep file_monitors ./ --exclude-dir=".svn" --include="*.erl"  -nr`
```bash
#~/.bashrc文件中
alias warn='f(){ grep $1 warn.log.2024-07-1*;};f'
alias login='f(){ grep $1 login.log.2024-07-1*;};f'
alias online='netstat -anl |grep 11010 |grep ESTABLISHED |wc -l'
```

目录文件对比
------------
`diff -uqr -x ".svn" ${exclude} ${1} $copy_dest_dir >${DiffLog}`

screen命令
-----------
`screen -S zzc` 创建会话，`screen -R zzc` 重进会话，快捷键ctrl+a,d断开当前会话(不是退出终止)

git
----
`git branch --set-upstream-to=origin/main`

python
-------
`python -m py_compile test.py` 将py编译成pyc,`python -m compileall D:\MyPython`将目录下的所有py都编译成pyc
打包成exe
`pyinstaller --optimize 2 -F -w .\db_read.py` upx.exe下载放到`venv\Scripts`目录即会生效，加了这2个会使9.83 MB的变小到8.03 MB

杂项
----

```bash
在win中直接以root身份运行wsl
wsl --user root
```
$$
A~n-1~*3
$$

