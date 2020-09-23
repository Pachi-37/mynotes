# 安装Arch随身系统

### 涉及到的使用工具

1. 移动硬盘
2. archlinux镜像
3. Vmware

### 新建一个虚拟机

前面步骤与创建虚拟机基本一致

##### 需要更改的配置

- 如果设备支持`usb3.0`
  - `setting` `usb controller` 选择 `usb 3.0` 



### 安装arch

启动虚拟机，安装系统

- 输入 `lsblk`，观察是否挂载入硬盘
  - 将硬盘连接到虚拟机

> VM > `Removable Devices` > `USB Device` >`Connect(Disconnect from Host)`

输入以上指令`lsblk`，查看是否挂载新的硬盘

##### 相关补充设置

- 使用 `putty` 方便复制命令
  - 启动 ssh 服务
    - `systemctl start sshd` 
  - 修改密码
    - `passwd`
  - 查找 `ip`
    - `ifconfig`
  - 使用`ip`连接虚拟机

- 改变字体大小

  ```bash
  setfont /usr/share/kbd/consolefont/LatGrKyr-12x22.psfu.gz
  ```

- 更改镜像源

  - 编辑 `/etc/pacman.d/mirrorlist`
  - 删除`/etc/pacman.conf`的`Color`注释

##### 安装命令

- 分区
- 格式化分区
- 挂载分区
- 安装操作系统
  - `pacstrap -i /mnt base base-devel linux linux-firmware`

### 配置系统

- 生成文件系统表
  -  `genfstab -U -p /mnt > /mnt/etc/fstab` 

- 进入新系统

  - `arch-chroot /mnt`

- 文字编码

  - 修改`/etc/locale.gen`，将 `zh_CN` 开头的行全部取消注释，再找到 `en_US.UTF-8 UTF-8`也取消注释
  - `locale-gen` 
  - `echo "LANG=en_US.UTF-8" /etc/locale.conf`

- 设置时区

  - ```bash
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime    //选择中国上海作为时区
    hwclock --systohc  		   //同步系统时间
    ```

- 设置主机名

  - `echo "arch" > /etc/hostname` 此处`arch`也可以为其他名字

- 网络设置

  - `vim /etc/hosts `//网络设置

    ```bash
      127.0.0.1	  localhost
      ::1	      	localhost
      127.0.1.1	  arch.localdomain	arch    //使用上一步设置的网络
    ```

- `vim /etc/mkinitcpio.conf`

  - ```bash
    # usr,fsck and shutdown hooks
    HOOKS=(base udev ==block== autodetect ……)
    ```

    > 添加==block==到上述行中

  -  `mkinitcpio -p linux` ，生成启动镜像

- `passwd` 修改密码

- 安装 ntfs 文件系统，以便访问 Windows 磁盘

  -  `pacman -S ntfs-3g` 

### 网络（存在问题）

1. 方法一

   1.  `pacman -S zd1211-firmware` 安装无线网卡驱动
   2.  `pacman -S iw wpa_supplicant wireless_tools net-tools` 安装网络工具

2. 方法二

   安装完系统后操作

   ### 重启后配置linux的用户及联网功能

   用root登入系统继续配置linux `df -lh` //查看系统安装磁盘容量信息

   ```
   ip link //查看网络连接状况
   ip link set ens33 up  //打开虚拟机的网卡
   ```

   `dhcpcd `//运行动态分配ip `ping baidu.com` //连接百度进行上网测试 `ip addr` //其作用类似于ifconfig `ip route` //其作用显示当前实际在使用的网卡端口状态和路由网关信息 `pacman -S netctl `//安装网络管理软件来管理网卡 `cp /etc/netctl/examples/ethernet-dhcp /etc/netctl/my_dhcp_profile `//将例子中的有线连接配置文件复制到目录下并改名为my_dhcp_profile `vim /etc/netctl/my_dhcp_profile `//修改配置文件

   ```
     Interface=ens33   //配置连接网络名
     Connection=ethernet   //为有线连接
     IP=dhcp   //自动分配ip地址
   ```

   `netctl start my_dhcp_profile` //启动网络连接服务 `netctl enable my_dhcp_profile` //设置开机启动网络连接服务 `pacman -S openssh` //安装openssh服务 `systemctl start sshd.service` //启动openssh服务 `systemctl enable sshd.service` //设置开机启动ssh服务 `vim /etc/ssh/sshd_config` //编辑sshd配置文件

   Authentication: //运行root用户进行ssh登入

   `LoginGraceTime 2m` //将注释#号去掉

   \#PermitRootLogin prohibit-password

   `PermitRootLogin yes `//添加一行 `StrictModes yes `//将注释#号去掉 `useradd -m -G wheel winnerwood` //添加一个用户在wheel用户组中 `passwd winnerwood` //给这个用户添加密码

   ------

   `pacman -S sudo` //安装sudo命令

   `ln -s /usr/bin/vim /usr/bin/vi `//编辑管理员权限时候可以用vim替代vi命令 `visudo` //编辑sudo文件

   `%wheel ALL=(ALL) ALL` //将注释#去掉，让这个组中用户可以执行任何命令。保存退出

## 配置引导

-  安装引导程序
  -  `pacman -S grub`
  -  `grub-install --target=i386-pc /dev/sdb` 
  -  `blkid` , 将 sdb2（安装系统的分区） 的 UUID 记下来，将所有出现的UUID全部改成 sdb2 的UUID——（正常情况下不需要操作）

##### 测试BIOS

- 新建虚拟机

> 选择磁盘时，选择 Use a physical disk(for advanced users)，选择移动硬盘两个分区

- 测试是否可以打开，如果能打开BIOS启动安装成功，关闭虚拟机

#### 安装UEFI引导

- 修改刚才安装系统的虚拟机，修改Firmware type`UEFI`，==不==要勾选 Enable Secure Boot
- 重新挂载，并进入系统
- 安装UEFI启动项
  - `grub-install --target=x86_64-efi --efi-directory=/boot/efi --removable` 

##### 测试UEFI引导

> Boot 虚拟机的启动模式为 UEFI，不要勾选 Enable Secure Boot,尝试启动，启动完成，安装成功