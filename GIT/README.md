## 1.master版本回退
```
先看一下提交的历史，确定一下回退到版本的commitID,执行：
git reset --hard commitID
如果现在在本地进行git push origin master的话，会报错，意思大概就是本地代码behind远程仓库的代码，执行下面命令：
git push -u origin master -f
强制把本地代码push到远程仓库。
```
