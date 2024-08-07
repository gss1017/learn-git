## git学习笔记
- 此文档通过观看 [廖雪峰git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000) 与 简书 Ruheng的 [一篇文章，教你学会Git](https://www.jianshu.com/p/072587b47515)所得
- 该笔记包含了学习git时的大部分指令，及部分概念和自己的一些感悟
- [前端早读课：Git项目管理](https://mp.weixin.qq.com/s/V9oV1AmOv83iBt-6x865kA)
- [15分钟成为 GIT 专家](https://mp.weixin.qq.com/s?__biz=MjM5MTA1MjAxMQ==&mid=2651229405&idx=1&sn=5fc3fdcdd56d835018513efff8e3c4f1&chksm=bd4955598a3edc4fa138ef0c8cdc069ac0a76ab57c61b7f870d1ca62884e0873ee5fe1242758&scene=21#wechat_redirect)
- [Git的使用--如何将本地项目上传到Github](https://blog.csdn.net/Lucky_LXG/article/details/77849212)
- [git Merge 原理](https://blog.csdn.net/u012937029/article/details/77161584)
- [git rebase 分支的管理](https://gitee.com/progit/3-Git-%E5%88%86%E6%94%AF.html#3.3-%E5%88%86%E6%94%AF%E7%9A%84%E7%AE%A1%E7%90%86)
- [git 合并多个commit](https://www.jianshu.com/p/964de879904a)

![image](https://upload-images.jianshu.io/upload_images/3985563-6b745d5fac15906c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/508)

>HEAD 指向当前分支最新的提交(即当前分支最新的版本)，通过HEAD可以来切换分支

>origin 远程仓库名称，git默认叫法。

## 安装git

> 指定git的 global参数，这台机器上的所有git仓库都会使用这个配置

```
git config --global user.name 'your name'

git config --global user.email 'your email'

git config --global color.ui true 让git显示颜色，命令输入更醒目
```

### 忽略特殊文件

>在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件
 所有配置文件可以直接在线浏览：https://github.com/github/gitignore

##### 忽略文件规则：

- 忽略操作系统自动生成的文件，比如缩略图等；
- 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
- 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

```
git add -f APP.class 强制添加忽略文件

git check-igonre -v <忽略文件> 检测.ignore 那个规则写错

git rm --cache . 清空工作区所有缓存
```

## git常用指令
```
git log ''|pretty=oneline 显示提交过的记录 | 显示提交过记录的Id

```
```
git reflog 查看命令历史，以便以回到某个版本
```

#### 初始化git 仓库
```
git init 将目录变成git可以管理的仓库（它会生成一个.git文件 git版本库）
```
#### 添加修改
```
git add <file-name> 给缓存区添加一个文件

git add  . 上传工作区所有文件到缓存区

git commit -m 'description' 提交文件到本地仓库

# --no-edit: 是跳过进入编辑器，直接提交
git commit --amend --no-edit 新修改的内容，添加到上次提交中，减少提交的日志
```

#### 查看状态与差异、提交记录
```
git status 实时查看工作区状态
```
```
git diff 查看工作区与缓存区（index/stage）差异  

git diff HEAD 查看工作区与当前分支最新commit之间的差异
```
```
git log 查看当前分支提交记录

git log --graph --pretty=oneline --abbrev-commit 查看分支合并情况

git log --pretty=oneline --abbrev-commit 查找历史提交的commit_id

git log master..env/dev 查看单个分支的提交记录 查看env/dev分支的提交记录（env/dev 是在master上拉出来的）
```



#### 版本回退
```
git reset --hard HEAD^ 回退到上一个版本
git reset --hard HEAD~100 回退到前第100个版本
git reset --hard <commit_id> 回到指定某个版本
git reset (–mixed) HEAD~1 回退一个版本,且会将暂存区的内容和本地已提交的内容全部恢复到未暂存的状态,
不影响原来本地文件(未提交的也不受影响) 
git reset –soft HEAD~1 
回退一个版本,不清空暂存区,将已提交的内容恢复到暂存区,不影响原来本地的文件(未提交的也不受影响) 
git reset –hard HEAD~1 
回退一个版本,清空暂存区,将已提交的内容的版本恢复到本地,本地的文件也将被恢复的版本替换

git push -f 提交回退的版本   (注：强制提交后，当前版本后面的提交版本将会删掉！)
```

```
git revert commit-sha1 主要用于回滚对人协同开发的公共分支，可以平稳回滚代码，但却保留提交记录，避免让协作的代码冲突
```
#### 撤销修改及还原文件
```
git checkout -- <file> 撤销工作区更改

git checkout HEAD^ -- <file> 将上一个版本库的指定文件检出到当前工作区(还原当前版本库删除的文件)

git checkout (本质就用版本库里的版本替换工作区的版本)

git checkout - 切换上一个分支

git checkout --track origin/dev 基于远程分支创建本地分支，并跟踪对应来自 ‘origin’ 的远程分支
```
```
git reset HEAD <file> 撤销缓存区更改到工作区
```
```
git rm <file> 删除工作区文件，并将删除动作提交到缓存区
```

```
git restore --staged 将文件从暂存区撤出，但不会撤销文件更改

git restore 将不再暂存区的文件撤销更改
```

#### 远程仓库的部分指令
```
git remote add origin git@github.com:gss1017/example.git 添加一个远程的仓库
```
```
git remote set-url origin <url> 设置(修改)改本地仓库指向远程仓库的地址
```
```
git push origin <branch-name> 推送本地分支到对应的远程分支
```
```
git remote rm origin 如果要重新关联新的远程仓库，应该删除已关联的远程仓库
```
> 一个本地仓库关联多个远程仓库

```
git remote rm origin 先删除远程的origin 仓库

git remote add githubR git@github.com:gss1017/dir.git 先关联github的远程仓库，远程仓库的名字叫 githubR

git remote add giteeR git@gitee.com:gtgs/learn.git 再关联gitee的远程仓库，名字叫giteeR

内容分别推送
git push githubR master

git push giteeR master
```

> 将一个库推到另一个远程库

```
1. 从原地址克隆一份裸版本库，比如原本托管于 GitHub。
git clone --bare git://github.com/username/project.git

2. 然后到新的 Git 服务器上创建一个新项目，比如 GitCafe。

3. 以镜像推送的方式上传代码到 GitCafe 服务器上。
cd project.git
git push --mirror git@gitcafe.com/username/newproject.git
```
> 给当前库换源
```
git commit -m "Change repo." # 先把所有为保存的修改打包为一个commit
git remote remove origin # 删掉原来git源
git remote add origin [YOUR NEW .GIT URL] # 将新源地址写入本地版本库配置文件
git push -u origin master # 提交所有代码
```

##### 多人协助模式图
![image](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384909239390d355eb07d9d64305b6322aaf4edac1e3000/0)

###### 创建SSH key
```git
ssh-keygen -t rsa -C 'your-email@163.com'
```

> 为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。
- > 本地Git仓库和GitHub仓库(remote repository)之间的传输是通过SSH加密的
- > 相当于给远程仓库上添加了你本机的身份标识，这样本地就可以与远程通信了
- > 生成的ssh-key 在用户目录下的.ssh中，里面有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。



#### 分支操作指令

> ！！！通常，git在合并分支的时候，会自动用fast forward模式，在这种模式下，删除分支后，会丢掉分支信息。
>如果强制禁用fast forword模式，git会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息了。
>当准备合并分支的时候，请注意--no-ff参数，表示禁用fast forword模式。

```
git branch <branch-name> 新建一个分支，但依然停留到当前分支

git branch -m old_branch new_branch 将本地分支进行改名

git checkout <branch-name> 切换到指定分支

git checkout commit-id 切换到指定的commit

git branch -f <branch-name> commit-id 将指定分支指向指定的commit

git checkout -b <branch-name> 新建一个分支，并切换到该分支

git branch -D <branch-name> 删除分支
git branch -d <branch-name> 删除完全合并的分支（没有merge的不可以）

git merge <branch-name> 合并指定分支到当前分支 (将当前分支(master)指向 指定分支(dev)的最新的提交)

git log --graph --pretty=oneline --abbrev-commit 查看分支合并情况

git merge --no-ff -m '提交信息' 

git checkout -b <branch-name> origin/<branch-name> 在本地创建与远程对应的分支

git branch -u origin/<branch-name> <branch-name> 指定本地分支追踪指定的远程分支

git branch --set-upstream <branch-name> origin/<branch-name> 建立本地分支与远程分支的关联

git push origin <branch-name>:<branch-name> 把新建的本地分支push到远程服务器，远程分支与本地分支同名（当然可以随意起名）

git push origin :<branch-name> 推送一个空的分支到远程，相当与删除远程分支

git push origin --delete <branch-name> 删除指定的远程

git push --set-upstream origin <branch-name> 将本地分支push到远程并与之关联

```

#### 工作区缓存指令
>> 一般是工作进行到一半，需要进行其他任务是使用

```
git stash 将当前工作区‘储藏’起来，等以后恢复了当前工作区又可以继续工作了

git stash list 查看缓存的工作区列表

git stash apply stash@{0} 恢复当前分支被隐藏的工作区，恢复后，stash内容并不删除

git stash pop 恢复当前分支被隐藏的工作区，但是恢复的内容在stash list 中被删除

git stash drop 删除stash 内容
```

#### 标签指令
>默认标签是打在最新提交的commit上的

```
git tag <name> 打一个新的标签

git tag 查看所有标签

git log --pretty=oneline --abbrev-commit 查找历史提交的commit_id

git tag v0.9 <commit_id> 给指定提交 加标签

git show <name> 查看标签信息

git tag -a <tag-name> -m <description> <commit_id> 创建带有说明的标签 -a指定标签名 -m指定说明文字 

git tag -s <tag-name> -m <description> <commit_id> 用私钥（PGP）签名一个标签
用PGP签名的标签是不可伪造的

git tag -d <tag-name> 删除指定标签

--标签一开始创建是储存在本地的，需手动推送到远程
git push origin <tag-name> 推送指定标签到远程

git push origin --tags 一次推送所有本地标签到远程

--删除远程标签，得先删除本地标签，再删除远程标签
git tag -d <tag-name> 删除本地标签
git push origin :refs/tags/<tag-name> 删除远程标签
```

#### git指令别名配置 
>配置Git的时候，加上--global是针对**当前用户**起作用的，如果不加，那只针对**当前的仓库**起作用。

>当前**用户**的Git配置文件放在**用户主目录**下的一个隐藏文件.gitconfig中：
```
git config --global alias.st status

git config --global alias.co checkout 

git config --global alias.ci commit

git config --global alias.br branch

git config --global alias.unstage 'reset HEAD' 

git config --global alias.last 'log -1'

git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

#### git 高级操作

```
git cherry-pick <commit-id>... 将一些指定提交复制到当前所在的位置（HEAD）下面

git rebase [主分支（目标分支、基分支）] [特性分支（当前分支、待变基分支）] 命令会先取出特性分支 ，然后在主分支上重演 
git rebase [主分支] 当前所在分支即为特性分支
git rebase -i  [startcommit-id]  [endcommit-id] -i的意思是--interactive，即弹出交互式的界面让用户编辑完成合并操作，[startcommit-id] [endcommit-id]则指定了一个编辑区间，如果不指定[endcommit-id]，则该区间的终点默认是当前分支HEAD所指向的commit(注：该区间指定的是一个前开后闭的区间);
内部参数：
pick：保留该commit（缩写:p）

reword：保留该commit，但我需要修改该commit的注释（缩写:r）

edit：保留该commit, 但我要停下来修改该提交(不仅仅修改注释)（缩写:e）

squash：将该commit和前一个commit合并（缩写:s）

fixup：将该commit和前一个commit合并，但我不要保留该提交的注释信息（缩写:f）

exec：执行shell命令（缩写:x）

drop：我要丢弃该commit（缩写:d）
```
