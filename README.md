<p align="center">
    <!-- community badges -->
    <a href="https://discord.gg/G2rSbAf8uP"><img src="https://img.shields.io/badge/Join-Discord-blue.svg"/></a>
    <!-- license badge -->
    <a href="https://github.com/Eladlev/AutoPrompt/blob/main/LICENSE">
        <img alt="License" src="https://img.shields.io/badge/License-Apache_2.0-blue.svg"></a>
</p>

# 📝 AutoPrompt


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

**Auto Prompt is a prompt optimization framework designed to enhance and perfect your prompts for real-world use cases.**

The framework automatically generates high-quality, detailed prompts tailored to user intentions. It employs a refinement (calibration) process, where it iteratively builds a dataset of challenging edge cases and optimizes the prompt accordingly. This approach not only reduces manual effort in prompt engineering but also effectively addresses common issues such as prompt [sensitivity](https://arxiv.org/abs/2307.09009) and inherent prompt [ambiguity](https://arxiv.org/abs/2311.04205) issues.


**Our mission:** Empower users to produce high-quality robust prompts using the power of large language models (LLMs).

# Why Auto Prompt?
- **Prompt Engineering Challenges.** The quality of LLMs greatly depends on the prompts used. Even [minor changes](#prompt-sensitivity-example) can significantly affect their performance. 
- **Benchmarking Challenges.**  Creating a benchmark for production-grade prompts is often labour-intensive and time-consuming.
- **Reliable Prompts.** Auto Prompt generates robust high-quality prompts, offering measured accuracy and performance enhancement using minimal data and annotation steps.
- **Modularity and Adaptability.** With modularity at its core, Auto Prompt integrates seamlessly with popular open-source tools such as LangChain, Wandb, and Argilla, and can be adapted for a variety of tasks, including data synthesis and prompt migration.
## Problem Description:

Recent advancements in Large Language Models (LLMs) have showcased significant improvements in generative tasks, yet these models remain highly sensitive to the specific prompts provided by users. This sensitivity manifests as variations in performance not only when prompts are slightly altered, but also when model versions change, leading to unpredictable shifts in behavior across a spectrum of tasks. Current strategies to address this include the use of soft prompts and meta-prompts that require iterative optimization and deep access to the LLMs themselves. However, these methods depend heavily on large, high-quality benchmarks which are often unavailable in real-world scenarios and are costly to iterate over. Moreover, without adequate calibration to user intentions, LLMs might produce inaccurate outputs due to misunderstood prompts.

This project introduces the Intent-based Prompt Calibration (IPC) system based on the paper "Intent-based Prompt Calibration: Enhancing prompt optimization with synthetic boundary cases" [4], designed to refine and optimize prompts based on synthetic boundary examples specifically generated to encapsulate the user’s task requirements. This system not only aims to mitigate the challenge of prompt sensitivity but also adapts the LLM's output to more accurately reflect the user's intended use case, particularly in environments like content moderation where data distributions are typically imbalanced. The IPC system also incorporates a novel ranking mechanism to further enhance prompt optimization for generative tasks, reducing reliance on extensive manual annotation and large-scale data requirements.

## Context of the Problem:

The importance of addressing prompt sensitivity in Large Language Models (LLMs) is multifaceted. Firstly, it enhances reliability and predictability, essential for consistent AI performance across various applications. Secondly, it promotes scalability and efficiency, enabling LLMs to be fine-tuned for specific tasks without extensive resources, thereby reducing computational and economic costs. Thirdly, optimizing prompts to align with user intentions allows for customized, effective solutions, crucial for broadening AI applicability and user satisfaction. Lastly, tackling this issue aids in democratizing AI technology, ensuring more organizations can leverage these advancements with less specialized knowledge, and improving model explainability and transparency for ethical AI practices. Addressing these challenges is vital for the practical and ethical deployment of LLMs in real-world scenarios.
## System Overview

![System Overview](./docs/AutoPrompt_Diagram.png)

The system is designed for real-world scenarios, such as moderation tasks, which are often  challenged by imbalanced data distributions. The system implements the [Intent-based Prompt Calibration](https://arxiv.org/abs/2402.03099) method. The process begins with a user-provided initial prompt and task description, optionally including user examples. The refinement process iteratively generates diverse samples, annotates them via user/LLM, and evaluates prompt performance, after which an LLM suggests an improved prompt.  

The optimization process can be extended to content generation tasks by first devising a ranker prompt and then performing the prompt optimization with this learned ranker. The optimization concludes upon reaching the budget or iteration limit.  


This joint synthetic data generation and prompt optimization approach outperform traditional methods while requiring minimal data and iterations. Learn more in our paper
[Intent-based Prompt Calibration: Enhancing prompt optimization with synthetic boundary cases](https://arxiv.org/abs/2402.03099) by E. Levi et al. (2024).




## Demo

![pipeline_recording](./docs/autoprompt_recording.gif)

## Evalulation
They used a high-capacity model, GPT-4 Turbo, to create ground truth data. This step is crucial as it provides a benchmark for comparing the effectiveness of different prompts. In addition they used adversarial synthetic data generated from 10 initial samples from the IMDB dataset. It involves creating examples that are specifically designed to challenge or 'fool' the model. These are known as boundary cases.

After synthetic adversarial examples are generated by the system, human annotators evaluate these examples to determine how well they align with the intended task requirements and whether they effectively challenge the model. This helps in ensuring that the synthetic data is of high quality and truly representative of potential real-world complexities.

Human annotators also review the responses generated by the LLM based on the current prompts. They assess whether the responses are accurate, relevant, and appropriately detailed, providing a human judgment that can capture nuances possibly missed by automated metrics

Finally the metaprompts are adjusted based on the human annotations.

The researchers evaluate the effectiveness of their Intent-based Prompt Calibration (IPC) system using three binary classification tasks: spoiler detection, sentiment analysis, and parental guidance detection.

The proposed method outperformed other methods such as the OPRO[5] and PE[6].The other methods exhibit a higher variance in results, which suggests they may be less reliable or consistent, especially when the number of training samples is small. This variance can be detrimental in real-world applications where stable and predictable outputs are necessary.The other methods exhibit a higher variance in results, which suggests they may be less reliable or consistent, especially when the number of training samples is small. This variance can be detrimental in real-world applications where stable and predictable outputs are necessary.

## Conclusion and Future Direction

Future work could be done to refine the meta-prompts themselves. This involves improving how the meta-prompts are generated and used within the system to make them even more effective at guiding the prompt optimization process. All multimodality could be introduced to help the model generate better prompts with help images and audio.

In Conclusion, the paper offers valuable learnings about improving the efficiency and effectiveness of Large Language Models (LLMs) through refined prompt engineering. The most important part according to me was the use of synthetic data to generate boundary cases, which aids in iteratively refining prompts to better align with user intentions, thereby addressing the high sensitivity of LLMs to prompt variations. The IPC method showcases a modular and flexible system architecture, allowing for easy adaptation across different tasks and settings, including multi-modality and in-context learning. Additionally, the paper highlights the benefits of minimizing human annotation efforts by relying on synthetic data for prompt calibration, demonstrating significant improvements in model performance with fewer data requirements. These insights underscore the potential of IPC to enhance the practical utility of LLMs in diverse real-world applications, particularly in scenarios with limited data availability or specific performance criteria.
## 📖 Documentation
 - [How to install](docs/installation.md) (Setup instructions)
 - [Prompt optimization examples](docs/examples.md) (Use cases: movie review classification, generation, and chat moderation)
 - [How it works](docs/how-it-works.md) (Explanation of pipelines)
 - [Architecture guide](docs/architecture.md) (Overview of main components)

## Features
- 📝 Boosts prompt quality with a minimal amount of data and annotation steps.
- 🛬 Designed for production use cases like moderation, multi-label classification, and content generation.
- ⚙️ Enables seamless migrating of prompts across model versions or LLM providers.
- 🎓 Supports prompt squeezing. Combine multiple rules into a single efficient prompt.


## QuickStart
AutoPrompt requires `python <= 3.10`
<br />

> **Step 1** - Download the project

```bash
git clone git@github.com:Eladlev/AutoPrompt.git
cd AutoPrompt
```

<br />

> **Step 2** - Install dependencies

Use either Conda or pip, depending on your preference. Using Conda:
```bash
conda env create -f environment_dev.yml
conda activate AutoPrompt
```

Using pip: 
```bash
pip install -r requirements.txt
```

Using pipenv:
```bash
pip install pipenv
pipenv sync
```

<br />

> **Step 3** - Configure your LLM. 

Set your OpenAI API key  by updating the configuration file `config/llm_env.yml`
- If you need help locating your API key, visit this [link](https://help.openai.com/en/articles/4936850-where-do-i-find-my-api-key).

- We recommend using [OpenAI's GPT-4](https://platform.openai.com/docs/guides/gpt) for the LLM. Our framework also supports other providers and open-source models, as discussed [here](docs/installation.md#configure-your-llm).

<br />

> **Step 4** - Configure your Annotator
- Select an annotation approach for your project. We recommend beginning with a human-in-the-loop method, utilizing [Argilla](https://docs.argilla.io/en/latest/index.html). Follow the [Argilla setup instructions](docs/installation.md#configure-human-in-the-loop-annotator-) to configure your server. Alternatively, you can set up an LLM as your annotator by following these [configuration steps](docs/installation.md#configure-llm-annotator-).

- The default predictor LLM, GPT-3.5, for estimating prompt performance, is configured in the `predictor` section of `config/config_default.yml`.

- Define your budget in the input config yaml file using the `max_usage parameter`. For OpenAI models, `max_usage` sets the maximum spend in USD. For other LLMs, it limits the maximum token count.

<br />


> **Step 5** - Run the pipeline

First, configure your labels by editing `config/config_default.yml`
```
dataset:
    label_schema: ["Yes", "No"]
```


For a **classification pipeline**, use the following command from your terminal within the appropriate working directory: 
```bash
python run_pipeline.py
```
If the initial prompt and task description are not provided directly as input, you will be guided to provide these details.  Alternatively, specify them as command-line arguments:
```bash
python run_pipeline.py \
    --prompt "Does this movie review contain a spoiler? answer Yes or No" \
    --task_description "Assistant is an expert classifier that will classify a movie review, and let the user know if it contains a spoiler for the reviewed movie or not." \
    --num_steps 30
```






