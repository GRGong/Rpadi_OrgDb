# Rpadi_OrgDb

## About the Database

The database has been updated! It now includes annotations performed using **FANTASIA** (12,698 genes assigned), **patched with NCBI-specific annotations** (351 genes assigned).  

- **NOTE:** FANTASIA tends to assign a gene to more GO terms, so the results may differ significantly from the previous NCBI-only annotations.

You can find the updated database and files at the following links:

- [Download updated OrgDb](https://drive.google.com/file/d/1Q8LY-uPVpm6F1UWzjZr-9DwoEJHFzrTP/view?usp=sharing)
- [Download TopGO format file](https://github.com/GRGong/Rpadi_OrgDb/raw/refs/heads/main/fantasia.patched_ncbi.topgo.txt.gz)

### Installation Instructions

1. **Download and Install the OrgDb Database**  
   First, download the `.tar.gz` file from the link above. After downloading, decompress the file (`tar -zxvf org.Rpadi.eg.db.tar.gz`) and install the database in R using the following command:

   ```r
   install.packages("PATH_TO/org.Rpadi.eg.db", repos = NULL, type = "source", force = TRUE)

2. **Install clusterProfiler**
   To use the clusterProfiler package, install it by running the following commands in R:

   ```r
   if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
   BiocManager::install("clusterProfiler")

**Example**

Once the database and clusterProfiler are installed, you're ready to perform GO enrichment analysis. Below is an example:

```r
library(clusterProfiler)
library(org.Rpadi.eg.db)

# Example gene list
genes <- c("LOC132916914", "LOC132916961", "LOC132917061", "LOC132917063", 
           "LOC132917180", "LOC132917253", "LOC132917261", "LOC132917313", 
           "LOC132917323")

# Perform GO enrichment analysis
go_results <- enrichGO(genes, keyType = "GID", OrgDb = "org.Rpadi.eg.db", ont = "ALL", pAdjustMethod = "BH")

# Visualize the results
dotplot(go_results)
barplot(go_results)
