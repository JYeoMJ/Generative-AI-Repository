## Generative AI with Large Language Models (By DeepLearning.AI & Amazon Web Services)

**About this Course**
In Generative AI with Large Language Models (LLMs), you’ll learn the fundamentals of how generative AI works, and how to deploy it in real-world applications.

By taking this course, you'll learn to:

Deeply understand generative AI, describing the key steps in a typical LLM-based generative AI lifecycle, from data gathering and model selection, to performance evaluation and deployment
- Describe in detail the transformer architecture that powers LLMs, how they’re trained, and how fine-tuning enables LLMs to be adapted to a variety of specific use cases
- Use empirical scaling laws to optimize the model's objective function across dataset size, compute budget, and inference requirements
- Apply state-of-the art training, tuning, inference, tools, and deployment methods to maximize the performance of models within the specific constraints of your project 
- Discuss the challenges and opportunities that generative AI creates for businesses after hearing stories from industry researchers and practitioners

This repository contains the lecture notes for this course and the associated jupyter notebooks for labs.

### Lab Directory:

* **Lab 1 - Generative AI Use Case: Summarize Dialogue**

  In this lab, you will do the dialogue summarization task using generative AI. You will explore how the input text affects the output of the model, and perform prompt engineering to direct it towards the task you need. By comparing zero shot, one shot, and few shot inferences, you will take the first step towards prompt engineering and see how it can enhance the generative output of Large Language Models.  
  
* **Lab 2 - Fine-Tune Generative AI Model for Dialogue Summarization**
  
  In this notebook, you will fine-tune an existing LLM from Hugging Face for enhanced dialogue summarization. You will use the FLAN-T5 model, which provides a high quality instruction tuned model and can summarize text out of the box. To improve the inferences, you will explore a full fine-tuning approach and evaluate the results with ROUGE metrics. Then you will perform PEFT fine-tuning, evaluate the resulting model and see that the benefits of PEFT outweigh the slightly-lower performance metrics.
  
* **Lab 3 - Fine-tune FLAN-T5 with reinforcement learning to generate more-positive summaries**

  In this notebook, you will fine-tune a FLAN-T5 model to generate less toxic content by Facebook's hate speech reward model. The reward model is a binary classifier that predicts either "not hate" or "hate" for the given text. You will use Proximal Policy Optimization (PPO) to fine-tune and detoxify the model.  
