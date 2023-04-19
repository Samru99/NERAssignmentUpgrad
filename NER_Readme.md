# ** Custom Named Entity Recognition

---
ccording to Wikipedia, Named Entity Recognition (NER) is a subtask of information extraction that seeks to locate and classify named entities mentioned in unstructured text into pre-defined categories such as person names, organizations, locations, medical codes, time expressions, quantities, monetary values, percentages, etc.
NER can be implemented with either statistical or rule-based methods, both of which require a large amount of labeled training data and are typically trained in a fully or semi-supervised manner.

Note: This repository houses the code for task 3 (Key Information Extraction from Scanned Receipts) of the ICDAR 2019 Robust Reading Challenge on Scanned Receipts OCR and Information Extraction.

---
## Problem Statement

"BeHealthy" is a health-tech company and has a web platform that allows doctors to list their services and manage patient interactions and provides services for patients such as booking interactions with doctors and ordering medicines online. Here, doctors can easily organise appointments, track past medical records and provide e-prescriptions. So, companies like "BeHealthy" are providing medical services, prescriptions and online consultations and generating huge data day by day.

The following snippet of medical data may be generated when a doctor is writing notes to his/her patient or as a review of a therapy that he or she has done. "The patient was a 62-year-old man with squamous cell lung cancer, which was first successfully treated by a combination of radiation therapy and chemotherapy."

As we can see in this text, a person with a non-medical background cannot understand the various medical terms. We have taken a simple sentence from a medical data set to understand the problem and where one can understand the terms 'cancer' and 'chemotherapy'.

We have been given such a data set in which a lot of text is written related to the medical domain. There are a lot of diseases that can be mentioned in the entire dataset and their related treatments are also mentioned implicitly in the text, which we saw in the aforementioned example that the disease mentioned is cancer and its treatment can be identified as chemotherapy using the sentence. However, note that it is not explicitly mentioned in the dataset about the diseases and their treatment, but we can build an algorithm to map the diseases and their respective treatment.

The train dataset is used to train the Continuous Random Field (CRF) model, and the test dataset is used to evaluate the built model.

---

 **Clinical Named-Entity Extraction** works on the basis of information extraction from clinical notes. The system is fed with clinical reports as an unstructured or unannotated form of a text and it has to produce an annotated form (structured form) of text by identifying and extracting entities that correspond to patient’s medical problems, tests,and treatments.

**CRF** based model performs clinical entity extraction from discharge summaries using both domain knowledge such as UMLS Metathesaurus (which is a large biomedical dictionary that contains medical terms, billing codes or drugs name) as well as linguistic features like wordshapes and ngrams.

---
## Process:
Feature Extraction
Features such as word unigram, last-2 characters, word shape, part-of-speech, regexes of units, length, umls-cui, umls-rel, umls-abr, prev3-unigrams, and next3-unigrams are extracted for every single token.

The tokenized words are converted into vector representation of words as a process of word embedding using DictVectorizer.

These features are then passed through the wrapper known as CRFsuites which is a fast implementation of Conditional Random Fields (CRFs) for labeling sequential data.

The performance of the system presented in this paper was evaluated using the standard measures of precision (fraction of extracted named entities that are correct), recall (fraction of named entities extracted out of all the gold-standard named entities) and F-measure (harmonic mean of precision and recall).These evaluation metrics depends on FN (False Negative), FP(False Positive) and TP(True Positive).

---

## Command line flags let you specify two different sequence classification algorithms:

1. CRF (default) - with linguistic and domain-specific features
2. LSTM