# ubuntu相关下的说明和指令备忘录

安装命令apt
-----------
1. `apt install ubuntu-gnome-desktop`安装指定包
2. `apt list --installed`查看安装了的包


文件查找
--------
`grep file_monitors ./ --exclude-dir=".svn" --include="*.erl"  -nr`

目录文件对比
------------
`diff -uqr -x ".svn" ${exclude} ${1} $copy_dest_dir >${DiffLog}`

screen命令
-----------
`screen -S zzc` 创建会话，`screen -R zzc` 重进会话，快捷键ctrl+a,d断开当前会话(不是退出终止)

git
----
`git branch --set-upstream-to=origin/main`

$$
A~n-1~*3
$$
