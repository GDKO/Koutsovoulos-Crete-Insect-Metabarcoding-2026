# Charting the insect biodiversity of southern-central Crete: insights from a pilot metabarcoding survey

## Reproducing the analysis

### Download Raw Sequencing Data (FASTQ)

Before running the analysis, you must download the raw sequencing files associated with BioProject **PRJEB114132**.

```
# Clone the ENA Browser Tools repository, scripts are inside the python3 folder
git clone https://github.com/enasequence/enaBrowserTools.git

# Get the sequencing data
enaGroupGet -f fastq -d ./crete_listaros PRJEB114132

# If some runes fail you can download them individually
enaDataGet -f fastq -d ./crete_listaros/PRJEB114132 ERR17386182

# Concatenate libraries for Dataset A 
./preprocess_libs.sh

```

### Run R2V2 for the two datasets separately
```
# Dataset A
R2V2 prepare -f files_datasetA_run1.lst -o datasetA_prep_run1 -c config_datasetA.yaml
R2V2 prepare -f files_datasetA_run2.lst -o datasetA_prep_run2 -c config_datasetA.yaml
cat datasetA_prep_run1/Samples.tsv datasetA_prep_run2/Samples.tsv > datasetA_both_runs.tsv
R2V2 dereplicate -f datasetA_both_runs.tsv -c config_datasetA.yaml -o datasetA_dereplicate
R2V2 cluster -f datasetA_dereplicate/Derep.valid.fasta -p datasetA_dereplicate/Derep.valid.aa.fasta -a datasetA_dereplicate/Abundance.tsv -c config_datasetA.yaml -o datasetA_denoise

# Dataset B
R2V2 prepare -f files_datasetB.lst -o datasetB_prep -c config_datasetB.yaml
R2V2 dereplicate -f datasetB_prep/Samples.tsv -c config_datasetB.yaml -o datasetB_dereplicate
R2V2 cluster -f datasetB_dereplicate/Derep.valid.fasta -p datasetB_dereplicate/Derep.valid.aa.fasta -a datasetB_dereplicate/Abundance.tsv -c config_datasetB.yaml -o datasetB_denoise
```

### Download BOLD formatted databases from Zenodo
```
https://doi.org/10.5281/zenodo.22919861
```

### Run raxtax
```
# Dataset A
raxtax -i datasetA_denoise/ASVs.fasta -d BOLD.tr.185-344.fasta.gz --skip-db -t 8 -o datasetA_raxtax --tsv

# Dataset B
raxtax -i datasetB_denoise/ASVs.fasta -d BOLD.tr.185-225.fasta.gz --skip-db -t 8 -o datasetB_raxtax --tsv
```
