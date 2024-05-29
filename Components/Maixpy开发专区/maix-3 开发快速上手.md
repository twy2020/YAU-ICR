# Maix-3 开发快速上手

## 0、烧录系统

- 参考网址：[AXera-Pi 上手指南 - Sipeed Wiki](https://wiki.sipeed.com/hardware/zh/maixIII/ax-pi/flash_system.html)

## 1、启动设备

- 安装TTL转USB CH340驱动

- 下载 [MobaXterm](https://mobaxterm.mobatek.net/download.html)

- 打开 MobaXterm

- Session -> Serial -> 选择 `COM#`  -> 选择 Speed : `115200`

- 插电源到 USB-OTG 口，插数据线到电脑 USB3.0 口

- 看到启动日志即可

- 默认登录用户名和密码都为 `root` 

## 2、连接无线网

- 运行指令打开图形化网络连接工具
  
  ```bash
  nmtui
  ```

- 选择 `activate a connection`

- 根据图形化页面连接上你的热点

## 3、远程ssh

- 打开 MobaXterm 先进行串口登录

- 运行命令查看 `wlan0` IP地址
  
  ```bash
  ifconfig
  ```

- 电脑连接同一热点

- MobaXterm 内 Session -> SSH -> 填写刚刚的IP地址到 `Host Name`

- 登录 login as : `root` password : `root`

## 4、安装VScode准备远程开发

- 去这个网址自动下载VScode（sipeed给的方法不可用）,因为 maix-3 基于 `armhf` ，必须下载 `armhf` 的安装包[Documentation for Visual Studio Code](https://code.visualstudio.com/docs/?dv=linuxarmhf_deb)

- 通过 MobaXterm 侧边栏的文件传输工具上传刚刚下载好的文件（`code_1.89.1-1715058914_armhf.deb`）（版本号可能不同，注意复制你自己的 VScode 安装包文件名）到 maix-3 上的根目录

- ssh 终端指令安装 VScode deb 包
  
  ```bash
  sudo dpkg -i ./code_1.89.1-1715058914_armhf.deb
  ```

- 若出现依赖缺少问题而报错，请先运行指令进行软件列表更新
  
  ```bash
  sudo apt-get update
  ```

- 运行下面的命令进行依赖修复，询问时输入 `y` 表示同意继续运行
  
  ```bash
  sudo apt --fix-broken install
  ```

- 再次运行
  
  ```bash
  sudo dpkg -i ./code_1.89.1-1715058914_armhf.deb
  ```

- 等待安装完成

## 5、安装VScode remote插件进行远程开发

- 输入官方教程给的插件安装指令
  
  ```bash
  code --install-extension ms-vscode-remote.remote-ssh
  ```

- 会提示 `root` 高权限安全风险问题
  
  ```bash
  You are trying to start Visual Studio Code as a super user 
  which isn't recommended. If this was intended, please add 
  the argument `--no-sandbox` and specify an alternate user 
  data directory using the `--user-data-dir` argument.
  ```

- 根据提示使用下面的命令授权安装（用户数据我选在放在 `--user-data-dir=./vscode/data` 路径下，可以更改路径按照你的喜好）
  
  ```bash
  sudo code --no-sandbox --user-data-dir=./vscode/data --install-extension ms-vscode-remote.remote-ssh
  ```

- 提示安装成功
  
  ```bash
  Installing extensions...
  Installing extension 'ms-vscode-remote.remote-ssh'...
  Extension 'ms-vscode-remote.remote-ssh-edit' v0.86.0 was successfully installed.
  Extension 'ms-vscode-remote.remote-ssh' v0.110.1 was successfully installed.
  Extension 'ms-vscode.remote-explorer' v0.4.3 was successfully installed.
  ```

## 6、使用本地VScode远程连接Maix-3开发

- 电脑安装 VScode （去官网下载电脑对应安装包安装即可），汉化（参考网上教程）

- 打开 VScode ，左边栏找到拓展，搜索 `Remote Development`

- 下载并等待安装完成

- 怎么连接，参考这篇文章[windows下使用vscode远程连接Linux服务器进行开发_vscode linux-CSDN博客](https://blog.csdn.net/irober/article/details/112724986)
