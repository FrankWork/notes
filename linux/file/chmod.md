r 4：读权限，
w 2：写权限，
x 1：执行权限，
- 0：无权限，
s ：特殊权限 

该命令有两种用法。一种是包含字母和操作符表达式的文字设定法；另一种是包含数字的数字设定法。
　　1）. 文字设定法:
　　	chmod ［who］ ［+ | - | =］ ［mode］ 文件名
　　2）. 数字设定法
　　我们必须首先了解用数字表示的属性的含义：0表示没有权限，1表示可执行权限，2表示可写权限，4表示可读权限，然后将其相加。所以数字属性的格式应为3个从0到7的八进制数，其顺序是（u）（g）（o）。
　　例如，如果想让某个文件的属主有“读/写”二种权限，需要把4（可读）+2（可写）＝6（读/写）。

chmod o+rwx file.txt