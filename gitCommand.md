```bash
git init
git add #只有add后再commit，修改才会被提交
git commit
git rm

git reset --hard HEAD^ / SHA1 
git reset filename
#git reset命令既可以回退版本，也可以把暂存区的修改撤回到工作区。
#当我们用HEAD时，表示最新的版本

git restore #丢弃工作区修改

git status
git diff filename
git log
git reflog  #查看历史命令

git push -u origin master  #第一次推送master分支的所有内容, -u参数只在第一次push时使用

git remote -v #查看远程仓库信息
git remote rm <name> #删除远程库（解除本地和远程的绑定关系）
```

**隐藏目录 .git** (git的版本库)

- ![](C:\Users\SHUHAN\OneDrive\归档\0.jpg)





