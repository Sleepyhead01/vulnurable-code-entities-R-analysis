# Studying Vulnerable Code Entities in R

![codeattack](https://github.com/Sleepyhead01/CodeAttack-R/assets/69421538/afc95115-beb8-45ac-978c-97e861efc7ea)

CodeAttack makes a small change to one token in the input code snippet which causes significant changes to the code
summary obtained from the SOTA pre-trained programming language models fine-tuned on R

## Overview

Pre-trained Code Language Models (Code-PLMs) have shown many advancements and achieved state-of-the-art results for many software engineering tasks in the past few years. These models are mainly targeted for popular programming languages such as Java and Python, leaving out many other ones like R. Though R has a wide community of developers and users, there is little known about the applicability of Code-PLMs for R. In this preliminary study, we aim to investigate the vulnerability of Code-PLMs for code entities in R. For this purpose, we use an R dataset of code and comment pairs and then apply CodeAttack, a black-box attack model that uses the structure of code to generate adversarial code samples. We investigate how the model can attack different entities in R. This is the first step towards understanding the importance of R token types, compared to popular programming languages (e.g., Java). We limit our study to code 
summarization. Our results show that the most vulnerable code entity is the identifier, followed by some syntax tokens specific to R. The results can shed light on the importance of token types and help in developing models for code
summarization and method name prediction for the R language.


## Installaton

To install the dependencies please execute the command ```pip install -r requirements.txt```. 

The R dataset used for this study is submitted to ICPR 2024 and will be made available after the paper is published.

```config_data.yaml``` and ```config_summary.yaml``` are used to set the dataset and model parameters for the attack.

Change the path to the R dataset and CodeT5 model finetuned on R dataset in [config_data.yaml](https://github.com/Sleepyhead01/vulnurable-code-entities-R-analysis/blob/main/configs/config_data.yaml) ```config_data.yaml``` also contains other parameters related to model generation that need no modification.

The parameters for ```bleu_theta``` and task can be changed from [config_summary.yaml](https://github.com/Sleepyhead01/vulnurable-code-entities-R-analysis/blob/main/configs/config_summary.yaml)

### Running Code Attack

To run the code, please execute ```python codeattack.py``` with the following arguments (optional):

|Argument |Description|
|--- |--- |
|--attack_model | Model that attacks |
|--victim_model | Model to attack |
|--task | The task to attack |
|--lang | The input programming language dataset [java_cs, cs_java, java_small] |
|--use_ast | A boolean flag for whether to use AST constraint |
|--use_dfg | A boolean flag for whether or not to use DFG as a constraint|
|--out_dirname | The output directory |
|--input_lang | The input programming language (only required for GraphCodeBERT)|
|--use_imp | A boolean flag to either attack random words or attack only important/vulnerable words|
|--theta | The percentage of tokens to attack|

## Analysis

On running ```python codeattack.py``` the result files are generated as <no. of samples>.json.

Use this json file to run the ```RAnalysis.ipynb``` to generate the importance and normalised plots. (Replace the path in ```df = pd.read_json('/content/CodeAttack Generation.json')``` )

![image](https://github.com/Sleepyhead01/vulnurable-code-entities-R-analysis/assets/69421538/9eed1cc7-bd13-4828-838b-181caa28fc70)

![image](https://github.com/Sleepyhead01/vulnurable-code-entities-R-analysis/assets/69421538/70b2e69f-f997-4c56-abf9-985eb695cb21)


This repository is heavily inspired by the code for the AAAI 2023 paper [CodeAttack: Code-based Adversarial Attacks for Pre-Trained Programming Language Models](https://arxiv.org/pdf/2206.00052.pdf).

Code for this repository has been adapted from [CodeXGLUE](https://github.com/microsoft/CodeXGLUE), [CodeBERT](https://github.com/microsoft/CodeBERT), and [TextFooler](https://github.com/jind11/TextFooler).

## Citation
To be updated soon.
