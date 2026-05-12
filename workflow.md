# Neuro-Genomics Final Project Workflow (Google Colab)

## Required input files
The notebook now downloads required files automatically from this public Google Drive folder:
`https://drive.google.com/drive/folders/1ZP0T8l5Qx1TJ5iihL9xCSKmbEc0MdC3r?usp=drive_link`

If files already exist locally in `Data/`, the notebook reuses them. Otherwise it downloads them into `Data/`.

- Bulk RNA-seq counts file (placeholder used in notebook): `bulk_counts_matrix.csv`
- `expression_matrix.csv`
- `locations_of_cells.csv`
- `marker_genes.csv`

If your file names differ, update the path variables in the notebook.

## How to run in Google Colab
1. Open `notebooks/final_project.ipynb` in Colab.
2. Upload this repository (or clone it into Colab).
3. Run the setup cell; it fetches missing files from the shared Google Drive folder into `Data/`.
4. Run cells top-to-bottom.
5. The notebook installs Python packages, R, and DESeq2 inside Colab. No local R installation is required.

## What Part 1 (bulk RNA-seq) does
1. Loads raw count matrix.
2. Builds sample condition table.
3. Runs DESeq2 in R through `rpy2`.
4. Exports normalized counts and DE results.
5. Filters significant genes (`padj < 0.05`).
6. Splits genes into upregulated/downregulated groups.
7. Produces PCA / MA-like / volcano plots.

Outputs are saved to `results/part1_bulk/`.

## What Part 2 (single-cell spatial) does
1. Loads expression matrix, cell locations, and marker genes.
2. Assigns likely cell type per cell from marker-based scores.
3. Computes immune-cell percentage.
4. Creates spatial maps for immune/tumor/other and PD-L1-positive cells.
5. Detects PD-L1 using `CD274` first (with fallback checks to alternative naming present in file).
6. Computes PD-L1-positive percentage.

Outputs are saved to `results/part2_single_cell/`.

## Output files created
### `results/part1_bulk/`
- `sample_conditions.csv`
- `counts_input_used.csv`
- `normalized_counts_deseq2.csv`
- `deseq2_results.csv`
- `significant_genes_padj_0.05.csv`
- `upregulated_genes.csv`
- `downregulated_genes.csv`
- `pca_samples.png`
- `ma_plot_like.png`
- `volcano_plot.png`

### `results/part2_single_cell/`
- `cell_type_assignments.csv`
- `cell_type_assignments_with_coarse_labels.csv`
- `immune_percentage.csv`
- `cell_annotations_with_pdl1.csv`
- `pdl1_percentage.csv`
- `spatial_merged_table.csv`
- `spatial_cell_classes.png`
- `spatial_pdl1_positive.png`

## Interpretation guidance
Only write biological conclusions after observing real computed outputs.
Do not claim differential-expression trends, immune enrichment, or PD-L1 status unless the generated result tables and plots support those claims.
