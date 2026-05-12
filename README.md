# Team_Team_Course_Project

1. A description of a computational tool, its authors, its history, and a survey of the kinds of biological data this tool has been used to analyze in the past.

OrthoFinder is a comparative genomics program that starts with protein FASTA files and infers evolutionary relationships among genes and across species.

The main outputs are orthogroups, orthologs, paralogs, gene trees, a species tree, and gene duplication statistics.

OrthoFinder was developed by David M. Emms and Steven Kelly. The original 2015 paper introduced OrthoFinder as a way to reduce major biases in whole genome orthogroup inference. The 2019 paper expanded OrthoFinder into a phylogenetic orthology inference tool. The current OrthoFinder 3 series adds faster and more complete workflows, including hierarchical orthogroups.

2. A summary and link to a step-by-step guide for the acquisition and installation of the program.

The installation of OrthoFinder is a simple string of Anaconda installation commands (presented below). Note: the current, most up-to-date version of OrthoFinder is OrthoFinder 3.1.4

Installation commands:

    conda create -n of3_env python=3.12
    conda activate of3_env
    conda install -c bioconda -c conda-forge orthofinder pandas matplotlib ipykernel
    python -m ipykernel install --user --name of3_env --display-name "OrthoFinder 3.1.4 (of3_env)"
    orthofinder -v

Link: https://orthofinder.github.io/OrthoFinder/download_and_install/

3. A complete description of the mathematical or computational theory that the tool is based on (e.g., describe what statistical tools the package is implementing and why).

OrthoFinder combines sequence similarity, clustering, and phylogenetic interpretation.

First, it compares all input proteins against each other using a fast sequence search program, here DIAMOND. Second, it normalizes similarity scores to reduce gene length and evolutionary distance biases. Third, it builds a graph where genes are nodes and similarity relationships are weighted edges, then clusters that graph using MCL.

After orthogroup inference, OrthoFinder aligns genes in orthogroups, infers gene trees, infers a species tree, roots the tree using duplication information, and reconciles gene trees with the species tree. This lets it distinguish orthologs from paralogs.

4. A brief description of your Notebook tutorial that demonstrates how the chosen computational tools can be applied to the analysis of the biological phenomenon under investigation.

Our notebook tutorial instructs how to install orthofinder and takes the example datasets provided for 4-6 different species of mycoplasma and several different gene sequences (very large datasets) and analyzes their orthological relations, including orthogroups, phylogenetic trees, speciation events, etc. 

5. Presentation and discussion of a few results that your group has obtained by using the software package.  For example, you could demonstrate and explain results that you were able to reproduce from a publication using the software.

By using the software package, we were able to extract orthological relations between the original four species of mycoplasma explored, specifically discovering 599 orthogroups, with 274 orthogroups containing all four species. Out of 2733 genes analyzed, 2216 were assigned to an orthogroup (81.1%). We were also able to generate rooted species trees to group *M. gallisepticum* with *M. genitalium* and *M. hyopneumoniae* with *M. agalactiae*.

6. A summary and conclusion.

OrthoFinder is a practical tool for comparative genomics because it turns protein FASTA files into evolutionary relationships among genes and species. For our tutorial dataset, it successfully assigned most genes into orthogroups and produced interpretable ortholog, duplication, and species tree outputs.

The main takeaway is that OrthoFinder is most useful when the biological question is evolutionary: which genes are shared, duplicated, lost, or expanded across a set of species?

7. Bibliography and acknowledgements of any assistance you received in completing the project.

Emms, D. M. and Kelly, S. (2015). OrthoFinder: solving fundamental biases in whole genome comparisons dramatically improves orthogroup inference accuracy. *Genome Biology*, 16, 157. https://doi.org/10.1186/s13059-015-0721-2

Emms, D. M. and Kelly, S. (2019). OrthoFinder: phylogenetic orthology inference for comparative genomics. *Genome Biology*, 20, 238. https://doi.org/10.1186/s13059-019-1832-y

Emms, D. M., Liu, Y., Belcher, L., Holmes, J. and Kelly, S. (2025). OrthoFinder3. bioRxiv. https://doi.org/10.1101/2025.07.15.664860

OrthoFinder documentation: https://orthofinder.github.io/OrthoFinder/

OrthoFinder GitHub repository: https://github.com/OrthoFinder/OrthoFinder

