# PETfold-container
This repository contains a Singularity container for:

- **PETfold** (version 2.2) performs Probabilistic Evolutionary and Thermodynamic folding of a multiple alignment of RNA sequences.
- **PETcofold** (verison 3.3) is an integrated framework with PETfold to fold and search for RNA-RNA interactions between two multiple alignments of RNA sequences.

When using these tools, please cite:

S.E. Seemann, A.S. Richter, J. Gorodkin, et al. **"Hierarchical folding of multiple sequence alignments for the prediction of structures and RNA-RNA interactions."** Algorithms Mol Biol 5, 22 (2010). https://doi.org/10.1186/1748-7188-5-22

S.E. Seemann, J. Gorodkin, R. Backofen. **"Unifying evolutionary and thermodynamic information for RNA folding of multiple alignments."**, Nucleic Acids Research, Volume 36, Issue 20, (2008), https://doi.org/10.1093/nar/gkn544

## How to use the container


We confirm that the container of this repository works with singularity with the following steps:

1. Download the container

    > singularity pull oras://ghcr.io/asgeissler/petfold:2.2

2. Run the tool within the container, for example for PETfold:

    > ls
    input-alignment.fna
    > singularity exec                                        \
        `# bind current directory to be visible by container` \
         -B $PWD:$PWD  petfold_2.2.sif                        \
        `# run tool from the container, eg PETfold`           \
        PETfold --fasta input-alignment.fna > output.txt
    > ls
    input-alignment.fna         output.txt

Note, thank to the  Open Container Initiative (OCI) and it's ORAS tool, this container should be able to be used by any supporting container infrastrucutre, which also includes Docker.

## Re-building the container

The container was build with the command:

    > singularity build petfold-2.2.simg Singularity

The now build container can be published to GitHub's container repository with:

    # Set up login credential for authentification
    > singularity remote login --username <user> oras://ghcr.io
    # Enter secret Personal Access Token (PAT)
    > singularity push petfold-2.2.simg oras://ghcr.io/<user>/petfold:2.2
