---
title: linux总结的常用指令
date: 2018-03-09 10:32:43
tags: 
- linux
- terminal
thumbnail: /images/Pic_linux.png
---
文件,文件夹操作相关
-----------------------
1. 移动、重命名等
```mv```   **eg:** *mv a.js b.js*
```cp -r 源文件夹名 备份文件夹名``` 拷贝文件 -r代表拷贝文件夹及其内部文件树 
```sz``` 下载文件
```rz``` 上传

2. 查看
  + ```ls```  查看文件
  + ```ls | wc```  查看文件数
  + ```ll```  查看文件详细信息
  + ```less``` 查看文件，支持前后翻阅文件
  + ```more``` 以百分比查看日志
  + ```cat``` 显示整个文件
  + ```cat name1 > name2``` 将两个文件合并查看
  + ```tail -f -100```  *-f* 实时刷新 *-100* 查看最近100行
  + ```pwd``` 查看当前目录的路径
  + ```du -sm``` 查看文件大小
  
3. 查找
```find [-type f] [-iname] "filename*"``` 全局搜索文件 *-type f* 只搜索文件 *-iname* 指模糊搜索
```find .|xargs grep -ri "搜索内容"``` -l
``` man find``` find的详细信息

4. 文件[夹]生成与删除
```rm [-rf]``` 删除指定目录，*-r* 会删除所有该目录下的自文件和文件夹，*-f* 在删除时取消提问
```mkdir [-p]``` 生成目录,*-p* 会自动生成中间文件夹
```rmdir [-p]``` 删除目录 ，*-p* 会删除中间文件夹

5. 编辑文件
  ```vi[m]``` 打开vim编辑器 
      + a 键     －－  后插入
      + i 键     －－  前插入
      + dd (按双下d键)   －－  删除一行
      + x 键     －－  删除当前字母
      + :q! (命令)     －－  无保存退出
      + :wq (命令)  －－  保存后退出
      + ESC 键  －－     切换编辑模式和命令模式

  ```nano``` 打开nano编辑器
6. 压缩文件
```.zip```,```.tar```,```.tgz``` 解压，解包 
```tar -zcvf folder.tar.gz folder/``` 压缩文件夹
```tar[unzip] -zxvf folder.tar.gz ```  解压压缩文件


操作系统相关
-----------------------
1. ```init 6```  重启服务器
2. ```passwd``` 修改密码
3. ```ps [-auxf] [-ef]``` 查看进程 *-ef* 查看server进程
4. ```pstree``` 树形结构显示进程
5. ```free``` 查看磁盘空间使用情况
6. ```fdisk -l``` 查看磁盘分区情况
7. ```hostname``` 查看hostname
8. ```ifconfig``` 查看主机ip
9. ```lsof -i:{port}``` 查看监听端口的进程
9. ```sudo chown -R {username} /path/to/repo/``` 给用户添加写文件的权限

软件相关
-----------------------
### nginx
1. ```sudo systemctl restart nginx``` --
   ```sudo service nginx restart``` --
   ```sudo /etc/init.d/nginx restart```  --- older ubuntu  重启nginx（启动start，停止stop，其他类似）
   ```sudo nginx -s reload``` mac重启nginx
   ```sudo nginx -t``` 检查nginx config配置是否正确

### hexo
1. ```hexo clean && hexo g && hexo d```  hexo博客编译及部署

### git
1. ```git status``` 查看当前状态
2. ```git add -A``` 添加所有的文件到代操作文件中
3. ```git commit -m``` "message desc" 提交
4. ```git push``` 推送到github
5. ```git subtree push --prefix=dist origin gh-pages``` 提交发布版本到github的展示服务器上
6. ```git config --global http[s].proxy socks5://127.0.0.1:1086``` git数据从shadowsocks途径下载
7. ```git checkout -b bugfix/XXX``` 切换分支，-b的作用是新建分支
8. ```git reset --hard logHash``` 回滚git的提交
9. 删除分支
    ```git push origin --delete <branch_name[tag_name]>``` 远程
    ```git branch[tag] -d <branch_name[tag_name]>``` 本地
10. ```git show-branch``` 查看本地所有分支 
11. 清除gitinore中忽略的但是已经提交的文件
     ```git ls-files -ci --exclude-standard``` 查看文件
    ```!git ls-files -ci --exclude-standard -z | xargs -0 git rm --cached``` 删除文件 
   ```git config --global alias.clear-gitignore '!git ls-files -ci --exclude-standard -z | xargs -0 git rm --cached'``` 将该命令添加到别名 
12. ```open "$HOME/.gitconfig"``` mac用默认编辑器打开.gitconfig文件
13. ```git config --global http.proxy socks5://127.0.0.1:{port}```  ```git config --global https.proxy socks5://127.0.0.1:{port} ``` git设置shadowsocks代理
```git config --global --unset http.proxy``` ```git config --global --unset https.proxy``` 重置设置
14. ```git branch --merged | egrep -v "(^\*|master|dev)" | xargs git branch -d``` 删除已经合并到develop和master的分支
15. ```git config core.ignorecase false``` windows,mac默认git不区分大小写，此项修改可以让git区分大小写

### npm | yarn
1. ```npm config set registry https://registry.npm.taobao.org``` 设置淘宝npm镜像
2. ```yarn unlink  => yarn install --check-files``` unlink所有npm包并重新安装依赖
3. ```nvm npm_mirror https://npm.taobao.org/mirrors/npm/``` nvm安装npm设置代理

### mac
1. ```ALL_PROXY=socks5://127.0.0.1:{port} brew upgrade``` homebrew走shadowsocks代理


### docker
1. ```docker ps``` 查看活跃的docker镜像
2. ```docker exec -it {id} /bin/sh/``` 进入某个ID的docker镜像
3. ```RUN echo 'deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse' >      /etc/apt/sources.list ``` =>
```RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 40976EAF437D05B5 && \
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys``` unbuntu下载使用阿里云