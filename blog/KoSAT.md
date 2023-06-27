# What will be the Korean KSAT proficiency of the LLM model?

### Introduction

The HAE-RAE project is developing a dataset for the Korean language model to enhance Polyglot-Ko inference and instruction-following. We are conducting research beyond translation of existing English datasets to create a specialized educational and benchmark dataset representing Korean culture and knowledge.

The Ko-SAT dataset team aims to evaluate the language model's Korean language proficiency by creating a dataset of the Korean SAT subject, similar to the English SAT and LSAT datasets. The Korean SAT subject consists of four main areas: reading, literature, rhetoric and composition, and language and media, evaluating literary interpretation and utilization, aesthetic and creative abilities in literary works, communication and writing skills, and Korean norms and media utilization skills.

### Dataset

We collected data from the KSAT (수능) administered from 2007 to 2022.   
For the exams administered between 2007 and 2011, which followed the 7th national curriculum, we collected data from the 2007 to 2011 exams.   
For the exams administered between 2012 and 2016, which followed the 2007 revised curriculum, we collected data from the 2012 to 2016 exams.     
For the exams administered between 2017 and 2020, which followed the 2009 revised curriculum, we collected data from the 2017 to 2020 exams.     
For the exams administered between 2021 and 2023, which followed the 2015 revised curriculum, we collected data from the 2021 to 2023 exams.  
We selected the most difficult exam for each curriculum to ensure the same train/test distribution (i.e., the exam with the highest standardized score) as the test set.  

### Details

For Korean language problems, expressions referring to a part of the text are frequently used, and problems interpreting tables and graphs frequently appear. The dataset has undergone several processing steps to ensure that the language model can understand them.

1. Add tokens <part start><part end> to indicate paragraphs in the problem, such as (a), (b), and (c).
Add tokens <word start><word end> for underlined words or characters (ㄱ), (ㄴ), and (ㄷ).
Add <part start><part end> for parts that are larger than words but smaller than paragraphs.
Add <etc start><etc end> to indicate figures, tables, and graphs.
2. Middle Korean cannot be encoded, so it is excluded.
3. Problems related to tables, graphs, and figures are changed to LaTeX syntax or texts containing only objective facts. For example, the expression in the example below is changed as follows:

![Untitled](https://github.com/keonju2/keonju2.github.io/assets/54880474/044ba752-59fe-43e7-b635-f59a2c1e23ea)

```
<part start> (가) 설문 조사(청소년 대상)
1. UCC 제작 경험
<etc start>
\\begin{table}[]
\\begin{tabular}{ll}
제작 경험 & 응답(\\%) \\\\
있음    & 28     \\\\
없음    & 72
\\end{tabular}
\\end{table}
<etc end>

```

### Benchmark Method

For Bard, GPT-turbo 3.5, and HyperClova LK-D2, the prompts used are as follows.

```
다음 질문을 읽고 아래 선택지 중 가장 적절한 답의 번호를 고르시오.
### 문제: {문제 내용}
### 참고: {문학 작품 등 보기 내용}
### 선택지: {1~5번의 선택지 내용}
### 정답:

```

The evaluation method for Polyglot-Ko, KoAlpaca, Kullm, XGLM, KoGPT, and mT5 is likelihood. After evaluating the probability of question-answer pairs for each option, the option with the highest log likelihood is presented as the answer. However, problems with token length exceeding 2048 are excluded.

### Result

| Model | Accuracy |
| --- | --- |
| GPT-turbo 3.5 | 0.31 |
| Bard | 0.36 |
| HyperClova LK-D2 | 0.18 |

| Model | Accuracy |
| --- | --- |
| polyglot-ko-1.3b | 0.19 |
| polyglot-ko-3.8b | 0.18 |
| polyglot-ko-5.8b | 0.20 |
| polyglot-ko-12.8b | 0.18 |
| polyglot-5.8B-CoT | 0.19 |
| KoAlpaca-Polyglot-12.8B | 0.14 |
| kullm-polyglot-12.8b-v2 | 0.18 |
| kogpt6B-ryan1.5b | 0.21 |
| xglm-1.7B | 0.20 |
| xglm-2.9B | 0.20 |
| xglm-7.5B | 0.21 |
| mt5-base | 0.17 |
| mt5-large | 0.21 |
| mt5-xl | 0.20 |

### Contributors 
나건주  
박수빈  
박은우  
손규진  
염제원  
유수빈  
조하늘  
진혜원  

### Copyright
The copyright of this material belongs to the Korea Institute for Curriculum and Evaluation and is prohibited from using it for research purposes.
