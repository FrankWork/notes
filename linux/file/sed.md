sed -r 's/(@@ )|(@@ ?$)//g'
sed  's/oldStr/newStr/g'

替换 		sed -e 's/^/-1\t/g' 1w.txt > 1w.txt.fast
删除空行 	sed  '/^$/d' head.txt
