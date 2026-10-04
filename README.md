# Cas Protein AI Analysis

A Google Colab notebook for comparing homologous protein sequences with a reference, identifying substitutions and indels, extracting pretrained ESM-2 embeddings, and exploring sequence relationships with PCA. Optional visualization maps substitutions to an existing PDB structure.

[Open in Google Colab](https://colab.research.google.com/github/Manobas19/Cas-Protein-AI-Analysis/blob/main/Cas_Protein_AI_Analysis.ipynb)

## Run the notebook

1. Open `Cas_Protein_AI_Analysis.ipynb` in Google Colab.
2. Select a GPU runtime for faster AI inference, then run the installation cell.
3. Try the default demonstration, or set `DEMO_MODE = False` to use your own data.
4. Upload `reference.fasta` with exactly one protein sequence and `queries.fasta` with one or more protein sequences. Use unique identifiers and the 20 standard amino acids.
5. Run cells in order and download the results ZIP from the final cell.

Use homologous reference and query sequences from one Cas family at a time. Set `RUN_AI = False` to run alignment analysis without AI inference. For optional structure visualization, set `VIEW_STRUCTURE = True`, select the chain and query, and upload a matching PDB file.

## Outputs

- Sequence summaries and reference-coordinate substitutions, insertions, and deletions
- Pairwise alignments and residue-difference chart
- ESM-2 embeddings and cosine distances, when enabled
- PCA coordinates and plot, when sufficient varying sequences are available
- Optional structure residue mapping
- Run manifest with settings, package versions, and sequence hashes

## Interpretation and validation

The default demo sequences are artificial and are **not Cas proteins**. This is exploratory sequence analysis; embedding distances do not predict editing efficiency, safety, stability, or mutation effects. The notebook does not identify Cas families, generate protein designs, train an activity predictor, or predict new 3D structures. Long-sequence embeddings use overlapping windows and lose interactions beyond each window.

Notebook format and Python cell syntax were checked before publication. Full pretrained-model inference and Colab upload/download interactions have not been verified in this publishing session. See the notebook for sources and further limitations.
