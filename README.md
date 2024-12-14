# TRIP_Team26
The Tiered Reasoning for Intuitive Physics (TRIP) Benchmark (Storks et al., 2021) conducts a tiered evaluation of a model's physical commonsense reasoning. Our project implements three approaches to improve performance on the TRIP benchmark: transfer learning, model selection, and advanced prompting techniques.

Our project primarily builds upon two previous papers: TRIP (https://aclanthology.org/2021.findings-emnlp.422/) and HAR (https://aclanthology.org/2023.emnlp-main.456/). Accordingly, the base of our repository comes from the repositories of these two papers.

## Approach 1: Transfer Learning with BERT

```
cd Transfer Learning
```

Model: “google-bert/bert-large-uncased”    

Datasets fot transfer learning: \
1)Conversational Entailment (CE) ; \
2)Physical Interaction: Question and Answering (PIQA)

Code Implementation: \
Finetuning: BERT_CE.ipynb, BERT_PIQA.ipynb; \
Training and Evaluation on TRIP: withBERT_CE.ipynb, withBERT_PIQA.ipynb



Results: The BERT model transferred from CE has increased the accuracy of the TRIP benchmark, but not the consistency and verifiability, while the BERT model transferred from PIQA do not have better performance.


Given the challenges of transfer learning, we switch to HAR with large language models.


## Approach 2: Model Selection: Use Large Language Model

```
cd Model Selection and Prompting
```

Our evaluation tests a variety of models that differ by developer (LLaMA vs. Mistral), number of parameters (7, 8, or 13 billion), instruction fine-tuning (included or not), and version (LLaMA 2 vs. LLaMA 3) in order to isolate which aspects of these models improve performance the most. Our best-performing model is Mistral-7b-Instruct-v0.3, which achieves strong performance of 61.97% accuracy, 40.14% consistency, and 27.46% verifiability on the TRIP benchmark.



## Approach 3: Incorporating Advanced Prompting Techniques
### Number Of Demonstrations
```
python trip_soft_chaining.py --lm_backbone mistral7B --reduce_option --model_path mistralai/Mistral-7B-v0.3 --demo_choice custom --example_list train_1 train_8 train_691 train_693 train_694
```
### Variance Due To Demo Selection

### Role-Playing Prompts










