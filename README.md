# Handy Note

## DB

Use navicat11 client to connect localhost mysql database and get 
`Client does not support authentication protocol requested by server; consider upgrading MySQL client`

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'newpass';
```

## IDE

idea2018 active code

```
http://idea.lanyus.com/
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

## linux

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

## gitlab

- [install-on-ubuntu](https://about.gitlab.com/installation/#ubuntu)
