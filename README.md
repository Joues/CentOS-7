# zhou
## CentOS7 安装日记

### 一、CentOS 7添加Win 7启动引导


#### 1、# vim /boot/grub2/grub.cfg
#### 2、找到  ### BEGIN /etc/grub.d/30_os-prober ###，在后面添加
     menuentry "Windows 7" {
          insmod ntfs
          set root=(hd0,1)
          chainloader +1
     }
（grub2从1计数，win7装在C盘上的可以在终端里输入 fdisk -l来确定下，一般win都是装在C的吧)
#### 3、保存并退出："Esc"    +    "："    +    "wq"，回车
#### 4、# vim 40_custom
> 写入以下内容
>    #!/bin/sh
     exec tail -n +3 $0
     # This file provides an easy way to add custom menu entries.  Simply type the
     # menu entries you want to add after this comment.  Be careful not to change
     # the 'exec tail' line above.
     menuentry 'Windows7'{
          set root=(hd0,1)
          chainloader +1
     }
#### 5、# reboot


### 二、CentOS 7+Win 7双系统，修改引导顺序（开机默认Win 7优先）：

#### 1. # sudo vim  /etc/default/grub
注释掉GRUB_DEFAULT=saved，在这一行的下面插入GRUB_DEFAULT='Windows 7'，保存并退出
#### 2.# grub2-set-default 'Windows 7' 验证默认启动项：
#### 3.# grub2-editenv list
> 输出：
     saved_entry=Windows 7


### 三、CentOS 7+Win 7双系统，修改引导顺序（开机默认Win 7优先）：

#### 1. # sudo vim  /etc/default/grub
注释掉GRUB_DEFAULT=saved，在这一行的下面插入GRUB_DEFAULT='Windows 7'，保存并退出
#### 2.# grub2-set-default 'Windows 7' 验证默认启动项：
#### 3.# grub2-editenv list
> 输出：
     saved_entry=Windows 7
