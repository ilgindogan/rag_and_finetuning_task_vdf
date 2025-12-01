# LLM Finetuning Task: Comparing PEFT Techniques on Gemma-3-1b-it

## Project overview and objectives

The aim of this task is finetuning the google/gemma-3-1b-it large language model (LLM) using two different Parameter-Efficient Fine-Runing (PEFT) techniques. The pure LLM model and two distinct LLM modes with different PEFT techniques are compared in the end in terms of BLEU-4 and ROUGE-L performances together with memory and time consumptions.

For this task, the base LLM is google/gemma-3-1b-it. On top of that two different PEFT techniques are applied. The first technique is Quantized Low-Rank Adaptation (QLoRA). The second one is Low-Rank Adaptation (LoRA). Both methods are fine-tuned for two epochs. For training and test set, 5k and 2k test samples are collected from tatsu-lab/alpaca, allenai/tulu-v2-sft-mixture, and HuggingFaceH4/ultrachat\_200k separetely. Final training and test sizes are 15k and 6k.

## Setup instructions - Step-by-step guide

Both the fine-tuning and the evaluation run on a Google Colab instance with a A100 GPU. Inference is slower with T4 GPU. 

The Colab Motebook consists of 7 steps.

* Step 0: Prepare environment
* Step 1: Enter your Hugging Face access token to be able to use Gemma
* Step 2: Create a combined dataset
* Step 3: Evaluate base model: google/gemma-3-1b-it
* Step 4: Finetune - QLoRA
* Step 5: Evaluate QLoRA
* Step 6: Finetune - LoRA
* Step 7: Evaluate LoRA

Here is the instructions.

* Firstly, run step 0 and restart the notebook in order to set environment correctly. Restart button appears after you run the cell.

* Secondly, run step 1 and enter your Hugging Face access token to be able to use Gemma. Be sure that you accepted the terms of Gemma.

* Thirdly, run step 2 in order to create a combined dataset.

* Now you have 3 options:

*  * To evaluate base model, run step 3.

* * To fine-tune with QLoRA and evaluate, run step 4 and step 5.

* * To fine-tune with LoRA and evaluate, run step 6 and step 7.

## Summary of the results

*   For further details, please refer to the report.

    | Technique | BLEU-4 (Before) | BLEU-4 (After) | ROUGE-L (Before) | ROUGE-L (After) | Peak Memory (GB) | Training Time (Hrs) |
    | :-------- | :-------------- | :------------- | :--------------- | :-------------- | :--------------- | :------------------ |
    | QLoRA     | 0.2625      | 0.5421       | 0.1137       | 0.1384       | 11.76 GB         | 2040.94 seconds            |
    | LoRA    | 0.2625      | 0.4482       | 0.1137       | 0.1296        | 11.58 GB         | 1559.89 seconds            |
    


## Final Report

[`finetuning/Finetuning-report.pdf`](./finetuning/Finetuning-report.pdf)


