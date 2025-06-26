# TE percent finding
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
Then R script used to plot correlation between TE% and Pseudogene%
```r
library(ggplot2)
library(readxl)
setwd("path/to/excel/file")
plot(df$TE, df$Pseudo,
     xlab = "TE",
     ylab = "Pseudo",
     main = "Correlation between TE% and ")
abline(lm(TE ~ Pseudo, data = df), col = "#9B2226")

correlation <- cor(df$TE, df$Pseudo, method = "pearson", use="complete.obs")

text(0.1, 0.9, paste("Correlation:", round(correlation, 2)), pos = 4, cex = 1.2)
ggplot(df, aes(x = TE, y = Pseudo)) +
  geom_point(color = "#F09C00", size =4) +
  geom_smooth(method = "lm", se = FALSE, color = "#9B2226", size = 3) +
  labs(x = "Percentage of TE", y = "Percentage of Pseudogenes") +
  scale_x_continuous(limits = c(1, 7)) +
  scale_y_continuous(limits = c(6, max(df$Pseudo, na.rm = TRUE))) +
  annotate("text", x = Inf, y = -Inf, label = paste("r =", correlation),
           hjust = 1.1, vjust = -1.1, size = 10) +
  theme_classic() +
  theme(
    legend.position = "none",
    axis.title.x = element_text(size = 30, color = "black"),
    axis.title.y = element_text(size = 30, color = "black"),
    axis.text.x = element_text(size = 30, hjust = 0.5, color = "black"),
    axis.text.y = element_text(size =30, color = "black", vjust = 0.6), 
    axis.line = element_line(size = 1.2, color = "black"),  # thickness here
    axis.ticks = element_line(size = 1.2, color = "black")  # thickness here
  )

ggsave("TE_Pseudo_Correlation.png", width = 10, height = 10, dpi = 300)

```
