# Graph of Records


Official implementation of the ACL'25 Main Conference Paper: Graph of Records: Boosting Retrieval Augmented Generation for Long-context Summarization with Graphs


<p align="center">
    <a href="https://ulab-uiuc.github.io/GoR/">
        <img alt="Build" src="https://img.shields.io/badge/Project-Page-blue">
    </a>
    <a href="https://arxiv.org/abs/2410.11001">
        <img alt="Build" src="https://img.shields.io/badge/arXiv-2410.11001-red?logo=arxiv">
    </a>
    <!-- <a href="xxx">
        <img alt="Build" src="https://img.shields.io/badge/Twitter-black?logo=X">
    </a> -->
    <a href="https://github.com/ulab-uiuc/GoR/blob/master/LICENSE">
        <img alt="License" src="https://img.shields.io/badge/LICENSE-MIT-green">
    </a>
    <br>
    <a href="https://github.com/ulab-uiuc/GoR">
        <img alt="Build" src="https://img.shields.io/github/stars/ulab-uiuc/GoR">
    </a>
    <a href="https://github.com/ulab-uiuc/GoR">
        <img alt="Build" src="https://img.shields.io/github/forks/ulab-uiuc/GoR">
    </a>
    <a href="https://github.com/ulab-uiuc/GoR">
        <img alt="Build" src="https://img.shields.io/github/issues/ulab-uiuc/GoR">
    </a>
</p>


<p align="center">
    <a href="https://ulab-uiuc.github.io/GoR/">🌐 Project Page</a> |
    <a href="https://arxiv.org/abs/2410.11001">📜 arXiv</a>
    <!-- <a href="xxx">📮 Twitter Post</a> -->
<p>


<!-- ![Method](./figures/model.png) -->

<div align="center">
  <img src="./figures/model.png" width="700" alt="GoR">
</div>



## News

**[2025.05.16]** 🎉 **GoR was accepted by ACL 2025 Main**.

**[2024.10.16]** 🌟 GoR is released.



## 📌Preliminary


### Environment Setup

```bash
# python==3.10
pip install torch==1.12.1+cu113 torchvision==0.13.1+cu113 torchaudio==0.12.1 --extra-index-url https://download.pytorch.org/whl/cu113
pip install dgl==1.0.0+cu113 -f https://data.dgl.ai/wheels/cu113/repo.html
pip install openai==0.28
pip install pandas
pip install langchain
pip install langchain-core
pip install langchain-community
pip install langchain-experimental
pip install tiktoken
pip install tqdm
pip install bert_score
pip install rouge_score
pip install networkx
pip install faiss-gpu
pip install transformers
```

### Dataset Preparation

[QMSum](https://github.com/Yale-LILY/QMSum)
[WCEP](https://huggingface.co/datasets/ccdv/WCEP-10)
[Booksum](https://huggingface.co/datasets/kmfoda/booksum)
[GovReport](https://huggingface.co/datasets/ccdv/govreport-summarization/tree/refs%2Fconvert%2Fparquet/document)
[SQuALITY](https://github.com/nyu-mll/SQuALITY)


Save the downloaded files in the `./data/[DATASET_NAME]` folder.


> \[!IMPORTANT\]
>
> Before running the experiment, please configure your API KEY in `"get_llm_response_via_api"` in `utils.py`



## ⭐Experiments



### Query Simulation and Graph Construction

Generate simulated queries and construct graphs. The constructed graphs are saved in the `./graph` folder.

```bash
# DATASET Choices: qmsum, wcep, booksum, govreport, squality
# Training Set
python graph_construction.py --cuda 0 --dataset [DATASET] --train
# Test Set
python graph_construction.py --cuda 0 --dataset [DATASET]
```


### Training Preparation

Pre-compute BERTScore and save training data in the `./training_data` folder.



```bash
# DATASET Choices: qmsum, wcep, booksum, govreport, squality
python training_preparation.py --cuda 0 --dataset [DATASET]
```



### Training


```bash
# DATASET Choices: qmsum, wcep, booksum, govreport, squality
python train.py --cuda 0 --dataset [DATASET]
```


### Evaluation


```bash
# DATASET Choices: qmsum, wcep, booksum, govreport, squality
# Generate summary results
python eval.py --cuda 0 --dataset [DATASET]
# Evaluation
python sum_eval.py --cuda 0 --file_name ./result/[DATASET].json
```



## Citation

```bibtex
@article{GoR,
  title={Graph of Records: Boosting Retrieval Augmented Generation for Long-context Summarization with Graphs},
  author={Haozhen Zhang and Tao Feng and Jiaxuan You},
  journal={arXiv preprint arXiv:2410.11001},
  year={2024}
}
```


<!-- <picture>
<source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=ulab-uiuc%2FGoR&theme=dark&type=Date">
<img width="100%" src="https://api.star-history.com/svg?repos=ulab-uiuc%2FGoR&type=Date">
</picture> -->