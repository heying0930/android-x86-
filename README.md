# android-x86-安装运行实验步骤纪要
##android-x86安装运行实验步骤纪要20160601
###1.创建磁盘映像.
    qemu-img create -f raw android.raw 20G
###2.启动android_x86.
    qemu-system-x86_64 -enable-kvm -m 2.5G -cdrom android_x86_64_6.0.iso -vga std -serial stdio -hda android.raw -boot d
###3.进入debug mode.
####（1）输入fdisk /dev/sda，创建分区1. 
       1）"n" （新建分区）<br>
       2）"p" （主分区）<br>
       3）"1" （分区号）<br>
       4）"1" （起始柱面号，回车取缺省值即可） <br>
       5）"xx"（结束柱面号）<br>
       6）"w"写入分区<br>
####（2）输入fdisk /dev/sda，创建分区2.
       1）"n" （新建分区）<br>
       2）"p" （主分区）<br>
       3）"2" （分区号）<br>
       4）"XX"（起始柱面号，回车取缺省值即可）<br> 
       5）"XX"（结束柱面号，回车取缺省值即可）<br>
       6) "w"写入分区<br>
####（3）输入"mdev -s".
####（4）输入"mke2fs -j -L DATA /dev/sda1" 
    格式化操作将分区1设置为数据分区.
####（5）输入"mke2fs -j -L SDCARD /dev/sda2" 
    格式化操作将分区2设置为SD卡外存分区.
####（6）输入"reboot -f"重启.
###4.进入安装模式.
    安装在第一个分区，分区格式为ext3，选择安装GRUB，跳过安装EFI GRUB2，选择可读写模式，安装android_x86.
###5.完成安装.
    重新启动reboot，然后关闭qemu.
###6.再次重启，进入安装后的android_x86系统 
    qemu-system-x86_64 -enable-kvm -m 2.5G -vga std -serial stdio -drive file=android.raw,format=raw,index=0,media=disk

  

  
