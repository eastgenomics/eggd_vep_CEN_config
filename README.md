# eggd_vep_CEN_config
Json configuration file for the implementation of VEP for the CEN assay.

## What does this config do?

Configuration file required to annotate a vcf using [Variant Effect Predictor](https://github.com/Ensembl/ensembl-vep) implementation [eggd_vep](https://github.com/eastgenomics/eggd_vep).

A variable level of annotation can be achieved by different combinations of custom annotation , vep plugins in addition to the required VEP resources.

## What does this config version contain?

This json file provides information about annotations,plugins, required fields and the genome version.

* Genome build: GRCh37
* VEP required files:
  * vep_v107.0.tar.gz
  * plugin_config.txt
  * homo_sapiens_refseq_vep_107_GRCh37.tar.gz
  * Homo_sapiens.GRCh37.dna.toplevel.fa.gz
  * Homo_sapiens.GRCh37.dna.toplevel.fa.gz.fai
  * Homo_sapiens.GRCh37.dna.toplevel.fa.gz.gzi
  * hs37d5.fasta-index.tar.gz
* Custom Annotation sources:
  * clinvar_20220412_grch37.vcf.gz
  * gnomad.genomes.r2.1.1.sites.all.noVEP_normalised_decomposed_PASS.dias_trimmed_v1.0.0.vcf.bgz
  * gnomad.exomes.r2.1.1.sites.noVEP_normalised_decomposed_PASS.dias_trimmed_v1.0.0.vcf.bgz
  * TWE_POPAF_N500_chr1-22_220413.vcf.gz
  * HGMD_Pro_2021.4_hg19.vcf.gz
* Plugin annotations:
  * REVEL (version May 2022)
    * revel_b37.tsv.gz
  * CADD (v1.6)
    * cadd_whole_genome_SNVs_GRCh37.tsv.gz
    * gnomad.genomes.r2.1.1.indel.tsv.gz
    * InDels_GRCh37.tsv.gz
  * SpliceAI
    * spliceai_scores.masked.snv.hg19.vcf.gz
    * spliceai_scores.masked.indel.hg19.vcf.gz




## Notes
  How to check the names of all the files included in the config:

```bash
config_file=you_file_name.json

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


