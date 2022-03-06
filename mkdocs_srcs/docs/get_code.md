# 获取源码

获取源码的方式主要有两种，一种是通过华为自己的包管理器 hpm 获得，
另一种是通过 Gitee 仓库获得

## 使用 hpm 获得源码

### 下载 Node.js

首先下载 Node.js 以及其包管理器 npm，
可以参考官方网站 <https://nodejs.org/en/> 的下载方式或直接从包管理器获得

```
sudo pacman -S nodejs npm
```

下载完成后可使用`node --version` `npm --version`查看是否下载成功

### 下载 hpm

使用 npm 下载 hpm

```
npm install -g @ohos/hpm-cli
```

下载完成后可使用`hpm -V`查看是否下载成功，注意此处`-V`为大写字母

### 使用 hpm 命令获取源码

进入一定开发目录，执行以下命令初始化一个工程

```
hpm init -t default
```

然后执行以下命令下载小熊派组件

```
hpm install @bearpi/bearpi_hm_nano
```

下载完成后会提示 Install successfully!

### 使用 hpm 编译源码

执行以下命令编译源码

```
hpm dist
```

## 使用 Gitee 仓库获取源码

### 下载 git

首先下载 git 工具

```
sudo pacman -S git
```

### 克隆源码仓库
    
使用 git 工具克隆 HarmonyOS 源码仓库
    
```
git clone https://gitee.com/bearpi/bearpi-hm_nano.git -b master
```

### 使用 python 脚本编译源码

执行以下命令编译源码

```
python build.py BearPi-HM_Nano
```
