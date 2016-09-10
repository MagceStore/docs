# 目录
* Unix & Linux 发展简史
* Linux 启动过程
* Linux 第一个进程 SysV init, Upstart, Systemd
* Systemd 功能介绍
* Systemctl 命令简介
* Unit service 配置文件简介
* Shadowsocket.service 示例


# Linux 发展简史
### UNIX 名字来源 (一个游戏和玩笑创造出来)
1965麻省理工决定开发一个大型的分时计算机系统，于是麻省理工学院找到通用电子公司,贝尔电话实验室开始一个叫做**MULTICS(Multiplexed Information and Computing Service)**的项目，1969年2月，MULTICS 计划在历经四年的奋战后，仍旧未达到原先规划设计的理 想，贝尔电话实验室决定退出计划，项目夭折。在退出贝尔实验室退出计划之后，实验室中的有个叫**Ken Thompson**的人，他为MULTICS这个操作系统写游戏了个叫**Space Travel**的游戏，在MULTICS上经过实际运行后，他发现游戏速度很慢而且耗费昂贵 —— 每次运行会花费75美元。退出这个项目以后。他为了让这个游戏能玩，所以他找来**Dennis Ritchie**为这个游戏开发一个极其简单的操作系统。他们的一个叫**Brian Kernighan**同事非常不喜欢这个系统，嘲笑Ken Thompson说：“你写的系统好真差劲，干脆叫**UNICS**算了。**UNICS**的名字就是相对于**MULTICS**的一种戏称，后来改成了**UNIX**。于是，Unix就在这样被游戏和玩笑创造了，当时是1969年8月。也就是这一年，**Linux**之父**Linus Torvalds**在芬兰出生了。

### UNIX 分支发展历史

[Unix History](https://www.levenez.com/unix/)  
[https://www.levenez.com/unix/unix.pdf](https://www.levenez.com/unix/unix.pdf) 
### UNIX 哲学
Unix遵循的原则是KISS (Keep it simple, stupid)  
* Everything (including hardware) is a file. (所有的事物（甚至硬件本身）都是一个的文件。)  
* Configuration data stored in text. (以文本形式储存配置数据。)  
* Small, single-purpose program. (程序尽量朝向小而单一的目标设计。)   
* Avoid captive user interfaces. (尽量避免令人困惑的用户接口。)  
* Ability to chain program together to perform complex tasks. (将几个程序连结起来，处理大而复杂的工作。)  


# Systemd
Linux Distribution | Version
--- | --- 
Fedora | 15
RedHat| 7
CentOS | 7
Debian | 8
ubuntu | 16.04
OpenSUSE | 12.3 
Arch | Yes
Gentoo | Optional

```bash
lsinitramfs -l /boot/initrd.img-4.4.0-34-generic
```

### static
Static units are those which cannot be enabled/disabled, but it doesn't mean they are always executed. They will only if another unit depends on them, or if they are manually started.
Actually, static units are simply those without an [Install] section. As enabling units means just creating a symlink to wherever [Install] mandates, those units without [Install] section cannot be enabled, as systemctl doesn't know where to place the symlink.
Of course, you can still manually create a symlink from a static unit to (for instance) /etc/systemd/system/multi-user.target.wants/, and it will be executed as any other enabled unit. But I suppose static units are not intended to be enabled in that way, and most probably you shouldn't need to do it.

![alt systemd](http://4.bp.blogspot.com/-iZ0FWqueNiQ/U8Jmd-byW4I/AAAAAAAACCk/20kfmmguByE/s1600/1000px-Linux_kernel_unified_hierarchy_cgroups_and_systemd.svg.png)
![alt systemd](http://www.ha97.com/wp-content/uploads/2014/07/Systemd_components.svg_.png)

```bash
systemd-cgls
ps xawf -eo pid,user,cgroup,args
```
### [Story](http://0pointer.de/blog/projects/systemd.html)

Base Event (Upstart)  
Base Dependence(Systemd)  
