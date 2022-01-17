## Introduction
This repository represents 5 models that were tried on the [DRSM-Corpus](https://github.com/chanzuckerberg/DRSM-corpus). The models mentioned in the below sections are some variation of transformers and neural networks. We have also given the minimum setup that will be required for running the noteboooks attached. 

These notebooks were build on Google Colab with the following configuration:

* GPU: Nvidia Tesla V100sxm2  
* GPU Memory: 16160MiB



## Data
Data is retrieved from the [DRSM-Corpus](https://github.com/chanzuckerberg/DRSM-corpus). This is a annotated literature corpus for NLP studies of 'Disease Research State' based on different categories of research (`DRSM` stands for `Disease Research State Model`)
The `initial-gold-standards` has following set of columns:
  `ID_PAPER`, `TITLE`, `ABSTRACT`, `PRIMARY CATEGORY`, `SECONDARY CATEGORY`, `IRRELEVANT`, `DISEASE_NAME`

Descriptions
* Size - `8919`
* Unique disease - `clinical characteristics or disease pathology`, `other`, `disease mechanism`, `therapeutics in the clinic`, `irrelevant`, `patient-based therapeutics`
* Classes related statistics:

| Disease                                       | Count |
|-----------------------------------------------|:-----:|
| disease mechanism                             | 108   |
| therapeutics in the clinic                    | 341   |
| irrelevant                                    | 342   |
| patient-based therapeutics                    | 1164  |     
| other                                         | 2800  |
| clinical characteristics or disease pathology | 4164  |


## Methods

| Model                               | micro F1 score |                         
|-------------------------------------|:--------------:|
| **BERT-base**                       |                |
| **PubMedBERT-LWAN**                  |                |
| **dualBERT ensemble**              |                |
| **Specter-LWAN**                    |                |
| **Specter dual-attention LWAN**     |                |


## Setup
* Step 1. Install dependencies
* Step 2. Set-up google drive
* Step 3. Download data
