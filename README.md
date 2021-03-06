[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Introduction
This repository represents 5 models that were experimented on the [DRSM-Corpus](https://github.com/chanzuckerberg/DRSM-corpus). The models mentioned in the below sections are some variation of transformers and neural networks. Our team (Team CUNI-NU) implemented similar approach in the [Track -5](https://biocreative.bioinformatics.udel.edu/tasks/biocreative-vii/track-5/) of [Biocreative VII](https://biocreative.bioinformatics.udel.edu/tasks/biocreative-vii/) conference. This shared task was a multi-label classification of Covid-19 literature annotation. As the [DRSM-Corpus](https://github.com/chanzuckerberg/DRSM-corpus) is a medical dataset, we implemented similar techniques to acheive optimal results.

We have also given the minimum setup that will be required for running the noteboooks attached. 

These notebooks were build on Google Colab with the following configuration:

* GPU: Nvidia Tesla V100sxm2  
* GPU Memory: 16160MiB



## Data
Data is retrieved from the [DRSM-Corpus](https://github.com/chanzuckerberg/DRSM-corpus). This is a annotated literature corpus for NLP studies of 'Disease Research State' based on different categories of research (`DRSM` stands for `Disease Research State Model`)
The `initial-gold-standards` has following set of columns:
  `ID_PAPER`, `TITLE`, `ABSTRACT`, `PRIMARY CATEGORY`, `SECONDARY CATEGORY`, `IRRELEVANT`, `DISEASE_NAME`

Descriptions
* Size - `8919`
* Unique classes - `clinical characteristics or disease pathology`, `other`, `disease mechanism`, `therapeutics in the clinic`, `irrelevant`, `patient-based therapeutics`
* Classes related statistics:

| Disease                                       | Count |
|-----------------------------------------------|:-----:|
| irrelevant                                    | 109   |
| patient-based therapeutics                    | 342   |
| other                                         | 342   |
| therapeutics in the clinic                    | 1166  |     
| disease mechanism                             | 2801  |
| clinical characteristics or disease pathology | 4166  |


## Methods

We have experimented using 5 different variations of transformers model. These variations are the experiments of the combination of various state-of-the-art BERT models and neural networks. One major component of many of these models is label-wise-attention([LWAN](https://aclanthology.org/D18-1508/)) network. LWAN architecture is responsible for improving individual word predictability by paying particular attention to the output labels. It uses an attention-mechanism-like strategy to allow the model to focus on specific words in the input rather than memorizing all of the essential features in a fixed-length vector.


* BioBERT: In this method we have trained the base [BioBERT](https://huggingface.co/dmis-lab/biobert-v1.1) model. 
* PubMedBERT-LWAN: In this method we have trained [PubMedBERT](https://huggingface.co/microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract-fulltext) along with LWAN.
* Specter-LWAN: In this method we have trained the base [SPECTER](https://huggingface.co/allenai/specter) model.
* Specter dual-attention LWAN: In this method we have used Specter embeddings with a dual-attention module. The link for this paper can be found [here](https://biocreative.bioinformatics.udel.edu/media/store/files/2021/TRACK5_pos_5_BC7_submission_188.pdf).

| Model                               | Micro F1 score |                                             Checkpoints                                            | Notebooks |                 
|-------------------------------------|:--------------:|:--------------------------------------------------------------------------------------------------:|:---------:|
| **BioBERT**                         |     0.8995     |     [Link](https://drive.google.com/file/d/1-hJESlTPM8St15hESS5-6hKeqnROJF_H/view?usp=sharing)     |    [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/gist/Nid989/a8085d197506c77fbfab08bdfee85442/biobert.ipynb)             |   
| **PubMedBERT-LWAN**                 |     0.9087     |     [Link](https://drive.google.com/file/d/1-pP49V3cF9PsBxrOkEZNx8DS6lbkNmmF/view?usp=sharing)     |    [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/gist/Nid989/479f7b1d2691b3b40839f636f7f73d30/pubmedbert-lwan.ipynb)     |
| **Specter-LWAN**                    |     0.9011     |     [Link](https://drive.google.com/file/d/1-WmSFVFNXnrmPhTNvhebizHCQeOJmQ0X/view?usp=sharing)     |    [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/gist/Nid989/3ee8e9f0f8248e3227ef2fa69b73fe1d/specter-lwan.ipynb)        |
| **Specter dual-attention LWAN**     |     0.9109     |     [Link](https://drive.google.com/file/d/1-JM6jog5By6aDczrtQ7q3U7tZa7tLxBG/view?usp=sharing)     |    [![Open In Collab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/gist/Nid989/0d50eb3626c28eb45c07d85cf077a313/dual_attention_lwan_specter.ipynb)                                                           | 

Below we have also attached the label-wise score from our best performing model i.e. Specter dual-attention LWAN.



![image](https://user-images.githubusercontent.com/44599944/150501432-6c842227-15f2-4e42-b257-7ccad76a8bf3.png)

Here, it is clearly visible that `disease mechanism`, `therapeutics in the clinic` and `irrelevant` classes have very less instances in the test dataset. Because of this large imblance, specially in case of `disease mechanism` our model may not give optimal results. One way to solve this probelm is to get more annotated data and try to maintain equal number of instances for each label. Another solution can be to ideate on a weighted approach for classification that can attentuate the problem caused the imbalance imbalance.

## Setup

As these notebooks were implemented using Google Colab, there is a basic setup required to run these notebooks. We recommend using google colab for avoinding any complications.

* Step 1. Upload the notebook on google colab or use the link provided in the above table and enable the GPU configuration.
* Step 2. Install all necessary dependencies that are mentioned in the initial cell blocks
* Step 3. Connect the notebook to your google drive. you can see the tutorial [here](https://colab.research.google.com/notebooks/io.ipynb)
* Step 3. Download data using the "wget" command. There is one cell dedicated to this command. 
* Step 4. The downloaded data will be saved in the `content` directory which is the runtime folder. Make sure you save this data in your google drive as it will be deleted once the colab session expires.
* Step 6. For every implementation we have provided the model checkpoints link so that the testing can be done easily. To use these checkpoints, download them from the above table and upload them into your connected google drive. After uploading them into your google drive you can enter it's path in the notebook.
* Step 5. After successful implementation of the above steps you can follow the instructions given in the notebook to get to the end result.

## Contributors

1. Tirthankar Ghosal (Oak Ridge National Laboratory, US):    tghosal@acm.org
2. Aakash Bhatnagar  (Navrachana University, Gujarat, India):  akashbharat.bhatnagar@gmail.com 
3. Nidhir Bhavsar    (Navrachana University, Gujarat, India):  nidbhavsar989@gmail.com


