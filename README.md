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

We have experimented using 5 different variations of transformers model. These variations are the experiments of the combination of various state-of-the-art BERT models and neural networks. One major component of many of these models is label-wise-attention([LWAN](https://aclanthology.org/D18-1508/)) network. LWAN architecture is responsible for improving individual word predictability by paying particular attention to the output labels. It uses an attention-mechanism-like strategy to allow the model to focus on specific words in the input rather than memorizing all of the essential features in a fixed-length vector.


* BioBERT: In this method we have trained the base [BioBERT](https://huggingface.co/dmis-lab/biobert-v1.1) model. 
* PubMedBERT-LWAN: In this method we have trained [PubMedBERT](https://huggingface.co/microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract-fulltext) along with LWAN.
* dualBERT ensemble: This approach was inspired by [AngryBERT](https://arxiv.org/abs/2103.11800) architecutre. For acheiving the below results we used 2 models: PubmedBERT and SPECTER
* Specter-LWAN: In this method we have trained the base [SPECTER](https://huggingface.co/allenai/specter) model.
* Specter dual-attention LWAN: In this method we have used Specter embeddings with a dual-attention module. The link for this paper can be found [here](https://biocreative.bioinformatics.udel.edu/media/store/files/2021/TRACK5_pos_5_BC7_submission_188.pdf).

| Model                               | Micro F1 score |  Checkpoints  |                       
|-------------------------------------|:--------------:|:-------------:|
| **BioBERT**                         |     0.8995     |     [Link](https://drive.google.com/file/d/1-hJESlTPM8St15hESS5-6hKeqnROJF_H/view?usp=sharing)     |     
| **PubMedBERT-LWAN**                 |     0.9087     |     [Link](https://drive.google.com/file/d/1-pP49V3cF9PsBxrOkEZNx8DS6lbkNmmF/view?usp=sharing)     |
| **dualBERT ensemble**               |                |     [Link]                                                                                         |
| **Specter-LWAN**                    |                |     [Link](https://drive.google.com/file/d/1-WmSFVFNXnrmPhTNvhebizHCQeOJmQ0X/view?usp=sharing)     |
| **Specter dual-attention LWAN**     |     0.9109     |     [Link](https://drive.google.com/file/d/1-pP49V3cF9PsBxrOkEZNx8DS6lbkNmmF/view?usp=sharing)     |

## Setup

As these notebooks were implemented using google collab, there is a basic setup required to run these notebooks. We recommend using google colab for avoinding any complications.

* Step 1. Upload the notebook on google colab and enable the GPU configuration.
* Step 2. Install all necessary dependencies that are mentioned in the initial cell blocks
* Step 3. Connect the notebook to your google drive. you can see the tutorial [here](https://colab.research.google.com/notebooks/io.ipynb)
* Step 3. Download data using the "wget" command. There is one cell dedicated to this command. 
* Step 4. The downloaded data will be saved in the `content` directory which is the runtime folder. Make sure you save this data in your google drive as it will be deleted once the colab session expires.
* Step 6. For every implementation we have provided the model checkpoints link so that the testing can be done easily. To use these checkpoints, download them from the above table and upload them into your connected google drive. After uploading them into your google drive you can enter it's path in the notebook.
* Step 5. After successful implementation of the above steps you can follow the instructions given in the notebook to get to the end result.
