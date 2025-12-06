# Part B Report — Neural Machine Translation

This report compares the BLEU scores of the global attention model **with and without input feeding**, as well as the performance of the local attention model.

## Model Comparison

| Model Configuration | Input Feeding | BLEU Score | Validation Loss |
|---------------------|--------------|------------|------------------|
| Global Attention    | No           | 0.2263     | 2.0757           |
| Global Attention    | Yes          | 0.2158     | 2.1308           |
| Local Attention     | Yes          | 0.1477     | 2.5320           |

## Analysis

It is somewhat surprising that input feeding does not improve results, as it is generally expected to do so by increasing the model's effective capacity. By concatenating the previous time step’s context vector with the current token embedding, the decoder receives explicit information about where it attended previously. This additional “memory” should help the model make more informed predictions, reduce redundant repetitions, and provide more context when generating each new token.

However, in this experiment, the dataset is relatively small (around 30,000 examples). In contrast, the original input feeding work was trained on approximately 1 million sentences. With such a limited dataset, the model likely does not have enough training signal or time to fully optimize all parameters associated with input feeding.

Additionally, our dataset contains fairly short sequences (maximum length around 205 symbols). Input feeding provides the greatest benefit for long sequences by improving coverage tracking—helping the decoder avoid repeating translations of the same source words or skipping parts of the sentence. With short sequences, this issue is less pronounced, so the benefit of input feeding diminishes.

Increasing the number of epochs or tuning other hyperparameters may allow the model to converge more effectively and yield better performance with input feeding.
