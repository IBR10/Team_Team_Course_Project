# Team_Team_Course_Project

1. A description of a computational tool, its authors, its history, and a survey of the kinds of biological data this tool has been used to analyze in the past.

OrthoFinder is a comparative genomics program that starts with protein FASTA files and infers evolutionary relationships among genes and across species.

The main outputs are orthogroups, orthologs, paralogs, gene trees, a species tree, and gene duplication statistics.

OrthoFinder was developed by David M. Emms and Steven Kelly. The original 2015 paper introduced OrthoFinder as a way to reduce major biases in whole genome orthogroup inference -- specifically, biases caused by gene length variation and uneven evolutionary distances across species, which plagued earlier tools. The 2019 paper expanded OrthoFinder into a phylogenetic orthology inference tool, adding the ability to reconcile gene trees with a species tree to distinguish orthologs from paralogs. What sets OrthoFinder apart from simpler clustering tools is this integration: it combines sequence similarity, statistical normalization, graph clustering, multiple sequence alignment, phylogenetic tree inference, and evolutionary reconciliation into a unified pipeline. The current OrthoFinder 3 series adds faster and more complete workflows, including hierarchical orthogroups for capturing nested ortholog relationships.

---

2. A summary and link to a step-by-step guide for the acquisition and installation of the program.

The installation of OrthoFinder is a simple string of Anaconda installation commands (presented below). Note: the current, most up-to-date version of OrthoFinder is OrthoFinder 3.1.4

### Installation Commands

    conda create -n of3_env python=3.12
    conda activate of3_env
    conda install -c bioconda -c conda-forge orthofinder pandas matplotlib ipykernel
    python -m ipykernel install --user --name of3_env --display-name "OrthoFinder 3.1.4 (of3_env)"
    orthofinder -v

### What Each Package Does

- **python=3.12**: OrthoFinder 3 requires Python 3.10 or newer for full compatibility.
- **orthofinder**: The main comparative genomics tool, installed from the bioconda channel where it is packaged with optimized dependencies.
- **pandas**: Used for data manipulation and table operations.
- **matplotlib**: Used to generate figures from analysis results.
- **ipykernel**: Registers the conda environment as a Jupyter kernel so we can use it in notebooks.

The bioconda and conda-forge channels provide pre-compiled binaries for biological tools like OrthoFinder and DIAMOND (the sequence search engine that OrthoFinder uses).

Link: https://orthofinder.github.io/OrthoFinder/download_and_install/

---

3. A complete description of the mathematical or computational theory that the tool is based on (e.g., describe what statistical tools the package is implementing and why).

OrthoFinder combines sequence similarity searching, statistical normalization, graph clustering, multiple sequence alignment, phylogenetic tree inference, and evolutionary reconciliation.

**Sequence Similarity and Normalization**: OrthoFinder compares all input proteins against each other using DIAMOND (orders of magnitude times faster than BLAST), a fast sequence search program that reports bit scores indicating sequence similarity. Raw bit scores are biased by gene length (longer proteins get higher scores) and evolutionary distance (more distant species have lower scores by default). OrthoFinder corrects these biases by normalizing scores using the "bit score per aligned length" metric, which makes cross-species comparisons more reliable.

**Graph Clustering with MCL**: After normalization, OrthoFinder constructs a graph where genes are nodes and normalized similarity scores are edge weights. This graph is then clustered using the Markov Cluster (MCL) algorithm, a method developed by Stijn van Dongen that simulates random walks on weighted graphs. MCL works by alternately expanding the transition matrix (spreading probability across edges) and inflating it (amplifying high-probability walks to favor strong clusters). This process identifies natural groups of highly similar genes—the orthogroups—without requiring a pre-specified number of clusters.

**Phylogenetic Tree Inference**: For each orthogroup, OrthoFinder aligns the member sequences using standard multiple sequence alignment methods, then infers a gene tree using maximum likelihood phylogenetics (typically with FastTree or IQ-TREE). Separately, OrthoFinder infers a species tree from the gene trees using a consensus approach.

**Gene Tree Reconciliation**: The final critical step is reconciling gene trees with the species tree using evolutionary reconciliation algorithms. This identifies which nodes in each gene tree represent speciation events (orthologs) versus duplication events (paralogs), enabling OrthoFinder to output precise ortholog relationships and duplication statistics. This reconciliation step is what distinguishes OrthoFinder from simpler sequence-similarity clustering tools.

### The Seven-Step Pipeline

1. **Sequence search**: All proteins in all input files are compared against each other using DIAMOND, producing a matrix of similarity scores.
2. **Normalization**: The similarity scores are normalized to correct for gene length and evolutionary distance biases.
3. **Orthogroup inference**: The normalized scores are used to construct a similarity graph, which is then clustered using the MCL algorithm to form orthogroups.
4. **Multiple sequence alignment**: Proteins in each orthogroup are aligned using standard alignment algorithms.
5. **Gene tree inference**: A phylogenetic tree is inferred for each orthogroup using maximum likelihood or similar methods.
6. **Species tree inference**: A species tree is inferred from the gene trees, representing the evolutionary relationships of the input species.
7. **Gene tree reconciliation**: The gene trees are compared to the species tree to identify orthologs, paralogs, and duplication events using reconciliation algorithms.

---

4. A brief description of your Notebook tutorial that demonstrates how the chosen computational tools can be applied to the analysis of the biological phenomenon under investigation.

Our notebook tutorial instructs how to install OrthoFinder and takes the example datasets provided for 4-6 different species of *Mycoplasma* (pathogenic bacteria with compact genomes and moderate evolutionary distance) and analyzes their orthological relations. The tutorial walks through the complete OrthoFinder workflow: loading protein FASTA files, running the analysis with 4 CPU cores, and interpreting the main output files. We examine orthogroups, pairwise ortholog tables, gene duplication events, and rooted species trees. The tutorial also demonstrates how adding more species (from 4 to 6) improves orthogroup assignment rates from 81.1% to 84.4% and provides richer evolutionary context. 

---

5. Presentation and discussion of a few results that your group has obtained by using the software package.  For example, you could demonstrate and explain results that you were able to reproduce from a publication using the software.

### Four-Species Dataset Results

By using the software package, we were able to extract orthological relations between the original four species of *Mycoplasma* explored, specifically discovering 599 orthogroups. Out of 2,733 genes analyzed, 2,216 were assigned to an orthogroup (81.1% assignment rate). The orthogroups ranged widely in size, with the largest ones representing species-specific gene expansions. We identified 95 gene duplication events across multiple nodes in the species tree. We generated a rooted species tree that groups *M. gallisepticum* with *M. genitalium* as one sister pair, and *M. hyopneumoniae* with *M. agalactiae* as another sister pair.

### Six-Species Dataset Results

To demonstrate how adding more related species affects the results, we expanded the analysis to include two additional *Mycoplasma* species (*M. arthritidis* and *M. haemocanis*) from the OrthoFinder example data. With six species and 4,385 total genes, OrthoFinder assigned 3,708 genes to 686 orthogroups (84.4% assignment rate). This comparison shows that species sampling can significantly affect orthogroup inference: the additional two species increased assignment rates by 3.3 percentage points and revealed 87 more orthogroups, providing richer evolutionary context for interpreting gene relationships.

---

6. A summary and conclusion.

OrthoFinder is a practical tool for comparative genomics because it turns protein FASTA files into evolutionary relationships among genes and species. For our tutorial dataset, it successfully assigned most genes into orthogroups and produced interpretable ortholog, duplication, and species tree outputs.

### Strengths

One major strength of OrthoFinder is that it is very straightforward to run. The input is simple: one protein FASTA file per species. From that, OrthoFinder produces many useful comparative genomics outputs including orthogroups, orthologs, gene trees, a species tree, and duplication statistics.

Another strength is that OrthoFinder uses evolutionary context. It does not only group genes based on sequence similarity; it also infers gene trees and a species tree, then reconciles them to distinguish orthologs (genes related by speciation) from paralogs (genes related by duplication).

### Weaknesses and Open Questions

A weakness is that the results depend on the quality of the input data. If the protein annotations are incomplete or inaccurate, the results may also be affected. Species sampling also matters, as we demonstrated when comparing the four-species and six-species datasets: adding just two more species increased orthogroup assignment by 3.3%.

Open questions for users include: How many species should be included for a strong analysis? When should users change default settings, such as the sequence search method or tree inference parameters? How do results change with very divergent species or with much larger datasets?

### Main Takeaway

OrthoFinder is most useful when the biological question is evolutionary: which genes are shared, duplicated, lost, or expanded across a set of species? The biggest takeaway is that OrthoFinder is not just a tool for grouping similar genes. It uses evolutionary information to help interpret gene relationships across species, making it useful for studying gene family evolution and comparing genomes.

---

7. Bibliography and acknowledgements of any assistance you received in completing the project.

Emms, D. M. and Kelly, S. (2015). OrthoFinder: solving fundamental biases in whole genome comparisons dramatically improves orthogroup inference accuracy. *Genome Biology*, 16, 157. https://doi.org/10.1186/s13059-015-0721-2

Emms, D. M. and Kelly, S. (2019). OrthoFinder: phylogenetic orthology inference for comparative genomics. *Genome Biology*, 20, 238. https://doi.org/10.1186/s13059-019-1832-y

Emms, D. M., Liu, Y., Belcher, L., Holmes, J. and Kelly, S. (2025). OrthoFinder3. bioRxiv. https://doi.org/10.1101/2025.07.15.664860

OrthoFinder documentation: https://orthofinder.github.io/OrthoFinder/

OrthoFinder GitHub repository: https://github.com/OrthoFinder/OrthoFinder

