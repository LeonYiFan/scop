# Run generalized principal components analysis (GLMPCA)

Run generalized principal components analysis (GLMPCA)

## Usage

``` r
RunGLMPCA(object, ...)

# S3 method for class 'Seurat'
RunGLMPCA(
  object,
  assay = NULL,
  layer = "counts",
  features = NULL,
  L = 5,
  fam = c("poi", "nb", "nb2", "binom", "mult", "bern"),
  rev.gmlpca = FALSE,
  ndims.print = 1:5,
  nfeatures.print = 30,
  reduction.name = "glmpca",
  reduction.key = "GLMPC_",
  verbose = TRUE,
  seed.use = 11,
  ...
)

# S3 method for class 'Assay'
RunGLMPCA(
  object,
  assay = NULL,
  layer = "counts",
  features = NULL,
  L = 5,
  fam = c("poi", "nb", "nb2", "binom", "mult", "bern"),
  rev.gmlpca = FALSE,
  ndims.print = 1:5,
  nfeatures.print = 30,
  reduction.key = "GLMPC_",
  verbose = TRUE,
  seed.use = 11,
  ...
)

# S3 method for class 'Assay5'
RunGLMPCA(
  object,
  assay = NULL,
  layer = "counts",
  features = NULL,
  L = 5,
  fam = c("poi", "nb", "nb2", "binom", "mult", "bern"),
  rev.gmlpca = FALSE,
  ndims.print = 1:5,
  nfeatures.print = 30,
  reduction.key = "GLMPC_",
  verbose = TRUE,
  seed.use = 11,
  ...
)

# Default S3 method
RunGLMPCA(
  object,
  assay = NULL,
  layer = "counts",
  features = NULL,
  L = 5,
  fam = c("poi", "nb", "nb2", "binom", "mult", "bern"),
  rev.gmlpca = FALSE,
  ndims.print = 1:5,
  nfeatures.print = 30,
  reduction.key = "GLMPC_",
  verbose = TRUE,
  seed.use = 11,
  ...
)
```

## Arguments

- object:

  An object. Can be a Seurat object, an assay object, or a matrix-like
  object.

- ...:

  Passed to the
  [glmpca::glmpca](https://rdrr.io/pkg/glmpca/man/glmpca.html) function.

- assay:

  Assay to use. `NULL` uses the default assay.

- layer:

  Assay layer to use.

- features:

  Features used instead of a reduction.

- L:

  The number of components to be computed.

- fam:

  The family of the generalized linear model to be used. Currently
  supported values are `"poi"`, `"nb"`, `"nb2"`, `"binom"`, `"mult"`,
  and `"bern"`.

- rev.gmlpca:

  Whether to perform reverse GLMPCA (i.e., transpose the input matrix)
  before running the analysis.

- ndims.print:

  The dimensions (number of components) to print in the output.

- nfeatures.print:

  The number of features to print in the output.

- reduction.name:

  Reduction to be stored in the Seurat object.

- reduction.key:

  The prefix for the column names of the basis vectors.

- verbose:

  Whether to print the message. Default is `TRUE`.

- seed.use:

  Random seed.

## Examples

``` r
data(pancreas_sub)
pancreas_sub <- RunStandardWorkflow(pancreas_sub)
#> ℹ [2026-11-15 23:33:10] Start standard processing workflow...
#> ℹ [2026-11-15 23:33:10] Checking a list of <Seurat>...
#> ! [2026-11-15 23:33:10] Data 1/1 of the `srt_list` is "unknown"
#> ℹ [2026-11-15 23:33:10] Perform `NormalizeData()` with `normalization.method = 'LogNormalize'` on 1/1 of `srt_list`...
#> ℹ [2026-11-15 23:33:11] Perform `FindVariableFeatures()` on 1/1 of `srt_list`...
#> ℹ [2026-11-15 23:33:11] Use the separate HVF from `srt_list`
#> ℹ [2026-11-15 23:33:11] Number of available HVF: 2000
#> ℹ [2026-11-15 23:33:11] Finished check
#> ℹ [2026-11-15 23:33:11] Perform `ScaleData()`
#> ℹ [2026-11-15 23:33:11] Perform pca linear dimension reduction
#> ℹ [2026-11-15 23:33:11] Use stored estimated dimensions 1:23 for Standardpca
#> ℹ [2026-11-15 23:33:11] Perform `Seurat::FindClusters()` with `cluster_algorithm = 'louvain'` and `cluster_resolution = 0.6`
#> ℹ [2026-11-15 23:33:11] Reorder clusters...
#> ℹ [2026-11-15 23:33:11] Skip `log1p()` because `layer = data` is not "counts"
#> ℹ [2026-11-15 23:33:11] Perform umap nonlinear dimension reduction
#> ✔ [2026-11-15 23:33:19] Standard processing workflow completed
pancreas_sub <- RunGLMPCA(pancreas_sub)
#> ℹ GLMPC_ 1 
#> ℹ Positive:  Col1a2, Col1a1, Col23a1, Col6a1, Tnni3, Islr, Anxa1, Sparcl1, Sp140, Galnt16 
#> ℹ      Col3a1, Ctsk, Ctgf, Hoxb4, Plscr2, Zfp385b, Isg15, P2ry2, Prickle2, Smpx 
#> ℹ      1110002O04Rik, D630011A20Rik, Pmp22, Krt20, Tstd1, Edn1, A730098A19Rik, Platr22, Gdf15, Nkain4 
#> ℹ Negative:  Barx2, Srrm3, Dusp26, Platr26, Ptger3, Ky, Nlgn1, Gm6086, Gm933, 3930402G23Rik 
#> ℹ      Il1r2, Gad1, Gm4319, Kcne2, Aard, A130057D12Rik, Cdkn2b, Gm3448, Bcas1os1, 4930426D05Rik 
#> ℹ      Fam71b, Mesp1, Ifit1bl1, Gpr6, Sult1d1, Pappa2, Ppp1r17, Lrrc6, Sdcbp2, Cypt3 
#> ℹ GLMPC_ 2 
#> ℹ Positive:  Klhl14, Dkk2, Sst, RP23-428N8.3, 4930539E08Rik, Fgb, Doc2a, Aif1, Crygn, Col25a1 
#> ℹ      Lgr5, 4930426D05Rik, Gm11789, Tnni3, Ppy, Sparcl1, Pyy, Col1a2, 1700001C02Rik, Rgs4 
#> ℹ      Gcg, Tac1, Nell1, Fbln5, Gm12689, Cbln4, Pnoc, Gad2, Rerg, Gm38112 
#> ℹ Negative:  Ncf2, Ifitm1, Prom2, P2ry14, Sema3g, Tgm7, Slfn2, Neurod2, Cmklr1, Gm15567 
#> ℹ      Fgf8, Nhlh1, Lynx1, Neurog3, Epb42, Bhlhe22, Siglece, Tox2, Laptm5, Ppp1r14a 
#> ℹ      Tfap2c, Eya2, Gm16140, Tspear, Tex36, Fn3krp, Pthlh, Crlf1, Rasgrp3, Fgf18 
#> ℹ GLMPC_ 3 
#> ℹ Positive:  Pid1, Depdc1a, Sapcd2, Egr4, Kif22, Iqgap3, Prc1, Spns2, Ccnb1, Nusap1 
#> ℹ      Mxd3, Aurka, Cldn18, Neil3, Kif11, Kpna2, Cdca2, Ube2c, Espl1, Sgol2a 
#> ℹ      Aurkb, Racgap1, Incenp, Hmmr, Pif1, Ncapg, Ccnf, Nuf2, Spc25, Ckap2l 
#> ℹ Negative:  Sst, Rac2, Tstd1, Lrrtm3, Itgb7, Kcne2, Arhgap22, Irs4, Sp140, Ngf 
#> ℹ      Fcgr3, Anxa1, Bmp2, Elovl4, Srgn, Fgf8, Ifit1bl1, Lst1, Gm17455, Mesp1 
#> ℹ      Foxd3, Tex36, Ghrl, D7Ertd443e, Smpx, Cbln4, St8sia2, Pou6f2, Gpr6, Cd37 
#> ℹ GLMPC_ 4 
#> ℹ Positive:  Gm10382, Cbln1, Ceacam10, Sst, Gtf2ird2, Tyrobp, Rac2, Fcgr3, Lst1, Gm6410 
#> ℹ      RP23-58K20.3, Itgb7, Srgn, Gm12689, Coro1a, Afap1l2, Igfbp3, Cpne5, Platr27, Cd37 
#> ℹ      Rasl11a, Adam32, Ly6a, Col25a1, Spock1, Pik3c2b, Syce1, Gip, Smagp, Acsbg1 
#> ℹ Negative:  Col1a1, Islr, Sparcl1, Galnt16, Kcnj8, Col1a2, Col3a1, Col6a1, Tmem119, Ghrl 
#> ℹ      Gcg, Col23a1, Col5a1, Bhlhe23, Calb1, Aspm, Sapcd1, Lsp1, Bcas1os1, Pif1 
#> ℹ      Guca2a, Ngf, Cdkn2c, Spp2, Irs4, Gad2, Klk11, Pou6f2, Cbln4, Pdcd1 
#> ℹ GLMPC_ 5 
#> ℹ Positive:  Anxa1, Gast, Sytl2, Nrn1, Gm29440, Tagln, A930017K11Rik, Nepn, Cxcl10, Calb1 
#> ℹ      Sapcd1, Ltb, Gcg, Fgf8, Fam212b, Cd36, Esyt3, Ccl28, RP23-4H17.3, Krt17 
#> ℹ      Rerg, Slfn9, Anxa3, Gm43000, Cxcl16, Pole, Ryr3, Pou6f2, Otc, Cypt3 
#> ℹ Negative:  Sparcl1, Guca2a, Sds, Cbln4, Rac2, Guca2b, Dlgap1, Ghrl, Ins1, Sst 
#> ℹ      Aspm, Srgn, Slfn2, Gsg1l, BC043934, Olfml2a, Aif1, Npy, Pif1, Cdc25c 
#> ℹ      Gm6878, Ccdc13, Oasl2, Itgb7, Sostdc1, Gm28875, Fam83d, P2ry2, Troap, BC030867 
CellDimPlot(
  pancreas_sub,
  group.by = "CellType",
  reduction = "glmpca"
)
```
