# iStoreOS 固件

iStoreOS 目标是提供一个人人会用的路由兼轻 NAS 系统，不管是作为路由还是 NAS，你都有相似的操作体验。

系统本身开源免费，目前系统代码开源在：[Github iStoreOS](https://www.github.com/istoreos/istoreos)，更多详细介绍请看我们[iStoreOS官网](https://site.istoreos.com/)

iStoreOS 来源于 OpenWRT，相较于原版 OpenWRT，iStoreOS 具有以下优势：

1. iStoreOS 提供了**软件中心**：[**iStore**](https://github.com/linkease/istore)，尽可能解决插件之间的依赖关系，可让大家自由自在安装插件，并且支持插件备份以及恢复。
2. iStoreOS 固件升级时会保留用户安装的插件，避免升级以后还要再安装一遍插件。
3. iStoreOS 官方支持的硬件都可以**在线升级**，无需手动下载固件升级。
4. iStoreOS 拥有**沙箱模式**。通过 U 盘进入沙箱模式，后续的软件安装更新以及系统配置都在沙箱进行。不管安装插件搞坏了系统还是配置错误导致系统故障，拔掉 U 盘就回到进沙箱前的状态。如果对当前状态满意还可以回写到非沙箱环境。沙箱模式本身也是系统扩容的最简单的方法。
5. iStoreOS 本身就是精简版本，所有的额外功能都是触发到了，依赖软件中心去额外安装插件实现。iStoreOS并不是臃肿的把所有用到的插件内置到固件中。

iStoreOS 还做了很多很多的交互简化，但是即使再简化，对于不同的用户级别，我们还是得提供了三套完全不一样的交互 UI：

## 入门极客版本 UI

iStoreOS 入门极客版本 UI 是默认的 UI，目标是提供给懂点技术的入门极客爱好者，或者偷懒极客老手，核心特性：

* 首页提供网络向导，磁盘向导，Docker 向导等等众多向导，不管是新手还是老手，都能快速配置自己想要的东西
* 修复众多 OpenWRT 不人性的小问题，比如 Samba 设置独立用户名密码很麻烦，磁盘挂载等
* 更多首页工具好帮手，比如在线升级，各种错误检测，网口图形化配置等
* 其它很多常用的，比如 DDNS 配置，Docker 配置等

### 入门极客版本预览

![首页](https://doc.linkease.com/assets/img/geek-preview1.9987f6a0.jpg)

更多皮肤介绍请看我们[iStoreOS官网](https://site.istoreos.com/)

## 支持硬件

* [EasePi-R1](https://item.taobao.com/item.htm?ft=t&id=851159153974) [官方硬件，没有这个硬件，就没有这个项目]
* X86
* R2S
* R4S
* R5S
* R68S

更多硬件请参考[设备支持](https://site.istoreos.com/device/)

### 功能组合

* 建议使用[易有云 APP](https://www.linkease.com) 做异地组网，相册备份，文件同步，远程应用导航等
* 建议用 [DDNSTO](https://www.ddnsto.com) 从网页域名远程访问路由器

### 固件下载

[下载地址](https://site.istoreos.com/firmware)

### 使用方法

* 默认IP http://192.168.100.1
* 默认密码：password
* 如果只有一个网口，默认的网口是 LAN，且DHCP自动获取 IP；如果大于一个网口，默认 eth0 是 WAN 口，其它都是 LAN。
* 如果在 LAN 口修改 IP，或者任何修改之后导致无法连接路由器，都会导致刚才的修改被回滚。所以要修改 LAN/WAN 口 IP，可以选择强制应用，保证修改肯定生效。

## 定制固件

如果想自己制作固件，也是可以的。

iStoreOS 来源于官方的 OpenWRT Release 分支源码，都是通过 OpenWRT 标准组件形式实现，100% 兼容 OpenWRT 的源主干分支。我们修改或者开发的部分，都以插件形式，具体源代码如下：

* [iStoreOS 固件](https://github.com/istoreos/istoreos) 核心固件源代码
* [nas-packages-luci](https://github.com/linkease/nas-packages-luci) 我们自己开发的插件 UI 代码
* [nas-packages](https://github.com/linkease/nas-packages) 我们自己开发插件的程序代码，部分程序并不开源
* [istore](https://github.com/linkease/istore) 软件中心核心代码，包含备份插件功能等，全部开源
* [istore-packages](https://github.com/linkease/istore-packages) 软件中心的一些非 OpenWRT 官方包
* [openwrt-app-actions](https://github.com/linkease/openwrt-app-actions) 其他一些软件包

iStoreOS 就是在 OpenWRT 最基础最原始的固件基础上，加上了上面插件的能力来实现。

### 编译参考

请动手能力强的人自己编译固件，跟标准 OpenWRT 一样。

### 离线包制作

iStoreOS离线包不是一个压缩包，也没啥黑科技，而是借助第三方软件实现。原理是[makeself项目](https://github.com/megastep/makeself)：

生成方法例子：
```
./makeself.sh --nox11 ./xxx ./out/xxx_x86.run "OneClick install" ./install.sh
```

install.sh脚本内容大致为：
```
opkg update
opkg install *.ipk
```

把 ipk 跟 install.sh 结合在一起，本质会生成一个包含所有 ipk 跟 install.sh 的自解压自运行的程序。

## 关注更新

更多iStoreOS 功能，请关注我们的账号：

* [酷友社B站账号](https://space.bilibili.com/1492058311?spm_id_from=333.788.0.0)
* [酷友社 Youtube](https://www.youtube.com/channel/UCvENMyIFurJi_SrnbnbyiZw)
* [QQ 群](https://www.koolcenter.com/posts/117)
* [TG 群](https://t.me/+QwxW7aimSMeRdQJX)
* 微信扫码关注公众号：
![istoreos-gongzhong](https://doc.linkease.com/assets/img/istoreos-gongzhong.7b082729.png)

## 问题反馈

* [提交反馈](https://github.com/linkease/istoreos/issues)

大家也可以选择加入 iStoreOS 固件互助群。（注意，QQ群没有官方人员长时间在线支持，如果购买了 DDNSTO/易有云 用户可以加入我们售后微信群）

* [入群](https://www.linkease.com/about/)

## 精力不足，求助一臂之力

因为各种原因，我们维护 iStoreOS 精力不足。如果有大神对本项目感兴趣，欢迎联系我们加入。

## 鸣谢

* [ziguayungui](https://github.com/ziguayungui)，[jjm2473](https://github.com/jjm2473)，[Koolshare LEDE 的作者 fw867](https://github.com/fw867)，[xiangfeidexiaohuo](https://github.com/xiangfeidexiaohuo)
* 感谢 LEAN 等相关人员，搞定了 i226 驱动等
* OpenWRT 官方团队
* 众多 OpenWRT 的固件或者插件开发者
* [KoolCenter](https://www.koolcenter.com)，[易有云](https://www.linkease.com) 团队相关同事

