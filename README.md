 Klebsiella oxytoca Genome Assembly and Annotation Project

Project Overview
This project involves the genome assembly and annotation of Klebsiella oxytoca using the publicly available dataset SRR32937950 from the NCBI Sequence Read Archive (SRA). The dataset is part of the "Microbiology Laboratory Reference and Control Strain Database" (BioProject: PRJNA981165, Study: SRP506074), submitted by the New Jersey Department of Health (NJDOH_PNGT). The primary aim is to assemble the genome, evaluate its quality, and annotate it for functional insights, with the potential for publication and collaboration.

Objectives
- Download and preprocess raw sequencing reads for *Klebsiella oxytoca*.
- Perform quality control and trimming of the sequencing data.
- Assemble the genome using SPAdes.
- Assess the assembly quality using QUAST.
- Annotate the genome using DFAST and RAST.
- Organize the project for sharing and potential publication.

Dataset Details
- Source: NCBI SRA
- Accession Number: SRR32937950
- BioProject: PRJNA981165
- Study: SRP506074
- Organism: Klebsiella oxytoca
-  Strain: NJDOH control strain
- Sequencing Platform: Illumina MiSeq
- Strategy: Whole Genome Sequencing (WGS)

- Run Details:
  - Number of Spots: 1,148,662
  - Number of Bases: 560.3M
  - Published: 2025-04-01

Project Workflow
The entire workflow is automated in a single Bash script, `scripts/run_pipeline.sh`, which executes the following steps:
1. Data Download
- Downloaded raw sequencing reads (`SRR32937950_1.fastq` and `SRR32937950_2.fastq`) from NCBI SRA using the SRA Toolkit (`prefetch` and `fasterq-dump`).
- Output: `input_data/SRR32937950_1.fastq`, `input_data/SRR32937950_2.fastq`.
2. Quality Control and Trimming
- **Quality Control (Raw Reads)**: Performed using FastQC to assess the quality of raw reads.
  - Output: `output/fastqc/raw/SRR32937950_1_fastqc.html`, `output/fastqc/raw/SRR32937950_2_fastqc.html`.
- Trimming: Trimmed low-quality bases and adapters using Trimmomatic with the following parameters: `LEADING:20 TRAILING:20 SLIDINGWINDOW:4:15 MINLEN:36`.
  - Output: `output/trimmed_reads/SRR32937950_1_trimmed_paired.fastq`, `output/trimmed_reads/SRR32937950_2_trimmed_paired.fastq`.
- Quality Control (Trimmed Reads): Performed using FastQC to verify the quality of trimmed reads.
  - Output: `output/fastqc/trimmed/SRR32937950_1_trimmed_paired_fastqc.html`, `output/fastqc/trimmed/SRR32937950_2_trimmed_paired_fastqc.html`.
3. Genome Assembly
- Assembled the trimmed reads using SPAdes (version 3.15.5).
- Output: `output/assembly/scaffolds.fasta` (final assembled genome).

4. Assembly Quality Assessment
- Evaluated the assembly quality using QUAST.
- Output: `output/quast/report.html`.
5. Genome Annotation
- DFAST: Annotated the assembled genome using DFAST.
  - Output: `output/dfast/` (includes GFF, protein sequences, and other annotation files).
- RAST: Annotated the assembled genome using the RAST web server.
  - Output: `output/rast/` (includes functional annotations, subsystems, and KEGG maps).

 Workflow Diagram
A visual representation of the workflow is available in `workflow_diagram.png` (optional). The workflow includes:
1. Data download from NCBI SRA.
2. Quality control with FastQC.
3. Trimming with Trimmomatic.
4. Assembly with SPAdes.
5. Quality assessment with QUAST.
6. Annotation with DFAST and RAST.

 Directory Structure
The project is organized as follows:
- `README.md`: This documentation file.
- `metadata.tsv`: Metadata for the dataset, prepared for GenBank.
- `input_data/`: Raw input data.
  - `SRR32937950.sra`: Original SRA file.
  - `SRR32937950_1.fastq`, `SRR32937950_2.fastq`: Raw sequencing reads.
- `scripts/`: Automation script.
  - `run_pipeline.sh`: A single Bash script that automates the entire workflow (download, quality control, trimming, assembly, and annotation).
- `output/`: Output files generated during the analysis.
  - `fastqc/raw/`: FastQC reports for raw reads.
  - `fastqc/trimmed/`: FastQC reports for trimmed reads.
  - `trimmed_reads/`: Trimmed reads after Trimmomatic.
  - `assembly/`: Assembly output (`scaffolds.fasta`).
  - `quast/`: QUAST quality assessment reports.
  - `dfast/`: DFAST annotation results.
  - `rast/`: RAST annotation results.
- `workflow_diagram.png`: Workflow diagram (optional).
- `environment.yml`: Conda environment file with tool dependencies.

Tools and Versions
The following tools were used in this project:
- SRA Toolkit: 3.0.0
- FastQC: 0.11.9
- Trimmomatic: 0.39
- SPAdes: 3.15.5
- QUAST: 5.2.0
- DFAST: [web-based tool]
- RAST: [web-based tool]

Results and Observations
- The assembly process generated a draft genome (`scaffolds.fasta`) with a reasonable number of contigs (pending QUAST metrics).
- DFAST and RAST annotations provided insights into the functional genes and metabolic pathways of Klebsiella oxytoca.
- A potential observation: The number of contigs was lower than expected, which may warrant further investigation (e.g., adjusting SPAdes parameters or checking for contamination).

Metadata
A metadata file (`metadata.tsv`) has been prepared for submission to GenBank or SRA. It includes details such as:
- Sample name: `K_oxytoca_SRR32937950`
- BioProject: PRJNA981165
- BioSample: SAMN47734333
- Organism: *Klebsiella oxytoca*
- Strain: NJDOH control strain
- Sequencing technology: Illumina MiSeq
- Assembly method: SPAdes 3.15.5
- Annotation methods: DFAST, RAST

