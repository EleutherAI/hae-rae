# CSAT-QA: How Far Can LLMs Reach in Korean Language Understanding?

### Introduction

In this blog post, we release CSAT-QA, a multiple choice question answering dataset for the Korean Language. The dataset collected questions from the College Scholastic Ability Test (CSAT), also known as the 대학수학능력시험 in South Korea, a standardized test required for university admissions in the country. In this project, we have gathered and made available 936 question and answer pairs from CSAT exams held between 2007 and 2022. These resources are now open-source for public use.

### Dataset Collection

The CSAT-QA dataset, encompasses four distinct curriculums: the 7th National Curriculum, the 2007 Revised Curriculum, the 2009 Revised Curriculum, and the 2015 Revised Curriculum. For the collected dataset we implement the following preprocessing steps:

Initially, due to the unreliability of publicly accessible Korean OCR systems, we opted to manually transcribe the CSAT test questions to ensure accuracy and precision in our dataset.

Second, we excluded questions related "Middle Korean," an ancient form of the language. This was necessary as the majority of language models cannot encode such vocabulary.

In the subsequent phase, we manually converted all tables and graphs into a LaTeX format, while translating images into descriptive, alternative texts. This strategy was designed to render complex information more digestible and language model-friendly.

Finally, we introduce four unique token pairs: <word> <word/>, <sent> <sent/>, <par> <par/>, and <etc> <etc/>. These tokens were incorporated to guide language models in comprehending questions that reference specific parts of the provided context, normally conveyed through italics or bold fonts.

### Dataset Analysis.

CSAT serves as a comprehensive assessment tool for evaluating various aspects of Korean proficiency, encompassing vocabulary, reading comprehension, literature, conversational situations, and more. As a result, the length of each sample in the dataset vary. 

In the subsequent analysis, we applied tokenizers provided by Polyglot and GPT-4 to measure the length of these samples and count the number of tokens each one contains. The results show that the average lengths of tokens for each category are as follows:

- The total_length, which implements a simple len() function in python, averages approximately 1895.31 tokens.
- The total_length_polyglot, tokenized using the Polyglot tokenizer, averages approximately 1084.72 tokens.
- The total_length_gpt4, tokenized using the GPT-4 tokenizer , averages approximately 1855.63 tokens.

Interestingly, it was found that on average, the total_length_gpt4 is approximately 1.71 times longer than total_length_polyglot. This suggest that the GPT-4 tokenizer is not as efficient in processing Korean language text compared to Polyglot, highlighting the need of native LLMs for optimized inference.

![Untitled](https://github.com/keonju2/keonju2.github.io/assets/54880474/044ba752-59fe-43e7-b635-f59a2c1e23ea)

### Evaluation:

IIn this blog post, we narrow our focus and conduct an evaluation on a specific subset of 188 questions selected based on the availability of students' response accuracy. For the purpose of this evaluation, we've employed two cutting-edge language models: GPT-4 and GPT-3.5-Turbo-16K. The following prompt was used for evaluation:
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
It should be noted that the text within the square brackets was not incorporated in the actual prompt. Rather, it has been provided here as a translation to facilitate better comprehension.
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
