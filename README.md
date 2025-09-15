# Conversation Management & Classification using Groq API

This project demonstrates how to perform two core conversational AI tasks using the Groq API, which is compatible with the OpenAI SDK. The implementation is done purely in Python within a Google Colab notebook, without relying on external frameworks like LangChain.

The two main tasks are:
1.  **Conversation History Management**: A system to maintain, truncate, and periodically summarize conversation histories to keep them concise and manage context length.
2.  **JSON Schema Classification**: A method to extract structured information (like user details) from natural language chats using Groq's tool-calling (function-calling) feature.

---

## ✨ Features

### Task 1: Conversation Management
- **Running History**: Maintains a list of user and assistant messages.
- **Periodic Summarization**: Automatically summarizes the conversation history after a configurable number of turns (`k`) and replaces the old history with the summary. This is crucial for managing long conversations without losing context.
- **Custom Truncation**: Provides methods to truncate the conversation history based on:
    - The number of recent turns (e.g., last 5 turns).
    - A maximum character length.

### Task 2: Structured Information Extraction
- **JSON Schema Definition**: A strict JSON schema is defined to extract five key details: `name`, `email`, `phone`, `location`, and `age`.
- **Tool Calling with Groq**: Leverages Groq API's tool-calling feature (compatible with OpenAI's function calling) to force the model's output into a structured JSON format.
- **Validation**: The output is validated against the defined schema, ensuring reliable and predictable data extraction from unstructured text.

---

## 🚀 Getting Started

This project is designed to be run in Google Colab.

### Prerequisites
- A Google Account to use Google Colab.
- A GroqCloud account and API Key. You can get one for free at [groq.com](https://groq.com/).

### Installation & Setup

1.  **Clone the Repository (Optional)**
    You can either clone this repository and upload the `.ipynb` file to Google Colab or simply copy the code from the notebook directly.
    ```bash
    git clone [https://https://github.com/Onkar-Ai.git](https://github.com/Onkar-Ai/Conversation-Management-Classification-using-Groq-API.git)
    ```

2.  **Open in Google Colab**
    - Go to [colab.research.google.com](https://colab.research.google.com/drive/1R4IFzf6tOcrgDu6moxd9HhLIW3U7CmZr?usp=sharing).
    - Click on `File` -> `Upload notebook` and select the `.ipynb` file from this repository.

3.  **Set Up Groq API Key**
    - In your Colab notebook, click the **key icon** (🔑) in the left sidebar to open the "Secrets" manager.
    - Create a new secret with the name `GROQ_API_KEY`.
    - Paste your Groq API key into the "Value" field.
    - Ensure the "Notebook access" toggle is enabled.

    

4.  **Run the Notebook**
    - Execute the single code cell in the notebook.
    - The script will first install the necessary `groq` library and then run the demonstrations for both Task 1 and Task 2.

---

## 🛠️ Usage

The notebook is divided into two main sections, each with a demonstration.

### Task 1 Demonstration
The script initializes a `ConversationManager` class. It then simulates a conversation by feeding it a series of user and assistant messages. You can observe how the conversation history grows and how it is automatically summarized and replaced after every 3rd assistant response. Finally, it demonstrates the truncation methods.

**Example Output:**
```
--- Triggering summarization after 3 runs. ---
--- Conversation summarized and history replaced. ---

>>> Current History (Run 3):
[
  {
    "role": "system",
    "content": "Summary of previous conversation: The user wants to book a flight from SFO to Tokyo for early October and has also inquired about hotels near Shinjuku station for the same dates. The assistant is currently searching for options."
  }
]
```

### Task 2 Demonstration
The script defines a JSON schema and a "tool" for user detail extraction. It then processes three sample chat messages:
1.  A message containing all required details.
2.  A message with partial information.
3.  A message with no personal details.

For each message, it calls the Groq API and forces it to use the `extract_user_details` tool, printing the structured JSON output.

**Example Output:**
```
--- Parsing Chat 1 ---
Parsing chat: 'Hi, my name is Jane Doe and I'm 29. My email is jane.d@example.com and I live in New York, USA. My number is 1-800-555-1234.'

>>> Extracted Information:
{
    "name": "Jane Doe",
    "email": "jane.d@example.com",
    "phone": "1-800-555-1234",
    "location": "New York, USA",
    "age": 29
}

   Validation: SUCCESS - Output matches the required schema keys.
```

---

## 📦 Dependencies

- `groq`: The official Python library for the Groq API.

The dependency is installed automatically by the first line in the notebook:
```python
!pip install groq -q
```
