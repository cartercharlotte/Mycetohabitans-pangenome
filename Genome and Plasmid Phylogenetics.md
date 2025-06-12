# Mycetohabitans Genomes Phylogenetics

## ANI

I ran a FastANI analysis of relevant species from *Burkholderia* sensu lato with the *Mycetohabitans* genomes, including *Candidatus* Vallotia representatives.

The genomes I pulled from NCBI to be representative included:

- NZ_CP012981.1 Burkholderia cepacia ATCC 25416 strain UCB 717
- NZ_JFHC01000001.1 Caballeronia glathei strain DSM 50014 contig1
- NZ_CP047396.1 Candidatus Vallotia cooleyia isolate 19-005_Vallotia chromosome
- NZ_CP047399.1 Candidatus Vallotia lariciata isolate Ad13-081_Vallotia chromosome
- NZ_CP080504.1 Candidatus Vallotia sp. (ex Adelges kitamiensis) isolate Adelges kitamiensis 18-608 chromosome
- NZ_OU343031.1 Candidatus Vallotia tarda isolate MYVALT chromosome 1
- NZ_ABLD01000070.1 Paraburkholderia graminis C4D1M
- NZ_RBZU01000001.1 Pararobbsia silviterrae strain DHC34 scaffold1
- NZ_LAQU01000001.1 Robbsia andropogonis strain ICMP2807 contig00001
- NZ_PTIR01000001.1 Trinickia symbiotica strain JPY-345 Ga0139055_101

I copied the relavant *Mycetohabitans* fasta files into the FastANI directory and then used `ls *.fasta > FastANI_List.txt` to create a list file for running FastANI

FastANI_List.txt

```bash
B10_CF126_Msp_rot.fasta
B12.fasta
B13.fasta
B14.fasta
B203_CF131_Mrh_rot.fasta
B23_CF11_Mef_rot.fasta
B29_CF13_Med_rot.fasta
B2_CF67_Msp_rot.fasta
B34_CF12_Mrh_rot.fasta
B3.fasta
B46_CF71_Msp_rot.fasta
B47.fasta
B48_CF04_Mrh_rot.fasta
B49.fasta
B50_CF05_Mrh_rot.fasta
B514_CF135_Msp_rot.fasta
B51_CF06_Mef_rot.fasta
B52_CF07_Mrh_rot.fasta
B53_CF08_Mef_rot.fasta
B55_CF75_Mrh_rot.fasta
B58_CF10_Mrh_rot.fasta
B5.fasta
B60.fasta
B62_rot_final.fasta
B75_CF02_Mef_rot.fasta
B82_CF03_Mrh_rot.fasta
B8_CF80_Msp_rot.fasta
Burkholderia_cepacia_ATCC_25416.fasta
Caballeronia_glathei.fasta
Candidatus_Vallotia_cooleyia.fasta
Candidatus_Vallotia_lariciata.fasta
Candidatus_Vallotia_sp.fasta
Candidatus_Vallotia_tarda.fasta
GCA_000198775_B1.fasta
Paraburkholderia_graminis_C4D1M.fasta
Pararobbsia_silviterrae.fasta
Robbsia_andropogonis.fasta
Trinickia_symbiotica.fasta
```

FastANI.slurm submission script

```bash
#!/bin/bash
#SBATCH --job-name=FastANI
#SBATCH --partition=Orion
#SBATCH --ntasks=1
#SBATCH --nodes=1
#SBATCH --mem=4gb
#SBATCH --time=01:00:00

echo "======================================================"
echo "Start Time  : $(date)"
echo "Submit Dir  : $SLURM_SUBMIT_DIR"
echo "Job ID/Name : $SLURM_JOB_NAME"
echo "======================================================"
echo ""

module load gcc
cd /projects/carter_lab/Mycetohabitans/FastANI

/projects/carter_lab/bin/FastANI/build/fastANI --ql /projects/carter_lab/Mycetohabitans/FastANI/FastANI_List.txt --rl /projects/carter_lab/Mycetohabitans/FastANI/FastANI_List.txt -o /projects/carter_lab/Mycetohabitans/FastANI/FastANIBurk_All_010725.out 

```

I then moved the output over to R to be able to tidy up the visualization.

```r
library(ggplot2)
library(reshape2)
library(ggdendro)
library(viridis)
library(tidyr)
library(scales)
setwd()

#read in and format data
ANI_data <- read.table("FastANIBurk_All_010725.out", header=F, sep = "\t")
ANI_data <- ANI_data[,1:3] #first 3 columns
colnames(ANI_data)<- c("Strain1", "Strain2", "ANI")

#to get rid of extra text in sample names
sample.correct <- function(x) { 
  x<- gsub("genomes/", "", x)
  x<- gsub(".fna", "", x)
  x<- gsub(".fasta", "", x)
}
ANI_data[,1:2] <- lapply(ANI_data[,1:2], sample.correct)

#To get it to cluster similar strains
ANI_matrix <-dcast(ANI_data, Strain1~Strain2) %>% replace(is.na(.), 77)
ANI_dendro <- as.dendrogram(hclust(d = dist(x = ANI_matrix)))
ANI_order <- order.dendrogram(ANI_dendro)
ANI_plot_data <- ANI_matrix %>% melt(id.vars="Strain1", variable.name="Strain2", value.name="ANI")
ANI_plot_data$Strain1 <- factor(x = ANI_plot_data$Strain1,
                               levels = ANI_matrix$Strain1[ANI_order], 
                               ordered = TRUE)
ANI_plot_data$Strain2 <- factor(x = ANI_plot_data$Strain2,
                            levels = ANI_matrix$Strain1[ANI_order], 
                            ordered = TRUE)

#Making the plot (hashed out part was to add in rectangles and species names and would need to be adjusted for this data)
ANI_plot<- ggplot(ANI_plot_data, aes(x=Strain1, y=Strain2, fill= ANI))+
  geom_tile()+
  scale_fill_gradientn(colors=c("#EBEBEB","#94D1BE","#E9D8A6FF","#AF1F12"), values=rescale(c(75,80,90,100)), limits=c(75,100), name='% ANI')+
  theme(
    panel.background=element_blank(),
    axis.text.x=element_text(angle = 45, size=12, hjust=0.95),
    axis.title.x=element_blank(),
    axis.text.y=element_text(size=12),
    axis.title.y=element_blank(),
    #legend.key=element_blank(),     #removes the border
    legend.text=element_text(size=10),
    legend.title=element_text(size=14, face="bold"))+
  annotate("rect", xmin = 10.5, xmax = 27.5, ymin =10.5, ymax = 27.5,
     fill = "transparent", color="#CA6702FF", lwd=1, linetype = "dotted")+
  annotate("rect", xmin = 27.5, xmax = 36.5, ymin = 27.5, ymax = 36.5,
    fill = "transparent", color="#005F73FF", linetype = "dotted", lwd=1)
#annotate("text", x = 20.25, y = 27.75, label = "M. endofungorum", color="white", size=7, fontface = "italic")+
#annotate("text", x = 13.5, y = 1.5, label = "M. rhizoxinica", color="white", size=7, fontface = "italic")
ANI_plot

#histogram
ANI_plot_hist<- ggplot(ANI_data, aes(x=ANI, fill=after_stat(x))) +
  geom_histogram(binwidth=0.1, show.legend = FALSE)+
  scale_y_continuous(expand = c(0, 0), limits = c(0, 62))+
  scale_x_continuous(expand = c(0, 0), limits = c(77.2, 100))+
  #scale_fill_gradientn(name="ANI", colors=c("#E9D8A6FF","#EE9B00FF","#EBEBEB","#0A9396FF"), values=rescale(c(75,80,90,100)), limits=c(75,100))+
  scale_fill_gradientn(colors=c("#EBEBEB","#94D1BE","#E9D8A6FF","#AF1F12"), values=rescale(c(75,80,90,100)), limits=c(75,100), name='% ANI')+
  theme_minimal()+
  ylab("Number of Comparisons")+
  xlab("% ANI (binned)")+
  theme(
    panel.background =element_rect(fill="#00141A"),
    panel.grid.major = element_blank(),
    panel.grid.minor = element_blank(),
    axis.text.x=element_text(size=16, hjust=0.95),
    axis.title.x=element_text(size=18),
    axis.text.y=element_text(size=16),
    axis.title.y=element_text(size=18))+
  annotate("segment", 
           x = 94,
           xend=94,
           y=0, 
           yend= 62, 
           linetype = "dotted", 
           lwd=1,
           colour = "darkgrey")

ANI_plot_hist
```

## GTDB-Tk

I used the GTDB-Tk to do phylogenetic analysis of the Mycetohabitans within *Burkholderia* sensu lato. *Glomeribacter* and *Mycoavidus* were included because they are closely related and also endofungal bacteria. *Pandoraea* as included as an outgroup. 

```bash
#!/bin/bash
#SBATCH --job-name=GTDB-TK_de_novo_myc
#SBATCH --partition=Orion
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=16
#SBATCH --mem=48G
#SBATCH --time=01:00:00

echo "======================================================"
echo "Start Time  : $(date)"
echo "Submit Dir  : $SLURM_SUBMIT_DIR"
echo "Job ID/Name : $SLURM_JOB_NAME"
echo "======================================================"
echo ""

cd /projects/carter_lab/
module load gtdbtk
gtdbtk de_novo_wf --genome_dir /projects/carter_lab/Mycetohabitans/genomes/all_fasta --extension fasta --bacteria --taxa_filter g__Mycetohabitans,g__Burkholderia,g__Paraburkholderia,g__Caballeronia,g__Trinickia,g__Pararobbsia,g__Robbsia,g__Mycoavidus,g__Glomeribacter,g__Pandoraea,g__Chitinasiproducens --outgroup_taxon g__Pandoraea --out_dir /projects/carter_lab/Mycetohabitans/gtdbtk --cpus 16

echo "======================================================"
echo "Stop Time  : $(date)"
```

From GTDB-Tk: “The `infer` step uses [FastTree](http://www.microbesonline.org/fasttree/) with the WAG+GAMMA models to calculate independent, *de novo* bacterial and archaeal trees. These trees can then be rooted using a user specified outgroup and decorated with the GTDB taxonomy.”

To run only our genomes, add the flag **`--skip_gtdb_refs`** and remove the outgroup and taxa flags.

## Plasmid phylogeny

I pulled the parA sequences by hand from all the plasmid genbanks, because they were annotated too differently to use my `extract_gene.py` script (below). But it could be done by blast. I used the script to pull dnaA genes from the chromosomes.

```python
from Bio import SeqIO
from Bio.SeqRecord import SeqRecord
import os

def extract_gene_from_genbank(gene_name, genbank_files, output_fasta):
    with open(output_fasta, "w") as fasta_out:
        for gb_file in genbank_files:
            filename= os.path.basename(gb_file)
            for record in SeqIO.parse(gb_file, "genbank"):
                for feature in record.features:
                    if feature.type == "gene" and "gene" in feature.qualifiers:
                        if gene_name in feature.qualifiers["gene"]:
                            gene_seq = feature.extract(record.seq)
                            gene_record = SeqRecord(gene_seq, id=f"{record.id}_{filename}_{gene_name}", description=f"Location: {feature.location}")
                            SeqIO.write(gene_record, fasta_out, "fasta")
                            print(f"Gene {gene_name} found in {gb_file} and written to {output_fasta}")

# Example usage
with open("gb_files.txt") as f:
    genbank_files = [line.strip() for line in f]
gene_name = "dnaA"
output_fasta = "dnaA_genes.fasta"
extract_gene_from_genbank(gene_name, genbank_files, output_fasta)
```

^I used CoPilot to help come up with this script (in Visual Studio Code) and it is written for biopython.

I then used MEGAX to align the parA sequences with MUSCLE using default parameters.

I constructed a Maximum likelihood tree, with 1000 bootstraps and default parameters.

We exported the newick files from MEXGAX and used an R script to generate the trees facing each other and then we drew lines between them in (not shown).