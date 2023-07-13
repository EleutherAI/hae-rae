# CSAT-QA: How Far Can LLMs Reach in Korean Language Understanding?

### Introduction

In this blog post, we release CSAT-QA, a multiple choice question answering dataset for the Korean language. The dataset includes questions collected from the College Scholastic Ability Test (CSAT), also known as the 대학수학능력시험 in South Korea, a standardized test required for university admissions in the country. In this project, we have gathered and made available 936 question-and-answer pairs from CSAT exams held between 2007 and 2022. These resources are now open-source for public use.

### Dataset Collection

The CSAT-QA dataset, encompasses four distinct curriculums: the 7th National Curriculum, the 2007 Revised Curriculum, the 2009 Revised Curriculum, and the 2015 Revised Curriculum. For the collected dataset, we implemented the following preprocessing steps:

Initially, due to the unreliability of publicly accessible Korean OCR systems, we opted to manually transcribe the CSAT test questions to ensure the quality of our dataset.

Second, we excluded questions related to "Middle Korean," an ancient form of the language. This was necessary as the majority of language models cannot encode such vocabulary.

In the subsequent phase, we manually converted all tables and graphs into the LaTeX format, while translating images into descriptive, alternative texts. This is done to fully represent complex questions in a language model-friendly manner.

Finally, we introduced four unique token pairs: \<word> \<word/>, \<sent> \<sent/>, \<par> \<par/>, and \<etc> \<etc/>. These tokens were incorporated to guide language models in comprehending questions that reference specific parts of the provided context, normally conveyed through italics or bold fonts.

### Dataset Analysis.

CSAT serves as a comprehensive assessment tool for evaluating various aspects of Korean proficiency, encompassing vocabulary, reading comprehension, literature, conversational situations, and more. As a result, the length of each sample in the dataset varies. 

In the subsequent analysis, we applied tokenizers provided by Polyglot-Ko and GPT-4 to measure the length of these samples and counted the number of tokens each one contains. The following results show the average lengths of tokens for each category.

- The total_length, which is implemented using simple len() function in python, averages approximately 1895.31 tokens.
- The total_length_polyglot, which is the number of tokens by the Polyglot-Ko tokenizer, averages approximately 1084.72 tokens. 
- The total_length_gpt4, which is the number of tokens by the GPT-4 tokenizer, averages approximately 1855.63 tokens.

Interestingly, it was found that on average, the total_length_gpt4 is approximately 1.71 times longer than total_length_polyglot. This suggests that the GPT-4 tokenizer is not as efficient in processing Korean language text compared to Polyglot-Ko, highlighting the need for native LLMs for optimized inference.

![Untitled](https://github.com/guijinSON/hae-rae/blob/main/blog/assets/csat_token.png)

In addition, we narrowed our focus and conducted an evaluation on a specific subset of 188 questions selected based on the availability of students' response accuracy. The subset comprises six distinct categories, namely Writing (WR), Grammar (GR), Reading Comprehension: Science (RCS), Reading Comprehension: Social Science (RCSS), Reading Comprehension: Humanities (RCH), and Literature (LI).

Rather than a conventional approach of balanced sampling, we filtered based on the availability of the response accuracy. As a result, the distribution of questions within our subset are imbalanced, as shown in the following figure.

![Untitled](https://github.com/guijinSON/hae-rae/blob/main/blog/assets/csat_histogram.png)

### Evaluation:

For evaluation, we compared two proprietary language models, GPT-4 and GPT-3.5-Turbo-16K, and one open-source language model, [Polyglot-Ko-12.8B](https://huggingface.co/EleutherAI/polyglot-ko-12.8b).

For GPT-4 and GPT-3.5-Turbo-16K, we used the following instruction with the model's temperature fixed at 0.01 to prompt the language model to generate the most probable answer. 
```
instruction = f"""다음을 읽고 정답으로 알맞은 것을 고르시요. [Please read the following passage and choose the correct answer.]
### Question: 
### Context: 
### Options:
(1) 
(2) 
(3) 
(4) 
(5) 
### Answer: 주어진 문제의 정답은[****The correct answer to the given question is****]"""
```
Note that the texts within the square brackets are not included in the actual prompt. They are translations for international researchers that see this post

For Polyglot-Ko-12.8B, we employed the [LM-Eval-Harness](https://github.com/EleutherAI/lm-evaluation-harness) framework for evaluation. Although all the evaluations were conducted in a zero-shot setting, the methodology used for GPT-4 and GPT-3.5-Turbo-16K is more challenging compared to the one used for Polyglot-Ko-12.8B. Consequently, direct comparisons among models using these distinct evaluation methods may potentially lead to misleading interpretations.

The evaluation results are as follows. 

| Category | Polyglot-Ko-12.8B | GPT-3.5-16k | GPT-4     | Human_Performance |
|----------|----------------|-------------|-----------|-------------------|
| WR       | 0.09           | 9.09        | 45.45     | **54.0**          |
| GR       | 0.00           | 20.00       | 32.00     | **45.41**         |
| LI       | 21.62          | 35.14       | **59.46** | 54.38             |
| RCH      | 17.14          | 37.14       | **62.86** | 48.7              |
| RCS      | 10.81          | 27.03       | **64.86** | 39.93             |
| RCSS     | 11.9           | 30.95       | **71.43** | 44.54             |
| Average  | 10.26          | 26.56       | **56.01** | 47.8              |


Our analysis shows an intriguing disparity between Language Models (LMs) and human proficiency across various tasks. Notably, while humans excel in writing (WR) questions, they comparatively underperformed in Reading Comprehension: Science (RCS) tasks. GPT-4, the latest AI model in this comparison, exhibits the opposite pattern. Despite struggling with writing, it demonstrated considerable strength in RCS tasks.

The GPT-4 also significantly outperformed GPT-3.5-16k and Polyglot-12.8B. This substantial leap in performance is aligned with expectations, given the much larger size of GPT-4, indicating the potential benefits of scaling up these models.

Lastly, the underperformance of Polyglot-Ko-12.8B is noteworthy. Its scores were below random guessing (20%), indicating limitations in the model's capabilities.

![Untitled](https://github.com/guijinSON/hae-rae/blob/main/blog/assets/csat_spyder.png)

### Release Notes

We are happy to release two versions of the dataset: CSAT-QA(FULL) and CSAT-QA(EVAL). CSAT-QA(EVAL) includes the specific 188 questions that were utilized for our evaluation, whereas CSAT-QA(FULL) includes all 936 questions contained in the complete dataset.

You can download the datasets using the following code.

<details>
<summary> CSAT-QA(FULL) </summary>

```
from datasets import load_dataset
dataset = load_dataset("HAERAE-HUB/CSAT-QA")
```
</details>

<details>
<summary> CSAT-QA(EVAL) </summary>

```
from datasets import load_dataset
import pandas as pd

dataset = load_dataset("HAERAE-HUB/CSAT-QA")
dataset = pd.DataFrame(dataset["train"]).dropna(subset=["Category"])
```
</details>

For the reproducibility of our research, we also release our instructions along with the responses generated by both the GPT-3.5-16K and GPT-4 models. 
[Download File](https://github.com/guijinSON/hae-rae/blob/main/blog/assets/test_results.csv)

### Contributors 
나건주  
박수빈  
박은우  
손규진  
염제원  
유수빈  
조하늘  
진혜원  

