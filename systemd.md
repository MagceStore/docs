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
