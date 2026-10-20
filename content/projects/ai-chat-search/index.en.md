---
title: AI search over company chat history
summary: Ask a question in plain language and get an answer from years of team chat.
problem: Decisions and context were buried in the history of the team's Mattermost chat, and finding them by hand took too long.
solution: A system that indexes the full chat history and answers questions right in the chat with a /memory command, for example "what did we decide about deployment last week?". It keeps up with new, edited and deleted messages in real time, works in several languages and shows each person only the channels they belong to. It runs with local models or OpenAI and DeepSeek.
result: In daily use, and now the knowledge source for the company's AI agent.
kind: client
weight: 1
stack:
- Python
- FastAPI
- PostgreSQL
- pgvector
- sentence-transformers
- OpenAI / DeepSeek
- Docker
- nginx
cover: ''
youtube: ''
video: ''
gallery: []
repo: ''
live: ''
credits: ''
---
