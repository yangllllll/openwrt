系统开发者：刘宇辰.

系统相关驱动开发：刘宇辰

自编译操作系统

1.准备工作
win10+Ubuntu虚拟机 或者 Ubuntu：
小米路由器4c
安装好python3 和 pip3。
安装好 telnet（Mac下：brew install telnet）。
路由器和电脑都已经连接上网络。//这点很重要！

2.开始破解：
安装OpenWRTInvasion：在Ubuntu系统中输入下列命令：
git clone https://github.com/acecilia/OpenWRTInvasion //可能需要vpn
cd OpenWRTInvasion
pip3 install -r requirements.txt
python3 remote_command_execution_vulnerability.py

3.获取stock：
执行脚本后，会要求输入Route IP和stok。stok的获取方法：访问小米路由器后台管理地址，例如http://192.168.1.1，再查看当前的路由器管理后台的URL，在URL中某个参数就是stok。执行过程需要联网。（注意stok是"stok="后面的全部内容）

脚本执行成功后，执行：

telnet 你路由器的ip//一般是：192.168.32.1

用户是root，不需要密码，回车即可进入。

4.获取breed
在命令行中输入：
小米3A，3C，4A百兆版，4C：cd /tmp && wget  --no-check-certificate https://breed.hackpascal.net/breed-mt7688-reset38.bin && mv breed-mt7688-reset38.bin breed.bin
小米3G 和 小米4：cd /tmp && wget  --no-check-certificate https://breed.hackpascal.net/breed-mt7621-xiaomi-r3g.bin && mv breed-mt7621-xiaomi-r3g.bin breed.bin
小米4A千兆版 :cd /tmp && wget  --no-check-certificate https://breed.hackpascal.net/breed-mt7621-pbr-m1.bin && mv breed-mt7621-pbr-m1.bin breed.bin
5.刷breed：
在命令行中输入：mtd write breed.bin Bootloader
等待完成

6.进入breed：
路由器断电
按住路由器的重置建后插电，直到指示灯闪烁后熄灭，松开重置键
在浏览器里输入：192.168.1.1
然后点击固件备份，点击EEPROM下载eeprom.bin

7.刷机：
下载我们编译好的openwrt固件//此固件只适用于小米路由器4C
进入固件更新
EEPROM选择我们刚下载的eeprom
固件选择我们下载的openwrt固件
点击上传
点击更新
等待路由器的灯变成蓝色
在电脑浏览器里输入：192.168.1.1
用户名：root
没有密码
点击登录就行了

