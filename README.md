# GeseqFold
GeseqFold is a tool processes transcriptomic data and conducts differential gene expression analysis using the ordinary least squares (OLS) regression model. It accepts input data in TSV or CSV format, ensuring compatibility with most RNA-seq datasets. Users can specify experimental groups, adjust parameters for data filtration and significance thresholds, fit a linear model for each gene using OLS regression, calculate p-values for differential expression, and apply multiple testing correction using the Benjamini-Hochberg method to control the false discovery rate, ensuring the reliability of identified differentially expressed genes (DEGs).
PS: GeSeqFold currently works with two conditions or treatments (e.g., control and treatment) and applies CPM normalization. Support for multiple factors and additional normalization methods will be available in the next release..

**Installation:**

```bash
git clone https://github.com/saifeldeen-bio/GeseqFold.git
cd GeseqFold/
sudo mv GeseqFold ../path-to/usr/bin
```
**Usage:**

```
Usage: GeseqFold -h [manual] -c <Count Matrix> -m <Meta Data> -fl <Filtration Level> -g1 <Group 1> -g2 <Group 2> -fdr <FDR Cutoff> -ng <nGenes> -hm <HeatMap Metric> -o <Output Dir>
```

**Parameters:**
- `<Count Matrix>`: Count matrix [File: Must be in a tsv or a csv format].
- `<Meta Data>`: Meta data consisting of two columns 'SAMPLE and STATE' [File: Must be in a tsv or a csv format] .
- `<Filtration Level>`: Pre filtration level to filter low expressed genes which make outliers in the Data [Int: 10, 20, 30].
- `<Group 1>`: The first or refrence group of samples in the experimental design [Str: Control, Normal, Treatment1,..].
- `<Group 2>`: The second group of samples in the experimental design [Str: Disease, Infection, Treatment2,..].
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

# Outputs
**Density plot:** 
show how gene expression counts are distributed across samples. it reveals patterns like the most common expression level, how spread out the values are, and any imbalances.

![image](https://github.com/saifeldeen-bio/GeSeqFold/assets/75811385/926016ba-8944-4184-8b00-1696c1554ca8)

**Box plot** 
summarize gene expression distributions for different samples. it shows the median (center), quartiles (spread), and potential outliers, allowing quick comparisons of expression patterns between conditions or samples.

![image](https://github.com/saifeldeen-bio/GeSeqFold/assets/75811385/ec609362-aca5-483a-af53-c52c98efe2f9)

**Heatmap** 
visualize expression levels of genes across samples. it uses the color intensity to represent expression values, with red typically indicating high expression and blue low expression.

![image](https://github.com/saifeldeen-bio/GeSeqFold/assets/75811385/3dad62cd-48b6-4e9f-9ed8-10817574c658)

**Volcano plot** combines the statistical significance with fold change. Each dot represents a gene, with the x-axis showing fold change (up or down regulation) and the y-axis showing the strength of that change (often minus log10 p-value).

![image](https://github.com/saifeldeen-bio/GeSeqFold/assets/75811385/fa1c911f-7dcb-4807-a4f8-f3b094732e64)

**Multidimensional Scaling (MDS)** 
It is a dimensionality reduction technique. It takes high-dimensional gene expression data and projects it onto a lower-dimensional space (often 2 or 3 dimensions) for visualization

![image](https://github.com/saifeldeen-bio/GeSeqFold/assets/75811385/cf660814-b54d-42b4-98e4-d6a3356fc47c)

**Principal Component Analysis (PCA)** 
It is another dimensionality reduction technique. Similar to MDS, it takes the high-dimensional gene expression data and condenses it into a lower-dimensional space (typically 2 or 3 principal components) for visualization. PCA focuses on capturing the most significant sources of variation in the data. 

![image](https://github.com/saifeldeen-bio/GeSeqFold/assets/75811385/3a418555-2f87-431f-bb78-cf0a0165adce)

**The Differential Gene Expression table** 
It is the core output of a differential expression analysis. It's a spreadsheet-like table summarizing key statistics for each gene compared between conditions

```
Genes,pvalue,log2FoldChange,FDR,exp.direction,software
LOC4332737,1.0273168267658248e-11,-7.029383551174482,2.4409047803956e-07,down,GeseqFold
LOC112939081,6.49384435627295e-11,-4.817655155020523,4.555769626842574e-07,down,GeseqFold
LOC4331849,5.956382883264818e-11,4.697528599519424,4.555769626842574e-07,up,GeseqFold
```







**Authorship:**
© Saifeldeen M. Ibrahim 2024
