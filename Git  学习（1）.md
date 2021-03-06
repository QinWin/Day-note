Git 学习
===========================================================

## Git 廖雪峰学习

### 1.git 常用命令
  
  安装完成后要配置git
  git config --global user.name "Your Name"
  git config --global user.email "email@example.com"
  
  git  init 初始化仓库
  git  add   把文件添加到仓库
  git  commit -m "dsc"  把文件提交到仓库  "dsc"该次提交的说明
  git  status 查看仓库当前状态
  git  diff   filename 查看文件发生的变化修改
  
  git  log  查看提交日志  排序从最近到最远
  git  log --pretty=oneline  格式化呈现 
  
  //分支切换推荐使用switch
  git branch branchname 创建分支
  git checkout branchname 切换到分支
  git checkout -b branchname  创建并切换到分支
  git branch -d branchname 删除分支
  git branch -D <name>  强行删除分支（一般指未合并的分支）
  //新版本
  git switch branchname 切换分支
  git switch -c branchname 创建并切换到分支
  
  git merge branchname 合并分支到当前分支
  
  git stash 把当前工作现场“储藏”起来，等以后恢复现场后继续工作
  git stash list 查看之前保存的工作现场
  git stash apply  恢复工作现场 
  git stash drop   删除保存的工作现场
  git stash pop   恢复工作现场并删除保存的工作现场
  
  git cherry-pick <commit> 把bug提交的修改“复制”到当前分支
  
  git rebase  操作可以把本地未push的分叉提交历史整理成直线
  
  //git last 显示最后一次提交信息 不好使
  
  //谨慎操作
  git  reset --hard HEAD^  回退一个版本
  git  reset --hard HEAD^^ 回退两个版本
  git  reset --hard HEAD~n  回退n个版本
  
  git  reset --hard commit-id  重置到id下版本(配合git  reflog 使用)
  git reflog  记录所用命令
  
  git diff HEAD -- filename 可以查看工作区和版本库里面最新版本的区别
  git checkout -- filename  撤销文件工作区修改 
  git reset HEAD -- filename 撤销暂存区修改
  
  git rm filename  删除文件
  
  
  git log --graph --pretty=oneline --abbrev-commit  图形化显示分支状态
  
  git merge --no-ff -m "message" branchname  合并分支到当前分支（记录合并点）
  
  git config --global alias.st status 创建别名
  
  //格式化分支显示样式
  git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
  
### 2.常识点
首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码
等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个
单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把
二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

Microsoft的Word格式是二进制格式

UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

千万不要使用Windows自带的记事本编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行
为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可
思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱
智行为带来的。  

Git跟踪并管理的是修改，而非文件。

从来没有被添加到版本库就被删除的文件，是无法恢复的！

master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用
命令git branch --set-upstream-to <branch-name> origin/<branch-name>

如何参与一个开源项目呢？比如人气极高的bootstrap项目，这是一个非常强大的CSS框架，你可以访问它的项目
主页https://github.com/twbs/bootstrap，点“Fork”就在自己的账号下克隆了一个bootstrap仓库，然后，从自己
的账号下clone：
git clone git@github.com:michaelliao/bootstrap.git
一定要从自己的账号下clone仓库，这样你才能推送修改。

### 3.名词释义

工作区 working reposity

版本库  reposity  
工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的
第一个分支master，以及指向master的一个指针叫HEAD。

### 4.远程仓库
 生成ssh key
 ssh-keygen -t rsa -C "youremail@example.com"
 
 若配置多个远程仓库，需对当前工程进行配置
 git config --local user.email "email"
 git config --local user.name  "name"
 
 关联远程仓库
 git remote add origin git@github.com:QinWin/learngit.git
 推送并关联远程仓库
 git push -u origin master
 推送分支到远程
 git push origin <name> 
 
 先创建远程库，然后，从远程库克隆
 git clone git@github.com:QinWin/gitskills.git
 
 git remote 查看远程仓库
 git remote -v 查看远程仓库详情
 
 创建远程分支到本地
 git checkout -b dev origin/dev
 问题
 fatal: 'origin/dev' is not a commit and a branch 'dev' cannot be created from it
  or Updates were rejected because the tip of your current branch is behind
 its remote counterpart.
 解决：推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，
 先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：
 git pull  
 If you wish to set tracking information for this branch you can do so with:
 git branch --set-upstream-to=origin/<branch> dev
 git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：
 git branch --set-upstream-to=origin/dev dev
 
 首次关联远程仓库 git pull
 问题
 fatal: refusing to merge unrelated histories
 解决：git pull origin <branch name> --allow-unrelated-histories
       
       git clean  -d  -fx
       d  -----删除未被添加到git的路径中的文件
       f  -----强制运行
       x  -----删除忽略文件已经对git来说不识别的文件
### 4.标签
发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，
取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。

git tag <name> 创建标签
git tag   查看所有标签
git tag -d <name> 删除标签
git show <name> 查看标签详情
git tag <name> <commit-id> 在一次提交上创建标签
git tag -a <name> -m "message" <commit-id>  创建一个带有描述的标签

git push origin <name> 同步标签到远程
git push origin --tags  同步所有标签到远程

删除远程标签 首先删除本地标签
git tag -d name
git push origin :refs/tags/name  删除远程标签

### 5.忽略文件
官方配置
https://github.com/github/gitignore/blob/master/Android.gitignore

git check-ignore -v <filename> 检查文件忽略规则
