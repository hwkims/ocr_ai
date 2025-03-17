# 🖼️ hwkims/ocr_ai

[![Open in Streamlit](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io/hwkims/ocr_ai/main/app.py)  
![image](https://github.com/user-attachments/assets/ac2b44b1-43cb-42ca-9c84-a101d965edc4)


## ✨ Introduction

This project is a Streamlit application that leverages AI to perform Optical Character Recognition (OCR) on images, extract text, provide descriptions, summarize the extracted text, and convert the analysis into spoken audio. It combines a local Large Language Model (LLM) via Ollama with Edge TTS for a complete image understanding solution.  The focus is on accurate OCR, followed by intelligent processing of the extracted text.

## 🌟 Features

*   **Image Upload:** Accepts JPG, JPEG, and PNG image formats.
*   **OCR and Text Extraction:**  Accurately extracts text embedded within the uploaded image.
*   **Image Description:** Generates a detailed description of the image's content, incorporating the extracted text.
*   **Text Summarization:** Provides a concise summary of the extracted text.
*   **Text-to-Speech (TTS):** Converts the entire analysis (description and summary) into natural-sounding speech using Edge TTS.
*   **Interactive Chat Interface:** Displays the conversation history with the AI, including text and audio.
*   **Korean Language Support:** Tuned for Korean language processing (prompt template and default TTS voice).

## 🚀 Tech Stack

*   **Streamlit:** For creating the interactive web application.
*   **Ollama:** For running a local LLM (specifically, the `gemma3:4b` model, but you can change this).  This allows for powerful, local image analysis *without* relying on external APIs.
*   **Edge TTS:** For fast, high-quality text-to-speech conversion.  Uses the `ko-KR-HyunsuNeural` voice by default.
*   **Requests:** For making HTTP requests to the Ollama API.
*   **Pillow (PIL):** For image processing.
*   **Asyncio:** For asynchronous operations (TTS).
*   **Python 3.7+**

## 🛠️ Setup and Installation

1.  **Install Ollama:**
    *   Download and install Ollama: [https://ollama.ai/](https://ollama.ai/)
    *   Pull the `gemma3:4b` model (or choose a different one):

        ```bash
        ollama pull gemma3:4b
        ```

    *   Start the Ollama server:

        ```bash
        ollama serve
        ```

2.  **Clone the Repository:**

    ```bash
    git clone https://github.com/hwkims/ocr_ai.git  # Use your actual repo URL
    cd ocr_ai
    ```

3.  **Install Dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

    **(Create a `requirements.txt` file):**  Make sure you have a `requirements.txt` file with:

    ```
    streamlit
    requests
    edge-tts
    Pillow
    ```

4.  **Run the Application:**

    ```bash
    streamlit run app.py  # Or whatever your main Python file is named
    ```

## ⚙️ Configuration

*   **`OLLAMA_HOST`:** Ollama server address. Defaults to `http://localhost:11434`.
*   **`VOICE`:** Edge TTS voice. Defaults to `ko-KR-HyunsuNeural`.  Use `edge-tts --list-voices` to see available voices.
*   **`PROMPT_TEMPLATE`:** The prompt template for the LLM.  Crafted for Korean, including instructions for OCR, description, and summarization. Customize to fine-tune the AI's behavior.  It's designed for few-shot prompting.
*   **LLM Model:** The code uses `gemma3:4b`. Change this in the `"model"` field of the `query_ollama` function.  Pull the model with `ollama pull <model_name>`.

## 📝 Usage

1.  Upload an image ("이미지를 업로드하세요" button).
2.  The app will automatically:
    *   Display the image.
    *   Send the image and prompt to Ollama.
    *   Parse the response to extract:
        *   Text from the image.
        *   Image description.
        *   Summary of the text.
    *   Display the results.
    *   Generate and play speech from the analysis.
3.  Conversation history is maintained (text and audio).

## 💡 Improvements and Future Work

*   **Error Handling:** Includes basic error handling.  More robust handling and user feedback could be added.
*   **Response Parsing:** Uses simple string splitting. A more robust approach (regex, dedicated parsing library) could handle variations in the LLM's output.
*   **User Input:** Adding a text input for follow-up questions could enhance interactivity.
*   **Model Selection:** Allow users to select different Ollama models.
*   **Temperature/Top-p Control:** Expose `temperature` and `top_p` parameters via sliders to control the LLM's randomness.
*   **Streaming Responses:** Implement streaming for a more interactive experience.
*   **Image Preprocessing:** Add preprocessing (resizing, noise reduction) to improve OCR accuracy.
*   **Batch Processing:** Allow uploading multiple images.

## 🤝 Contributing

Contributions are welcome! Submit issues or pull requests.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details. (Create a LICENSE file with the MIT License text.)

## 📞 Contact

Questions or suggestions?

*   GitHub: [hwkims](https://github.com/hwkims)

---
