# 搭建过程

> 官方搭建 HarmonyOS 编译环境使用的是 Ubuntu 操作系统，
> 不过因为 Ubuntu 系统本身安装时自带了很多用不上的程序，不够简洁，
> 因此尝试使用更加简洁的 Archlinux 操作系统搭建编译环境。

Archlinux 系统的安装在此处不做赘述，
可以在 Archlinux 的官方网站或在各种博客中找到安装方法。

Archlinux 官方网站为 <https://archlinux.org/>

HarmonyOS 编译环境搭建官方教程为 <https://device.harmonyos.com/cn/docs/documentation/guide/guide-description-0000001054913231>

小熊派开源社区也有编译环境搭建教程可以参考，为 <https://gitee.com/bearpi/bearpi-hm_nano>

下面我将介绍如何在 Archlinux 中搭建编译环境

## 安装基础编译工具

使用包管理器安装 base-devel

其中包含了 gcc 以及 make 等基础编译工具

```shell
sudo pacman -S base-devel
```

## 安装 Python 环境

使用包管理器安装 Python 与 pip 包管理器

```shell
sudo pacman -S python python-pip
```

可以将 pip 源切换至清华或中科大源以加速 pip 包的下载

安装完成后需要安装一些 pip 包

- 安装 kconfiglib 与 pycryptodome

```shell
sudo pip install kconfiglib pycryptodome
```

- 安装 six 与 ecdsa

```shell
sudo pacman -S python-six python-ecdsa
```

## 安装 Scons

使用包管理器安装 Scons

```shell
sudo pacman -S scons
```

安装完成后可使用`scons --version`查看是否安装成功

## 安装交叉编译工具

需要的编译工具有 gn 与 ninja 以及 gcc_riscv32

三种工具的功能简介与下载地址如下表

|工具|主要功能|下载地址|
|:--:|:------:|:------:|
|gn\(generate ninja\)|类似 Makefile 的构建文件|[gn 华为云下载](https://repo.huaweicloud.com/harmonyos/compiler/gn/1523/linux/gn.1523.tar)|
|ninja|类似 make 的工程构建工具|[ninja 华为云下载](https://repo.huaweicloud.com/harmonyos/compiler/ninja/1.9.0/linux/ninja.1.9.0.tar)|
|gcc_riscv32|交叉编译器|[gcc_riscv32 华为云下载](https://repo.huaweicloud.com/harmonyos/compiler/gcc_riscv32/7.3.0/linux/gcc_riscv32-linux-7.3.0.tar.gz)|

- 安装 gn 与 ninja

在 Archlinux 中可以直接使用包管理器安装

```shell
sudo pacman -S gn ninja
```

- 安装 gcc_riscv32

使用上面的网站下载 gcc_riscv32 压缩包，
然后解压到一定位置并将该位置下的`bin/`目录添加到`$PATH`变量中

```shell
wget https://repo.huaweicloud.com/harmonyos/compiler/gcc_riscv32/7.3.0/linux/gcc_riscv32-linux-7.3.0.tar.gz
tar xvf gcc_riscv32-linux-7.3.0.tar.gz -C ~/
echo "export PATH=\$PATH:~/gcc_riscv32/bin" >> ~/.bashrc
source .bashrc
```

完成上述步骤后可使用`gn --version` `ninja --version` `riscv32-unknown-elf-gcc -v`
命令查看是否安装成功

> 在 AUR 中有 riscv-gnu-toolchain 包含有了许多交叉编译工具，
> 但在我的使用中发现编译 HarmonyOS 源码时会出现编译错误，
> 因此在此处依然使用官方提供的交叉编译器
