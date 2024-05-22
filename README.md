# 第一次提交

```bash
echo "# GIT_test" >> README.md`
git init `这行命令是在当前目录下初始化一个Git仓库。`
git add README.md `这行命令是将README.md文件添加到Git的暂存区，准备提交。`
git commit -m "first commit" `这行命令是提交README.md文件到本地仓库，并添加了一条提交信息 "first commit"。`
git branch -M main `这行命令是将当前的分支（通常是master）重命名为main。`
git remote add origin git@github.com:Yangzepeng5382/GIT_test.git `添加为本地仓库的远程仓库，并将其命名为origin。`
git push -u origin main `这行命令是将本地仓库的main分支推送到远程仓库的main分支，并将它们关联起来。`
```


# 时光穿梭机

##版本回退

```bash
git diff readme.txt  `查看现在的修改与上一次的提交有什么区别`
git log `查看所有提交的分支`
git log --pretty=oneline `更加简洁`
git reset --hard HEAD^ `回退到上一个版本 最新一次提交的上一次 版本 回退到add distributed` 
git reset --hard 1094a `回退到log看到的版本`                
git reflog `查看历史git命令`
┌────┐
│HEAD│
└────┘
   │
   └──▶ ○ append GPL
        │
        ○ add distributed
        │
        ○ wrote a readme file
        
┌────┐											
│HEAD│                   
└────┘
   │
   │    ○ append GPL
   │    │
   └──▶ ○ add distributed
        │
        ○ wrote a readme file
```



![1](./tupian/1.png)

##撤销修改

```bash
git checkout -- readme.txt `撤销修改`
```

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

## 删除文件

一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用`rm`命令删了：

```bash
$ rm test.txt
```

现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`：

```bash
$ git rm test.txt
rm 'test.txt'

$ git commit -m "remove test.txt"
[master d46f35e] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
```

现在，文件就从版本库中被删除了。

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

```bash
$ git checkout -- test.txt
```

`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

# 远程仓库

##添加远程库

如果添加的时候地址写错了，或者就是想删除远程库，可以用`git remote rm <name>`命令。使用前，建议先用`git remote -v`查看远程库信息：

```bash
$ git remote -v
origin  git@github.com:michaelliao/learn-git.git (fetch)
origin  git@github.com:michaelliao/learn-git.git (push)
```

然后，根据名字删除，比如删除`origin`：

```bash
$ git remote rm origin
```

##克隆远程仓库

现在，远程库已经准备好了，下一步是用命令`git clone`克隆一个本地库：

```bash
$ git clone git@github.com:michaelliao/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
```

# 分支管理

Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`



***

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

```ascii
                  HEAD
                    │
                    │
                    ▼
                 master
                    │
                    │
                    ▼
┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘
```

```bash
$ git checkout -b dev  `创建一个节点`
```

```ascii
                 master
                    │
                    │
                    ▼
┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘
                    ▲
                    │
                    │
                   dev
                    ▲
                    │
                    │
                  HEAD
```

```bash
$ git add .
$ git commit -m "" `在dev上提交一次` 
```



```ascii
                 master
                    │
                    │
                    ▼
┌───┐    ┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘    └───┘
                             ▲
                             │
                             │
                            dev
                             ▲
                             │
                             │
                           HEAD
```

```bash
$ git merge dev `合并当前分支和dev`
```

```ascii
                           HEAD
                             │
                             │
                             ▼
                          master
                             │
                             │
                             ▼
┌───┐    ┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘    └───┘
                             ▲
                             │
                             │
                            dev
```

```bash
$ git branch -d dev `删除dev节点`
```

```ascii
                           HEAD
                             │
                             │
                             ▼
                          master
                             │
                             │
                             ▼
┌───┐    ┌───┐    ┌───┐    ┌───┐
│   │───▶│   │───▶│   │───▶│   │
└───┘    └───┘    └───┘    └───┘
```

真是太神奇了，你看得出来有些提交是通过分支完成的吗？

``` bash
$ git log --graph --pretty=oneline --abbrev-commit  `查看分支结构`
```

## 解决冲突

```
$ git checkout -b featurel `创建一个新的分支准备修改`
$ git add .
$ git commit -m "" `在新的分支进行一次提交`
```

```
$ git checkout main
$ git add .
$ git commit -m `在原本的分支进行一次提交`
```

```
`情况1:两次修改没有任何冲突`
$ git merge featurel `在原本你的分支上对修改分支进行合并`
`情况2:两次修改修改了相同的地方`
$ git merge featurel
$ git add .
$ git commit -m "fix" `提交之后会告诉你`
```



## 分支管理策略

```bash
`通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。`
$ git merge --no-ff -m "merge with no-ff" dev
`情况1：
`		创建了一个分支在分支上提交了然后在原分支上没有提交直接合并那么就会直接快速合并保留分支地址`
`情况2：`
`		创建了一个分支在这个分支上更改提交了然后又在原分支上更改提交了这个时候合并不会是快速合并而是保留着两个地址`
`情况3：`
`		创建了一个分支在分支上提交了然后在原分支上没有提交用no-ff合并那么就会直接快速合并保留两个分支地址`
```

![2](.\tupian\2.png)

```bash
`只看最上面两个提交一个是在dev的提交一个是合并之后的总提交`
`如果在合并分支的时候遇到了冲突那么需要解决然后add然后commit`
```

