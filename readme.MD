---
title: AI Professional Persona
emoji: 👩‍💻
colorFrom: indigo
colorTo: purple
sdk: gradio
sdk_version: 5.12.0
app_file: app.py
pinned: false
---

---
title: AI_Professional_Persona
app_file: app.py
sdk: gradio
sdk_version: 5.49.1
---

# AI Career Digital Twin

This is an experimental AI agent designed to represent my professional background. Think of it as a "interactive resume"—instead of hitting Ctrl+F on a static PDF to find my experience with React or API integration, you can just ask the agent directly.

## Why I Built This

I wanted to build a practical application using the **OpenAI Agents SDK** that solved a real problem: keeping my portfolio accessible and queryable 24/7.

I recently pivoted my focus to Agentic AI after 7+ years in full-stack development and system integration. This project was my way of getting hands-on with the new frameworks while building something actually useful for recruiters and hiring managers.

## Engineering Decisions: The Move from DeepSeek to OpenAI

You might notice in the commit history that I started this project using **DeepSeek-V3**. It was a great way to prototype without racking up API costs, but I eventually refactored the entire backend to use **GPT-4o-mini**.

Here is why I made that switch:

1. **Response Quality:** The DeepSeek model was fun to experiment with, but the answers tended to be a bit rambling. For a professional tool representing me, I needed the agent to be concise and precise—just like I am in a real interview.
2. **Latency:** The "time to first token" was inconsistent. A chat interface needs to feel snappy, or users will just close the tab.
3. **Tool Reliability:** I found that GPT-4o-mini was significantly more reliable at understanding when to trigger the `record_user_details` function versus when to just answer a question.

## How It Works (The "Under the Hood")

The architecture is a straightforward **RAG (Retrieval-Augmented Generation)** pipeline with function calling capabilities.

1. **Ingestion:** The app reads my `linkedin.pdf` and `summary.txt` using `pypdf`.
2. **Context Injection:** It injects that text directly into the system prompt. I chose this over a vector database for now because the dataset (my resume) is small enough to fit in the context window, which keeps the architecture simple and the retrieval 100% accurate.
3. **Tool Execution:** I gave the agent two specific tools:
* `record_unknown_question`: If the agent doesn't know the answer, it logs the question so I can update the context later.
* `record_user_details`: If someone wants to get in touch, the agent captures their info.



## Roadmap (Work in Progress)

This is currently a functional prototype, but the RAG implementation is solid. There are a few things I plan to tackle next:

* **Error Handling:** Right now, if the API times out, the UI just hangs. I need to add graceful error messages.
* **Memory:** I want to implement persistent memory so the agent remembers context across different sessions.
* **Frontend:** The current UI is a basic Gradio interface. I’d like to build a custom React frontend to match my full-stack background.

## Setup & Installation

If you want to poke around the code:

1. **Clone the repo:**
```bash
git clone https://github.com/bmt3755/AI-Interactive-Resume.git

```


2. **Install dependencies:**
```bash
pip install -r requirements.txt

```


3. **Add your keys:**
Create a `.env` file and add your `OPENAI_API_KEY`.
4. **Run it:**
```bash
python app.py

```

