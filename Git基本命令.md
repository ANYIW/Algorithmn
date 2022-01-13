# Git简介
**托管中心**`维护远程库`

- 内网：自己搭建一个GitLab服务器
- 外网：码云、Github

**版本控制工具**

- 集中式：CSV ，**SVN**，VSS
- 分布式：**Git**，Darcs，...
- 分布式相较于集中式，避免了单点故障

# Git命令行操作
## 1.1 本地库初始化

* 进入文件夹
* `git init`
* 生成的 .git 目录是隐藏的，其中存放本地库相关文件

## 1.2 设置签名
* 仅用于区别不同开发人员身份
* 就近原则：有仓库级别，优先使用仓库级别
* 不允许二者都无

项目(仓库)级别：仅在当前本地库有效
  ```
  git config user.name anyi          #设置用户名anyi
  git config user.email anyi@qq.com  #设置用户邮箱
  ```
查看保存位置
 ```
 cat .git/config  #信息保存在git/config文件
 ```

系统用户级别：仅在当前登录的操作系统有效
  ```
  git config --global user.name anyi
  git config --global user.email anyi@qq.com
  ```
查看保存位置
  ```
  cat ~/.gitconfig  #家目录/c/users/asus下
  ```
- 补充
  ```
  git原理：哈希
  pwd   #显示当前所在目录
  cd ~  #跳转到家目录/c/users/asus
  cd -  #跳转回上级目录
  ```
  ***
## 1.3 基本操作
- 补充
  ```
  CR：Carriage Return，\r，回车
  CRLF：Carriage Return & Linefeed，\r\n，回车并换行

  空格：下一页
  b：上一页
  q：退出

  左键选中会自动复制，中键粘贴
  复制：CTRL+INSERT
  粘贴：SHIFT+INSERT
  清屏：CTRL+L

  ```
***
### 1.3.1 状态查看

```
git status  #查看工作区、暂存区状态
```

### 1.3.2 工作区到暂存区
```
git add fileName          #指定文件
git add .                 #所有文件
git rm --cached fileName  #撤销添加
```

### 1.3.3 暂存区到本地库
法一：进入Vim编辑器

 ```
 git commit fileName    #指定文件
 :set nu                #Vim下显示行号，number
 按i：编辑模式，insert
 输入本次提交的消息
 按ESC：退出编辑
 :wq                    #编辑退出
 ```
法二：不进入Vim编辑器

 ```
 git commit -m "commit message" fileName  #指定文件
 git commit -m "commit message" .         #所有文件
 ```
### 1.3.4 查看历史记录

```
git log                   #详细
git reflog                #HEAD@{移动到当前版本需要多少步}
git log --greph           #图形显示,更直观
git log --pretty=oneline  #一行行显示完整Harsh
git log --oneline         #显示部分Harsh
```

### 1.3.5 版本前进后退

法一：基于索引值`可进可退`

  ```
  git reset --hard a6ace91 (reflog 下 Harsh 的一部分)
  ```

法二：使用 **^** 符号`只能后退`

  ```
  git reset --hard HEAD^  #几个 ^ 表示后退几步
  ```

法三：使用 **~** 符号`只能后退`

  ```
  git reset --hard HEAD~n  #后退n步
  ```

### 1.3.6 reset的三个参数比较

```
HEAD指针只在本地库内移动

soft: 
  - 仅本地库移动HEAD指针
mixed:
  - 在本地库移动HEAD指针
  - 重置暂存区
hard:
  - 在本地库移动HEAD指针
  - 重置暂存区
  - 重置工作区
```

### 1.3.7 删除文件并找
~~~
git reset --hard 历史位置  #删除已commit
git reset --hard HEAD     #删除未commit
~~~

### 1.3.8 文件差异比较

```
git diff 文件名        #工作区和暂存区比较
git diff 哈希值 文件名  #工作区和某个历史版本比较
git diff               #分别列出多个文件自身差异
```
---
## 2.1 分支管理

### 2.1.1 什么是分支管理

![](image\分支.png)

### 2.1.2 分支的好处

- 同时并行推进多个功能开发，提高效率
- 某一分支开发失败，不会对其它分支有任何影响
---
### 2.1.3 分支操作

创建分支

~~~
git branch 分支名
~~~

查看分支

~~~
git branch
git branch -v 
~~~

切换分支

~~~
git checkout 分支名
git checkout -b 分支名   #创建分支并直接切换到该分支
~~~

合并分支`把修改了的文件拉取过来`

~~~
git checkout a  #先切换到被合并的分支
git merge b     #将b分支并入a分支
~~~

删除分支

~~~
git branch -d 分支名
~~~
---
### 2.1.4 解决冲突

冲突的表现

![](image\冲突.png)

冲突的解决
1. 编辑，删除特殊标记`<<<` `===` `>>>`
2. 修改到满意为止，保存退出
3. 添加到缓存区 `git  add 文件名`
4. 提交到本地库 `git commit -m "日志信息" ` `不能带文件名`