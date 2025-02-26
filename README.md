# Multilingual Question Answering System (XQuAD) 

This project implements a multilingual question answering system using transformer models, specifically focusing on the XQuAD dataset. The system evaluates various pre-trained models on their zero-shot and fine-tuned performance across multiple languages.

## Overview

This notebook (`Multilingual_Question_Answering_System_XQUAD.ipynb`) performs the following tasks:

1.  **Dataset Loading and Preparation:**
    * Loads the XQuAD dataset for multiple languages (Arabic, German, Chinese, Vietnamese, English, Spanish, Hindi, Greek, Thai, Turkish, Russian, Romanian).
    * Loads the SQuAD dataset for training.
    * Prepares the datasets for training and evaluation by tokenizing the questions and contexts, handling long contexts, and mapping answers to token positions.
2.  **Model Training and Evaluation:**
    * Fine-tunes various pre-trained transformer models (mBERT, XLM-RoBERTa, etc.) on the SQuAD dataset or a translated version of the XQUAD dataset.
    * Evaluates the models' performance on the XQuAD test set in a zero-shot setting and fine-tuned settings.
    * Evaluates the models on the translated test set in the XQUAD dataset.
3.  **Performance Analysis:**
    * Calculates and reports the F1 score and exact match (EM) score for each model and language.
    * Saves the results to CSV files for further analysis.
4.  **Hugging Face Integration:**
    * Logs into Hugging Face and pushes the trained models to the Hugging Face Model Hub.
    * Logs into Hugging Face and pushes the processed dataset to the Hugging Face Dataset Hub.

## Dependencies

* `transformers`
* `datasets`
* `torch` (implicitly required by transformers)
* `huggingface_hub`
* `google-colab` (for Google Colab environment)
* `tqdm`
* `collections`
* `numpy`
* `pandas`
* `git-lfs`

## Setup

1.  **Install Dependencies:**
    ```bash
    pip install accelerate -U
    pip install transformers[torch]
    pip install huggingface-hub
    pip install datasets
    git lfs install
    ```
2.  **Login to Hugging Face:**
    * Run the `notebook_login()` and `huggingface-cli login` commands in the notebook and provide your Hugging Face API token.
3.  **Clone the Dataset Repository:**
    ```bash
    git clone [https://huggingface.co/datasets/juletxara/xquad_xtreme](https://huggingface.co/datasets/juletxara/xquad_xtreme)
    ```
4.  **Mount Google Drive (If using Google Colab):**
    * Run the `drive.mount('/content/drive')` command in the notebook and authorize Google Colab to access your Google Drive.
5.  **Create the Dataset Repository (If needed):**
    ```bash
    huggingface-cli repo create xquad_xtreme --type dataset
    ```

## Usage

1.  **Open the Notebook:**
    * Open `Multilingual_Question_Answering_System_XQUAD.ipynb` in Google Colab or your preferred Jupyter environment.
2.  **Run the Notebook:**
    * Execute the cells in the notebook sequentially.
3.  **Analyze Results:**
    * The results (F1 and EM scores) will be printed in the notebook and saved to CSV files in the `results/xquad/` directory.

## Key Components

* **Dataset Loading:**
    * `load_dataset()`: Loads the XQuAD and SQuAD datasets from Hugging Face Datasets.
* **Tokenization:**
    * `AutoTokenizer.from_pretrained()`: Loads the tokenizer for the pre-trained model.
    * Tokenization with truncation, padding, and stride to handle long contexts.
* **Data Preparation:**
    * `prepare_train_features()`: Prepares the training data by mapping answers to token positions.
    * `prepare_validation_features()`: Prepares the validation data by handling long contexts and mapping token positions to character positions.
* **Model Training:**
    * `AutoModelForQuestionAnswering.from_pretrained()`: Loads the pre-trained model.
    * `TrainingArguments()`: Configures the training parameters.
    * `Trainer()`: Trains and evaluates the model.
* **Post-processing:**
    * `postprocess_qa_predictions()`: Post-processes the model predictions to extract the best answer.
* **Evaluation:**
    * `load_metric("squad")`: Loads the SQuAD evaluation metric.
    * Calculates F1 and EM scores.
* **Result Handling:**
    * `results_df()`: Creates a pandas DataFrame from the evaluation results.

## Model Details

This project evaluates the following models:

* `bert-base-multilingual-cased` (mBERT)
* `xlm-roberta-base`
* `xlm-roberta-large`
* `bert-large-cased-whole-word-masking-finetuned-squad`
* `roberta-base-squad`
* `roberta-large-squad-v1`
* `bertserini-bert-base-squad`
* `saattrupdan/xlmr-base-texas-squad-es`
* `salti/bert-base-multilingual-cased-finetuned-squad`
* `vanichandna/xlm-roberta-finetuned-squad`
* `Palak/xlm-roberta-large_squad`
* `thatdramebaazguy/roberta-base-squad`
* `csarron/roberta-large-squad-v1`

## Results

The evaluation results are saved in the `results/xquad/` directory as CSV files, including:

* Zero-shot performance of mBERT, XLM-RoBERTa, and XLM-RoBERTa-large.
* Performance of fine-tuned models on the translated test sets.
* Performance of mBERT and XLM-RoBERTa trained on the spanish translated training set.

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues to improve this project.
