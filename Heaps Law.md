# Heap's Law 
Generate a presence/absence matrix from the [pangenome](https://github.com/cartercharlotte/Mycetohabitans-pangenome/blob/main/Pangenome%20creation%20pipeline.md).
```
anvi-script-gen-function-matrix-across-genomes --genomes-storage genomesdbs/GENOMES.db --annotation-source NCBI_PGAP --gene-caller NCBI_PGAP --output-file-prefix OutputFilePrefix
```
Creates 2 matrix files - frequency and presence/absence:
```bash
Functions across genomes (frequency) .........: <path>/OutputFilePrefix-FREQUENCY.txt
Functions across genomes (presence/absence) ..: <path>/OutputFilePrefix-PRESENCE-ABSENCE.txt
```
We use the presence/absence table and put it into R to create a rarefaction curve and generate alpha values
```r
library(dplyr)
library(tidyverse)
library(ggplot2)
library(vegan)

setwd("path to working directory")
genes_df <- read.delim("April21_WG-PRESENCE-ABSENCE.txt", header = TRUE, row.names = 1)
genes_pa_only <- genes_df[1:(length(genes_df)-1)]

set.seed(42)
accum_curve <- specaccum(t(genes_pa_only), method = "random", permutations = 1000)
genomes <- accum_curve$sites
unique_genes <- accum_curve$richness

# Fit Heap’s Law: G(N) = K * N^α
heap_model <- nls(unique_genes ~ K * genomes^alpha, 
                  start = list(K = max(unique_genes), alpha = 0.5))  # Initial guesses for K and α

# Extract fitted coefficients
heap_params <- coef(heap_model)
K_value <- heap_params["K"]
alpha_value <- heap_params["alpha"]

# Predict values for the fitted curve
fitted_values <- K_value * genomes^alpha_value

plot_data <- data.frame(Genomes = genomes, Unique_Genes = unique_genes, Fitted_Heap = fitted_values)

# Plot using ggplot2
plot <- ggplot(plot_data, aes(x = Genomes, y = Unique_Genes)) +
  geom_line(aes(y = Fitted_Heap), color = "#F09C00", size = 3) +  # Fitted Heap's Law curve
  geom_point(color = "#9B2226", size = 3) +  # Observed rarefaction points
  labs(x = "Number of Genomes", y = "Genes", 
       title = paste("Heap’s Law Fit (α = ", round(alpha_value, 2), ")", sep = "")) +
  theme_classic() +
  theme(
    axis.title = element_text(size = 40, face = "bold"),
    axis.text = element_text(size = 40, face = "bold"),
    axis.line = element_line(size = 2),
    plot.title = element_text(size = 40, face = "bold")
  )
plot

#ggsave("curve_final.png", plot = plot, width = 17, height = 10, units = "in", dpi = 500)
```
ChatGPT was used for writing the above code
