# Whole-Exome Sequencing (WES) Analysis Pipeline

This repository contains a script for analyzing whole-exome sequencing (WES) data using commonly used bioinformatics tools. The workflow includes quality control, alignment, duplicate marking, base quality score recalibration, and variant calling.

## Overview

The analysis pipeline performs the following steps:
1. Quality control of raw sequencing reads using FastQC and MultiQC.
2. Alignment of reads to a reference genome using BWA.
3. Conversion, sorting, and indexing of alignment files using SAMtools.
4. Marking of duplicate reads using GATK.
5. Base quality score recalibration (BQSR) using GATK.
6. Variant calling using GATK HaplotypeCaller.
7. Filtering of variants using bcftools.

## Requirements

### Software
- [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- [MultiQC](https://multiqc.info/)
- [BWA](http://bio-bwa.sourceforge.net/)
- [SAMtools](http://www.htslib.org/)
- [GATK](https://gatk.broadinstitute.org/hc/en-us)
- [bcftools](http://samtools.github.io/bcftools/)

### Data
- Raw FASTQ files from WES experiments.
- Reference genome in FASTA format.
- BED file for exome capture regions.
- Known sites VCF file for BQSR.

## Setup

1. Install the required software tools.
2. Ensure the raw FASTQ files, reference genome, BED file for exome capture regions, and known sites VCF file are prepared.

## Usage

1. Clone this repository or download the script.

```bash
git clone https://github.com/arbazattar11/wes
cd wes
```

2. Modify the variables in the script (`wes_analysis.sh`) to match your data and paths:
    - `SAMPLE_NAME`: Name of your sample.
    - `FASTQ_DIR`: Directory containing the raw FASTQ files.
    - `OUTPUT_DIR`: Directory where output files will be saved.
    - `REF_GENOME`: Path to the reference genome.
    - `INTERVALS`: Path to the BED file for exome capture regions.
    - `BWA`: Path to the BWA executable.
    - `GATK`: Path to the GATK executable.
    - `THREADS`: Number of threads to use for alignment.
    - `KNOWN_SITES`: Path to the known sites VCF file.

3. Make the script executable:

```
chmod +x wes_analysis.sh
```

4. Run the script:

```
./wes_analysis.sh
```

## Script Details

### wes_analysis.sh

This bash script performs the following steps:

1. **FastQC**: Runs quality control checks on raw sequence data.
2. **MultiQC**: Aggregates FastQC reports into a single report.
3. **BWA**: Aligns raw reads to the reference genome.
4. **SAMtools**: Converts, sorts, and indexes the alignment files.
5. **GATK MarkDuplicates**: Marks duplicate reads.
6. **GATK BaseRecalibrator**: Recalibrates base quality scores using known sites.
7. **GATK ApplyBQSR**: Applies base quality score recalibration.
8. **GATK HaplotypeCaller**: Calls variants and generates a GVCF file.
9. **GATK GenotypeGVCFs**: Converts GVCF to VCF.
10. **bcftools**: Filters and indexes the VCF file.

## Output

The script generates several output files and directories:
- `fastqc/`: Directory containing FastQC reports.
- `multiqc_report.html`: Aggregated report from MultiQC.
- `alignment/`: Directory containing alignment files (SAM, BAM, and index files).
- `variants/`: Directory containing variant call files (GVCF, VCF, and filtered VCF).

## Troubleshooting

If you encounter any issues, ensure that:
- All paths and filenames are correct.
- All required software tools are installed and accessible.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Babraham Bioinformatics](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) for FastQC.
- [MultiQC](https://multiqc.info/) for aggregating QC reports.
- [BWA](http://bio-bwa.sourceforge.net/) for read alignment.
- [HTSlib](http://www.htslib.org/) for SAMtools.
- [Broad Institute](https://gatk.broadinstitute.org/hc/en-us) for GATK.
- [SAMtools](http://samtools.github.io/bcftools/) for bcftools.

## Contact

For any questions or issues, please contact [Arbaz] at [arbazattar1137@gmail.com].
