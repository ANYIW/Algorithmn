# Git结合Github

## 1.1 创建远程库地址别名

~~~
git remote -v                #查看远程地址别名
git remote add 别名 远程地址  #为远程地址创建别名
git remote add origin https://xx
git remote rm 别名           #移除别名
git remote rename 旧名 新名   #重命名
~~~

## 1.2 本地推送到远程

- 前提：
- commit 提交到了本地库
- 是远程库的团队成员

~~~
git push 别名 分支名
git push origin master

git push -u 别名 分支名  #-u指定默认主机
~~~

## 1.3 远程克隆到本地
~~~
git clone 远程地址
git clone https://xx
~~~

## 1.4 拉取远程的修改

```
git fetch 别名 分支名  #本地还没有改变
git merge 别名 分支名  #本地和远程统一

pull = fetch + merge
git pull 别名 分支名   #一气呵成
```

## 1.5 解决冲突
- **团队成员**基于**最新版**做出修改
- 不是基于远程库最新版做的修改不能推送，必须先 pull，若有冲突手动解决
- 解决冲突后的提交不能带文件名

## 1.6 团队内部合作
- 邀请成员
`Settings` --> `Collaborators` --> `填写用户名` --> `邀请链接`
- 团队成员可 clone、**push**

## 1.7 跨团队合作
- 贡献开源代码

    `将A的远程库 fork 到B的远程库` --> `B将其clone到本地，修改后 push 到B的远程库`  --> `B点击 pull request` --> `Create pull request 发消息` --> `A merge pull`