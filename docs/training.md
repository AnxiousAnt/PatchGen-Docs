# Base Model used for this project: Mistral 7B
I utilized the **Mistral 7B** model from Mistral AI, which is one of the best open-sourced language models of its size.
To read more about the model, visit: [MistralAI](https://mistral.ai/news/announcing-mistral-7b/)

# Training Phases
#### The training process was carried out in two stages:
### Phase 1: Continued Pretraining

- **Objective**: Expose the model to Pd syntax and structure.
- **Method**: I continued-pretraining the model using qLoRA on a large dataset of patches.
- **Dataset**: [ParZiVal04/Pd-patches-14k-dataset](https://huggingface.co/datasets/ParZiVal04/Pd-patches-14k-dataset) – Contains approximately 14,000 Pd patches.
- **Training Duration**: ~20 hours on a **Tesla T4 GPU**.

This phase provided the model with foundational knowledge of Pd’s syntax and structural elements.

### Phase 2: Instruction Fine-Tuning
- **Objective**: Equip the model to generate Pd patches from natural language instructions.
- **Method**: I used qLoRA for fine-tuning on a dataset with annotated examples of prompts and their corresponding Pd patches.
- **Dataset**: [parzi-parzi/patch-gen-dataset-v0.8.7](https://huggingface.co/datasets/parzi-parzi/patch-gen-dataset-v0.8.7) – Contains approximately 3,000 annotated examples.
- **Training Duration**: ~12 hours on a **Tesla T4 GPU**.

This phase enables the model to interpret and respond to specific user prompts. 