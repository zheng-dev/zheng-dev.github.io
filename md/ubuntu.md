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

date "+%Y%m%d%H%M%S"
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
`pyinstaller --optimize 2 -F -i a2.ico -w --add-data="a.ico;." ..\db_read.py` upx.exe下载放到`venv\Scripts`目录即会生效，加了这2个会使9.83 MB的变小到8.03 MB

```py
def get_resource_path(relative_path):
    """获取资源文件绝对路径，用于打包后的程序访问资源文件"""
    import sys, os

    try:
        # PyInstaller 创建的临时文件夹，存放资源文件
        base_path = sys._MEIPASS
    except Exception:
        # 没有打包或者不是通过 PyInstaller 打包
        base_path = os.path.abspath(".")

    return os.path.join(base_path, relative_path)
```

```bat
@echo off
::汉字路径
chcp 65001
cd /d  d:\my_all_test\server_tools\yk_tool\jira\.db\
call ..\venv\Scripts\activate.bat
pyinstaller --optimize 2 -F -i a.ico -w ..\db_read.py
xcopy /y /f dist\db_read.exe  G:\后台\db_game\
TortoiseProc.exe/command:commit /path:"G:\后台\db_game\" /closeonend:2  /logmsg:"new xx"
pause
```

杂项
----

```bash
在win中直接以root身份运行wsl
wsl --user root
```
vim配置
-------
`Ctrl + [`来代替esc;`^u`向上翻页`^d`向下翻页;`7j`下跳7行,`7k`上跳7行;`w`跳到下个单词开头，`b`前跳;
`f`再界要找的字母直接定位;`0`本行首,`$`本行尾;`gg`文件首;
`yaw`复制本单词(yank all words),`yy`cp本行`y4j`cp下4行,可组合定范围;
`daw`删除本单词,`dd`删除本行,可组合定范围;
`O`向上插入一行,`o`向下插入一行

```bash
set number
set noexpandtab
set tabstop=4
set syntax=on
set cursorline
set mouse=a
set selection=exclusive
set selectmode=mouse,key
set showmatch
map <C-S> :w<CR>
nmap ; :
set noswapfile		".swp
set statusline +=%2*/%L%*               "total line

```

$$
A~n-1~*3
$$

