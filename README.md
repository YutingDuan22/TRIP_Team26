# TRIP_Team26
Three approaches to improve performance on the TRIP benchmark: transfer learning, model selection, and fine-tuning

We implement three approaches to improve reasoning on the TRIP Benchmark mainly based on two previous papers, TRIP (https://aclanthology.org/2021.findings-emnlp.422/) and HAR (https://aclanthology.org/2023.emnlp-main.456/).

## Approach 1: Transfer Learning with BERT
Model: “google-bert/bert-large-uncased”    

Datasets fot transfer learning: \
1)Conversational Entailment (CE) ; \
2)Physical Interaction: Question and Answering (PIQA)

Results: The BERT model transferred from CE has increased the accuracy of the TRIP benchmark, but not the consistency and verifiability, while the BERT model transferred from PIQA do not have better performance.


Given the challenges of transfer learning, we switch to HAR with large language models.



## Approach 2: Model Selection: Use Large Language Model

[table]

## Approach 3: Prompting Techniques 

### 

## Citation






