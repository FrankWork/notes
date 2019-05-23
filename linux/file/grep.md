grep 'word' filename
grep 'word' file1 file2 file3
grep 'string1 string2'  filename
cat otherfile | grep 'something'
command | grep 'something'
command option1 | grep 'data'
grep --color 'data' fileName

grep '[a-zA-Z]'
grep '^\w$'
grep -e pattern 指定多个模式

匹配制表符 grep  '1'$'\t''2'
           grep  '1 2'  制表符的打法是ctrl-v + tab
           grep $'\t''1' tmp
           
次数匹配       grep 'a \{2,3\}b' 1 ---匹配2或3个空格
分组           grep '\(ab\)\{2,\}' 
        grep '\('$'\t''0\)\{100,\}' train.vec
        
