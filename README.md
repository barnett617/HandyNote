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

### use zsh as the default shell in vscode

1. Open `User Settings` and search `terminal.integrated.shell.osx`

2. Set it to `/bin/zsh`

### use `code` command to open a project with vscode quickly in shell

1. `Command+Shift+P` and search `shell command`

2. Choose `Install 'code' command in PATH`

### preview markdown file real time in vscode

1. `Command+Shift+P` and search `markdown`

2. Choose `Open locked preview to the side`

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

## Terminal

- nslookup 域名相关

### TODO

- [ ] nslookup
