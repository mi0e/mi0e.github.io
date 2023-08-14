---
layout: post
cid: 81
title: 基于Linux-Anaconda部署AzurLaneAutoScript
slug: 81
date: 2022/04/13 09:59:00
updated: 2022/05/28 11:30:54
status: publish
author: mi0e
categories: 
  - 教程
  - Linux
tags: 
  - linux
  - 碧蓝航线
  - Python
customSummary: 
mathjax: auto
noThumbInfoEmoji: 
noThumbInfoStyle: game
outdatedNotice: no
parseWay: auto
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


# 在 Linux 上部署 AzurLaneAutoScript

## Anaconda相关

### 下载anaconda3

```
wget https://repo.continuum.io/archive/Anaconda3-5.2.0-Linux-x86_64.shanaconda
```

### 修改权限

```
chmod +x Anaconda3-5.2.0-Linux-x86_64.sh
```

### 安装

```
./Anaconda3-5.2.0-Linux-x86_64.sh
# 一路yes&enter
```

## 拉取Alas

移动到欲安装alas目录下，git整个仓库

```
cd /home
git clone https://github.com/LmeSzinc/AzurLaneAutoScript.git
# 如果下载速度缓慢，可换用gitee
```

## 安装依赖

### python环境

```
conda create -n alas python=3.7.6
conda activate alas
cd AzurLaneAutoScript
pip install -r requirements-in.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
# 可换用其他源
```

> 由于某些 python 库在不同 os 下的依赖不同，直接从 requirements-in.txt 安装即可，pip会自动处理依赖。当然也可以从 requirements.txt 安装，但是需注释掉 pywin32

### adb

下载 [SDK Platform Tools for Linux](https://developer.android.com/studio/releases/platform-tools) 并解压，将adb放在`/usr/bin`目录下

### uiautomator2

若运行 alas 后无法正常初始化 uiautomator2，可按此方法手动安装，安装过程参考 [uiautomator2](https://github.com/openatx/uiautomator2)

运行 `adb connect <address>` 连接你的云手机，确保运行 `adb device` 后可以看到设备

在 alas python 环境下运行 `python` 打开 python 命令行窗口，输入以下命令

```
import uiautomator2 as u2

d = u2.connect() # connect to device
print(d.info)
```

等待一段时间，输出类似如下内容，说明安装成功

```
{'currentPackageName': 'net.oneplus.launcher', 'displayHeight': 1920, 'displayRotation': 0, 'displaySizeDpX': 411, 'displaySizeDpY': 731, 'displayWidth': 1080, 'productName': 'OnePlus5', '
screenOn': True, 'sdkInt': 27, 'naturalOrientation': True}
```

### 修改deploy.yaml

因为Alas默认使用了Windows下的配置文件，所以我们要手动修改

```
# 修改gitee仓库
Deploy.Git.Repository : https://gitee.com/LmeSzinc/AzurLaneAutoScript

# git位置
Deploy.Git.GitExecutable : /usr/bin/git

# python位置
Deploy.Python.PythonExecutable : [Anaconda安装路径]/envs/alas/bin/python

# adb位置
Deploy.Adb.AdbExecutable : /usr/bin/adb
```

## 使用 shell 脚本启动停止 alas

编写脚本

```
#!/bin/bash

start(){
    source <conda_path>/bin/activate alas # <miniconda_path> 替换为实际 conda 安装路径
    cd <AzurLaneAutoScript_path> # <AzurLaneAutoScript_path> 替换为 alas 路径
    git pull origin master
    nohup python gui.py >/dev/nul 2>&1 &
    echo "start alas"
}

stop(){
    kill -9 $(pgrep -f alas) 
    echo "kill alas"
}

case $1 in
    "start" ) start;;
    "stop" ) stop;;
    * ) stop;start;;
esac
```

将文件保存为 alas，放在`/usr/bin`，修改权限

```
chmod 755 alas
```

可用以下命令控制 alas

```
alas start # 启动
alas stop # 停止
alas # 重启
```

## 遇到一些问题

### ERROR:Permission denied

```
# 权限相关问题，激活环境时用以下代码
source activate alas
```

### ERROR:Conda command not found

```
# 打开系统变量
vim ~/.bashrc

# 添加系统变量
export PATH=/[path]/anaconda3/bin:$PATH # [path]为anaconda3的安装路径

#重新加载配置
source ~/.bashrc
```

### ERROR:XXX is not a trusted or secure host

```
pip install 库包名 -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com
# 这里将pip源换成清华源、阿里源等都适用。
```

---

## 总结

感谢Lme大佬的 [AzurLaneAutoScript](https://github.com/LmeSzinc/AzurLaneAutoScript) ~~MAGA 让碧蓝航线再次伟大！~~

教程参考了群内大佬 **Alas部署.md - freesrz**

再一次感谢各位群大佬
