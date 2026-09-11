# Multi-Agent Email System

## Overview
This intelligent, multi-agent email processing pipeline is built using LangGraph and LangChain. Designed to act as an autonomous executive assistant, it evaluates incoming emails, intercepts spam, and drafts context-aware professional responses for legitimate messages.

Handling high volumes of correspondence and filtering noise is a common challenge in data engineering and machine learning workflows. This project demonstrates stateful LLM orchestration, inter-agent communication, prompt engineering, and deterministic routing using Groq's high-speed inference API.

## Multi-Agent Architecture
The system uses a LangGraph `StateGraph` to pass an `EmailState` dictionary between two specialized AI agents:

1. **Sentinel (Intelligence & Triage Agent):** Analyzes the sender and body to determine if the email is SPAM or HAM. If legitimate, it generates a strategic briefing dossier identifying the sender's intent and priority level.
2. **Scribe (Executive Communications Agent):** Receives the briefing dossier from Sentinel and drafts a tailored, professional response. It then autonomously saves the formatted draft to a local disk directory for auditability.

**Deterministic Routing:** A conditional edge actively reads Sentinel's verdict. Spam is instantly diverted to a quarantine node (halting further execution and saving API tokens), while legitimate mail is passed to Scribe.

## Tech Stack
* **Orchestration Framework:** LangGraph, LangChain
* **Large Language Model:** Groq API (`openai/gpt-oss-20b` for high-throughput inference)
* **Environment Management:** Python 3, `python-dotenv`

## Setup and Installation
1. Clone the repository to your local machine.
2. Install the required dependencies:
   ```bash
   pip install -q langgraph langchain-groq python-dotenv
3. Create a .env file in the root directory and securely add your Groq API key:
   '''bash
   GROQ_API_KEY=your_api_key_here
4. Run the Jupyter Notebook to see the multi-agent team process example emails.

## Example Output
When processing a legitimate recruitment email, Sentinel analyzes the context and hands a briefing over to Scribe to draft the reply:

```text
[Sentinel] Verdict: HAM
[Sentinel] Handing off dossier to Scribe:
-> "The recruiter seeks to engage Waryam for a Machine Learning Engineer position. Prioritize a courteous reply that confirms interest..."
[Scribe] Receiving dossier from Sentinel. Crafting response...
[Scribe] Draft generated and successfully archived to: saved_drafts/draft_Machine_Learning_Engineer_Role_20260911_151416.txt
   
