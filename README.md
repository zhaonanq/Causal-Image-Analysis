# Causal Image Analysis

This probject explores the application of causal inference methods to image classification and prediction tasks in medical applications. More specifically, we are interested in locating the causal components of images that are relevant, in terms of physiology or pathology, when using images to predict kidney or lung diseases, and estimating the causal effect of these components.
 
## Run GWAS

### load packages
```
ml load biology
ml load htslib
ml load R
```

### set plink path
```PATH=$PATH:/scratch/groups/mrivas/ukbb24983/phenotypedata/2005693/41413/bulk/ukb2005693.41413.20202/pancreas_images/all_patients/```
```PATH=$PATH:/scratch/groups/mrivas/ukbb24983/phenotypedata/2005693/41413/bulk/ukb2005693.41413.20204/liver_images/all_patients/```

### generate phenotype files
```cat all_patients.csv > pcs_pancreas.phe```

```sdev -p mrivas -m 300Gb -t 48:00:00```

### run gwas
```python3 /oak/stanford/groups/mrivas/users/mrivas/repos/rivas-lab/ukbb-tools/04_gwas/gwas.py --run-array-combined --pheno pcs_pancreas.phe --population white_british --out /scratch/groups/mrivas/ukbb24983/phenotypedata/2005693/41413/bulk/ukb2005693.41413.20202/pancreas_images_new/all_patients/ --log-dir /scratch/groups/mrivas/ukbb24983/phenotypedata/2005693/41413/bulk/ukb2005693.41413.20202/pancreas_images_new/all_patients/ --run-now```

```python3 /oak/stanford/groups/mrivas/users/mrivas/repos/rivas-lab/ukbb-tools/04_gwas/gwas.py --run-array-combined --pheno pcs_pancreas.phe --population white_british --out /scratch/groups/mrivas/ukbb24983/phenotypedata/2005693/41413/bulk/ukb2005693.41413.20204/liver_images/all_patients/ --log-dir /scratch/groups/mrivas/ukbb24983/phenotypedata/2005693/41413/bulk/ukb2005693.41413.20204/liver_images/all_patients/ --run-now```

## Manhattan Plot

```for i in {1..20}; do Rscript /scratch/groups/mrivas/ukbb24983/phenotypedata/2005693/41413/bulk/ukb2005693.41413.20204/ukbb-tools/04_gwas/check_gwas/plots/gwas_plot_manhattan.R /scratch/groups/mrivas/ukbb24983/phenotypedata/2005693/41413/bulk/ukb2005693.41413.20202/pancreas_images_new/all_patients/ukb24983_v2_hg19.pcs_pancreas.array-combined.one_array.PHENO$i.glm.linear /oak/stanford/groups/mrivas/ukbb24983/array-combined/annotation/annotation_20201012/ukb24983_cal_hla_cnv.annot_20201023.tsv ~/manhattan_pancreas_pcs$i.png; done```

## Miscellaneous
count number of files: ```ls -lR /path/to/dir/*.jpg | wc -l```

zip manhattan plots: ```zip pancreas.zip manhattan_pancreas*```
