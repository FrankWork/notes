按列合并

$ cat 1.txt 
1
2
3
4
5
$ cat 2.txt 
q
w
e
r
t
y
$ paste 1.txt 2.txt 
1   q
2   w
3   e
4   r
5   t
    y


可以使用 -d 参数 加分割符

$ paste -d: 1.txt 2.txt 
1:q
2:w
3:e
4:r
5:t
:y