# Handy Note

## DB

Use navicat11 client to connect localhost mysql database and get 
`Client does not support authentication protocol requested by server; consider upgrading MySQL client`

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'newpass';
```

## IDE

### idea2018 active code

```
http://idea.lanyus.com/
```

### use zsh as the default shell in 



1. Open `User Settings` and search `terminal.integrated.shell.osx`

2. Set it to `/bin/zsh`

### use `code` command to open a project with vscode quickly in shell

1. `Command+Shift+P` and search `shell command`

2. Choose `Install 'code' command in PATH`

### preview markdown file real time in vscode

1. `Command+Shift+P` and search `markdown`

2. Choose `Open locked preview to the side`

### vscode避免打开新的文件覆盖当前文件

> 因为默认设置是预览文件，需要把预览文件设置为false

```
"workbench.editor.enablePreview": false
```

## Maven 

### 环境变量

```
vim ~/.bash_profile
export M2_HOME=/Users/username/Documents/maven #这里是你maven的路径
export PATH=$PATH:$M2_HOME/bin
source ~/.bash_profile

mvn -v
```

### 插件使用

- [maven-install-plugin](http://maven.apache.org/plugins/maven-install-plugin/usage.html)
- [maven-install-plugin/examples](http://maven.apache.org/plugins/maven-install-plugin/examples/specific-local-repo.html)

### 插件问题

- [maven-plugins-can-not-be-found-in-intellij](https://stackoverflow.com/questions/20496239/maven-plugins-can-not-be-found-in-intellij/27168770)

## Linux

### 查看Linux系统版本

```
lsb_release -a
```
lsb = Linux Standard Base

### CPU使用情况

```
top
```

### CPU信息

```
cat /proc/cpuinfo |more
```

### 查看内存

```
free -m
```

### 查看磁盘

```
df -h
```

```
fdisk -l
```

### 命令解读

#### which&where
- [which & whereis](https://superuser.com/questions/40301/which-whereis-differences)

#### /usr/bin和/usr/local/bin区别
- [/usr/bin & /usr/local/bin](https://unix.stackexchange.com/questions/259231/difference-between-usr-bin-and-usr-local-bin)

## MacOS

### use zsh as the default shell

1. See the shells you already installed with the command

```code
cat /etc/shells
```

2. Set zsh as the default shell

```
chsh -s /usr/local/bin/zsh
```

3. (Optional)If you want to configure zsh mannually, use

```
vim ~/.zshrc
```

4. After change `.zshrc`, do remember to `source` it to make it work

```
source ~/.zshrc
```

5. (Restore default shell)

```
chsh -s /bin/bash
```

### Java默认Home
```
/Library/Java/JavaVirtualMachines
```

## Git

### 初始化git

1. 查看配置

```
git config --list
```

2. 初始化用户和邮箱

```
git config --global user.name "your name"
git config --global user.email your email
```

### 本地生成ssh key并放在远端以实现SSH访问

1. Generate a ssh key locally

```
ssh-keygen -o
```

2. Catch your key just generated before

```
cat ~/.ssh/id_rsa.pub
```

3. Put it into your ssh keys in your romote repository

4. Or copy the local already exist ssh key to clipboard directly(for macOS)

```
pbcopy < ~/.ssh/id_rsa.pub
```

### 解决使用vs code打开从github上git clone下来的项目，修改后并做git remote关联，在git push时每次都要输入账号和密码

#### 存储全局账号

```
git config --global credential.helper wincred
```

### git全局配置用户名，因误操作产生多条配置，导致无法修改

#### 产生背景

使用如下错误命令及参数修改配置

```
git config --global user.name = "M1kewang"
```

首先修改配置项user.name并不需要等号，也不需要引号

这样配置的结果就是产生了两条user.name，如下

```
git config -l

user.name=magi
user.name==
```

即产生了一条user.name值为一个等号的记录

此时再去对user.name这个属性操作即会报错，因为存在两条同属性名的属性，git会混乱，而不知道你要操作的是哪个属性配置

#### 具体报错

```
warning: user.name has multiple values
error: cannot overwrite multiple values with a single value
       Use a regexp, --add or --replace-all to change user.name.
```

#### 解决方案

先看一下git存在哪些配置参数

```
git config
```

发现里面有个`--unset`参数，用于remove一个variable（在git中，配置被当做全局变量被存储，这和MySQL很像）

但是尝试这样修改，并不理想，会提示你要修改的属性存在多条记录

```
warning: user.name has multiple values
```

正确的方法应该是对这个属性进行批量操作，即对所有同名的属性值进行修改

```
git config --global --replace-all user.name M1kewang
```

这样就git会把修改后的两条相同属性合并为一条，恢复正常

### 常用撤销操作

#### 已经add && commit，发现提交错分支

##### 指定版本（指一次push前的多次commit）

###### 查找提交历史

```
git log
```

拷贝`要恢复到`的提交记录ID

![gitlog](./static/images/gitlog.png)

```
git reset [<mode>] [<commit>]
```

mode参数不加，默认为mixed，会将已提交的文件恢复到指定历史版本，并将本地的修改保留，可以重新add进暂存区

```
git reset c9061153d10be3683762c5301ba9afce586935a6
```

![gitreset](./static/images/gitreset.png)

将修改放进临时存储，切换分支，将临时存储中内容倒出

```
git stash
git checkout -b new-branch
git stash pop
```

![gitstash](./static/images/gitstash.png)


##### 撤销最近版本（上次提交 或 上上次）

###### 回到上次提交后的状态（即撤销本次提交commit）

```
git reset HEAD^
```

或

```
git reset HEAD~1
```

此效果等同于通过`git log`找到上一个提交ID，并通过`git reset ID`撤销本次commit，`git reset`只会撤销提交，并且从`git log`中删除，但是在不添加参数，即使用默认参数mixed，则不会撤销本地文件的修改，所以用户可以重新考虑本地提交要如何编辑文件

回到上上次，则为

```
git reset HEAD~2
```

### TODO

- [ ] git revert
- [ ] git rebase

### 项目改变远端仓库地址（相当于转移，比如从github转移到gitlab）

#### 先拉下项目，可以看到git提交记录，查看当前的远程仓库

```
git remote -v
```

#### 修改远程仓库地址

```
git remote set-url origin(远程连接名称) git@47.98.34.171:codemonkeys/cm-server.git(新的远程仓库地址) git@gitee.com:code-monkeys/code-monkeys.git(旧的远程仓库地址)
```

#### 拉取新的远程仓库代码

```
git pull
```

#### 会提示本地拒绝合并未关联的历史提交

```
warning: no common commits
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From 47.98.34.171:codemonkeys/cm-server
 * branch            master     -> FETCH_HEAD
 + 6c61229...1eb4e0e master     -> origin/master  (forced update)
fatal: refusing to merge unrelated histories
```

#### 可添加`--allow-unrelated-histories`参数允许合并未关联的提交记录

```
git pull --allow-unrelated-histories
```

#### 然后会自动合并新的远程仓库和本地的git项目，如果有冲突会提示解决

```
Auto-merging README.md
CONFLICT (add/add): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

#### 提交远程

```
git push origin master
```

![gitremote](./static/images/gitremote.png)

### 本地项目向远端提交报错

![gitfatal](./static/images/gitfatal.png)

#### 情况分析

> 本地git配置的用户名和邮箱与生成ssh-key的邮箱不匹配，导致使用ssh方式推送时，识别到邮箱的不匹配而拒绝访问

#### 解决方案

1. 使用https方式，通过输入远程仓库用户名和密码推送

2. 将本地git邮箱的配置生成ssh-key并添加到远端仓库

3. 修改本地git配置为远程ssh-key中的邮箱

### 使用http方式下载项目失败，提示`Git: fatal: The remote end hung up unexpectedly`

> Maximum size in bytes of the buffer used by smart HTTP transports when POSTing data to the remote system.
For requests larger than this buffer size, HTTP/1.1 and Transfer-Encoding: chunked is used to avoid creating a massive pack file locally. Default is 1 MiB, which is sufficient for most requests.

```
git config --global http.postBuffer 1048576000
```

## Github

### 上传本地项目到github

1. Get into your project folder and `git init`, then a `.git` folder was created.

2. Add your files to git.

```
git add .
```

3. Commit your added files to the stage area.

```
git commit -m "write your comment"
```

4. Link your local git project with your GitHub repository.

```
git remote add origin https://github.com/youraccount/yourrepository.git
```

5. Pull the existed files of your current GitHub repository.

```
git pull origin master
```

6. Fix the conflicts if there exist.

7. Push your local project managed by git to your remote GitHub repository.

```
git push -u origin master
```

8. Done.

## Gitlab

- [install-on-ubuntu](https://about.gitlab.com/installation/#ubuntu)
- [社区版](https://www.cnblogs.com/restran/p/4063880.html)
- [configuring-the-external-url](https://docs.gitlab.com/omnibus/settings/configuration.html#configuring-the-external-url-for-gitlab)

## Terminal

- nslookup 域名相关

### TODO

- [ ] nslookup

## NPM

### 查看某个包的可用版本

```
npm view jquery versions
```

## 浏览器

### Chrome将超链接用新的标签打开

> command + 点击链接
