cat nohup.out | awk '{print $3 $9}' | grep 0.77

awk 'BEGIN{FS="\t"}{print $13}'

awk -v FS='\t' -v OFS='\t' '{print $3, $4}' test.txt
awk  -F ':'  '{print "filename:" FILENAME ",linenumber:" NR ",columns:" NF ",linecontent:"$0}' /etc/passwd


```
# 根据nid去重后，统计分类出现频次，按照频次降序输出，输出格式：分类\t频次

cat nid_subcate_att | awk -v FS='\t' -v OFS='\t' \
    '!nid[$1]++{cate_count[$2]+=1}END{for(cate in cate_count)
    print cate, cate_count[cate] | "sort -nr -k2"
}'

# 去除utf-8 BOM标记

awk '{if(NR==1)sub(/^\xef\xbb\xbf/,"");print}' INFILE > OUTFILE


#根据nid去重后，统计兴趣点出现频次，按照频次降序输出，输出格式：兴趣点\t频次


#wc -l nid_subcate_att

cat nid_subcate_att | awk -v FS='\t' -v OFS='\t' \
    '!nid[$1]++{split($3, atts, ";");for(i in atts) att_count[atts[i]]+=1
}END{
    for(att in att_count) print att, att_count[att] | "sort -k2nr -k1r"
}'

#根据nid去重后，统计共现频次最高的10000对兴趣点。降序输出，输出格式：兴趣点1\t兴趣点2\t频次

#wc -l nid_subcate_att

cat nid_subcate_att | awk -v FS='\t' -v OFS='\t' \
    '!nid[$1]++{n=split($3, atts, ";");
    asort(atts, atts_sorted);
    for(i in atts_sorted)
        for(j=i+1;j<=n;j++){
            p=atts_sorted[i]";"atts_sorted[j];
            pair_count[p]+=1;
    }
}END{
    for(pair in pair_count){
        split(pair, pa, ";");
        print pa[1], pa[2], pair_count[pair] | "sort -nr -k3nr -k1r";
    }
}' | head -n 10000


# 根据键值合并两个文件

awk  'BEGIN{FS=OFS=","}NR==FNR{a[$1]=$2}NR>FNR{print $1,a[$2]}' b.txt a.txt
FNR #已读入当前文件的记录数
NR  #已读入的总记录数

```
# 统计频率
awk 'BEGIN{FS=OFS="\t"}!nid[$1]++{freq[$2]+=1}END{for(key in freq) print key, freq[key] }' tmp.tsv
awk 'BEGIN{FS=OFS="\t"}{freq[$4]+=1}END{for(key in freq) print key, freq[key] }' tmp

# 排序
awk 'BEGIN{FS=OFS="\t"}NR==FNR{a[$1]=$0}NR>FNR{print a[$1]}' tmp sort.nid > tmp.tsv

# 求和
awk '{sum += $1};END {print sum}' test

# 删除某列

awk -F, '{$2=null;print $0}'

# 正则表达式

awk ‘/REG/{action}’
/REG/为正则表达式，可以将$0中，满足条件记录 送入到：action进行处理.

gawk 'match($0, /nid=(.+)/, a){print a[1]}' tmp 
