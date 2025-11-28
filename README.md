### Tiny Siri: Edge-Optimized Intent Classification

#### A Quantized DistilBERT model for On-Device Voice Assistants (97% Accuracy)

#### The Problem
Modern Voice Assistants (like Siri/Alexa) rely on massive cloud models (BERT/GPT). This causes privacy concerns and high latency. Running these models on-device (Edge AI) is difficult because they consume too much battery and memory.

#### The Solution
I engineered a lightweight intent classification pipeline designed for mobile deployment. By utilizing **Dynamic Quantization**, I compressed a fine-tuned Transformer model by **50%** while retaining **97% accuracy**, making it suitable for real-time, on-device inference.

#### Tech Stack
*   **Model:** DistilBERT (Fine-tuned on synthetic dataset)
*   **Optimization:** PyTorch Dynamic Quantization (INT8)
*   **Training:** Google Colab (NVIDIA T4 GPU)
*   **Deployment:** Streamlit & Hugging Face Spaces

#### Results: Quantization Impact

| Metric | Original Model (FP32) | **Quantized Model (INT8)** | Impact |
| :--- | :--- | :--- | :--- |
| **Model Size** | 255 MB | **132 MB** | 🔻 **48% Smaller** |
| **Accuracy** | 97.4% | **97.1%** | 🤏 Negligible Loss |
| **Inference Speed** | ~45ms | ~**20ms** | ⚡ **2x Faster** |

#### How to Run Locally

1. **Clone the repo**
   ```bash
   git clone https://github.com/YOUR_USERNAME/tiny-siri-edge.git
   cd tiny-siri-edge

2. **Install dependencies
   ```bash
   pip install -r requirements.txt

4. **Run the App
   ```bash
   streamlit run streamlit_app.py

#### Methodology

* Data Augmentation: Solved the "Cold Start" problem by generating 500+ synthetic training examples using LLMs to simulate varied speech patterns.
* Transfer Learning: Fine-tuned distilbert-base-uncased to classify 10 distinct user intents (e.g., Set_Timer, Get_Weather).
* Quantization: Converted model weights from 32-bit floating point to 8-bit integers using torch.quantization.

  
