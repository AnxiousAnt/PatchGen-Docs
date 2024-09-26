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
- **Git LFS**: Download and install Git Large File Storage (LFS) from [here](https://git-lfs.github.com/).

## 2. Clone the Project Repository
1. Open a terminal and clone the project repository:
    ```bash
    git clone <repository-url>
    cd <repository-name>
    ```

2. Make sure Git LFS is initialized:
    ```bash
    git lfs install
    ```

## 3. Install Ollama
1. Visit [Ollama's website](https://ollama.com/) and follow the instructions to download and install Ollama for your operating system.
   
2. After installation, verify that Ollama is running:
    - Open a browser and navigate to `http://localhost:11434`. You should see a message saying "Ollama is running".

## 4. Download the PatchGen Model
1. **Ensure Git LFS is installed and initialized** (if not already done in step 2).

2. Clone the PatchGen model from Hugging Face:
    ```bash
    git clone https://huggingface.co/ParZiVal04/patch-gen-v1-t
    ```

3. This will download the `gguf` model and a `modelfile` needed for Ollama.

## 5. Create the Ollama Model
1. Use the `ollama` CLI tool to create the model:
    ```bash
    ollama create patch-gen -f path/to/modelfile
    ```

2. To verify that the model has been created successfully, run:
    ```bash
    ollama list
    ```
   You should see `patch-gen` listed among the models.

## 6. Setting Up the Python Environment

1. Navigate to the project directory:
    ```bash
    cd <project-directory>
    ```

2. Create and activate a virtual environment:
    ```bash
    python -m venv env
    source env/bin/activate  # For Windows use `env\Scripts\activate`
    ```

3. Install the required Python packages:
    - Create a `requirements.txt` file with the following contents:
        ```
        pandas
        rich
        ollama
        ```
    - Install the requirements:
        ```bash
        pip install -r requirements.txt
        ```

## 7. Running the Script

1. Place the `patch-gen-dataset-v0.8.7.csv` file in the same directory as the Python script or update the `csv_file_path` variable in the script to point to the correct location of the CSV file.

2. Run the Python script:
    ```bash
    python <script_name>.py
    ```
    You should see a menu interface appear, allowing you to generate patches based on user inputs or random prompts from the dataset.

## 8. Testing and Troubleshooting

- If you encounter any issues with Ollama not recognizing the model, ensure the `modelfile` path is correctly specified when creating the model.
- Make sure that the required Python packages are installed. You can reinstall them using:
    ```bash
    pip install -r requirements.txt
    ```

## 9. Exiting the Program

- To exit the program, choose option `3` in the menu interface or press `Ctrl+C` in the terminal.

