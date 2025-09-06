# Linkdin-Post-Generator
+-----------------+         HTTP POST         +-----------------+       LLM Call       +-----------------------------+
|                 |  -------------------->   |                 |  ----------------->  |                             |
|  Streamlit UI   |  User inputs: topic,     |  FastAPI Backend |  generate_post()     |  LangChain Agent Function   |
|                 |  language, length, tone  |                 |                      |                             |
+-----------------+                           +-----------------+                      +-----------------------------+
        ^                                             |                                             |
        |                                             |                                             |
        |                                             | Prompt with example + user inputs           |
        |                                             v                                             |
        |                                 +----------------------------+                           |
        |                                 |    GroqLLM class wraps     |                           |
        |                                 |   API call to Groq LLM    |                           |
        |                                 +----------------------------+                           |
        |                                             |                                             |
        |                                             | payload:                                   |
        |                                             | model="openai/gpt-oss-120b"               |
        |                                             | prompt=prompt                               |
        |                                             v                                             |
        |                                 +----------------------------+                           |
        |                                 |  Groq API Endpoint         |                           |
        |                                 | https://api.groq.com/v1/   |                           |
        |                                 | generate                   |                           |
        |                                 +----------------------------+                           |
        |                                             |                                             |
        |                                             | Returns generated text (LinkedIn post)     |
        |                                             v                                             |
        |                                 +----------------------------+                           |
        |                                 |  LangChain Agent returns   |                           |
        |                                 |     post_text to FastAPI   |                           |
        |                                             |                                             |
        |                                             v                                             |
        |                                 +----------------------------+                           |
        |                                 |  FastAPI returns JSON:     |                           |
        |                                 |  {"post": post_text}       |                           |
        |                                             |                                             |
        +---------------------------------------------v---------------------------------------------+
                                                      |
                                                      v
                                           +-----------------+
                                           | Streamlit UI    |
                                           | Displays LinkedIn|
                                           | Post to user     |
                                           +-----------------+
