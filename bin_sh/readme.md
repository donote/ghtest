### bash命令/工具使用记录

#### - awk命令

``` bash
# 1. 对文件随机取行
awk -vN=1000 -vC="`wc -l new.pass`" 'BEGIN{srand(); while(n<N){i=int(rand()*C+1); if(!(i in a)){a[i]++;n++}}} NR in a' filename

# 2. 找出url1和url2的交集/差集
awk 'NR==FNR {a[$1]=1} NR>FNR {if($1 in a){} else {print $0} }' url1 url2 > url

# 3. 统计相同的行
awk '{a[$1]++} END {for (j in a) print a[j],j}'

# 4. 按第一列去重
awk '{a[$1]=$0}; END{for(i in a) print a[i];}' sim.t


# 5. 变量递增
awk 'BEGIN{OFS="\t";lid=10001}{print lid++,0,$1}'

# 6. 统计
awk '{if($1<1000) {a[1]++} else if($1>=1000 && $1<2000){a[2]++} else {a[3]++} }END{for (j in a) print a[j],j}' sprint10_urls_labels.txt.sort


# 7. 求和
cat data | awk '{sum+=$1} END {print "Sum = ", sum}'

# 8. 输出除第一列外的其他列
awk '{for(i=2;i<=NF;++i) printf $i "\t";printf "\n"}' test.txt

# 9. 把文件的一列并到另一文件
awk -F'\t' 'BEGIN{i=0;j=0;} NR==FNR{a[++i]=$1;} NR>FNR {print a[++j]"\t"$0} END{}' predict_result short_64w.txt > short_64w.eval

# 参考：http://blog.csdn.net/shangboerds/article/details/49449291
# 10. 第三列包含字符串字段
awk -F'\t' '$3~/5858408/' bdy.ocr.format.txt

# 11. 求交集，ARGIND表示第几个文件，后面的-表示管道文件
awk -F"\t" '$2==1' ocr.result.1 | awk -F"\t" 'ARGIND==1{s[$1]}ARGIND==2{if($1 in s)print $0}' - bdy.ocr.format.txt > bdy.g.70
```

**awk内建变量**

- $0	当前记录（这个变量中存放着整个行的内容）
- $1~$n	当前记录的第n个字段，字段间由FS分隔
- FS	输入字段分隔符 默认是空格或Tab
- NF	当前记录中的字段个数，就是有多少列
- NR	已经读出的记录数，就是行号，从1开始，如果有多个文件话，这个值也是不断累加中。
- FNR	当前记录数，与NR不同的是，这个值会是各个文件自己的行号
- RS	输入的记录分隔符， 默认为换行符
- OFS	输出字段分隔符， 默认也是空格
- ORS	输出的记录分隔符，默认为换行符
- FILENAME	当前输入文件的名字


##### - bash命令

```
# 查找并替换文件的内容
find ./ -name *.conf | xargs sed -i 's/str01/str02/g'

# 或者使用shuf命令
shuf -n1000 filename
shuf filename

# 使用sed进行行输出, 输出10~20行，$表示最后行
sed -n '10, 20p' filename
sed -n '10, $p' filename
```