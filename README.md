# Reproducibility Challenge - Fall 2022 (CS 421: Natural Language Processing)
This repository is our submission of source code for Reproducibility Challenge for CS421.

## Team Members:
- Samihan Nandedkar (snande3@uic.edu)
- Chinmay Wadnerkar (cwadne2@uic.edu)

## Paper:
FaiRR: Faithful and Robust Deductive Reasoning over Natural Language [[paper]](https://arxiv.org/abs/2203.10261)

Code used to reproduce this paper is referenced from the source code provided by the authors of the paper. <br/>
Source Code: [[Link to Repository]](https://github.com/INK-USC/FaiRR.git)



## Steps to reproduce the paper results

To reproduce the paper results following steps were performed in sequential order. 

<hr/>

### Code Changes & Dataset:
- The authors have provided the datasets(D* and Pararules) they have used to achive the results in the paper. 
- The D* dataset can be divided into D0 to D5 subsections and each of these subsections contains certain number of THeories, Questions & Conclusions.
- Updates to the code base were required to fix some of the compilation arose while running the preprocessing script.
- In addition, it can also be seen that the default batch size need to updated to adhere to our hardware configuration. 

<hr/>

### Hardware Requirements:
- The project had extensive hardware requirements. 
- As a significant number of computations will be carried out in the GPU using CUDA tookit, the project requires dedicated GPU access. 
- Authors have recommended RTX-8000 GPU with 48GB GPU memory. 
- To meet the system requirements of the project, we have provisioned a linux machine using a [[cloud service provider]](https://datacrunch.io/) with dedicated GPU access. 
- Machine Configuration:
    - Ubuntu linux instance
    - 10 core system with 60GB ram
    - RTX-A6000 GPU with 48 GB memory

<p align="center">
<img src="images/image_1.png" alt="image one" width="200" />
</p>

<hr/>

### Setting Up the Dependencies:
- Intially before running the code it could be seen that the dependency requirements for the project were not clearly outlined. 
- A significant amount of time was spent in retrieving all the required dependencies for the project to setup it's environment.
- requirements.txt file mentions few of the required python modules with outdated version. These were install pip package manager. 

```bash
pip install -r requirements.txt
```

The required packages for the projects are as mentioned below. 
- nltk
- torch
- scikit_learn
- pickle5
- torch & pytorch_lightning
- hydra & hydra_core
    - hydra_core requires <Python.h> header file to be installed on the system. Which can be done by running following command on Ubuntu Linux Machine:-  

    ```bash 
    apt install python3-dev
    ```
- transformers
- jsonlines, datasets, numpy, pandas

<hr/>

### Preprocess Data and Train Models
<br/>
<p align="center">
<img src="images/image_2.png" alt="image one" width="800" />
</p>

- There are three seperate models for which preprocessing and training needs to be completed sequentially as shown in the figure.

#### Rule Selector Model

- To preprocess the data for the rule selector model following the command can be run on the terminal. 

```bash
# --fairr_model signifies in the model to preprocess data for the model
python3 process_proofwriter.py --dataset pwq_leq_0to3 --fairr_model fairr_rule --arch roberta_large
```
- To train the model following command starts the training for the system.
```bash
# We have passed in the model name and dataset to the main directory
python3 main.py --override fairr_ruleselector,pwq_leq_0to3_OWA_rule
```



