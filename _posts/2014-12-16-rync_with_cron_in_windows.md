# 安装Rsync
## 安装cygwin
参考[Installing Cygwin and Starting the SSH Daemon](Installing Cygwin and Starting the SSH Daemon)

## 安装Rsync client
下载 [cwRsync - Rsync for Windows](https://www.itefix.net/cwrsync) , 并且安装

# windows环境使用Rsync同步远程数据 (SSH/SMB)
## 使用Rsync同步Windows文件共享(SMB)
* 删除虚拟盘 K:
```shell
#删除虚拟盘 K:
net use k: /del /y
```

* 创建虚拟盘 K:
```shell
#{REPLACE_YOUR_USER} 替换成真实的用户名
#{REPLACE_YOUR_PASSWORD} 替换为真是的用户密码
use k: \\10.180.6.128\OFcvco5.1.0_KSUPP_Librar ${REPLACE_YOUR_PASSWORD} /user:${REPLACE_YOUR_USER}
```
* 从K:(远程源文件系统),同步文件到目标地址 `/cygdrive/d/mirror/OFcvco5.1.0_KSUPP_Librar/`
```shell
C:\cygwin64\bin\bash.exe -l -c "rsync  -avzh  /cygdrive/k/ /cygdrive/d/mirror/OFcvco5.1.0_KSUPP_Librar/ > /var/log/cron-OFcvco5.1.0_KSUPP.log"
```

## 使用rsync同步SSH文件共享

* 创建SSH免登陆密钥(假设windows已经安装cygwin)

具体参考[密钥(无需密码)方式实现SSH访问]({% post_url 2014-01-01-login_to_ssh_without_password %})


* 同步远程文件系统到本地目标目录
```sh
C:\cygwin64\bin\bash.exe -l -c "rsync -avzh {REPLACE_YOUR_USER}@{REPLACE_YOUR_PASSWORD}:{REPLACE_YOUR_SRC_DIR} {REPLACE_YOUR_LOCAL_TARGET_DIR} > /var/log/cron-510ITR1-host.log"
```

# 使用windows任务计划程序来运行rsync
1. 访问 `控制面板\所有控制面板项\管理工具\任务计划程序`
2. 创建任务,使用rsync步骤,需配置如下
  1. 操作: `启动程序`
  2. 程序或脚本: `C:\cygwin64\bin\bash.exe`
  3. 添加参数: `-l -c "rsync  -avzh  /cygdrive/k/ /cygdrive/d/mirror/OFcvco5.1.0_KSUPP_Librar/ > /var/log/cron-OFcvco5.1.0_KSUPP.log"`
  4. 起始于 `C:\cygwin64\bin`


## Links
* [Rsync Examples over SSH](https://calomel.org/rsync_tips.html)
* [脱机时使用网络文件](http://windows.microsoft.com/zh-cn/windows/working-with-network-files-offline#1TC=windows-7)
