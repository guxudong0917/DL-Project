# Git

> 关于git的学习是必要的，因为只有学好了它，才能优雅的提交维护代码，我之前一直对这一部分一知半解，所以现在决定好好总结一下。

## Git的三个区域

### 工作区
文件修改，新增，删除的地方，Git只是观察，还没开始记录，有untracked(未追踪)和modified两种状态。

### 暂存区
通过`git add 文件名`将文件放到暂存区，是提交前的快照区，可以通过`git add .` 把当前文件的所有文件都放在暂存区，但是这样可能会把一些没必要提交到仓库的文件也交上去，比如数据集，占用大量空间。

### 仓库区repository
相当于档案库，用来存放不同时期提交的档案，每次提交有一次特殊的id，可以根据id回溯。提交方式：`git commit -m“提交说明”`,写好提交说明是非常有必要的！可以写清楚这次更改了什么东西，不然等到需要要回溯的时候就遭罪了。

## 文件的状态流动

用一个形象的流程展示数据在各区域的移动，这是最基础的 Git 使用流程：

1. **在工作区创建 / 修改文件**：你在本地文件夹中编写`test.py`，或修改已有的文件；
2. **将修改添加到暂存区**：执行`git add test.py`，把`test.py`的修改加入暂存区（标记为待提交）；
3. **将暂存区修改提交到本地版本库**：执行`git commit -m "添加test.py文件"`，此时修改被永久保存到本地.git 目录；
4. **将本地版本库提交推送到远程版本库**：执行`git push origin main`，把本地的提交同步到云端（如 GitHub），供他人查看 / 拉取；
5. **从远程版本库拉取最新代码**：执行`git pull origin main`，将云端的最新修改同步到本地，更新工作区和本地版本库。

## gitignore

`.gitignore` 告诉 Git：哪些文件我不想被版本控制，这些文件不会被 `git add .` 加进去。

<aside>
⚠️

.gitignore 只对 未被追踪的文件 生效

</aside>

语法

```
#直接写出忽视的文件
test.py
#忽视一个目录下的所有文件
document/
#忽视特定目录下的某个文件，其他目录下的temp文件不会被忽略
dataset/temp
#用*，匹配任意个字符
*.py

```

在更改gitignore后，需要先把它提交到暂存区，然后git commit，这样之后才会生效

### 如果不小心加错了

**`git rm -r --cached .idea/` 用这条命令去把特定某一文件夹下的文件移除**

## 如何把仓库关联到远程

首先，在github上建立仓库，然后记下远程仓库的地址

`git@github.com](mailto:git@github.com):guxudong0917/DL-Project.git`

### git remote

```
# 格式：git remote add <远程仓库别名> <远程仓库地址>
# 常用别名：origin（默认/推荐，可自定义）
# 远程地址：复制你在远程平台创建仓库后的 HTTPS 或 SSH 地址
```

建立关联
`git remote add origin git@github.com:guxudong0917/DL-Project.git` 

### git push

```
# 格式：git push -u <远程仓库别名> <本地分支名>
# -u：关联本地分支与远程分支，后续推送可直接用 git push（无需重复写别名和分支名）
```