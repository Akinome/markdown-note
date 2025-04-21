# Git常用命令

master和main的切换

```PowerShell
git config --global init.defaultBranch master|main
git branch -M master|main
```

[把git的默认分支master修改成main](https://zhuanlan.zhihu.com/p/455988463)

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

![https://files.catbox.moe/wch2sk.png](https://files.catbox.moe/wch2sk.png)

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
ssh-keygen
```

## 2. 添加SSH密钥到ssh-agent（第一次默认配置好）

```PowerShell
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

## 3. 添加SSH密钥到GitHub
通过网页Github的个人设置里添加

```PowerShell
cat ~/.ssh/id_rsa.pub //  查看公钥
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