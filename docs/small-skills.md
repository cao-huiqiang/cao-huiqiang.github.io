# 星星点点

## Dbeaver快捷键

按键组合|功能
:---|:---
Ctrl + D|删除当前行
Ctrl + Shift + ↑/↓ |向上/向下移动当前行  
Ctrl + Alt + ↑/↓|向上/向下复制当前行
Ctrl + Shift + F|SQL格式化
Alt + Shift + A | 多行编辑

## redis常用命令

作用|命令
:---|:---
选择数据库|select 1
设值|set key value
hash设值|hset key hkey hvalue
取值|get key
hash取值|hget key hkey

### redis设置密码
```shell script
# 查看密码
> config get requirepass
# 设置密码
> config set requirepass password
# 登录
> auth password
# 再次查看密码
> config get requirepass
```

### redis修改配置文件
```shell script
# 运行中的redis修改redis.conf配置后，再次启动未生效
> redis-server ./redis.conf
# 需要shutdown后再启动 
> redis-cli shutdown 
> redis-server ./redis.conf
```

## git

### Git global setup
```shell script
git config --global user.name "username"
git config --global user.email "exmpale@163.com"
```

### Create a new repository
```shell script
git clone https://example.git
cd example
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

### Push an existing folder
```shell script
cd existing_folder
git init
git remote add origin https://example.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

### Push an existing Git repository
```shell script
cd existing_repo
git remote rename origin old-origin
git remote add origin https://example.git
git push -u origin --all
git push -u origin --tags
```
只显示了master分支，其他分支没有。

### git迁移仓库地址（保留分支和历史提交）

1. 先克隆老项目的镜像  (old.git 为老项目的git地址)  
```git clone --mirror old.git```
2. 进入老项目的目录  
```cd old.git```
3. 移除老项目的地址替换成新项目git地址 (new.git)  
```git remote set-url --push origin  new.git ```
4. 将镜像推到远程  
```git push --mirror```  

[qtl_crazy的CSDN博客地址](https://blog.csdn.net/qtl_crazy/article/details/81019097)


### git 仓库合并文档查找
https://dev.to/nabbisen/git-merging-repositories-with-local-clones-81m
https://www.cnblogs.com/arnoldlu/p/11130600.html
https://majing.io/posts/10000053151232

查看所有分支
git branch -a

git提交空文件夹
文件夹中新建.gitkeep空文件

https://dev.mysql.com/doc/refman/8.0/en/declare-handler.html  
https://dev.mysql.com/doc/mysql-errors/8.0/en/server-error-reference.html

GNU nano 4.8

### git仓库合并操作
```shell script

git clone https://all.git
cd enquiry-merge/
mkdir common
cd common/
touch .gitkeep
git add .
git commit -m 'add blank directory common'
git push
git remote add common https://common.git
git fetch common
git merge -X subtree=common common/master --allow-unrelated-histories
git push origin master

git checkout -b dev
mkdir common
cd common/
touch .gitkeep
git add .
git commit -m 'add blank directory common'
git push --set-upstream origin dev
git merge -X subtree=common common/dev --allow-unrelated-histories
git push origin dev

git checkout master
```


## windows

> 查看端口进程
```shell script
netstat -aon|findstr "8080"
```

>引入子项目的两种方式  

1. 打开父pom， 修改父pom
2. 打开父pom所在文件夹

## ubuntu20.04

>安装fctix-googlepinyin，reboot后，未显示
> ==> 在设置中，添加输入法后，卡死
> ==> 强制重启
> ==> 登录后黑屏

```shell script
# ctrl + alt + f2 进入ttf
> im-config
# 发现 ~/.xinputrc,
> vim ~/.xinputrc;
:xrun_im fcitx
# 注释掉:xrun_im fcitx
> reboot
# 登录后恢复正常
```

## appimagelauncher
```shell script
# 安装与卸载
> ./appimagelauncher-lite-2.1.4-travis987-7cb4d70-x86_64.AppImage install
> ./appimagelauncher-lite-2.1.4-travis987-7cb4d70-x86_64.AppImage uninstall
# appimagelauncher安装后把下载的.AppImage文件放在launcher扫描文件夹
# 
```

## mongodb

### mongodb 安装 与 连接

```shell script
## 下载tgz安装包
sudo apt-get install libcurl4 openssl liblzma5
tar -zxvf mongodb-linux-*-4.4.1.tgz
sudo cp <mongodb-install-directory>/bin/* /usr/local/bin/
sudo mkdir -p /var/lib/mongo
sudo mkdir -p /var/log/mongodb
sudo chown `whoami` /var/lib/mongo     # Or substitute another user
sudo chown `whoami` /var/log/mongodb   # Or substitute another user
# 启动 -- 后台运行
mongod --dbpath /var/lib/mongo --logpath /var/log/mongodb/mongod.log --fork
# 连接
mongo
# 使用配置文件
mongod --config /etc/mongod.conf

# 绑定所有ip
mongod --bind_ip 0.0.0.0 
# 绑定多个ip
mongod --bind_ip 127.0.0.1,10.64.226.180

# 启动：
./mongod -f ../etc/mongo.conf
# 关闭:
./mongod -f ../etc/mongo.conf --shutdown
# -f 和 --config 等效

mongod --dbpath /var/lib/mongo --logpath /var/log/mongodb/mongod.log --bind_ip 127.0.0.1,192.168.1.180 --fork

mongod --dbpath /var/lib/mongo --logpath /var/log/mongodb/mongod.log --bind_ip 127.0.0.1,192.168.1.180 --shutdown
```


## window

>mongod.exe --config "C:\Program Files\MongoDB\Server\4.4\bin\mongod.cfg"  
>mongod.exe --config "C:\Program Files\MongoDB\Server\4.4\bin\mongod.cfg" --install  
>net start MongoDB  


[DMS数据库文档](https://www.yuque.com/)



