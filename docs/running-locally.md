# PatchGen local Setup 

## 1. Prerequisites
Before you begin, make sure you have the following installed on your system:

- **Python 3.8+**: Check your Python version using:
    ```bash
    python --version
    ```
- **pip**: the package installer for Python, check by running:
    ```bash
    pip --version
    ```
- **Git**: Make sure Git is installed on your system. You can check by running:
    ```bash
    git --version
    ```
- **Git LFS** (optional): Download and install Git Large File Storage (LFS) from [here](https://git-lfs.github.com/).

## 2. Clone the Project Repository
1. Open a terminal and clone the project repository:
    ```bash
    git clone https://github.com/AnxiousAnt/PATCH-GEN-LOCAL.git
    cd PATCH-GEN-LOCAL
    ```

## 3. Install Ollama
1. Visit [Ollama's website](https://ollama.com/) and follow the instructions to download and install Ollama for your operating system.
   
2. After installation, verify that Ollama is running:
    - Open a browser and navigate to `http://localhost:11434`. You should see a message saying "Ollama is running".

## 4. Download the PatchGen Model
### Two ways to do this: 
#### 1. Using Git LFS:
1. Make sure Git LFS is initialized:
    ```bash
    git lfs install
    ```

2. Clone the PatchGen model from Hugging Face:
    ```bash
    git clone https://huggingface.co/parzi-parzi/PatchGen-v1-gguf
    ``` 
    This will download the `gguf` model and a `modelfile` needed for Ollama.    
    note: this might take a while depending on your internet speed. 

#### 2. Manually downloading from the Hugging Face repository:
1. navigate to https://huggingface.co/parzi-parzi/PatchGen-v1-gguf/tree/main and
   download the GGUF Model and the Modelfile (using the download button next to the files) and place them in the same directory.

## 5. Create the Ollama Model
1. Once the model is downloaded, use the `ollama` CLI tool to create the model:
    ```bash
    ollama create patch-gen -f path/to/modelfile
    ```

2. To verify that the model has been created successfully, run:
    ```bash
    ollama list
    ```
   You should see `patch-gen` appear in the list of models.

## 6. Install the required Python packages

1. Install the requirements:
        ```bash
        pip install -r requirements.txt
        ```

## 7. Running the Text-UI 

2. Run
    ```bash
    python run.py
    ```
    or
    ```bash
    python3 run.py
    ``` 
    You should see a menu interface appear, allowing you to generate patches based on user inputs or random prompts from the dataset.

## 8. Testing and Troubleshooting

- If you encounter any issues with Ollama not recognizing the model, ensure the `modelfile` path is correctly specified when creating the model.

## 9. Exiting the Program

- To exit the program, choose option `3` in the menu interface or press `Ctrl+C` in the terminal.

