# Chatbot Project with LangChain, OpenRouter, and Gradio

This project demonstrates a simple conversational AI chatbot built using LangChain, integrated with OpenRouter for model access, and exposed via a Gradio interface.

## Features

- **LangChain Integration**: Utilizes LangChain's `ConversationChain` and `ConversationBufferMemory` for managing conversation history.
- **OpenRouter API**: Connects to the OpenRouter API to leverage various language models (specifically `openai/gpt-oss-120b:free` in this example).
- **Gradio Interface**: Provides a user-friendly web interface for interacting with the chatbot.

## Setup and Installation

Follow these steps to get the project up and running locally.

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd <your-repository-name>
```

### 2. Create a Virtual Environment (Recommended)

```bash
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

Make sure your `requirements.txt` contains the following:

```
gradio
langchain==0.1.0
langchain-openai==0.0.5
langchain-community==0.0.12
openai
tiktoken==0.5.2 # Pinning version due to potential build issues on some platforms
```

### 4. Set Up API Key

You will need an OpenRouter API key. Replace `"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"` in the code or set it as an environment variable.

It is highly recommended to use environment variables for API keys for security.

**Option A: Environment Variable (Recommended)**

Set the `OPENAI_API_KEY` environment variable:

```bash
export OPENAI_API_KEY="your_openrouter_api_key_here"
```

**Option B: Directly in Code (Less Secure for Production)**

Locate the line `os.environ["OPENAI_API_KEY"]="your_api_key_here"` in your `app.py` (or main Python script) and replace `your_api_key_here` with your actual OpenRouter API key.

## Running the Application Locally

After completing the setup:

1.  **Ensure your virtual environment is active.**
2.  **Run the Python script containing your Gradio app:**

    If your Gradio interface code is in a file named `app.py`, you would run:

    ```bash
    python app.py
    ```

    This will typically output a local URL (e.g., `http://127.0.0.1:7860`) and potentially a public Gradio share link.

## Deployment on Hugging Face Spaces

To deploy this project to Hugging Face Spaces, follow these steps:

### 1. Create a New Space

- Go to [Hugging Face Spaces](https://huggingface.co/spaces).
- Click on 'Create new Space'.
- Choose a Space name, select 'Gradio' as the Space SDK, and choose a hardware option (e.g., 'CPU basic').

### 2. Upload Files

- **Option A: Web Interface:** Upload your `app.py` (or the Python script containing your Gradio code) and `requirements.txt` directly through the Space's 'Files' tab.
- **Option B: Git:** Clone the Space's Git repository to your local machine, add your files, and push them back.

### 3. Ensure `requirements.txt` is Correct

Your `requirements.txt` should contain all necessary dependencies with their versions, as shown in the "Install Dependencies" section above.

### 4. Set Environment Variables for API Key

- In your Hugging Face Space, go to the 'Settings' tab.
- Under 'Repository secrets', add a new secret named `OPENAI_API_KEY` and paste your OpenRouter API key as its value.

   *Note: Ensure your Python code reads the API key from `os.environ["OPENAI_API_KEY"]`.*

### 5. Configure Python Version (Crucial for `tiktoken`)

Hugging Face Spaces often use a recent Python version by default (e.g., 3.13). The `tiktoken` library, a dependency for `langchain-openai`, can have build issues on very new Python versions if pre-built wheels are not available. To avoid this, explicitly set a stable Python version:

- Create a file named `.python-version` in the root of your Hugging Face Space.
- Inside `.python-version`, add the desired Python version, for example:

  ```
  3.10.13
  ```
  Or if 3.11 is preferred:
  ```
  3.11.9
  ```
  *(Choose a stable Python 3.10 or 3.11 version that has good package support.)*

### 6. Restart the Space

After making these changes (especially to `requirements.txt` or `.python-version`), restart your Hugging Face Space to trigger a new build. The Space should then successfully install all dependencies and launch your Gradio application.
