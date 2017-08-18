[comment1]: id "rgb(44,44,110)四级标题"
[comment2]: id "rgb(110,110,0)三级标题"
[comment3]: id "rgb(0,110,110)二级标题"
[comment4]: id "rgb(110,0,110)一级标题"

<h1 align="center"><span style="color: rgb(110,0,110)">GIT</span></h1>

<h2 align="center"><span style="color:rgb(0,110,110)">Table of contents</span></h2>

* [1. GitHub基础使用](#0)
    * [1.1 增加SSH到GitHub账号](#1.1)
    * [1.2 使用Git的基本命令](#1.2)
    * [1.3 忽略一些文件](#1.3)
    * [1.4 文件操作](#1.4)
    * [1.5 查看提交历史](#1.5)
    * [1.6 GIT分支](#1.6)
    * [1.7 远程库](#1.7)
    * [1.8 Some git config](#1.8)

<h2 name="1"><span style="color: rgb(0,110,110)">1. GitHub基础使用</span></h2>

<h3 name="1.1"><span style="color: rgb(110,110,0)">1.1 增加SHH到GitHub账号</span></h3>

<h4 name=""><span style="color: rgb(44,44,110)">生成 SSH-Key</span></h4>

``` bash
ssh-keygen -t rsa -b 4096 -C "email"
```

默认生成的SSH-Key位于*~/.ssh*下.可以用`ls ~/.ssh`查看存在的SSH-Key.

<h4 name=""><span style="color: rgb(44,44,110)">增加SSH-Key到SSH-Agent</span></h4>

``` bash
# start the ssh-agent in the background
eval $(ssh-agent -s)
Agent pid 59566

# add ssh private key to the ssh-agent
ssh-add ~/.ssh/id_rsa
```
<h4 name=""><span style="color: rgb(44,44,110)">增加SSH-Key到GitHub</span></h4>

``` bash
# download xclip, and copies the contens of the id_rsa.pub file to your clipboard
sudo apt install xclip
xclip -sel clip < ~/.ssh/id_rsa.pub
```
再粘贴到github添加ssh的地方即可.
``` bash
ssh -T git@github.com
# 测试使用
```

<h3 name="1.2"><span style="color: rgb(110,110,0)">1.2 使用Git的基本命令</span></h3>

<h4 name=""><span style="color: rgb(44,44,110)">在目录初始化Git repository</span></h4>

``` bash
git init
```

<h4 name=""><span style="color: rgb(44,44,110)">配置Git</span></h4>

``` bash
# user.email and user.name is enssential for use git
git config --global user.email "your email"
git config --global user.name "your name"
```

<h4 name=""><span style="color: rgb(44,44,110)">从现有的repository中克隆</span></h4>

``` bash
git clone {<url>|<file-path>} [path]
```

<h4 name=""><span style="color: rgb(44,44,110)">一些基本的本地命令</span></h4>

``` bash
# 添加文件到暂存区
git add {<file>}

# 将暂存区的文件提交
git commit -m { comment }

# 检查当前的状态
git status
```

<h3 name="1.3"><span style="color: rgb(110,110,0)">1.3 忽略一些文件</span></h3>

*.gitignore文件*
将要忽略的文件名添加到`.gitignore`下  

> *`<.gitignore>`的一些语法*  

+ '\#'之后的为注释
+ '*.a'忽略以'.a'结尾的文件
+ '!except.a'不忽略'except.a'
+ 'dir/'忽略'dir'目录下的所有文件
+ '*'不匹配文件绝对路径的'/'
+ '**'能匹配文件绝对路径的'/'
+ '[ab]'匹配一次'a'或'b'

<h3 name="1.4"><span style="color: rgb(110,110,0)">1.4 文件操作</span></h3>

<h4 name=""><span style="color: rgb(44,44,110)">移除文件</span></h4>

``` bash
# 移除目录下的文件
rm <file-name>

# 移除repository的文件
git rm <file-name>  # 如果在暂存区需要`-f`

# 只移除repository的文件
git rm --cached <file-name>
```

<h4 name=""><span style="color: rgb(44,44,110)">移动文件</span></h4>

``` bash
# 移动操作
git mv <source-file> <dest-file>

# 上面的命令相当与下面的命令
mv <source-file> <dest-file>
git rm <source-file>
git add <dest-file>
```

<h3 name="1.5"><span style="color: rgb(110,110,0)">1.5 查看提交历史</span></h3>

<h4 name=""><span style="color: rgb(44,44,110)">使用`git log`</span></h4>

<h3 name="1.6"><span style="color: rgb(110,110,0)">1.6 分支</span></h3>

<h4 name=""><span style="color: rgb(44,44,110)">新建分支</span></h4>

``` bash
# 新建一个名为example的分支
git branch example [old-name]

# 切换到example分支
git checkout example

# 新建一个名为example的分支并切换到该分支
git checkout -b example [old-name]

# 以上各个命令, 若[old-name]存在，则新建的分支从[old-name]复制
```

<h4 name=""><span style="color: rgb(44,44,110)">删除分支</span></h4>

``` bash
# delete example branch
git branch -d example

# force delete example branch
git branch -D example
```

<h4 name=""><span style="color: rgb(44,44,110)">合并分支</span></h4>

``` bash
# 当前在branch1, 合并branch2
git merge branch2
```
<h3 name="1.7"><span style="color: rgb(110,110,0)">1.7 远程库</span></h3>

<h4 name=""><span style="color: rgb(44,44,110)">查看远程库</span></h4>

``` bash
# 查看远程库的名称
git remote
origin #example

# 显示远程库的名称和地址
git remote -v # -v verbose(详细)
origin git://github.com/example/exam.git (fetch)
origin git://github.com/example/exam.git (push)
```

<h4 name=""><span style="color: rgb(44,44,110)">增加远程库</span></h4>

``` bash
# add remote repository
git remote add [short-name] [url] # Then can use short-name to push fetch repository.
```

<h4 name=""><span style="color: rgb(44,44,110)">推送到远程库</span></h4>

``` bash
# push local branch to remote
git push [-f] {remote-repository} {local-branch} # Here using the '-f' option to force update

# push local branch to remote branch
git push [-f] {remote-repository} {local-branch}:{remote-branch}

# delete remote branch
git push {remote-repository} :{remote-branch}
```

<span style="color:green">if use ssh to push local branch to remote repositoty, should use "git@github.com:user-name/repository-name" format with remote url.</span>

<h4 name=""><span style="color: rgb(44,44,110)">抓取远程库</span></h4>

``` bash
# this command in below will generate a new branch, which named be {repository}/[repository-branch].But that branch can't change, if the [repository-branch] isn't exist, it default is master.
git fetch {repository} [repository-branch]

# track remote branch
git checkout --track {repository}/{branch}
```

<h3 name="1.8"><span style="color: rgb(110,110,0)">1.8 Some git config</span></h3>

<h4 name=""><span style="color: rgb(44,44,110)">Total config introduce</span></h4>

*git的配置文件*

* `/etc/gitconfig` # 首先读取，用 `--system` option 进行读写
* `~/.gitconfig` # 其次读取，用 `--global` option 进行读写
* `./.git/config` # 最后读取，在目录下运行进行读写

*Git配置命令`git config`的选项*

> `core.editor` # 这个选项指定编辑器给git调用  
> `commit.template` # 这个选项指定 `git commit` 命令的模板  
> `core.pager` # 这个选项指定当使用`diff`, `log`输出的分页器  
> `user.signingkey` # 这个选项指定默认的`tag`的GPG密匙  
> `core.excludesfile` # 和`.gitignore`相似，用于排除文件  
> `help.autocorrect` # 用于修正命令

<h4 name=""><span style="color: rgb(44,44,110)">Git中的着色</span></h4>

`color.ui` 用于开关是否着色, `true`表示开启着色， `false`表示关闭着色， `always`表是即使重定向也输出着色  

* `color.diff` # `true` or `false`
* `color.branch` # `true` or `false`
* `color.interactive` # `true` or `false`
* `color.status` # `true` or `false`

``` bash
# example

git config color.status.untracked "red green bold"
# that will changed the untracked file name output with red foreground greeen backgroung bold font
```

*可选的颜色有`normal, black, red, green, yellow, blue, magenta, cyan, white`, 字体的可选属性有`bold, dim, ul, blink, reverse`.

``` bash
# use the command change the output color
git config color.X.Y "`foreground-color` `background-color` `font`"
```

<h4 name=""><span style="color: rgb(44,44,110)">Git Alias</span></h4>

``` bash
# there are some example alias

git config [--system|--global] alias.st status
# so `git st` is equal `git status`
git config [--system|--global] alias.unstage 'reset HEAD --'
# so `git unstage filea` is equal `git reset HEAD filea`
```
