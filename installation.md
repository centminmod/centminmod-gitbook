# Installation

Choose between the stable and beta versions of Centmin Mod:

For the latest 124.00stable version with PHP 5.6, 7.0, 7.1, 7.2, 7.4, 8.0, 8.1 support. CentOS 7 only supported:

```bash
curl -O https://centminmod.com/installer.sh && chmod 0700 installer.sh && bash installer.sh
```

For the 130.00beta01 version with PHP 5.6, 7.0, 7.1, 7.2, 7.4, 8.0, 8.1 and 8.2 support. CentOS 7, AlmaLinux 8 and Rocky Linux 8 supported:

```bash
curl -O https://centminmod.com/betainstaller.sh && chmod 0700 betainstaller.sh && bash betainstaller.sh
```

\* PHP 5.6 to 7.4 EOL releases have backported security patch support

### System Requirements

For AlmaLinux 8.x / Rocky Linux 8.x:

* For AlmaLinux or Rocky Linux 8, the minimum system requirements are 1GB memory and 20GB disk. Recommended system requirements are at least 2GB memory and 40GB disk.
* For Centmin Mod on AlmaLinux & Rocky Linux 8, the minimum system requirements are 2GB memory and 40GB disk. If you have less than 2GB memory, setup at least 2GB swap disk - using a swap disk when there's no enough memory will still allow Centmin Mod to operate just it will be a lot slower - as slow as the swap disk's underlying disk performance. Recommended system requirements are at least 3GB memory and 60GB disk. If you plan to install any type of Linux anti-malware/virus scanning software, you would want to add at least another 1-4GB of memory on top of those requirements. The optimal CPU core/threads is between 2-4. Though 1 CPU core is fine. The more CPU cores/threads, the faster the Centmin Mod source compiled routines will complete and the more concurrent workloads your server stack will generally be able to handle.

For CentOS 7.x (will be end of life by May 2024):

* Minimum system requirements are 1GB memory for CentOS 7.x 64bit and 20GB disk space for OpenVZ VPS virtualization & 30GB for KVM and Xen virtualisation. These requirements were recently revised [here](https://community.centminmod.com/threads/6075/).
* Recommended memory & disk requirements are double the mininum for CentOS 7.x 64bit at 2GB memory and disk space of 40GB for OpenVZ and 60GB for KVM/Xen virtualisation.

### General Installation Notes

1. SELINUX must be disabled.
2. Initial Centmin Mod installation needs to be done as full root user rather than as sudo user and `centmin.sh` shell based menu needs to be run as full root user.
3. For best security and performance you would want to use AlmaLinux 8 or Rocky Linux 8 with KVM based VPS server or dedicated servers. Centmin Mod can detect whether OpenVZ or Xen/KVM virtualization is being used and auto optimise the server environment based on that info. OpenVZ VPS due to the limitations and use of host level Kernel can not be auto optimized to the level that KVM, Xen or dedicated servers can.
4. Centmin Mod currently DOES NOT fully support LXD/LXC containers due to the fact that not all web hosts properly configure LXD/LXC container at the LXD/LXC host level for CentOS support. Centmin Mod 123.09beta01 and newer, has preliminary and on-going developmental LXD support if LXD containers are properly configure at LXD host node level first. But it's still a work in progress. See comment [here](https://community.centminmod.com/threads/csf-locked-up-vps-twice.17567/#post-74314) & some of the LXD config issues LXD web host providers need to be aware of for CentOS [here](https://discuss.linuxcontainers.org/t/centos-7-5-container-operation-not-permitted/1957). If you're using and configuring your own server with LXD containers, then you'd need to properly configure LXD at LXD host level. For least problems, use KVM VPSes instead.
5. For best performance and latest feature improvements, ensure you're using PHP 7.4+, 8.0+ or 8.1+ provided your web app supports the versions. See [PHP 7.4 vs 7.3 vs 7.2 vs 7.1 vs 7.0 benchmarks here](https://community.centminmod.com/threads/php-benchmarks-7-4-vs-7-3-vs-7-2-vs-7-1-vs-7-0-php-fpm.18741/) and [PHP 8.0 JIT vs 8.0 vs 7.4 vs 7.3 vs 7.2 vs 7.1 vs 7.0 benchmarks here](https://community.centminmod.com/threads/php-8-0-0-ga-stable-release.20739/).
6. Currently, only x86/x86\_64 architecture is supported and ARMv7/8 based cpus isn't supported fully due to CentOS ARM compatibility with 3rd party YUM repositories that Centmin Mod uses. Hopefully, in future it maybe so keep an eye on [Centmin Mod Community Forum's Beta Release forums](https://community.centminmod.com/forums/beta-release-code.9/) for any updates.
7. For disk partitioning it's recommended to have one large single root `/` partition. Especially for [CentOS 7.x.](https://community.centminmod.com/threads/tip-centos-7-do-not-have-usr-on-separate-partition.11832/). If you plan to use Docker, pay attention to default file system used EXT4 versus XFS when formatting partitions (on dedicated servers). Details [here](https://community.centminmod.com/threads/using-docker-on-centos-7-choose-ext4-over-xfs.12492/).
8. Optimally, for KVM/Xen/VMWare or dedicated you should configure your server with at least 1GB to 2GB swap space if possible. This does not apply to OpenVZ VPS where you may not have control over swap depending on how OpenVZ is configured.
9. Choose non-OpenVZ based VPS server i.e. dedicated, KVM, Xen or VMWare if you want to be able to tune TCP settings (sysctl.conf), update and use own Linux Kernels. You are not able to do those tasks with OpenVZ VPSes.
10. If you plan on using PHP [Composer](https://getcomposer.org/) for your web applications, you will want to have at least 3-4GB of memory on your server as Composer can use up to 1.5+ GB memory requirements itself and may require you raising the [PHP memory\_limit up to 1.5GB or more](https://getcomposer.org/doc/articles/troubleshooting.md#memory-limit-errors)

### AlmaLinux 8 / Rocky Linux 8 Installation Notes

1. Centmin Mod EL8 installs will default to GCC 11.2 for compilation routines instead of the current Centmin Mod 130.00beta01 default for GCC 10.2 and EL8 system default GCC 8.5
2. Centmin Mod EL8 installs will default to PHP 8.0.x installation (PHP-FPM). EL9 OS will default to a minimum PHP 8.1.x version and PHP versions below PHP 8.1 won't work right now with EL9 OSes. If you need PHP 7.4 to 8.0 then stick with EL8 OSes like Alma Linux 8 or Rocky Linux 8.
3. Centmin Mod EL8 installs as at September 27, 2022 onwards, will switch from official MariaDB YUM repo provided MariaDB 10.3 which has support ending May 2023 to native EL8 Appstream module provided MariaDB 10.3 version which has [extended support until May 2029](https://access.redhat.com/support/policy/updates/rhel-app-streams-life-cycle#rhel8\_application\_streams)
4.  Centmin Mod EL8 installs on AlmaLinux 8 or Rocky Linux 8 require SELinux to be disabled. However, EL9 and also Linux Kernel 6.4 will [remove run time disabling of SELinux](https://github.com/SELinuxProject/selinux-kernel/wiki/DEPRECATE-runtime-disable). So to anticipate the potential in future of EL8 folks updating to Linux 6.4 and alike Kernels, the EL8 installers will check if SELinux is disabled and prompt the user to reboot their server to properly disable SELinux before actually running Centmin Mod installers. Example, when you run Centmin Mod installer on EL8 OS, you may be greeted with the following if you have a EFI setup for /boot/efi/EFI/almalinux/grub.cfg, you'll see:\
    \


    ```
    Detected SELinux NOT disabled for EL8
    Adding selinux=0 to Kernel GRUB_CMDLINE_LINUX line in /etc/default/grub
    GRUB_CMDLINE_LINUX="rd.auto nomodeset console=tty0 selinux=0"
    Regenerating GRUB2 configuration
    grub2-mkconfig -o /boot/efi/EFI/almalinux/grub.cfg
    Added selinux=0 to Kernel GRUB_CMDLINE_LINUX line in /etc/default/grub to disable SELinux
    This is the right way to disable SELinux in future as other run-time methods deprecated
    If you intend to use own custom Linux Kernels i.e. ELRepo, ensure you have selinux=0 set
    Please reboot system to disable SELinux then install Centmin Mo 
    ```
