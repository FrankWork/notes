1。卸载文件系统
	umount /data0
2。建立文件系统，指定inode节点数
	mkfs.ext3 /dev/sda6 -N 18276352
3。修改fstab文件
	vi /etc/fstab
		/dev/sda6               /data0                  ext3    defaults        1 2
4，挂载文件系统
	mount -a
4。查看修改后的inode参数
	dumpe2fs -h /dev/sda6 | grep node


[注意]调整inode数会格式化磁盘，执行前应确定磁盘上没有重要数据或是先备份数据
