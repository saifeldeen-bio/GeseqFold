# GeSeqFold
GeSeqFold is a robust tool designed to process transcriptomic data and perform differential gene expression analysis using linear models. It aims to provide researchers with a streamlined, efficient way to analyze RNA-seq data, delivering clear insights into gene expression changes under various conditions. Ideal for both novice and experienced researchers, GeSeqFold ensures accurate and insightful analysis of transcriptomic datasets.

**Installation:**

```bash
git clone https://github.com/saifeldeen-bio/GeSeqFold.git
cd GeSeqFold/
sudo mv GenomeScratch ../path-to/usr/bin
```
**Usage:**

```
Usage: GeSeqFold -h [manual] -c <Count Matrix> -m <Meta Data> -fl <Filtration Level> -g1 <Group 1> -g2 <Group 2> -fdr <FDR Cutoff> -ng <nGenes> -hm <HeatMap Metric> -o <Output Dir>
```

**Parameters:**
- `<Count Matrix>`: Count matrix [File: Must be in a tsv or a csv format].
- `<Meta Data>`: Meta data consisting of two columns 'SAMPLE and STATE' [File: Must be in a tsv or a csv format] .
- `<Filtration Level>`: Pre filtration level to filter low expressed genes which make outliers in the Data [Int: 10, 20, 30].
- `<Group 1>`: The first or refrence group of samples in the experimental design [Str: Control, Normal, Treatment1,..].
- `<Group 2>`: The second group of samples in the meta data experimental design [Str: Disease, Infection, Treatment2,..].
- `<FDR cutoff>`: The level of significance utilized in the Analysis [Float: 0.05, 0.01].
- `<nGenes>`: The number of significant genes to visualize [int: 100, 200, ....].
- `<HeatMap Metric>`: The HeatMap Metric used in the HeatMap [Str: euclidean, correlation].
- `<Output Dir>`: Output directory.

**Example Usage:**
```bash
GeSeqFold -c PRJNA880891.tsv -m META.csv -fl 10 -g1 Control -g2 Salinity -fdr 0.05 -ng 100 -hm euclidean --out results
```
# Input format
**Count Matrix Format:**
The count matrix should be provided in either CSV (Comma-Separated Values) or TSV (Tab-Separated Values) format. Each row in the matrix represents a feature (e.g., gene, transcript), and each column represents a sample. Here is an example:
```
Genes,Sample1,Sample2,Sample3
Gene1,10,15,20
Gene2,5,8,12
Gene3,NA,6,10
```
**Metadata Format**:
The metadata should also be provided in either CSV (Comma-Separated Values) or TSV (Tab-Separated Values) format. This file should contain two columns: SAMPLE and STATE. The SAMPLE column should list the sample names in the same order as they appear in the count matrix. The STATE column should specify the group or category to which each sample belongs. Here is an example:
```
SAMPLE,STATE
Sample1,Control
Sample2,Treatment
Sample3,Control
```
**Authorship:**
© Saifeldeen M. Ibrahim 2024
