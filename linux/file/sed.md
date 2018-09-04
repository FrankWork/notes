sed -r 's/(@@ )|(@@ ?$)//g'
sed  's/oldStr/newStr/g'

sed -e 's/^/-1\t/g' 1w.txt > 1w.txt.fast