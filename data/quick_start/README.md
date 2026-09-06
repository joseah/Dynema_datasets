# Quick-start demo dataset

Small, fully synthetic dataset for the Dynema.jl:

300 donors, 4,050 cells, 3 genes with 500 cis-variants each.

Each gene demonstrates one eQTL effect:

| gene    | chr   | strand | simulated effect                           |
|---------|-------|--------|--------------------------------------------|
| CTSS    | chr1  | -      | G x treg_activation, no main effect        |
| ACTB    | chr7  | -      | none (negative control)                    |
| TSPAN32 | chr11 | +      | main eQTL + G x cytotoxicity               |

Gene names/ids are real; variant positions and alleles are illustrative,
not real genomic loci.

Files:

- `genotypes.vcf.gz` -- 1,500 variants x 300 donors, `GT:DS`. **Plain gzip,
  deliberately not BGZF and not indexed**, so the tutorial's
  `dynema-prepare-vcf` step does real work. Do not "fix" this.
- `expr.mtx.gz` + `expr.features.gz` + `expr.barcodes.gz` -- 10x-style
  Matrix Market triplet (3 genes x 4,050 cells; features file has
  gene_id / gene_name / type columns). No `.dgx` sidecar shipped --
  `dynema-prepare-expr` builds it.
- `meta.tsv` -- one row per cell: `cell_id`, `donor_id`, contexts
  (`cytotoxicity`, `treg_activation`, `central_memory` -- the last never
  interacts with genotype), and covariates (`scaled_age`, `sex`,
  `scaled_log_nUMI`, `percent_mito`, `gPC1-5`, `ePC1-5`).
- `genes.bed` -- `chr  start  end  gene  strand`, one row per gene
  (TSS = start on +, end on -).
