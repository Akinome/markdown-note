# Git常用命令

## master和main的切换

```PowerShell
git config --global init.defaultBranch master|main
```

#### 以上方法只是让以后创建的项目默认分支为main, 但对于已经创建的项目则无能为力, 所以我们还需要对已存在的项目逐个进行修改.

> 配置文件一般在用户目录下的.gitconfig文件中, 可以使用文本编辑器打开进行修改, 也可以使用git命令进行修改上面也是使用git命令修改的

## 修改已创建项目的主分支为main
```PowerShell
git branch -M main
```

#### 使用git branch -M main命令, 把当前master分支改名为main, 其中-M的意思是移动或者重命名当前分支

## 修改远程仓库的主分支为main
```PowerShell
git push -u origin main
```

#### 使用git push -u origin main命令, 把本地的main分支推送到远程仓库origin上, 并建立追踪关系, 也就是把本地的main分支和远程的main分支关联起来

[把git的默认分支master修改成main](https://zhuanlan.zhihu.com/p/455988463)

## 删除远程仓库的master分支
```PowerShell
git push origin --delete master
```

#### 使用git push origin --delete master命令, 删除远程仓库origin上的master分支

## 修改远程仓库的默认分支为main
```PowerShell
git push --delete origin master
git push --set-upstream origin main
```

> 使用git push --delete origin master命令, 删除远程仓库origin上的master分支, 然后使用git push --set-upstream origin main命令, 把本地的main分支推送到远程仓库origin上, 并建立追踪关系, 也就是把本地的main分支和远程的main分支关联起来

## Git常用命令

"git clone" 命令 克隆远程仓库

```PowerShell
git clone <URL>
```

"git pull" 命令 拉取远程仓库的更新

```PowerShell
git pull
```

```PowerShell
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
```

"git config" 命令 创建用户名配置

```PowerShell
git config --global user,name <name>
git config --global user.email <email>
//  示例 名字有空格加""
git config --global user,name Akinome
git config --global user.email ziecen233@gmail.com
```

"git init" 命令 初始化文件夹，生成 .git 文件夹

```PowerShell
git init
//  git 配置 --全局 初始化.默认分支 <名称>
git config --global init.defaultBranch <name>
```

"git status" 命令 查看当前状态

```PowerShell
git status
```

## Git工作流

![git工作流示意图](https://gitee.com/akime/markdown-note/raw/main/img/wch2sk.png)

"git add" 命令 将文件添加到暂存区并追踪(stage)

```PowerShell
git add <file name.txt>
```

"git commit" 命令 将文件提交到本地仓库

```PowerShell
git commit
//  常用组合
git commit -a -m <message commit>   // -a(add) -m(message)
git commit -am <message commit>     // -am(-a + -m)
```

"git branch" 命令 创建,删除和查看分支

```PowerShell
//  创建分支
git branch <branch name>
//  删除分支
git branch -d <branch name>
//  查看分支
git branch
```

"git checkout" 命令 切换分支

```PowerShell
git checkout <branch>
//  创建并切换分支
git checkout -b <branch>
```

"git merge" 命令 把别的分支合并到当前所处的分支上

```PowerShell
git merge <branch name>
```

"git remote" 命令 查看本地仓库和远程仓库的联系

```PowerShell
//  配置推送地址
git remote add <name> <URL>
//  查看本地仓库和哪些远程仓库有联系
git remote -v
//  删除远程仓库
git remote rm <name>
//  修改远程仓库的地址
git remote set-url <name> <URL>
```

"git push" 命令 将本地仓库推送到远程仓库

2021年起，GitHub不支持账号密码登录，要通过token登录

```PowerShell
"git fetch" 命令 拉取远程仓库的更新

"git diff" 查看远程仓库和本地仓库的差异
```

# 以下是通过SSH方式连接远程仓库（新版本）
## 1. 生成SSH密钥对

```PowerShell
ssh-keygen -t rsa -C "your_email@example.com"
//  简单命令，生成密钥对后，选择是否输入密钥，默认会保存在
//   ~/.ssh/ 目录下
```

## 2. 添加SSH密钥到ssh-agent（第一次默认配置好）

```PowerShell
eval "$(ssh-agent -s)"
//  启动并启动 SSH 代理（ssh-agent）
ssh-add ~/.ssh/id_rsa
//  将指定的 SSH 私钥添加到已启动的 SSH 代理中
```

## 3. 添加SSH密钥到GitHub
通过网页Github的个人设置里添加

```PowerShell
cat ~/.ssh/id_rsa.pub //  查看公钥内容
```

## 4. 添加远程仓库

```PowerShell
git remote add origin git@github.com:username/repo.git
// 直接使用
git remote add [项目名] [SSH地址]
```

# 更改SSH的端口号，避免特殊网络环境无法使用的问题如PAC代理等
ssh默认端口号：22  
测试使用命令： telnet github.com 22  
在.ssh文件夹内新建一个config文件，并添加以下内容

```PowerShell
Host github.com
  Hostname ssh.github.com  # 关键地址
  Port 443                 # 使用HTTPS备用端口
  User git  # 指定用户名 git GitHub 的 SSH 服务要求所有用户以 git 作为用户名连接
  IdentityFile ~/.ssh/id_ed25519  # 指定密钥路径（可选）
```