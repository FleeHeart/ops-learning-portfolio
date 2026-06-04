# linux 基础命令笔记

## 文件位置相关命令

### pwd
wd（英文全拼：print work directory） 命令用于显示当前用户所在的工作目录的完整路径。

常用写法示例：
1. 输入：pwd
-  输出：/workspaces/ops-learning-portfolio <!-- 逻辑路径 -->
2. 输入：pwd -P
-  输出：/workspaces/ops-learning-portfolio <!-- 物理路径 -->

工作场景：确认自己现在在哪个目录，避免删错或改错文件

我的思考：
1. pwd 和 echo $PWD 有什么区别？
-  pwd 是一个内置命令，而 $PWD 是一个环境变量。在大多数情况下，它们输出相同，但 pwd 命令可以带选项（如 -P），而 $PWD 总是显示逻辑路径。
2. 为什么需要 -P 选项？
-  当你在一个符号链接目录中工作时，有时需要知道实际的物理位置而不是符号链接路径，这时 -P 选项就很有用。
3. pwd 命令会失败吗？
-  在正常情况下 pwd 不会失败，但如果当前目录被删除（在另一个终端会话中），pwd 可能会显示错误。

### ls
ls（英文全拼： list directory contents）命令用于显示指定工作目录下之内容（列出目前工作目录所含的文件及子目录)。

常用写法示例：
1. 输入：ls
-  输出：01-linux-notes  README.md
2. 输入：ls -l <!-- 以长格式显示当前目录中的文件和目录 -->
-  输出：
    total 8
    drwxrwxrwx+ 2 codespace codespace 4096 Jun  4 04:06 01-linux-notes
    -rw-rw-rw-  1 codespace root       530 Jun  4 03:58 README.md
3. 输入：ls -a <!-- 显示当前目录中的所有文件和目录，包括隐藏文件 -->
-  输出：.  ..  .git  01-linux-notes  README.md
4. 输入：ls -lh                   # 以人类可读的方式显示当前目录中的文件和目录大小
-  输出：
    total 8.0K
    drwxrwxrwx+ 2 codespace codespace 4.0K Jun  4 04:06 01-linux-notes
    -rw-rw-rw-  1 codespace root       530 Jun  4 03:58 README.md
5. 输入：ls -t <!-- 按照修改时间排序显示当前目录中的文件和目录 -->
-  输出：01-linux-notes  README.md
6. 输入：ls -R <!-- 递归显示当前目录中的所有文件和子目录 -->
-  输出:
    .:
    01-linux-notes  README.md

    ./01-linux-notes:
    linux-basci-commit.md
7. 输入：ls -l /etc/passwd        # 显示/etc/passwd文件的详细信息
-  输出：-rw-r--r-- 1 root root 1115 Mar 11 12:11 /etc/passwd

工作场景：显示当前目录的文件或者文件夹，可以快速知道所在目录是否有需要的文件

我的思考：
1. ls 命令的输出颜色可以通过 --color 选项控制：
蓝色：目录
绿色：可执行文件
红色：压缩文件
青色：链接文件
黄色：设备文件
2. 在脚本中使用 ls 时要注意，直接解析 ls 的输出可能不可靠，建议使用其他方法。

### cd
Linux cd（英文全拼：change directory）命令用于改变当前工作目录的命令，切换到指定的路径。
若目录名称省略，则变换至使用者的 home 目录 (也就是刚 login 时所在的目录)。
另外，~ 也表示为 home 目录 的意思， . 则是表示目前所在的目录， .. 则表示目前目录位置的上一层目录。

常用写法示例：
1. 输入：➜ /workspaces/ops-learning-portfolio (main) $ cd 01-linux-notes <!-- 切换路径 -->
-  输出：➜ /workspaces/ops-learning-portfolio/01-linux-notes (main) $ 
2. 输入：➜ /workspaces/ops-learning-portfolio/01-linux-notes (main) $ cd .. <!-- 切换到上级目录 -->
-  输出：➜ /workspaces/ops-learning-portfolio (main) $ 
3. 输入：➜ /workspaces/ops-learning-portfolio (main) $ cd ~ <!-- 切换到用户主目录 -->
-  输出：➜ ~ $ 
4. 输入：➜ ~ $ cd - <!-- 切换到上次访问的目录 -->
-  输出：
    /workspaces/ops-learning-portfolio
    ➜ /workspaces/ops-learning-portfolio (main) $ cd ~

工作场景：在 Linux 系统中进行目录切换操作。

## 文件操作相关命令

### mkdir
Linux mkdir（英文全拼：make directory）命令用于创建目录。

常见使用示例：
1. 输入：mkdir -p mkdir/test
-  解释：在工作目录下的 mkdir 目录中，建立一个名为 test 的子目录。若 mkdir 目录原本不存在，则建立一个。
  （注：本例若不加 -p 参数，且原本 mkdir 目录不存在，则产生错误。）
  
### touch
touch命令用于修改文件或者目录的时间属性，包括存取时间和更改时间。若文件不存在，系统会建立一个新的文件。

常见使用示例：
1. 要求，将mkdir/test文件的时间属性修改为当前系统时间
-  输入：➜ /workspaces/ops-learning-portfolio/01-linux-notes/mkdir (main) $ ls -l test <!-- 查看文件属性 -->
-  输出：total 0
-  输入：➜ .../ops-learning-portfolio/01-linux-notes/mkdir/test (main) $ touch test <!-- 修改文件时间属性为当前系统时间 -->
-  输入：@FleeHeart ➜ .../ops-learning-portfolio/01-linux-notes/mkdir/test (main) $ ls -l test <!-- 查看文件属性 -->
-  输出：-rw-rw-rw- 1 codespace codespace 0 Jun  4 10:22 test

我的思考：使用指令"touch"时，如果指定的文件不存在，则将创建一个新的空白文件。

### cp

### mv

### rm