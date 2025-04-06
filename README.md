### 压缩与解压

#### 压缩

```
tar -cvzf MusicParty_0.1.tar MusicPartyBak/
tar -cvzf MusicParty_0.2.tar MusicParty/
tar -cvzf MusicParty_0.3.tar MusicParty/
```

解压

```
// linux
tar -xvzf MusicParty_0.2.tar -C ./
// windows
tar -xvzf MusicParty_0.2.tar -C .\
```



### docker镜像制作

分别是网易音乐api、qq音乐api、后端、前端

```
docker build -t musicparty-neteaseapi:latest --file Dockerfile-neteaseapi .
docker build -t musicparty-qqmusicapi:latest --file Dockerfile-qqmusicapi .
docker build -t musicparty-backend:latest --file Dockerfile-backend .
docker build -t musicparty-frontend:latest --file Dockerfile-frontend .
```

```
删除悬空标签REPOSITORY和TAG都是<none>的镜像
docker image prune
```

合并为一条指令

```
docker build -t musicparty-frontend:latest --file Dockerfile-frontend . && docker build -t musicparty-backend:latest --file Dockerfile-backend . && docker build -t musicparty-neteaseapi:latest --file Dockerfile-neteaseapi . && docker build -t musicparty-qqmusicapi:latest --file Dockerfile-qqmusicapi . && docker image prune
```

注意，没有安装nodejs与npm是构建不了的，会有报错
安装nodejs与npm，正常安装nodejs会自带npm，若没有则手动安装一下
```
sudo apt install -y nodejs
sudo apt install -y npm
```
推荐的nodejs安装方式
```
# 添加 NodeSource 官方源（以 Node.js 20.x 为例）
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
# 安装 Node.js 和 npm
sudo apt install -y nodejs
```




### 版本说明

#### MusicParty_0.1.tar

此版本是修改原项目后，第一个稳定使用的版本

修改的地方：

- 修复了b站无法使用（修改了两个过时的api）
- 添加了音量控件



#### MusicParty_0.2.tar

修改的地方：

- 使用 localStorage 来持久化音量设置（这样即使页面刷新后，音量值也能够保持
- 添加封面图片（只添加了网易音乐与B站的，qq的直接返回的空
- 修改原音乐进度`13/362`为`00:13 / 06:02`



#### MusicParty_0.3.tar

由[Yamds](https://github.com/Yamds)修改，代码改动不详

目前观察到的改动：

- 增加了循环模式
- 增加了列表歌曲删除按钮
- 修改了歌名与封面的文件位置，用来适配手机



小问题：

- ~~切歌失效（已修复）~~
- https://github.com/Yamds/MusicParty/tree/main/music-party中的MusicParty/music-party/package.json 第8行的 -p 4000要删掉，不然docker-compose的端口不起作用







### 小工具

#### 正则替换

**目的**
保留每行开头`"`和`\MusicParty`及其后面的文本

查找目标

```
^"([^"]*\\MusicParty)
```

替换

```
"\1
```









