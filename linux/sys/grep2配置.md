这是一个默认启动Ubuntu的例子：

note: ubuntu中使用greb, 不是greb2
=================================
$ cat /boot/grub/grub.cfg | grep Ubuntu
结果：
	menuentry 'Ubuntu，Linux 3.13.0-32-generic'  
	menuentry 'Ubuntu, with Linux 3.13.0-32-generic (recovery mode)' 
	menuentry 'Ubuntu，Linux 3.13.0-24-generic' 
	menuentry 'Ubuntu, with Linux 3.13.0-24-generic (recovery mode)' 
# sudo grub-set-default "Ubuntu，Linux 3.13.0-32-generic"
$ grub-editenv list
结果：
	saved_entry=Ubuntu，Linux 3.13.0-32-generic
# sudo grub-mkconfig -o /boot/grub/grub.cfg
结果：
	Generating grub configuration file ...
	Found linux image: /boot/vmlinuz-3.13.0-32-generic
	Found initrd image: /boot/initrd.img-3.13.0-32-generic
	Found linux image: /boot/vmlinuz-3.13.0-24-generic
	Found initrd image: /boot/initrd.img-3.13.0-24-generic
	Found memtest86+ image: /boot/memtest86+.elf
	Found memtest86+ image: /boot/memtest86+.bin
	Found Windows 8 (loader) on /dev/sda1
=================================
1. 首先找到Windows的menuentry.
# cat /boot/grub2/grub.cfg | grep Windows
结果：
menuentry "Windows 7 (loader) (on /dev/sda1)" --class windows --class os {
2. 设置Windows 作为默认的启动项（这儿只能使用上面命令输出中双引号 “ ” 或者单引号 ‘ ‘ 中的内容)

# grub2-set-default "Windows 7 (loader) (on /dev/sda1)"

3. 验证默认启动项
# grub2-editenv list
输出：
saved_entry=Windows 7 (loader) (on /dev/sda1)
4. 生成，更新 grub.cfg (可选）

下面的命令会使用/etc/grub.d下的自动配置脚本和/etc/default/grub中定义的变量，自动生成GRUB2配置文件（包括在 /boot下的内核），
-o 指定输出文件，/boot/grub2/grub.cfg是默认配置文件。如果是多系统，它会自动的把它们找出来，加入到启动菜单列表中去。

# grub2-mkconfig -o /boot/grub2/grub.cfg
/etc/default/grub 中可以配置timeout，背景图片等。
如：
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="Fedora"
GRUB_DEFAULT=saved
GRUB_CMDLINE_LINUX="rd.md=0 rd.lvm=0 rd.dm=0 KEYTABLE=us quiet SYSFONT=latarcyrheb-sun16 rhgb rd.luks=0 LANG=en_US.UTF-8"
GRUB_BACKGROUND=/boot/grub2/background.png
GRUB_TERMINAL_OUTPUT=gfxterm
GRUB_THEME=/boot/grub2/mytheme/theme.txt
================ 
备注： 下面的命令设置Fedora作为默认启动项：

# cat /boot/grub2/grub.cfg |grep Fedora
结果：
menuentry 'Fedora Linux, with Linux 3.1.2-1.fc16.i686.PAE' --class fedora --class os {
menuentry 'Fedora Linux, with Linux 3.1.1-1.fc16.i686.PAE' --class fedora --class os {
menuentry 'Fedora Linux, with Linux 3.1.0-7.fc16.i686.PAE' --class fedora --class os {
# grub2-set-default "Fedora Linux, with Linux 3.1.2-1.fc16.i686.PAE"
# grub2-editenv list
# grub2-mkconfig -o /boot/grub2/grub.cfg

