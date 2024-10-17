# Training Code Documentation

This document explains the various sections of the training code for the **PatchGen** model based on the **Mistral 7B** model. The training was performed using qLoRA (quantized Low-Rank Adaptation) for continued-pretraining and fine-tuning the base model on task-specific datasets.

**Training code:**  [![Training code](_images/colab.svg)](https://colab.research.google.com/drive/1eD9mpqKKMzibqrldz7SlQIGrpNBmpKLG?usp=sharing)

Refer to the following docs for more details:
- [lora parameters encyclopedia](https://docs.unsloth.ai/basics/lora-parameters-encyclopedia)
- [Hugging face Supervised Fine-tuning Trainer docs](https://huggingface.co/docs/trl/sft_trainer)

## Dependencies

Ensure the following libraries are installed before running the training code:

- **torch** (v2.4.0): Provides the deep learning framework used for the model's operations.
- **xformers** (v0.0.27.post2): Provides memory-efficient transformer components.
- **triton**: For optimizing model execution.
- **unsloth**: Provides helper classes and tools for working with models, including LoRA.

```python
#colab
!pip install unsloth
!pip uninstall unsloth -y && pip install --upgrade --no-cache-dir "unsloth[colab-new] @ git+https://github.com/unslothai/unsloth.git"
```
```python
#kaggle 
# Install required libraries and remove previous versions of torch
!pip install pip3-autoremove
!pip-autoremove torch torchvision torchaudio -y
!pip install "torch==2.4.0" "xformers==0.0.27.post2" triton torchvision torchaudio
!pip install "unsloth[kaggle-new] @ git+https://github.com/unslothai/unsloth.git"

import os
os.environ["WANDB_DISABLED"] = "true"  # Disable Weights and Biases tracking
```

---

## 1. Model Loading

The model is loaded using the **FastLanguageModel** class from the **unsloth** library. This model is based on Mistral 7B and is loaded with a maximum sequence length of 2048 tokens and 4-bit quantization.

```python
from unsloth import FastLanguageModel
import torch

# Define parameters for loading the model
max_seq_length = 2048  # Maximum token length
dtype = None  # Data type (default)
load_in_4bit = True  # Load model using 4-bit quantization

# Load pre-trained model
model, tokenizer = FastLanguageModel.from_pretrained(
    model_name="unsloth/mistral-7b-v0.3-bnb-4bit",
    max_seq_length=max_seq_length,
    dtype=dtype,
    load_in_4bit=load_in_4bit,
)
```

---

## 2. Model Configuration with LoRA

In this section, we configure **LoRA (Low-Rank Adaptation)** for the model. This technique reduces the number of trainable parameters and focuses on specific model layers to adapt efficiently with fewer resources.

```python
model = FastLanguageModel.get_peft_model(
    model,
    r=128,  # LoRA rank
    target_modules=["q_proj", "k_proj", "v_proj", "o_proj", "gate_proj", 
                    "up_proj", "down_proj", "embed_tokens", "lm_head"],  # Target layers for LoRA
    lora_alpha=32,  # Scaling factor for LoRA
    lora_dropout=0,  # No dropout for LoRA layers
    bias="none",  # No bias adaptation
    use_gradient_checkpointing="unsloth",  # Efficient memory usage
    random_state=9984,  # Random seed
    use_rslora=True,  # Use Random Sparse LoRA
    loftq_config=None,  # Quantization config (if applicable)
)
```

---

## 3. Data Loading and Preprocessing

This section loads the dataset and prepares it for training, followed by shuffling and batching the data.

```python
format_prompt = """
{}"""

EOS_TOKEN = tokenizer.eos_token # add EOS_TOKEN
def formatting_prompts_func(examples):
    texts  = examples["Patch Contents"]
    outputs = []
    for text in texts:
        text = format_prompt.format(text) + EOS_TOKEN
        outputs.append(text)
    return { "text" : outputs, }
pass

from datasets import load_dataset

dataset = load_dataset("ParZiVal04/Pd-patches-14k-dataset", split = "train",)

dataset = dataset.map(formatting_prompts_func, batched = True,)

for row in dataset[:5]["Patch Contents"]:
    print("=========================")
    print(row)
```

---

## 4. Training Loop (Continued Pretraining)

The training process is executed here with a progress tracker. This section includes the core training loop, loss calculation, and checkpoint saving.

```python
from transformers import TrainingArguments
from unsloth import is_bfloat16_supported
from unsloth import UnslothTrainer, UnslothTrainingArguments

trainer = UnslothTrainer(
    model = model,
    tokenizer = tokenizer,
    train_dataset = dataset,
    dataset_text_field = "text",
    max_seq_length = max_seq_length,
    dataset_num_proc = 2,

    args = UnslothTrainingArguments(
        per_device_train_batch_size = 2,
        gradient_accumulation_steps = 8,

        warmup_ratio = 0.1,
        num_train_epochs = 1,

        learning_rate = 5e-5,
        embedding_learning_rate = 1e-5,

        fp16 = not is_bfloat16_supported(),
        bf16 = is_bfloat16_supported(),
        logging_steps = 1,
        optim = "adamw_8bit",
        weight_decay = 0.01,
        lr_scheduler_type = "linear",
        seed = 3407,
        output_dir = "outputs",
    ),
)

trainer_stats = trainer.train()
```

---

## 5. Inference

For inference, the model is used to generate new patches based on input prompts. This section sets the model in inference mode and processes a prompt for generation.

```python
FastLanguageModel.for_inference(model)

# Define the input prompt for patch generation
inputs = tokenizer(
    [
        alpaca_prompt.format(
            "create a Pd patch that matches the following request.",  # Instruction
            "Create a Pure Data patch that takes an integer and shifts its binary representation to the right by a specified number of places.",  # Input
            "",  # Leave output blank for generation
        )
    ], return_tensors="pt"
).to("cuda")  # Use GPU for inference

# Stream the generated text
from transformers import TextStreamer
text_streamer = TextStreamer(tokenizer)

# Generate the patch
_ = model.generate(**inputs, streamer=text_streamer, max_new_tokens=512)
```

---

## 6. Model Export to GGUF Format

This section handles exporting the trained model to **GGUF** for compatibility with different inference tools, such as **Ollama, llama.cpp**.

```python
# Save model to different GGUF formats
if False: model.save_pretrained_gguf("model", tokenizer)
if False: model.push_to_hub_gguf("hf/model", tokenizer, token="")

# Save to 16-bit GGUF
if False: model.save_pretrained_gguf("model", tokenizer, quantization_method="f16")
if False: model.push_to_hub_gguf("hf/model", tokenizer, quantization_method="f16", token="")

# Save to q4_k_m GGUF
if False: model.save_pretrained_gguf("model", tokenizer, quantization_method="q4_k_m")
if False: model.push_to_hub_gguf("hf/model", tokenizer, quantization_method="q5_k_m", token="")
```

---
