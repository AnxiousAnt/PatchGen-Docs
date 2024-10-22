# Training Your Custom PatchGen Model

## Introduction
This guide will walk you through the process of training your own custom version of the **PatchGen** model using either your own data or the datasets already collected. By following these steps, you'll be able to fine-tune the model to generate Purr Data (Pd) patches from natural language prompts, tailored to your specific use case.

## Choosing and Preparing the Dataset
You can either use the datasets already curated for this project or your own set of Pd patches.

### 1. Pre-existing Datasets:
- **14k Dataset**: A filtered and cleaned dataset containing only simple and small Pd patches. This is recommended for those who want more straightforward and easier-to-handle data for their model.
- **39k Dataset**: A larger dataset with a wider variety of Pd patches. If you're looking to expose the model to more complex patches and a diverse set of examples, this is the dataset to use.
- **3k annotated examples**: The dataset contains **~3,000** examples of annotated prompts and their corresponding Pd patches.This dataset was used for **instruction fine-tuning** in the second phase of training. The goal was to teach the model to generate patches based on natural language instructions.
  
To use these datasets, visit the following links:
- [14k Dataset](https://huggingface.co/datasets/ParZiVal04/Pd-patches-14k-dataset)
- [39k Dataset](https://huggingface.co/datasets/ParZiVal04/pd-patches-dataset)
- [3k annotated dataset](https://huggingface.co/datasets/parzi-parzi/patch-gen-dataset-v0.8.7)

### 2. Using Your Own Dataset:
If you wish to train the model with your own data, ensure that your Pd patches are structured correctly:
- **Patch Contents**: The actual content of each Pd patch should be clearly written in Pure Data’s format.
- **Annotations (if applicable)**: Include prompts and explanations if you intend to fine-tune the model for generating patches from natural language instructions.

## Training the Model
To train your custom version of the PatchGen model, you have several options for hardware and environments:

### 1. Google Colab
You can run the training script on **Google Colab**, which provides free access to GPUs but has some limitations:
- **Free Tier**: Allows around 3 hours of continuous usage before the runtime is disconnected.
- **Upgrading to Colab Pro**: If you need longer training times or more powerful GPUs, consider upgrading to **Colab Pro** for uninterrupted access.

### 2. Kaggle
Alternatively, you can run the training code on **Kaggle**, which also provides access to free GPUs for machine learning.

### 3. Local or Cloud GPUs
If you have access to local hardware with a GPU, you can run the training script on your own machine. Additionally, renting cloud GPUs from platforms like **AWS** or **Google Cloud** is an option for longer and more resource-intensive training sessions.

## Running the Training Script

Notebook: [![Training code](_images/colab.svg)](https://colab.research.google.com/drive/1eD9mpqKKMzibqrldz7SlQIGrpNBmpKLG?usp=sharing)

You can use the provided Python notebook to train the model. Follow these steps to begin the training:

1. **Set Up Environment**: Make sure the required libraries (such as `torch`, `transformers`, and `unsloth`) are installed in your environment.
2. **Configure the Model**: Load the base Mistral 7B model (or any other model), set up LoRA (Low-Rank Adaptation) parameters, and configure the training process.
3. **Run Training**: Execute the training script using the chosen dataset, monitor the training progress, and save checkpoints for later use.

For more detailed instructions and parameter configurations, refer to the following documents:
- [LoRA Parameters Encyclopedia](https://docs.unsloth.ai/basics/lora-parameters-encyclopedia)
- [Hugging Face Supervised Fine-tuning Trainer Docs](https://huggingface.co/docs/trl/sft_trainer)
