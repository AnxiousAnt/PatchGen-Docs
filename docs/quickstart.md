# Quick start

The easiest way to start using the model is by running the python notebook linked below.

[![Open In Colab](_images/colab.svg)](https://colab.research.google.com/drive/1V6L_Kc7IFd9UTT0TyVOaxZ8rAfF1lAxt?usp=sharing)

## Using the Colab Notebook

The notebook allows users to interact with the model and generate Pd patches. The notebook has a **text-based user interface** where you can either:
1. **Provide a custom prompt**, or
2. **Generate a random patch**

### Custom Prompts
When you enter a custom prompt, the model will attempt to generate a Pd patch based on your input. However, as the model has not been extensively trained on a large variety of annotated examples, the quality of the results may vary, especially for complex patches.

### Random Patch Generation
When selecting the random patch generation option, the model will "prompt itself" using a random example from the training data. Since the model has seen these examples before, the results are generally more accurate and functional compared to custom prompts. However, the generated patch may still have limitations in its functionality due to the model's incomplete understanding of more intricate Pd concepts.

See the [Running PatchGen Locally](running-locally.md) for local inference.
