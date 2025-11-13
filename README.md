# Project Siri: On-Device Intent Classification

### An End-to-End Analysis of Model Complexity vs. Data Availability

## Project Overview

This project simulates a core component of a voice assistant like Apple's Siri: the intent classification module. The goal is to take a user's voice command and accurately classify their intent (e.g., `get_weather`, `set_timer`).

The motivation stems from the challenges of building efficient on-device AI. This project provides a comprehensive, multi-stage investigation into the critical trade-off between model complexity and data availability. Three models of increasing complexity were built and evaluated across datasets of varying sizes:

1.  **A Simple Baseline:** TF-IDF with Logistic Regression.
2.  **A Sequential Deep Learning Model:** An LSTM network.
3.  **A State-of-the-Art Transformer:** A fine-tuned DistilBERT model.

## Methodology

The project was conducted in Google Colab and structured as a three-stage experiment to find the optimal model.

1.  **Experiment 1 (Small Dataset - 60 Examples):**
    *   A baseline and an LSTM model were trained on a small, 5-intent dataset.
    *   **Result:** The baseline was superior (67% accuracy). The LSTM severely **overfit**, proving that complex models fail in low-data environments.

2.  **Experiment 2 (Medium Dataset - 120 Examples):**
    *   The dataset was expanded to 120 utterances across 10 intents.
    *   All three models (Baseline, LSTM, Transformer) were trained.
    *   **Result:** The baseline remained the champion (67% accuracy). The LSTM's performance improved but still overfit. The powerful Transformer **failed completely (12.5% accuracy)**, confirming it was too complex for the limited data.

3.  **Experiment 3 (Large Dataset - 400 Examples):**
    *   **Hypothesis:** A significantly larger dataset would provide enough data for the Transformer to learn effectively and overcome overfitting.
    *   The dataset was expanded to 400 utterances (40 per intent).
    *   The Transformer model was re-trained and re-evaluated.
    *   **Result:** The hypothesis was proven correct. The Transformer's performance skyrocketed, achieving state-of-the-art results.

## Final Results & Analysis

The final comparison across all models and datasets demonstrates a clear narrative. The Transformer, once supplied with sufficient data, emerged as the definitive winner.

| Model | Description | Dataset Size | Final Test Accuracy |
| :--- | :--- | :--- | :--- |
| **Transformer**| "Formula 1 Car" | 400 Examples | 🏆 **87.34%** |
| **Baseline** | Simple "Go-Kart" | 120 Examples | 66.67% |
| **LSTM** | "Family Sedan" | 120 Examples | 54.17% |

#### Key Observations:

*   **Data is the Deciding Factor:** This project empirically proves that the success of a complex model is critically dependent on the volume of training data. The Transformer went from being the worst-performing model to the best-performing model solely by increasing the dataset size.

*   **Overcoming Overfitting:** With only 120 examples, the LSTM and Transformer models failed by memorizing the training data (overfitting). With 400 examples, the Transformer was able to generalize and learn the true underlying patterns in the language, leading to its high accuracy.

*   **The Power of Transfer Learning:** The final success of the DistilBERT model showcases the power of transfer learning. Once given enough data, its vast pre-trained knowledge of the English language was successfully "fine-tuned" to excel at our specific classification task.

## Project Conclusion

The primary conclusion of this comprehensive experiment is that **while simple baselines are optimal in low-data environments, state-of-the-art models like Transformers unlock superior performance once a sufficient data threshold is met.**

This project successfully navigated a realistic, end-to-end machine learning workflow. It began with an analysis that correctly identified a simple baseline as the best initial solution. It then diagnosed the failure of more complex models, formed a data-centric hypothesis, and executed a plan that validated this hypothesis, ultimately achieving an **87.34% accurate** intent classification model. This journey highlights the importance of a methodical, iterative approach to model selection and the foundational principle that data is the key to unlocking the potential of advanced AI.

## Future Work

With a high-performing intent classifier now successfully trained, future work could focus on deployment and optimization:

1.  **Model Quantization:** Convert the fine-tuned Transformer to a smaller, faster format (like TensorFlow Lite or ONNX) to analyze its performance and size for a true on-device deployment.
2.  **Full Pipeline Integration:** Integrate this intent classification model into a full voice assistant pipeline, including speech-to-text input and action-mapping output.
3.  **Explore More Efficient Transformers:** Benchmark other lightweight, on-device-focused Transformers (like MobileBERT) to see if similar accuracy can be achieved with an even smaller footprint.
