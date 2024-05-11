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

## 撤销修改

```bash
git checkout -- readme.txt `撤销修改`
```

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。
