## Immune Deconvolution

**Module authors:** Komal Rathi ([@komalsrathi](https://github.com/komalsrathi))

### Description

The goal of this analysis is to use the R package `immunedeconv` to quantify and compare various immune cell types in the tumor microenvironment (TME) across various PBTA histologies. 
The package `immunedeconv`, provides six deconvolution (and similar) methods: xCell (n = 64; immune and non-immune cell types), CIBERSORT (n = 22; with and without absolute mode), TIMER (n = 6), EPIC (n = 6), quanTIseq (n = 10) and MCP-Counter (n = 8). 

### Method selection

We chose xCell as the method of choice because it: 
1) is the most comprehensive deconvolution method and is able to deconvolute the maximum number of immune and non-immune cell types 
2) is highly robust against background predictions and 
3) can reliably identify the presence of immune cells at low abundances (0-1% infiltration depending on the immune cell type).

xCell outputs immune scores as arbitrary scores that represent cell type abundance. 
Importantly, these scores may be compared between samples (inter-sample comparisons), but _may not_ be compared across cell types or cancer types, as described in the [`immunedeconv` documentation](https://icbi-lab.github.io/immunedeconv/articles/immunedeconv.html#interpretation-of-scores). This is in part because xCell is actually a signature-based method and not a deconvolution method, as is described in the [xCell Publication](https://doi.org/10.1186/s13059-017-1349-1):
> Unlike signature-based methods, which output independent enrichment scores per cell type, the output from deconvolution-based methods is the inferred proportions of the cell types in the mixture.


### Analysis scripts

#### 01-immune-deconv.R

1. Inputs from data download

```
pbta-gene-expression-rsem-fpkm-collapsed.polya.rds
pbta-gene-expression-rsem-fpkm-collapsed.stranded.rds
```

2. Function

This script deconvolutes immune cell types using `xCell`.

3. Output: 

`results/deconv-output.RData`

The results in the RData object are predicted immune scores per cell type per input sample. 
These scores are not actual cell fractions but arbitrary scores which can be compared within samples, across samples and/or between various cancer types. 
Depending on the user requirement, the output can be used to create various visualizations. 


### Running the analysis

```sh
bash run-immune-deconv.sh
```



