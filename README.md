<div align="center">
<img src="https://i.imgur.com/SekZcgb.png" alt="Image">
  <p>
    𝕏 <a href="https://twitter.com/maximelabonne">Follow me on X</a> • 
    🤗 <a href="https://huggingface.co/mlabonne">Hugging Face</a> • 
    💻 <a href="https://mlabonne.github.io/blog">Blog</a> • 
    📙 <a href="https://github.com/PacktPublishing/Hands-On-Graph-Neural-Networks-Using-Python">Hands-on GNN</a>
  </p>
   <p><em>Curated list of datasets and tools for post-training.</em></p>
</div>
<br/>

## 👍 What is a good dataset?

Data is the most valuable asset in LLM development. When building a dataset, we target the three following characteristics:

* **Accuracy**: Samples should be factually correct and relevant to their corresponding instructions. This can involve using solvers for math and unit tests for code.
* **Diversity**: You want to cover as many use cases as possible to make sure you're never out of distribution. High diversity is essential as it leads to better generalization.
* **Complexity**: Answers should be both detailed (to maximize helpfulness) and include system 2 techniques like chain of thought (to force step-by-step reasoning).

Measuring accuracy is easy in most cases but near-impossible with open-ended, subjective questions. On the other hand, clustering datasets by topic is a good way of evaluating data mixture diversity. Finally, complexity can be assessed using other LLMs acting like judges.

## 📅 Open SFT datasets

Once a model has been pre-trained on a next-token prediction task, Supervised Fine-Tuning (SFT) is used to turn it into an assistant capable of answering questions and following instructions. These datasets contain pairs of instructions and outputs to train LLMs to understand conversational structure. Unless otherwise noted, all datasets listed here are under permissive licenses (Apache 2.0, MIT, CC-BY-4.0, etc.).

### General-purpose mixtures

General-purpose datasets offer balanced mixtures of different types of data, including chat, code, and math. These datasets can be used to create general-purpose models that can handle various types of queries.

| Dataset                                                                                               | #     | Authors            | Date     | Notes                                                                                                                                                                                                                                                        |
| ----------------------------------------------------------------------------------------------------- | ----- | ------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Infinity-Instruct](https://huggingface.co/datasets/BAAI/Infinity-Instruct)                           | 7.45M | BAAI               | Aug 2024 | High-quality evolved samples based on a collection of open-source datasets.                                                                                                                                                                                  |
| [WebInstructSub](https://huggingface.co/datasets/chargoddard/WebInstructSub-prometheus)               | 2.39M | Yue et al.         | May 2024 | Instructions created by retrieving document from Common Crawl, extracting QA pairs, and refining them. See the [MAmmoTH2 paper](https://arxiv.org/abs/2405.03548) and [full set](https://huggingface.co/datasets/TIGER-Lab/WebInstructFull) (13.5M samples). |
| [The-Tome](https://huggingface.co/datasets/arcee-ai/The-Tome)                                         | 1.75M | Arcee AI           | Jul 2024 | Reranked and filtered collection of datasets with a focus on instruction following. See my [100k subset](https://huggingface.co/datasets/mlabonne/FineTome-100k).                                                                                            |
| [open-perfectblend](https://huggingface.co/datasets/mlabonne/open-perfectblend)                       | 1.42M | Xu et al., Labonne | Oct 2024 | Open reproduction of the dataset described [in this paper](https://arxiv.org/abs/2409.20370). It's a solid general-purpose instruction dataset with chat, math, code, and instruction-following data.                                                        |
| [smoltalk](https://huggingface.co/datasets/HuggingFaceTB/smoltalk)                                    | 1.1M  | Hugging Face       | Nov 2024 | Mix of existing and new datasets used to train [SmolLM2](https://huggingface.co/HuggingFaceTB/SmolLM2-1.7B-Instruct) with proper evaluations.                                                                                                                |
| [orca-agentinstruct-1M-v1](https://huggingface.co/datasets/mlabonne/orca-agentinstruct-1M-v1-cleaned) | 1.05M | Microsoft          | Nov 2024 | Subset of the AgentInstruct dataset (~25 samples) designed for Orca-3-Mistral, using raw text publicly available on the web as seed data.                                                                                                                    |
| [tulu3-sft-mixture](https://huggingface.co/datasets/allenai/tulu-3-sft-mixture)                       | 939k  | AI2                | Nov 2024 | (CC-BY-NC-4.0) SFT mixture used to train the [Tulu 3](https://huggingface.co/collections/allenai/tulu-3-models-673b8e0dc3512e30e7dc54f5). It uses public datasets and new synthetic versions, including persona-based answers for diversity.                 |
| [Open-Platypus](https://huggingface.co/datasets/garage-bAInd/Open-Platypus)                           | 24.9k | Lee et al.         | Sep 2023 | Collection of datasets that were deduplicated using Sentence Transformers (it contains an NC dataset). See [Platypus paper](https://arxiv.org/abs/2308.07317).                                                                                               |
### Math

LLMs often struggle with mathematical reasoning and formal logic, which has led to the creation of specialized datasets. These datasets can include systematic thinking and step-by-step reasoning.

| Dataset                                                                             | #    | Authors       | Date      | Notes                                                                                                                                                                      |
| ----------------------------------------------------------------------------------- | ---- | ------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [OpenMathInstruct-2](https://huggingface.co/datasets/nvidia/OpenMathInstruct-2)     | 14M  | Nvidia        | Sep 2024  | Augmented samples from GSM8K and MATH (training set) using Llama-3.1-405B-Instruct.                                                                                        |
| [NuminaMath-CoT](https://huggingface.co/datasets/AI-MO/NuminaMath-CoT)              | 859k | Jia Li et al. | July 2024 | Data used to win the first progress prize of the AI Math Olympiad. See the tool-integrated reasoning version [here](https://huggingface.co/datasets/AI-MO/NuminaMath-TIR). |
| [MetaMathQA](https://huggingface.co/datasets/meta-math/MetaMathQA)                  | 395k | Yu et al.     | Dec 2023  | Bootstrap mathematical questions by rewriting them from multiple perspectives. See [MetaMath paper](https://arxiv.org/abs/2309.12284).                                     |
| [MathInstruct](https://huggingface.co/datasets/TIGER-Lab/MathInstruct)              | 262k | Yue et al.    | Sep 2023  | Compiled from 13 math rationale datasets, six of which are newly curated, and focuses on chain-of-thought and program-of-thought.                                          |
| [Orca-Math](https://huggingface.co/datasets/microsoft/orca-math-word-problems-200k) | 200k | Mitra et al.  | Feb 2024  | Grade school math world problems generated using GPT4-Turbo. See [Orca-Math paper](https://arxiv.org/pdf/2402.14830.

