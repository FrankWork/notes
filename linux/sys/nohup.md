# before

$ nohup ping www.ibm.com &
$ setsid ping www.ibm.com


# after
$ ctrl+z  # 暂停任务
$ jobs 	# 列出任务号
[1]+	Stopped	sh main.sh &
$ bg %1
[1]+	Running	sh main.sh &
