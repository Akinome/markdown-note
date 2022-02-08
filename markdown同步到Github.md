# Markdown同步到Github

## 1.安装git

[Git官网](https://git-scm.com/)

[Git菜鸟教程](https://www.runoob.com/git/git-status.html)

## 2.Github部分

### 新建库

![](https://s4.ax1x.com/2022/02/08/H31mTI.png)

### 新建 SSH 密钥

命令行输入下方命令创建key

```
ssh-keygen -o
```

在路径里找到 id\_rsa.pub 这个文件打开并复制到 github 里面新建key

![](https://s4.ax1x.com/2022/02/08/H31Zmd.png)Github打开 SSH 方式

Github 上打开 settings 找到 SSH and GPG keys 选项

## 3.新建文件夹

有文件夹后，右键文件夹选择 Git Bash Here 在 bash 中打开，如何没有此选项请检查 Git 是否安装正确

![](https://s4.ax1x.com/2022/02/08/H31e0A.png)

## 上传操作

### 链接 Gitbub 库

在 bash 中输入

```
git clone 此处替换Github库的SSH地址
```

### 本地设置账户

在 bash 中输入

```
git config --global user.email "you@example.com"  
git config --global user.name "Your Name"
```

或者在隐藏的 .git 文件夹中的 config 文件里加入下面的代码

```
[user]
 
name = XXX(自己的名称)
 
email = XXXX(邮箱)
```

[详细文章](https://blog.csdn.net/qq_46036214/article/details/116275598)

### 开始上传

按顺序输入执行以下命令

```
git status
git add .
git commit -m "add fiels"
git push 
```

我们分别解释一下这四条命令:

git status 命令用于查看在你上次提交之后是否有对文件进行再次修改。

git add . 表示把本地修改的文件都添加到本地git仓库管理列表,“"表示所有文件。

git commit -m "add fiels”表示将刚才添加或修改的文件提交到本地仓库，“-m"表示后面的双引号内是注释，注释内容可

以根据自己的需要填写。

git push origin master ,

表示将本地的代码推送到github的远端仓库，origin表示当前目录绑定的远端仓库，master表示推

送到github仓库的哪个分支，我们没有建分支，所以默认写master；origin也可以使用刚才从仓库文件页负责的仓库地址替代，

如：

git push <https://github.com/xxx/markdown.git> master

平时我们对markdown文件有修改时，在修改完成，可以重复执行以上后三条命令提交文件。
