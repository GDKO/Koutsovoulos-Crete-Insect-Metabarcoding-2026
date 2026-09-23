# Charting the insect biodiversity of southern-central Crete: insights from a pilot metabarcoding survey

## Reproducing the analysis

### Download Raw Sequencing Data (FASTQ)

Before running the analysis, you must download the raw sequencing files associated with BioProject **PRJEB114132**.
```
# Create the raw data directory if it doesn't exist
mkdir -p data/raw/fastq

# Fetch the list of Run accessions for PRJEB114132 and download them
prefetch PRJEB114132

# Convert the SRA files to paired-end FASTQ format
fasterq-dump --split-files --outdir data/raw/fastq/ PRJEB114132
```

### Run R2V2 for the two datasets separately
```
which configs etc
```

### Download BOLD formatted databases from Zenodo
```
10.5281/zenodo.22919861
```

### Run raxtax
```
command
```

### Visualisation plots
```
Krona
Lifemap
```
