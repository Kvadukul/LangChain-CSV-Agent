# LangChain-CSV-Agent

An autonomous Generative AI data analyst built using LangChain and Google Gemini. This project allows users to input a datasets in plain English, having the AI write, execute, and debug live Python Pandas code behind the scenes to fetch exact numerical answers.

---


| Library | Purpose |
| :--- | :--- |
| **`pandas`** | Loads and structures the transaction dataset into memory as a dataframe for row/column manipulation. |
| **`ChatGoogleGenerativeAI`** | Connects Gemini (gemini-3.8-flash) to the code (temperature=0 to ensure strict logic and prevent made up numbers). |
| **`create_pandas_dataframe_agent`** | Binds the Gemini model to the pandas dataframe, turning it into an interactive input agent. |


---


### 1. Handling Parsing Errors (handle_parsing_errors)
During development,  execution can occasionally output errors when trying to run complex data structures. To solve this, agent_executor_kwargs={"handle_parsing_errors": True} was added to the agent configuration. This acts as a safety net, allowing the agent to catch its own syntax errors, re evaluate its output formatting, and attempt the input again.

### 2.  Dataset Scale (2,500 Rows)
Even when testing against a relatively small financial transaction dataset of roughly 2,500 lines, inputs take a amount of time to process. An LLM agent takes much longer as it must first read the prompt, inspect the dataframe columns, generate a Python prompt, executes it, read the terminal output, and finally translate it back into natural language. While slightly slower, it provides an great search layer for raw spreadsheets.

### 2.  Text File for Results
csv_agent_answers.txt - Automatically appends user questions and AI responses into a local text file for permanent testing and evaluation tracking. 

---
