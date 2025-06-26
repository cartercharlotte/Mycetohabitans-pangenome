# Pangenome creation pipeline

## Step1: [`anvi-script-process-genbank`](https://anvio.org/help/main/programs/anvi-script-process-genbank/)

We choose to use our own annotated GenBank files. Hence, before beginning the textbook Anvi’o workflow, this additional step of **telling Anvi’o that we will use .gbk/.gb files instead of .fa/.fasta files.**

```bash
#go to file where the genomes are (change based on your file location)
path=`pwd`
cd $path

#make a text file gbks.txt listing all .gb files in that location
ls *.gb $path/genbanks > $path/genbanks/genbank_filelist.txt

#make directories for output files created by this code
mkdir genecalls
mkdir functions
mkdir fastas

#run "anvi-script-process-genbank" on all files listed in genbank_filelist.txt
for sample in `cat $path/genbanks/genbank_filelist.txt`
do
anvi-script-process-genbank  -i  $path/genbanks/$sample  \ #input files
--output-fasta  $path/fastas/${sample:0:-3}.fa  \ #output fastas; saving everything in the filename except the ".gb"
--output-gene-calls  $path/genecalls/${sample:0:-3}.txt  \ 
--output-functions  $path/functions/${sample:0:-3}.txt
done
```

## Step2: [`anvi-gen-contigs-database`](https://anvio.org/help/7/programs/anvi-gen-contigs-database/)
```bash
cd $path/fastas
ls *.fa > fasta_filelist.txt

#fix our fastas to only have nucleotides and not weird characters
for file in `cat $path/fastas/fasta_filelist.txt`
do
	anvi-script-reformat-fasta  --seq-type  NT  \ #specifying the sequence type to nucelotide
	$path/fastas/$file  \ #input fasta file
	--overwrite-input  \ #doesn't create new files, instead overwrites the source fastas
	--prefix  ${file:0:-3} #Adding the filename as the prefix to fasta headers for easier future handling of entries using ${file:0:-3} removes the last ".fa" part
done

#make a directory for contig-db files to go into
mkdir $path/contigdbs

#the fastas are ready to be made into contig-db
for file in `cat $path/fastas/fasta_filelist.txt`
do
    anvi-gen-contigs-database -f $path/chr-fasta/$file \ #input fasta file
    -n ${file} \ #"name" of the job being set same as the filename
    -o $path/contigdbs/${file}.db \ #output filename with the extension .db
    --external-gene-calls $path/genecalls/${file:0:-3}.txt #specifying that the annotations come from the genecalls we generated from genbanks in previous steps and the files are not to be annotated by anvio
done
```

## Step 3: Import functions from the functions directory and other sources
```bash
path=`pwd`

cd  $path/contigdbs
ls  *.db  >  contigdb_filelist.txt

#setting up the extra functional annotation sources
mkdir $path/setups
anvi-setup-scg-taxonomy  --scgs-taxonomy-data-dir  $path/setups/scg_setup  --reset
anvi-setup-kegg-data  --kegg-data-dir  $path/setups/kegg_setup
anvi-setup-modelseed-database  --dir  $path/setups/modelseed_setup

for  file  in  `cat  $path/contigdbs/contigdb_filelist.txt`
do
	anvi-run-hmms  -c  $path/contigdbs/$file
	anvi-run-scg-taxonomy  -c  $path/contigdbs/$file  --scgs-taxonomy-data-dir  $path/setups/scg_setup
	anvi-scan-trnas  -c  $path/contigdbs/$file
	anvi-import-functions  --contigs-db  $path/contigdbs/$file  -i  $path/functions/${file:0:-3}.txt #from functions directory
	anvi-run-kegg-kofams  --contigs-db  $path/contigdbs/$file  --kegg-data-dir  $path/setups/kegg_setup 
	anvi-reaction-network  -c  $path/contigdbs/$file  --ko-dir  $path/setups/kegg_setup  --modelseed-dir  $path/setups/modelseed_setup
	#any of these can be split into threads using --num-threads x
done

#to check scg, trna and hmm annotations for the contigdbs, the following command can be used
cd $path/contigdbs
anvi-display-contigs-stats --report-as-text -o chr-contigstats.txt *db
```

## Step 4: Make genome storage databases
```bash
path=`pwd`
cd  $path
mkdir  genomesdbs

anvi-script-gen-genomes-file  --input-dir  $path/contigdbs  -o  $path/genomesdbs/external-genomes.txt

anvi-gen-genomes-storage  -e  $path/genomesdbs/external-genomes.txt  -o  $path/genomesdbs/GENOMES.db  --gene-caller  NCBI_PGAP #specifying gene caller here
```

## Step 5: Create the pangenome
```bash
path=`pwd`
cd  $path

anvi-pan-genome -g $path/genomesdbs/GENOMES.db \ #genomes storage database
--project-name Project_Name \ #giving the pangenome a meaningful name
--num-threads 4 

anvi-compute-genome-similarity  --external-genomes  $path/genomesdbs/external-genomes.txt  \ #external genomes table created in the previous step
--program  fastANI  \ #choice of ANI program
--output-dir  $path/ANI  \
--num-threads  4  \
--pan-db  $path/ProjectName/ProjectName-PAN.db #what the pangenome gets saved as
```
To view the pangenome, run this command in your terminal:
```bash
anvi-display-pan  -p  ProjectName/ProjectName-PAN.db  -g  genomesdbs/GENOMES.db
```
