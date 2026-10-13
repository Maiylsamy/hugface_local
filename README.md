# Hugging Face Local AI Model

## 📌 Project Overview

This project runs a lightweight AI language model locally using Hugging Face Transformers. It uses **SmolLM2-135M-Instruct** to generate responses to user questions.

The project provides two ways to interact with the model:

1. **Command-Line Interface (CLI):** Ask questions directly through the terminal.
2. **REST API:** Send questions through a FastAPI endpoint and receive AI-generated answers.

The model is downloaded once and stored locally, allowing it to be loaded from the local model directory for subsequent runs.

## 🤖 Model Used

- **Model:** `HuggingFaceTB/SmolLM2-135M-Instruct`
- **Purpose:** Generate text responses to user prompts.
- **Execution:** Runs locally on your machine using the Transformers library and PyTorch.

## ✨ Features

- Downloads the pretrained model from Hugging Face Hub.
- Saves the model files in the local `model/` directory.
- Generates responses to user questions through the terminal.
- Exposes an HTTP API to receive questions and return AI-generated answers.
- Loads the locally stored model for inference.

## 🛠️ Technologies and Libraries

| Library | Why we use it |
|---|---|
| `huggingface_hub` | Downloads the pretrained model files from Hugging Face Hub using `snapshot_download()`. |
| `transformers` | Loads the language model and generates text using the `pipeline()` API. |
| `torch` | Provides the deep-learning framework required to run the model. |
| `fastapi` | Creates the REST API endpoint that accepts questions and returns answers. |
| `uvicorn` | Runs the FastAPI application as an HTTP server. |

### Why these libraries?

- **Hugging Face Hub:** Provides access to pretrained models and downloads their files.
- **Transformers:** Simplifies loading the model and generating responses without implementing the inference logic manually.
- **PyTorch:** Performs the underlying tensor computations used during model inference.
- **FastAPI:** Makes the model accessible through an HTTP endpoint.
- **Uvicorn:** Starts the web server that receives API requests.

## 📁 Project Structure

```text
Hugging_Face_Model/
├── model/                  # Downloaded model files (generated locally)
├── venv/                   # Python virtual environment (local only)
├── api.py                  # FastAPI application
├── download_and_run.py     # Downloads the model and runs CLI chat
├── requirements.txt        # Python dependencies
└── .gitignore              # Files excluded from Git
```

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/hugface.git
cd hugface
```

Replace `YOUR_USERNAME` with your GitHub username.

### 2. Create and activate a virtual environment

**Windows:**

```bash
python -m venv venv
venv\Scripts\activate
```

**Linux/macOS:**

```bash
python -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

## 🚀 How to Run

### Option 1: Run the model through the terminal

```bash
python download_and_run.py
```

The script downloads the model if necessary, loads it, and starts an interactive chat session.

Example:

```text
You: What is artificial intelligence?
AI: Artificial intelligence is the ability of machines to perform tasks that typically require human intelligence.
You: exit
```

Type `exit` to stop the chat.

### Option 2: Run the REST API

First, ensure the model has been downloaded by running `download_and_run.py` at least once.

Then start the API:

```bash
python api.py
```

The API runs at:

```text
http://127.0.0.1:8000
```

### API Endpoint

**GET `/ask`**

Pass your question using the `question` query parameter.

Example URL:

```text
http://127.0.0.1:8000/ask?question=What%20is%20AI
```

Example JSON response:

```json
{
  "answer": "Artificial intelligence enables machines to perform tasks that normally require human intelligence."
}
```

You can also explore the interactive API documentation at:

```text
http://127.0.0.1:8000/docs
```

## 🔄 How It Works

1. The model is downloaded from Hugging Face Hub and saved locally.
2. Transformers loads the local model using the text-generation pipeline.
3. A user submits a question through the CLI or REST API.
4. The question is formatted as a user message and passed to the model.
5. The model generates a response, limited to 100 new tokens.
6. The generated answer is displayed in the terminal or returned as JSON by the API.

## 🔒 Notes

- The initial model download requires an internet connection.
- Subsequent inference can run offline if all required model files and dependencies are available locally.
- Response quality and speed depend on the model, hardware, and input.
- The API binds to `127.0.0.1`, so it is accessible only from the local machine by default.
- The model is lightweight, but inference performance still depends on available system resources.

## 📌 Future Improvements

- Add conversation history.
- Add error handling and input validation.
- Support POST requests for question submission.
- Add a web-based chat interface.
- Add authentication and configurable API deployment.

## 📄 License

Check the model's license on Hugging Face before redistributing the model or deploying it commercially.
