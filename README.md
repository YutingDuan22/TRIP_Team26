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

## Before we start Approach 2 and 3
Download `glove.6B.50d.txt` into the folder:

```
cd "Model Selection and Prompting"/ICL
wget https://nlp.stanford.edu/data/glove.6B.zip
unzip glove.6B.zip -d glove.6B
rm glove.6B.zip
```

We only need `glove.6B.50d.txt``, you can delete the other glove files if space is an issue.

## Approach 2: Model Selection: Use Large Language Model
Our evaluation encompasses a range of models that vary across several dimensions, including architecture (e.g., LLaMA vs. Mistral), parameter scale (7B, 8B, or 13B), the application of instruction fine-tuning, and model versions (LLaMA 2 vs. LLaMA 3) to isolate which aspects of these models improve performance the most. Our best-performing model is Mistral-7b-Instruct-v0.3, which achieves 61.97% accuracy, 40.14% consistency, and 27.46% verifiability on the TRIP benchmark.

Run the following commands to reproduce Table 4 results.
### LLaMA-2-7B
```
python trip_soft_chaining.py --lm_backbone llama7B --reduce_options --model_path meta-llama/Llama-2-7b-hf
```
### LLaMA-2-13B
```
python trip_soft_chaining.py --lm_backbone llama13B  --reduce_options --model_path meta-llama/Llama-2-13b-hf
```
### LLaMA-3.1-8B
```
python trip_soft_chaining.py --lm_backbone llama3-8B --reduce_options --model_path meta-llama/Llama-3.1-8B
```
### LLaMA-3.1-8B-instruct
```
python trip_soft_chaining.py --lm_backbone Llama-3.1-8B-Instruct --reduce_options --model_path meta-llama/Llama-3.1-8B-Instruct
```
### Mistral-v0.3-7B
```
python trip_soft_chaining.py --lm_backbone mistral7B --reduce_options --model_path mistralai/Mistral-7B-v0.3
```
### Mistral-instruct-v0.3-7B
```
python trip_soft_chaining.py --lm_backbone mistral7B-instruct --reduce_options --model_path mistralai/Mistral-7B-Instruct-v0.3
```

## Approach 3: Incorporating Advanced Prompting Techniques

### Number Of Demonstrations
```
python trip_soft_chaining.py --lm_backbone Llama-3.1-8B-Instruct --reduce_options --model_path meta-llama/Llama-3.1-8B-Instruct --demo_choice custom --example_list train_1 train_8 train_691 train_693 train_694
```
### Demo Selection
#### Mistral-v0.3-7B
Run following command to use 4 explicit demostrations and 0 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B --reduce_options --model_path mistralai/Mistral-7B-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 4 0
```
Run following command to use 3 explicit demostrations and 1 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B --reduce_options --model_path mistralai/Mistral-7B-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 3 1
```
Run following command to use 2 explicit demostrations and 2 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B --reduce_options --model_path mistralai/Mistral-7B-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 2 2
```
Run following command to use 1 explicit demostrations and 3 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B --reduce_options --model_path mistralai/Mistral-7B-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 1 3
```
Run following command to use 0 explicit demostrations and 4 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B --reduce_options --model_path mistralai/Mistral-7B-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 0 4
```

#### Mistral-instruct-v0.3-7B
Run following command to use 4 explicit demostrations and 0 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B-instruct --reduce_options --model_path mistralai/Mistral-7B-Instruct-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 4 0
```
Run following command to use 3 explicit demostrations and 1 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B-instruct --reduce_options --model_path mistralai/Mistral-7B-Instruct-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 3 1
```
Run following command to use 2 explicit demostrations and 2 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B-instruct --reduce_options --model_path mistralai/Mistral-7B-Instruct-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 2 2
```
Run following command to use 1 explicit demostrations and 3 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B-instruct --reduce_options --model_path mistralai/Mistral-7B-Instruct-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 1 3
```
Run following command to use 0 explicit demostrations and 4 implicit demonstration
```
python trip_soft_chaining.py --lm_backbone mistral7B-instruct --reduce_options --model_path mistralai/Mistral-7B-Instruct-v0.3 --demo_choice auto_select --n_of_explicit_and_n_of_implicit_demos 0 4
```

### Role-Playing Prompts
#### Mistral-v0.3-7B
Run following command to use "careful story editor" role
```
python trip_soft_chaining.py --lm_backbone mistral7B --reduce_options --model_path mistralai/Mistral-7B-v0.3 --role careful_story_editor
```
Run following command to use "interior decorator" role
```
python trip_soft_chaining.py --lm_backbone mistral7B --reduce_options --model_path mistralai/Mistral-7B-v0.3 --role interior_decorator
```

#### Mistral-instruct-v0.3-7B
Run following command to use "careful story editor" role
```
python trip_soft_chaining.py --lm_backbone mistral7B-instruct --reduce_options --model_path mistralai/Mistral-7B-Instruct-v0.3 --role careful_story_editor
```
Run following command to use "interior decorator" role
```
python trip_soft_chaining.py --lm_backbone mistral7B-instruct --reduce_options --model_path mistralai/Mistral-7B-Instruct-v0.3 --role interior_decorator
```













