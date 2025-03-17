# 🖼️ hwkims/AI-Image-Analyzer-with-Text-Extraction-and-Voice

[![Open in Streamlit](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io/hwkims/ai-image-analyzer-with-text-extraction-and-voice/main/app.py)  
**(Replace the above link with your actual Streamlit sharing link)**

## ✨ Introduction

This project is a Streamlit application that leverages AI to analyze images, extract text from them, provide a comprehensive description, summarize the text, and convert the analysis into spoken audio.  It combines the power of a local Large Language Model (LLM) via Ollama with the speed of Edge TTS for a complete image understanding solution.

## 🌟 Features

*   **Image Upload:** Accepts JPG, JPEG, and PNG image formats.
*   **Text Extraction:**  Accurately extracts text embedded within the uploaded image.
*   **Image Description:** Generates a detailed description of the image's content, combining visual elements and extracted text.
*   **Text Summarization:**  Provides a concise summary of the extracted text.
*   **Text-to-Speech (TTS):**  Converts the entire analysis (including description and summary) into natural-sounding speech using Edge TTS.
*   **Interactive Chat Interface:** Displays the conversation history with the AI, including both text and audio responses.
*   **Korean Language Support:**  Specifically tuned for Korean language processing, including the prompt template and the default TTS voice.

## 🚀 Tech Stack

*   **Streamlit:**  For creating the interactive web application.
*   **Ollama:**  For running a local LLM (specifically, the `gemma3:4b` model, but you can change this).  This allows for powerful, local image analysis *without* relying on external APIs like OpenAI's.
*   **Edge TTS:**  For fast, high-quality text-to-speech conversion.  Uses the `ko-KR-HyunsuNeural` voice by default.
*   **Requests:**  For making HTTP requests to the Ollama API.
*   **Pillow (PIL):**  For image processing.
*   **Asyncio:** For asynchronous operations (TTS).
*   **Python 3.7+**

## 🛠️ Setup and Installation

1.  **Install Ollama:**
    *   Download and install Ollama from the official website: [https://ollama.ai/](https://ollama.ai/)
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
    git clone https://github.com/hwkims/AI-Image-Analyzer-with-Text-Extraction-and-Voice.git  # Use your actual repo URL
    cd AI-Image-Analyzer-with-Text-Extraction-and-Voice
    ```

3.  **Install Dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

    **(Create a `requirements.txt` file):**  Make sure you have a `requirements.txt` file in your repository with the following content:

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

    This will open the Streamlit app in your web browser.

## ⚙️ Configuration

*   **`OLLAMA_HOST`:**  The address of your Ollama server.  Defaults to `http://localhost:11434`.  Change this if your Ollama server is running on a different host or port.
*   **`VOICE`:**  The voice used by Edge TTS.  Defaults to `ko-KR-HyunsuNeural`.  You can find a list of available voices by running `edge-tts --list-voices`.
*   **`PROMPT_TEMPLATE`:** The prompt template used for interacting with the LLM. This is specifically crafted for Korean, including instructions for text extraction, description, and summarization.  You can customize this template to fine-tune the AI's behavior.  It's designed for few-shot prompting, guiding the model's response format.
*  **LLM Model:** The code currently uses `gemma3:4b`. You can change this to any other model supported by Ollama by modifying the `"model"` field in the `query_ollama` function. Make sure you have pulled the desired model using `ollama pull <model_name>`.

## 📝 Usage

1.  Upload an image using the "이미지를 업로드하세요" button.
2.  The application will automatically:
    *   Display the uploaded image.
    *   Send the image and a prompt to the Ollama server.
    *   Parse the response to extract:
        *   The text found within the image.
        *   A description of the image.
        *   A summary of the extracted text.
    *   Display these results in the Streamlit interface.
    *   Generate speech from the analysis and play it.
3.  The conversation history is maintained, showing both the AI's text responses and the audio playback.

## 💡 Improvements and Future Work

*   **Error Handling:**  The code includes basic error handling for Ollama API requests and TTS.  More robust error handling and user feedback could be added.
*   **Response Parsing:** The current response parsing uses simple string splitting. A more robust approach (e.g., using regular expressions or a dedicated parsing library) could be implemented to handle variations in the LLM's output format more reliably.
*   **User Input:** While the current version is fully automated after image upload, adding a text input box for follow-up questions or specific instructions could enhance interactivity.
*   **Model Selection:** Allow the user to select different Ollama models from within the Streamlit app.
*   **Temperature/Top-p Control:**  Expose the `temperature` and `top_p` parameters to the user through Streamlit sliders, allowing them to control the randomness and creativity of the LLM's responses.
*   **Streaming Responses:**  Implement streaming of the LLM's response for a more interactive experience, especially with larger images or more complex analyses.
*   **Image Preprocessing:** Consider adding image preprocessing steps (e.g., resizing, noise reduction) to potentially improve text extraction accuracy.
*   **Batch Processing:** Allow users to upload multiple images for batch analysis.

## 🤝 Contributing

Contributions are welcome!  Please feel free to submit issues or pull requests.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.  (You'll need to create a LICENSE file and add the MIT License text to it.)

## 📞 Contact

If you have any questions or suggestions, feel free to reach out to me:

*   GitHub: [hwkims](https://github.com/hwkims)

---

This README provides a comprehensive overview of your project, making it easy for others to understand, use, and contribute.  Remember to replace placeholders (like the Streamlit sharing link and your repository URL) with your actual information.  Good luck!
