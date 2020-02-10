# git bash note
![git-logo -w100](https://i.loli.net/2020/02/10/fTa6NyegZhoPiJY.png)
[Git](https://git-scm.com) is the most leading version control system in the world.
> This documentation is helping to memorize the most common command line instructions.

 You may keep original version control like this.
 ![original-version-control -w150](https://i.loli.net/2020/02/10/TEq18Rg2dOaXkJm.png)
Saving n duplications to trace files, but most of them are low efficiency, even you are confused about which version are you exactly want.
That's the reason why Linus Torvalds invent git.

## Config
### Installation
`brew install git`
### After Installation
```
git config --global user.name "FION"
git config --global user.email "fion@kr.ci"
```
`--global` means for all user on this computer.
### Advance Config

## Useful Command Line
```
cd ~/Workspaces/_Repo/git-learning/
git init
```
**ATTENTION!** 
*DO NOT USE WINDOWS SELF-INSTALLED NOTEPAD*
We strongly recommend ***Notepad++***.
Set `UTF-8` as encode of files.

 `git add README.md`means submit file into Stage (Index).
 
 `git commit -m "add new README.md"` means commit Index into Repository.
`-m` message
 ![three-trees-relationship](https://i.loli.net/2020/02/10/ZzAfnHb3JXcrgNR.png)

`git status` for files current status.

`git diff`

`git log`
`--decorate`
`--oneline`
`--graph`


`git reset`

`git checkout`
file for `-- filename`

`git reflog`

`git rm filename`

## Remote Repository
`ssh-keygen -t rsa -C "fion@kr.ci"`

Login your github account and add a new repo

`git remote add origin git@github.com:uxfion/git-learning`

`git push`
`git push origin master`
Para `-u` attach remote and local repository.

`git clone`

## Branch Management
`git branch`
`git branch <name>`
`git checkout <name>` or `git switch <name>`
`git checkout -b <name>` or `git switch -c <name>`
`git merge <name>`
`-m`
`--no-ff` for no fast forward
`git branch -d <name>`

### Bug Branch
情景：手上开发分支进行到一半，还没法提交，但有一个bug需要立即解决。
`git stash` 将工作现场“储存起来”
用 `git status` 查看现实clean
切换到主分支并从主分支创建临时分支
`git checkout -b issue-101`
```
git add README.md
git commit -m "fix bug 101"
git switch master
git merge --no-ff -m "merged bug fix 101" issue-101
git switch dev
git status
```
显示工作区是干净的，刚才的工作现场存哪去了？
用 `git stash list` 查看
`git stash apply`恢复，但恢复后stash内容不删除，需要用`git stash drop`来删除
or
`git stash pop` 恢复的同时把stash内容也删除了。

可以多次stash，然后`git stash apply stash@{0}`

在master分支上修复了bug后，我们要想一想，dev分支是早期从master分支分出来的，所以，这个bug其实在当前dev分支上也存在。**有！**
同样的bug，要在dev上修复，我们只需要把`4c805e2 fix bug 101`这个提交所做的修改“复制”到dev分支。注意：我们只想复制`4c805e2 fix bug 101`这个提交所做的修改，并不是把整个master分支merge过来。
为了方便操作，Git专门提供了一个`cherry-pick`命令，让我们能复制一个特定的提交到当前分支
`git cherry-pick 4c805e2`
git自动给dev分支做了一次提交

### Collaboration
查看远程仓库信息 `git remote`
更详细的信息 `git remote -v`
#### Push Branch
`git push origin master`推送主分支
`git push origin dev`推送dev分支

当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的master分支。



