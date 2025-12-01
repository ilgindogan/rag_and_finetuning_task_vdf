# Advanced RAG Task: Hierarchical Retrieval from Literature on Constrained Resources

## Project overview, chosen book, and objectives

The objective of this task is building a Retrieval-Augmented Generation (RAG) system. This RAG system is evaluated using google/gemma-3-1b-it LLM. The evaluation results are compared with pure model just using google/gemma-3-1b-it LLM. The comparison is reported. The RAG system is based on a book from Project Gutenberg which is the knowledge source. It is indexed using hierarchical chunking into an on-disk database.

For this task, candidate books are identified from the NarrativeQA dataset. *The Tale of Two Bad Mice* is chosen. The story is indexed using character-based hierarchical chunking into Qdrant on-disk vector database. Both the development and the evaluation run on a Google Colab free tier instance with a T4 GPU.

## Setup instructions - Step-by-step guide

Both the fine-tuning and the evaluation run on a Google Colab free tier instance with a T4 GPU.

The Colab Motebook consists of 7 steps.

* Step 0: Prepare environment
* Step 1: Enter your Hugging Face access token to be able to use Gemma
* Step 2: Data selection & preparation
* Step 3: Indexing Strategy: Hierarchical Chunking
* Step 4: Retrieval and Evaluation

Here is the instructions.

* Firstly, run step 0 in order to set environment correctly. 

* Secondly, run step 1 and enter your Hugging Face access token to be able to use Gemma. Be sure that you accepted the terms of Gemma.

* Finally, run step 2, 3, and 4 sequentially.


##  Clear description of the hierarchical chunking strategy, embedding model choice, db, and retrieval logic (k, parent retrieval) and the prompt

For hierarchical chunking different strategies are applied such as character based, word based and token based using an embedding model. The best results are obtained using character-based. The advantages of this method are simple implementation, compatibility with long texts and easy to control exact chunk size. When the same embedding model used in the next steps is used for tokenization, it is impossible to use even mid-size chunks due to its maximum allowed input length which is 256 tokens. The parent size, the child size and overlap are set as 1000, 200 and 20 respectively as the total story length is almost 5k. 5 parents and 28 children are obtained in the end of this process.

The chosen sentence-transformer model is all-MiniLM-L6-v2. The main reason of this selection is its size. It is small and fast. It gives high quality results compared to its size. Therefore, it is appropriate for the Colab free tier.

Qdrant is selected as the vector database for various reasons. It works fully on-disk. It is compatible with Colab. It has simple Python API. It performs well at small-to-medium scale.

Retrieval stretegy is as follows. Since it is a small story, k is set to 3. It gives a balanced selection between precision and noise. All parents are retrieved for all top-k children in order to give broader narrative context which is essential for short story with faster context flow across chunks.

Finally, the prompt is designed to restrict the model to give answers in 1-3 words. Since it is a short children's story, the answers to the questions are really simple. Without giving restriction to the model answers become long sentences and even paragraphs. Similar prompt is given for the baseline and the RAG system. The RAG one obviously includes the retrieved context.

## Summary of the results 

*   For further details, please refer to the report.

    | Approach       | BLEU-4 (vs. Ground Truth) | ROUGE-L (vs. Ground Truth) | Notes / Qualitative Resource Impact                                  |
    | :------------- | :------------------------ | :------------------------- | :------------------------------------------------------------------- |
    | Baseline (No RAG) | 1.4639                  | 0.0407                   | 0.24 seconds per question inference                                   |
    | RAG (Hierarchical) | 14.1561                  | 0.3042                  | 0.35 seconds per question inference, extramemory & time for indexing |

## Final Report

[`RAG-report.pdf`](RAG-report.pdf)

