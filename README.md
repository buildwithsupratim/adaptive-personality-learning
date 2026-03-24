# adaptive-personality-learning
An AI-powered teaching engine that combines personality, curriculum graphs, and books to deliver adaptive, personalized learning experiences.

# LoRA Personality & Curriculum Teaching System

This repository contains a framework for training AI personalities using **LoRA (Low-Rank Adaptation)** and implementing a structured, curriculum-based teaching system. Designed for **Google Colab (T4 GPU)**, the system allows you to fine-tune a model to adopt a specific "persona" (like a supportive tutor) and then use that persona to teach subjects based on uploaded textbooks and curriculum maps.

## 📂 Repository Contents

* **`LoRA_personality_script.txt`**: The core Python script (Gradio UI + Training Logic).
* **`Training Data_Sensitivechat.txt`**: Conversational pairs used to train the model's supportive and empathetic personality.
* **`cirriculum.json`**: The structured learning path (nodes and edges) for the subject (e.g., French Revolution).
* **`TextBook.txt`**: The source material the AI references to ensure factual teaching.

---

## 🛠️ Requirements & Setup

### Hardware
* **Google Colab T4 GPU**: This script is optimized for ~12GB of VRAM. Ensure your Colab runtime is set to **T4 GPU**.

### Libraries
The script handles installations automatically, but relies on:
* `transformers` & `peft` (Fine-tuning)
* `bitsandbytes` (4-bit quantization)
* `gradio` (Interface)

---

## 📖 Step-by-Step Instructions

### 1. Launch the Environment
1.  Open **Google Colab**.
2.  Upload `LoRA_personality_script.txt` to a cell or copy/paste the code.
3.  Go to **Runtime > Change runtime type** and select **T4 GPU**.
4.  Run the cell. It will install dependencies and provide a `gradio.live` URL. Click that link.

### 2. Fine-Tune the Personality
1.  In the Gradio web UI, go to the **Personality Management** tab.
2.  Upload **`Training Data_Sensitivechat.txt`**.
3.  Give your personality a name (e.g., *SupportiveTutor*).
4.  Click **Train Personality**. The model (TinyLlama-1.1B) will learn the conversational style from your text file.

### 3. Load the Curriculum and Textbook
1.  Switch to the **Curriculum & Books** tab.
2.  **Upload Curriculum**: Select your **`cirriculum.json`**. This defines the order of topics.
3.  **Upload Book**: Select **`TextBook.txt`**.
    * *Note:* Ensure the "Book Title" you enter in the UI matches the `book` field inside your JSON file (e.g., "French Revolution Basics").

### 4. Start the Teaching Session
1.  Go to the **Chat** tab.
2.  Select your trained personality from the dropdown menu.
3.  Send a message like "Hello" to begin.
4.  **The Teaching Loop**:
    * **Negotiate**: The AI asks what you already know about the first topic.
    * **Teach**: Once you are ready, it explains the topic using excerpts from `TextBook.txt`.
    * **Advance**: After confirming your understanding, the AI automatically moves to the next node in the `cirriculum.json`.

---

## ⚙️ Curriculum Structure Reference
Your `cirriculum.json` uses a graph-based structure. Here is how it should look:

```json
{
  "title": "French Revolution",
  "start": "france_before_revolution",
  "nodes": [
    {
      "id": "france_before_revolution",
      "title": "France Before the Revolution",
      "description": "Understanding the social structure.",
      "book": "French Revolution Basics"
    }
  ],
  "edges": [
    { "from": "france_before_revolution", "to": "three_estates" }
  ]
}


## ⚖️ License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---
*Disclaimer: This tool is for educational purposes. Ensure your training data and textbooks comply with local copyright and data privacy regulations.*
