交集

sort a.txt b.txt | uniq -d

并集

sort a.txt b.txt | uniq

差集a.txt-b.txt:

sort a.txt b.txt b.txt | uniq -u

