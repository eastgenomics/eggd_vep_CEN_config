# eggd_vep_CEN_config

Json configuration files for the implementation of VEP for the CEN assay.

## What does this config do?

Configuration file required to annotate a vcf using [Variant Effect Predictor](https://github.com/Ensembl/ensembl-vep) implementation [eggd_vep](https://github.com/eastgenomics/eggd_vep).

A variable level of annotation can be achieved by different combinations of custom annotation, vep plugins in addition to the required VEP resources.

## What does this config version contain?

This config repo contains two json files for the genome builds GRCh38 and GRCh37.
These json files provides information about annotations, plugins, required fields and the genome version.

| Key | GRCh37 | GRCh38 |
|--------------|--------------|--------------|
| **vep_docker** | vep_v107.0.tar.gz | vep_v107.0.tar.gz |
| **plugin_config** | plugin_config.txt | plugin_config.txt |
| **vep_cache** | homo_sapiens_refseq_vep_107_GRCh37.tar.gz | homo_sapiens_refseq_vep_107_GRCh38.tar.gz |
| **reference_fasta** | Homo_sapiens.GRCh37.dna.toplevel.fa.gz | Homo_sapiens.GRCh38.dna.toplevel.fa.gz |
| **reference_fai** | Homo_sapiens.GRCh37.dna.toplevel.fa.gz.fai | Homo_sapiens.GRCh38.dna.toplevel.fa.gz.fai |
| **reference_gzi** | Homo_sapiens.GRCh37.dna.toplevel.fa.gz.gzi | Homo_sapiens.GRCh38.dna.toplevel.fa.gz.gzi |
| **ref_bcftools** | hs37d5.fasta-index.tar.gz | GRCh38_GIABv3_no_alt_analysis_set_maskedGRC_decoys_MAP2K3_KMT2C_KCNJ18_noChr.fasta-index.tar.gz |
| **ClinVar** | clinvar_20250415_GRCh37.vcf.gz | clinvar_20251019_GRCh38.vcf.gz |
| **gnomAD genomes** | gnomad.genomes.r2.1.1.sites.all.noVEP_normalised_decomposed_PASS.dias_trimmed_v1.0.0.vcf.bgz | gnomad.genomes.v4.1.sites.all.trimmed_normalised_decomposed_PASS.no_chr.vcf.bgz |
| **gnomAD exomes** | gnomad.exomes.r2.1.1.sites.noVEP_normalised_decomposed_PASS.dias_trimmed_v1.0.0.vcf.bgz | gnomad.exomes.v4.1.sites.all.trimmed_normalised_decomposed_PASS.no_chr.vcf.bgz |
| **CEN** | - | CEN38_POPAF_chr1-22_240503.vcf.gz |
| **TWE** | TWE_POPAF_N500_chr1-22_220413.vcf.gz | TWE38_POPAF_chr1-22_241126.vcf.gz |
| **Medicover** | - | Medicover38_POPAF_chr1-22_241125.vcf.gz |
| **HGMD** | HGMD_Pro_2025.1_hg19.vcf.gz | HGMD_Pro_2025.3_hg38.vcf.gz |
| **REVEL** | revel_b37.tsv.gz (v1.3, May 2022) | revel_b38.tsv.gz (v1.3, May 2022) |
| **CADD** | cadd_whole_genome_SNVs_GRCh37.tsv.gz, gnomad.genomes.r2.1.1.indel.tsv.gz, InDels_GRCh37.tsv.gz | cadd_1.7_b38_whole_genome_SNVs.tsv.gz, cadd.1.7.b38.gnomad.genomes.r4.0.indel.tsv.gz |
| **SpliceAI** | spliceai_scores.masked.snv.hg19.vcf.gz, spliceai_scores.masked.indel.hg19.vcf.gz | spliceai_scores.masked.snv.hg38.vcf.gz, spliceai_scores.masked.indel.hg38.vcf.gz |
| **IncludeVariant** | GRCh37_inclusion_list_v1.0.1.vcf.gz | GRCh38_inclusion_list_v1.0.0.vcf.gz |
| **ExcludeVariant** | GRCh37_optimised_filtering_excluded_variants_v1.0.1.vcf.gz | GRCh38_exclusion_list_v1.1.0.vcf.gz |


## Notes

  How to check the names of all the files included in the config:

```bash
config_file=<config_filename>.json

# Get the Vep Resources filenames
for file in  $(jq -r ' .vep_resources | .[]' $config_file);
do dx describe $file --json | jq -r '.name';
done

# Get Custom Annotation filenames
for file in  $(jq -r ' .custom_annotations[]|.resource_files[]|.file_id' $config_file);
do dx describe $file --json | jq -r '.name';
done

# Get Plugin Annotation filenames
for file in  $(jq -r ' .plugins[]|.resource_files[]|.file_id' $config_file);
do dx describe $file --json | jq -r '.name';
done

```
