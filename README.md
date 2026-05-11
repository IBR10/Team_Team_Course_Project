# Team_Team_Course_Project


Course Project - GitHub Page: 
The final deliverable of your course project is your GitHub Page.  This will build substantially off of your team's submissions for the previous assignments.

The GitHub repository will contain two major elements. Note that these requirements are identical to those required for the video tutorial presentation, and you only need to make one set of materials.

README - your GitHub README will contain a full description of your team's project. The README will contain:

1. A description of a computational tool, its authors, its history, and a survey of the kinds of biological data this tool has been used to analyze in the past.

OrthoFinder is a comparative genomics program that starts with protein FASTA files and infers evolutionary relationships among genes across species.

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

3. A complete description of the mathematical or computational theory that the tool is based on (e.g., describe what statistical tools the package is implementing and why).

OrthoFinder combines sequence similarity, clustering, and phylogenetic interpretation.

First, it compares all input proteins against each other using a fast sequence search program, here DIAMOND. Second, it normalizes similarity scores to reduce gene length and evolutionary distance biases. Third, it builds a graph where genes are nodes and similarity relationships are weighted edges, then clusters that graph using MCL.

After orthogroup inference, OrthoFinder aligns genes in orthogroups, infers gene trees, infers a species tree, roots the tree using duplication information, and reconciles gene trees with the species tree. This lets it distinguish orthologs from paralogs.

4. A brief description of your Notebook tutorial that demonstrates how the chosen computational tools can be applied to the analysis of the biological phenomenon under investigation.



5. Presentation and discussion of a few results that your group has obtained by using the software package.  For example, you could demonstrate and explain results that you were able to reproduce from a publication using the software.



6. A summary and conclusion.



7. Bibliography and acknowledgements of any assistance you received in completing the project.

Emms, D. M. and Kelly, S. (2015). OrthoFinder: solving fundamental biases in whole genome comparisons dramatically improves orthogroup inference accuracy. *Genome Biology*, 16, 157. https://doi.org/10.1186/s13059-015-0721-2

Emms, D. M. and Kelly, S. (2019). OrthoFinder: phylogenetic orthology inference for comparative genomics. *Genome Biology*, 20, 238. https://doi.org/10.1186/s13059-019-1832-y

Emms, D. M., Liu, Y., Belcher, L., Holmes, J. and Kelly, S. (2025). OrthoFinder3. bioRxiv. https://doi.org/10.1101/2025.07.15.664860

OrthoFinder documentation: https://orthofinder.github.io/OrthoFinder/

OrthoFinder GitHub repository: https://github.com/OrthoFinder/OrthoFinder


The README could be done entirely in markdown, it could contain a series of slides or images that you create in PowerPoint, or some combination of the two.

Notebook - You will also create a Python notebook or set of Python scripts that demonstrate the program that you have researched.  This notebook should contain thorough explanation of the tools and discussion of the results.  This notebook can be adapted from existing online materials (with appropriate citations), but it must be modified to solve new problems of interest by your specific team.

Please note that the GitHub portion and the video tutorial are asking for nearly identical things. You are welcome to present your tutorial directly from your GitHub README or as a regular set of presentation slides.

Please make sure that the GitHub repository is clearly organized so that all materials needed for the tutorial are easy to find. The organization and usability of the repository will be a major aspect of the grade.
