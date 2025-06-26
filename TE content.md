#TE percent finding
We used ISEScan to predict the % of genome masked by TEs. Since we use the UNC Charlotte HPC, we arrayed through the genome files to run the tool.
```
#!/bin/bash
#SBATCH --job-name=ISEScan_WG
#SBATCH --partition=Orion
#SBATCH --array=0-27
#SBATCH --cpus-per-task=4
#SBATCH --mem=8G
#SBATCH --time=06:00:00
#SBATCH --output=logs/isescan_%A_%a.out

path=/projects/carter_lab/Mycetohabitans/Pangenome/TE
cd $path

genome_list=genomes.txt
genome=$(sed -n "$((SLURM_ARRAY_TASK_ID + 1))p" $genome_list)
outdir=outputs/$genome

mkdir $outdir

isescan.py --seqfile $genome --output $outdir --nthread 4
```
