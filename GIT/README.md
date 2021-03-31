## 1.master版本回退
```
先看一下提交的历史，确定一下回退到版本的commitID,执行：
git reset --hard commitID
如果现在在本地进行git push origin master的话，会报错，意思大概就是本地代码behind远程仓库的代码，执行下面命令：
git push -u origin master -f
强制把本地代码push到远程仓库。
```

## 2.github高效搜索
[你真的会高效的在GitHub搜索开源项目吗?](https://mp.weixin.qq.com/s?__biz=MzI3MTEwODc5Ng==&mid=2650860167&idx=1&sn=9d3dfd8907a3da595dda38d09c8d68fd&chksm=f1329554c6451c42ffefdaa20af3150a4da0a4f9981e5dee66dda6d289819515f2bf5d08f632&scene=21#wechat_redirect)
