## Introduction


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
| **BERT-base **                      |                |
| **pubmednlp-LWAN**                  |                |
| **dual-BERT ensemble**              |                |
| **Specter-LWAN**                    |                |
| **Specter dual-attention LWAN **    |                |


## Head1 




This approach implements the SPECTER model, which incorporates SciBERT to produce the
document-level embedding using citation-based transformers. SciBERT can decipher the
dense bio-medical vocabulary in the COVID-19 literature, making it the ideal choice.
Furthermore, a Dual-attention module is used, consisting of two self-attention layers applied
to the embeddings in sequential order. These Self-attention layers allow each input to
establish relationships with other instances. To obtain unique vectors, i.e., query (Q), key (K),
and value (V), three individually learned matrices are multiplied with the input vector. A
single self-attention layer can learn the relationship between contextual semantics and
sentimental tendency information. While the dual-self-attention mechanism helps retain more
information contained in the sentence and thus generate a more representative feature vector
for the sentence. However, the dual-self-attention mechanism can only generate relationships
amongst the input instances while completely discarding the output. A Label-Wise-Attention-
Network(LWAN) is used to improve the results further and overcome the limitation of dual-
attention. LWAN provides attention to each label in the dataset and improves individual word
predictability by paying special attention to the output labels. It uses attention to allow the
model to focus on specific words in the input rather than memorizing all of the essential
features in a fixed-length vector. Label-wise attention mechanism repeatedly applies attention
L (number of labels) times, where each attention module is reserved for a specific label.
Weighted binary cross-entropy is used as a loss function. This loss function was most
appropriate as it gives equal importance to the different classes during training, which was
necessary due to the significant imbalance in the data. 

## Setup
* Step 1. Install dependencies
* Step 2. Set-up google drive
* Step 3. Download data
