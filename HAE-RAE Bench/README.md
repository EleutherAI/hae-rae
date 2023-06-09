# HAE-RAE BENCH

## About HAE-RAE BENCH
 HAE-RAE Bench is a specialized benchmark developed to assess the proficiency of language models within the Korean context. 
 This benchmark, encompassing six comprehensive tasks spanning vocabulary, history, and general knowledge, is tailored to test the ability of a language model 
 to both comprehend and retain information exclusive to Korean corpora.

## HAE-RAE BENCH (v1)
Following table is an overview of the HAE-RAE benchmark. 
"-" for source denotes that the questions were crafted by the contributors of the project.

| Category                  | Sample Size | Source |
|---------------------------|-------------|--------|
| Loan Words (LW)           | 169         | NIKL   |
| Rare Words (RW)           | 405         | -      |
| Standard Nomenclature (SN)| 153         | NIKL   |
| Reading Comprehension (RC)| 447         | KLAT   |
| General Knowledge (GK)    | 176         | -      |
| History (HI)              | 188         | -      |

#### Benchmark Results (Ongoing)

##### Evaluation Methods 

  - 3-shot: For LLMs (Text-Davinci-003 & HyperClova LK-D2) we provide three instructive examples and an initially incomplete example, with the model expected to respond with a number from one to five, indicative of its most probable answer.   
  
- log-likelihood: For the remaining models, we evaluate the probability of an instruction-answer pair for each available option in every question. The option with the highest log-likelihood indicates the most probable answer 
  
  - **Disclaimer: 3-shot is more challenging than the log-likelihood method, therefore direct comparisons between models using these different evaluation methods can be misleading.**



  
| Models            | LW | RW | SN | RC | HI | GK | Av. (w/o KGK) |
|-------------------|------------|------------|----------------------|-----------------------|---------|-------------------|---------------|
| Text-Davinci-003  | 62.2       | 62.2       | 58.7                 | 60.1                  | 30.3    | 21.4              | 49.2 (54.7)   |
| HyperClova LK-D2  | 83.1       | 82.3       | 78.0                 | 54.5                  | 81.6    | 45.1              | 70.8 (75.9)   |
| Polyglot-Ko 1.3B  | 42.0       | 41.0       | 38.6                 | 33.1                  | 48.4    | 25.6              | 38.1 (40.6)   |
| Polyglot-Ko 3.8B  | 48.5       | 42.5       | 41.8                 | 36.0                  | 58.0    | 22.7              | 41.6 (45.4)   |
| Polyglot-Ko 5.8B  | 52.1       | 51.6       | 46.4                 | 43.2                  | 67.0    | 27.8              | 48.0 (52.1)   |
| Polyglot-Ko 12.8B | 68.6       | 48.6       | 41.2                 | 40.3                  | 68.6    | 28.4              | 49.3 (53.5)   |
| KoGPT-ryan-6B     | 49.1       | 46.7       | 45.8                 | 37.4                  | 62.2    | 25.6              | 44.4 (48.2)   |
| XGLM-1.7B         | 21.3       | 22.2       | 29.4                 | 28.9                  | 17.6    | 26.1              | 24.2 (23.9)   |
| XGLM-2.9B         | 26.6       | 24.4       | 32.7                 | 32.0                  | 23.4    | 26.7              | 27.6 (27.8)   |
| XGLM-7.5B         | 37.9       | 25.7       | 41.2                 | 33.6                  | 27.7    | 26.1              | 32.0 (33.2)   |
| mT5-Base          | 36.1       | 18.8       | 22.9                 | 23.7                  | 19.1    | 25.6              | 24.4 (24.7)   |
  

<details>
<summary>Polyglot-12.8B Variants (KoAlpaca, KuLLM)</summary>
<div markdown="1">

| Models            | LW | RW | SN | RC | HI | GK | Av. (w/o KGK) |
|-------------------|------------|------------|----------------------|-----------------------|---------|-------------------|---------------|
| Polyglot-Ko 12.8B | 68.6       | 48.6       | 41.2                 | 40.3                  | 68.6    | 28.4              | 49.3 (53.5)   |
| kullm-v2 (w/o template) | 57.4 | 40.0       | 48.4                 | 38.3                  | 71.8    | 29.0              | 47.5 (51.2)   | 
| kullm-v2 (w template)   | 85.2 | 40.0       | 44.9                 | 38.7                  | 60.6    | 27.8              | 49.5 (53.9)   |  
| KoAlpaca-Polyglot-12.8B (w/o template) | 67.5 | 63.2      | 61.4   | 44.3                  | 80.3    | 30.0              | **57.8 (63.3)**   | 
 
  
  - We used the template from [prompt_no_input](https://github.com/nlpai-lab/KULLM/blob/master/templates/kullm.json) for kullm-v2 (w template). 

</div>
</details>

## How to Use

If you are interested in accessing, using this dataset for your research, or being included in the HAE-RAE BENCH leaderboard, please reach out to us.
You can contact us via email at [spthsrbwls123@yonsei.ac.kr](mailto:spthsrbwls123@yonsei.ac.kr).

## Acknowledgement
This project was made possible thanks to OnelineAI(https://www.onelineai.com/).

## Citation and Related Information
### BibTeX entry

If you find our work useful, please consider citing:

```bibtext
@misc{haeraebench,
    author = {Son, Guijin and Lee, Hanwool and Kim, Suwan and Kim, Huiseo and Lee, Jae Cheol and Yeom, Je Won and Jung, Jihyu and Kim, Jung Woo and Kim, Songseong},
    title = {HAE-RAE Bench: Evaluation of Korean Knowledge in Language Models},
    year = {2023},
    publisher = {GitHub},
    journal = {GitHub repository}
    howpublished = {\url{https://github.com/EleutherAI/hae-rae/tree/main/HAE-RAE%20Bench}},
}
```

<details>
<summary><strong> References </strong></summary>
<div markdown="1">

 ```bibtex
@misc{polyglot-ko,
  title = {{Polyglot-Ko: Open-Source Korean Autoregressive Language Model}},
  author = {Ko, Hyunwoong and Yang, Kichang and Ryu, Minho and Choi, Taekyoon and Yang, Seungmu and Hyun, jiwung and Park, Sungho},
  url = {https://www.github.com/eleutherai/polyglot},
  month = {9},
  year = {2022},
}
```

```bibtex
@misc{alpaca,
  author = {Rohan Taori and Ishaan Gulrajani and Tianyi Zhang and Yann Dubois and Xuechen Li and Carlos Guestrin and Percy Liang and Tatsunori B. Hashimoto },
  title = {Stanford Alpaca: An Instruction-following LLaMA model},
  year = {2023},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/tatsu-lab/stanford_alpaca}},
}
```

```bibtex
@misc{kullm,
  author = {NLP & AI Lab and Human-Inspired AI research},
  title = {KULLM: Korea University Large Language Model Project},
  year = {2023},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/nlpai-lab/kullm}},
}
```
 
```bibtex
 @article{lin2021few,
  title={Few-shot learning with multilingual language models},
  author={Lin, Xi Victoria and Mihaylov, Todor and Artetxe, Mikel and Wang, Tianlu and Chen, Shuohui and Simig, Daniel and Ott, Myle and Goyal, Naman and Bhosale, Shruti and Du, Jingfei and others},
  journal={arXiv preprint arXiv:2112.10668},
  year={2021}
}
 ```
 
 ```bibtex
 @inproceedings{kim-etal-2021-changes,
    title = "What Changes Can Large-scale Language Models Bring? Intensive Study on {H}yper{CLOVA}: Billions-scale {K}orean Generative Pretrained Transformers",
    author = "Kim, Boseop  and
      Kim, HyoungSeok  and
      Lee, Sang-Woo  and
      Lee, Gichang  and
      Kwak, Donghyun  and
      Dong Hyeon, Jeon  and
      Park, Sunghyun  and
      Kim, Sungju  and
      Kim, Seonhoon  and
      Seo, Dongpil  and
      Lee, Heungsub  and
      Jeong, Minyoung  and
      Lee, Sungjae  and
      Kim, Minsub  and
      Ko, Suk Hyun  and
      Kim, Seokhun  and
      Park, Taeyong  and
      Kim, Jinuk  and
      Kang, Soyoung  and
      Ryu, Na-Hyeon  and
      Yoo, Kang Min  and
      Chang, Minsuk  and
      Suh, Soobin  and
      In, Sookyo  and
      Park, Jinseong  and
      Kim, Kyungduk  and
      Kim, Hiun  and
      Jeong, Jisu  and
      Yeo, Yong Goo  and
      Ham, Donghoon  and
      Park, Dongju  and
      Lee, Min Young  and
      Kang, Jaewook  and
      Kang, Inho  and
      Ha, Jung-Woo  and
      Park, Woomyoung  and
      Sung, Nako",
    booktitle = "Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing",
    month = nov,
    year = "2021",
    address = "Online and Punta Cana, Dominican Republic",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2021.emnlp-main.274",
    doi = "10.18653/v1/2021.emnlp-main.274",
    pages = "3405--3424",
 ```
 
 ```bibtex
 @inproceedings{xue-etal-2021-mt5,
    title = "m{T}5: A Massively Multilingual Pre-trained Text-to-Text Transformer",
    author = "Xue, Linting  and
      Constant, Noah  and
      Roberts, Adam  and
      Kale, Mihir  and
      Al-Rfou, Rami  and
      Siddhant, Aditya  and
      Barua, Aditya  and
      Raffel, Colin",
    booktitle = "Proceedings of the 2021 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies",
    month = jun,
    year = "2021",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2021.naacl-main.41",
    doi = "10.18653/v1/2021.naacl-main.41",
    pages = "483--498",
}
 ```

 ```bibtex
 @article{ouyang2022training,
  title={Training language models to follow instructions with human feedback},
  author={Ouyang, Long and Wu, Jeffrey and Jiang, Xu and Almeida, Diogo and Wainwright, Carroll and Mishkin, Pamela and Zhang, Chong and Agarwal, Sandhini and Slama, Katarina and Ray, Alex and others},
  journal={Advances in Neural Information Processing Systems},
  volume={35},
  pages={27730--27744},
  year={2022}
}
 ```
 </div>
</details>
 


  





