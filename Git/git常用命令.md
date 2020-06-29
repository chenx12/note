## git常用命令

### git项目创建

1. 创建工作目录
2. git配置
3. git init初始化成git项目
4. 添加.gitignore文件 *文件更新不会被git感知*
5. 添加README.md文件 对项目进行介绍

### git开发流程

1. 建立个人分支
2. 文件操作（增删改）
3. 查看状态 `git status`
4. 添加到暂存区 `git add`
5. 提交到本地仓库 `git commit`
6. 推送到远端 `git push`

#### 1.git config

- 查看配置项 `git config --list`  
  在根目录下 `/--global`查看全局配置  
  项目目录下 `/--local`查看项目单独配置  
- 设置全局某一配置项 `git config --global Configuration 'value'`  
  去掉`global`或使用`--local`可以设置当前仓库的配置
- 给命令设置别名 `git config --global alias.aliasName command`

config优先级 local>global>system

#### 2.git clone
- 克隆远程仓库master分支 `git clone url`
- 克隆指定分支 `git clone -b branchName url` 

#### 3.git tag
- 查看所有标签 `git tag`
- 添加标签 `git tag -a tagName -m 'msg'`  
  *信息一般可以与标签名相同*
- 查找指定内容 `git tag -l 'content'`  
  *可以使用\*通配符*
- 向以往提交的版本打标签 `git tag -a tagName uuid -m 'msg'`

#### 4.git log
- 查看提交记录 git log  
  `--pretty=oneline` 将查看记录在一行展示
- `--oneline` 展示简略id 
- `|grep 'content'` 过滤指定内容

#### 5.git add
- 将文件添加到暂存区 `git add fileName`
- 提交全部不在暂存区的文件 `git add -A` 或 `git add .`
- 把当前文件夹创建成git可管理的仓库 `git init`
- 查看修改状态 `git status`

#### 6.git diff
- 查看工作区与本地版本库最新版本的区别 `git diff`
- 查看暂存区与最新版本区别 `git diff --stage` 

#### 7.git commit
将改动提交到本地的版本仓库 `git commit -m 'message'`  
message一般是header.格式:type(scope): subject
- type类型（必选）：
  - feat：新功能（feature）
  - fix：修补bug
  - docs：文档（documentation）
  - style： 格式（不影响代码运行的变动）
  - refactor：重构（即不是新增功能，也不是修改bug的代码变动）
  - test：增加测试
  - chore：构建过程或辅助工具的变动
  - perf: 优化相关，比如提升性能、体验
- scope 模块名（可选）
- subject 描述信息（必选）

#### 8.git branch
- 查看分支 `git branch`  
  *表示当前分支
- 创建一个新的分支 `git branch branchName`
- 切换分支 `git checkout branchName`
- 创建新分支并切换到这个分支 `git checkout -b branchName` *常用*
- 删除分支 `git branch -d branchName`
- 分支合并 `git merge` 提交的分支名或已将拉取的远程仓库更新到本地  
  切换到要提交的分支后更新到本地仓库
- 拉取远程仓库 `git fetch` *不更新到本地*
- 拉取远程仓库并更新到本地 `git pull`
- 推送到远端分支 `git push origin branchName` *origin默认连接库分支名*
- 强制提交覆盖 `git push origin branchName--force` *无法恢复 少用*
- 删除远端分支 `git push -d branchName`
- 推送标签 `git push --tag` *可以多个标签添加后同时推送到远端*

#### 9.git remote
- 查看已经存在的远程分支 `git remote`
- 显示分支的分支名/远程地址 `git remote -v`
- 将本地仓库跟远程仓库连接 `git remote add origin url`
- 删除远程仓库连接 `git remote remove origin`
- 分支合并`git rebase`

##### Merge和rebase区别
Merge合并后保留两个分支的记录并出现合并后的分支；解决冲突后需要手动git add、git commit生成提交；一次性解决之前提交的所有冲突

#### 10.git撤销和回滚
- Rebase 展示合并后的记录，合并后生成新的提交的副本；  
  解决冲突后自动生成新的提交；  
  只能单次解决冲突，多次解决需要重复操作
- 修改一项冲突后需要使用`git rebase --continue`显示下一个冲突
- 将未存入暂存区的文件撤销 `git checkout -- fileName`  
  对所有将未存入暂存区的文件撤销 `git checkout -- .`
- 将已存入暂存区的文件撤销到未添加暂存区的状态 git reset HEAD fileName  
将所有已存入暂存区的撤销到未添加暂存区的状态 git reset HEAD
- 撤销已经提交到远端的提交 git revert id  
  id是提交id revert已经revert的提交会恢复提交
- 回滚 git reset --hard 提交id 
  回滚到提交id对应的提交 后面的提交都失效 无法恢复
- 储藏工作中的变更 git stash *切换分支但是不想提交当前工作*  
  恢复变更 git stash pop
