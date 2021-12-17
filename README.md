# Signal-Detection-for-Adverse-Drug-Reaction-using-Twitter-Data-

## Introduction 

With the rise in popularity of machine learning for natural language processing (NLP) tasks, there is an intrinsic demand for large-scale social-media datasets aimed at such tasks in the field of pharmacovigilance, specifically for the identification of Adverse Drug Reactions (ADRs)

Adverse drug events (ADEs), which include drug interactions, have a huge impact on patient health and cost a lot of money.

 Each Adverse Event (AE) linked with a drug based on data from the Safety Reporting System is published on the drug label and serves as the basis for training and testing machine learning algorithms.

Unknown ADR refers to an AE that has been identified and may be linked to the drug.

## Dataset

We will be using Twitter data by extracting tweets for 2021 and 2020 - https://developer.twitter.com/en

A known list of Known ADR will be used from US FDA website. - https://open.fda.gov/data/downloads/

## Methodology

### Tweets Extraction
### Data Scrubbing:
Removing links, user names,emojis,#tags,numbers etc
Removing duplicate rows and empty rows.
Cleared Stopwords 
Data Analysis and changing to unique terms.
### Spark NLP:
We have used bellow NLP models for tweet clasification.
#### DocumentAssembler:
an entry point to Spark NLP annotators.
The raw data must be annotated. This is an unique transformer that takes care of it for us; the text is split into an array of sentences and a new column “sentences” in Document type is created, which annotators bellow can utilize later.
#### Tokenizer:
Identifies tokens with tokenization open standards
sentences” column is fed into Tokenizer() (AnnotatorModel) and each sentence is tokenized and a new column “token” in Token type is created. And so on.
#### Embedding with BioBerT:
Used Bert Embeddings that maps tokens to vectors in a bidirectional way.
BertEmbeddings pretrained "biobert_pubmed_base_cased" model is used for converting "sentence" and "token" into "embeddings".
#### Ade biobert Clasiffier:
 Classify if a sentence is ADE-related (True) or not (False).
Used "classifierdl_ade_biobert" clasification model to classify an ade.
It uses  "sentence" and  "sentence_embeddings" to classify an ade.
#### Pretrained ADE Pipeline:
A pipeline for Adverse Drug Events (ADE) with ner_ade_healthcare, and classifierdl_ade_biobert. It will extract ADE and DRUG clinical entities, and then assign ADE status to a text(True means ADE, False means not related to ADE). Also extracts relations between DRUG and ADE entities (1 means the adverse event and drug entities are related, 0 is not related).
Used 'explain_clinical_doc_ade' clasification model to extract ADE and DRUG.


