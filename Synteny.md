# Synteny circos plot
colors.txt:
```
c2=rgb(1,95,116)
c6=rgb(240,156,0)
c8=rgb(175,31,18)
```
script to run syny:
```
path=/path/to/script
cd  $path
COLORS=path/to/script/inputs/colors.txt

#syny stuff
conda  init  bash
source  ~/.bashrc
conda  activate  syny

run_syny.pl  --annot  *.gbff \ #everything in input folder that ends with .gbff
 --evalue  1e-10  \ #alignment identity threshold
 --outdir  outputs  \
 --circos  all  \
 --label_size  80  \
 --no_ntbiases  --no_skews  --labels  names  \
 --custom_file  $COLORS
```
