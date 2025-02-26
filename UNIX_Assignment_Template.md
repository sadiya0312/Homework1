#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes`

```

head -n 5 fang_et_al_genotypes.txt
vim fang_et_al_genotypes.txt
:set nowrap


By inspecting this file I learned that:

1. It has a header
2. It is tab delimited
3. First collumn is sample_id and third is group


###Attributes of `snp_position.txt`

```
head -n 5 snp_position.txt
vim snp_position.txt
:set nowrap

By inspecting this file I learned that:

1. It has a header
2. It is tab delimited
3. SNP_ID is the first column and Chromosome is the third column.



##Data Processing

tail -n +3 transposed_genotypes.txt > transposed_oneheader.txt
sed 's/Group/SNP_ID/g' transposed_oneheader.txt | head -n -1 > transposed_changedhead.txt
ll
vim transposed_changedhead.txt
join -1 1 -2 1 snp_position.txt transposed_changedhead.txt > joined_oneheader.txt
cut -d $' ' --complement -f2 joined_oneheader.txt > seqcol.txt
 vim seqcol.txt
 seqcol.txt > joined_seqcol.txt
 mv seqcol.txt > joined_seqcol.txt

 1. transposed_genotypes.txt had 3 headers, removed 2 headers
 2. Joined snp_position.txt with transposed_genotypes.txt
 3. Removed the second collumn from the joined file since its not required
 4. joined_seqcol.txt is the main file from where we will work

###Maize Data
Maize data is found in folder maize

```
head -n1 joined_seqcol.txt | tr ' ' '\n' | nl | grep "ZMMIL" > maize/ZMMIL.txt
head -n1 joined_seqcol.txt | tr ' ' '\n' | nl | grep "ZMMLR" > maize/ZMMLR.txt
head -n1 joined_seqcol.txt | tr ' ' '\n' | nl | grep "ZMMMR" > maize/ZMMMR.txt
cut -d $' ' -f1,2,3,2507-2796,1224-2479,2480-2506 joined_seqcol.txt > maize_data.txt
( head -n 1 maize_data.txt && tail -n +2 maize_data.txt | sort -k2,2n ) > sort_maize.txt
for i in {1,2,3,4,5,6,7,8,9,10}; do     grep -P "^\S+\s+$i\s" sort_maize.txt > ch$i.txt;     cat head.txt ch$i.txt > chromosome_$i.txt; done
mv ch1.txt ch2.txt ch3.txt ch4.txt ch5.txt ch6.txt ch7.txt ch8.txt ch9.txt ch10.txt inter_file/
mkdir sort_increase
mkdir sort_decrease
for i in {1,2,3,4,5,6,7,8,9,10}; do  sort -k3,3n chromosome_i.txt > sort_increase/ch_in_i.txt; sort -k3,3nr chromosome_i.txt > sort_decrease/ch_in_i.txt; done
for i in {1,2,3,4,5,6,7,8,9,10}; do  sort -k3,3n chromosome_$i.txt > sort_increase/ch_in_$i.txt; sort -k3,3nr chromosome_$i.txt > sort_decrease/ch_in_$i.txt; done
grep -P "^\S+\s+"unknown"\s" sort_maize.txt > inter_file/ch_unknown.txt;cat head.txt inter_file/ch_unknown.txt > chromosome_unknown.txt;
grep -P "^\S+\s+"multiple"\s" sort_maize.txt > inter_file/ch_multiple.txt;     cat head.txt inter_file/ch_multiple.txt > chromosome_multiple.txt;
```

1. Extracted collumn numbers for each group
2. Extracted all collumns with those collumn numbers in maize.txt
4. Sorted Maize.txt to sort_maize.txt
5. For loop to extarct rows for each chromosomes.(chromosome_$i.txt)
6. For loop to sort each chromosome file in increasing and decresing order.
7. Grep unknow and multiple chromosomes in different files.


###Teosinte Data
Teosinte data is found in folder teosinte
```
head -n1 joined_seqcol.txt | tr ' ' '\n' | nl | grep "ZMPBA" > teosinte/ZMPBA.txt
head -n1 joined_seqcol.txt | tr ' ' '\n' | nl | grep "ZMPIL" > teosinte/ZMPIL.txt
head -n1 joined_seqcol.txt | tr ' ' '\n' | nl | grep "ZMPJA" > teosinte/ZMPJA.txt
cut -d $' ' -f1,2,3,88-987,1177-1217,988-1021 joined_seqcol.txt > teosinte/teosinte_data.txt
( head -n 1 teosinte_data.txt && tail -n +2 teosinte_data.txt | sort -k2,2n ) > sort_teosinte.txt
for i in {1,2,3,4,5,6,7,8,9,10}; do     grep -P "^\S+\s+$i\s" sort_teosinte.txt > ch$i.txt;     cat head.txt ch$i.txt > chromosome_$i.txt; done
mv ch1.txt ch2.txt ch3.txt ch4.txt ch5.txt ch6.txt ch7.txt ch8.txt ch9.txt ch10.txt inter_file/
mkdir sort_increase
mkdir sort_decrease
for i in {1,2,3,4,5,6,7,8,9,10}; do  sort -k3,3n chromosome_i.txt > sort_increase/ch_in_i.txt; sort -k3,3nr chromosome_i.txt > sort_decrease/ch_in_i.txt; done
for i in {1,2,3,4,5,6,7,8,9,10}; do  sort -k3,3n chromosome_$i.txt > sort_increase/ch_in_$i.txt; sort -k3,3nr chromosome_$i.txt > sort_decrease/ch_in_$i.txt; done
grep -P "^\S+\s+"unknown"\s" sort_teosinte.txt > inter_file/ch_unknown.txt;cat head.txt inter_file/ch_unknown.txt > chromosome_unknown.txt;
grep -P "^\S+\s+"multiple"\s" sort_teosinte.txt > inter_file/ch_multiple.txt;     cat head.txt inter_file/ch_multiple.txt > chromosome_multiple.txt;

```

 Extracted collumn numbers for each group
2. Extracted all collumns with those collumn numbers in teosinte.txt
4. Sorted Maize.txt to sort_teosinte.txt
5. For loop to extarct rows for each chromosomes.(chromosome_$i.txt)
6. For loop to sort each chromosome file in increasing and decresing order.
7. Grep unknow and multiple chromosomes in different files.
