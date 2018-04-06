cat nohup.out | awk '{print $3 $9}' | grep 0.77

awk 'BEGIN{FS="\t"}{print $13}'
