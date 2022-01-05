# System Flow



## Install Arch Linux

### 验证引导模式

`ls /sys/firmware/efi/efivars`

如果没有报告错误，证明系统使用UEFI模式引导，否则使用MBR进行引导。

### 连接到网络

通常会自动连接，使用`ping domain`进行检查

### 更新系统时间

确保时间准确

`timedatectl set-ntp true`

如果失败，检查服务状态

`timedatectl status`

### 建立硬盘分区

检查系统硬盘状态并且列出所有硬盘

`fdisk -l`

使用fdisk进行分区

`fdisk /dev/sda`

BIOS和MBR分区表

| 挂载点 | 分区      | 分区类型   | 建议大小 |
| ------ | --------- | ---------- | -------- |
| SWAP   | /dev/swap | Linux swap | 1GB      |
| /mnt   | /dev/root | Linux      | 所有剩余 |

在fdisk新建MBR分区表O

在fdsik新建分区N

在分区结束后检查确认并使用W保存

### 格式化分区

使用EX4文件系统格式化根分区

`mkfs.ext4 /dev/sdaroot`

初始化swap分区

`mkswap /dev/sdaswap`

### 挂载分区

挂载根分区

`mount /dev/sdaroot /mnt`

启用swap分区

`swapon /dev/sdaswap`

### 安装

安装最小主义组件

`pacstrap /mnt base linux linux-firmware`



