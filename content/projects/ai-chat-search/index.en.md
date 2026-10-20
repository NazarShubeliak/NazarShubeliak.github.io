---
title: AI assistant for team chat
summary: Ask a question in plain language and get an answer from years of team chat.
kind: client
weight: 1
cover: ai-chat-cover.png
youtube: ""
video: ""
problem: The team needed an AI assistant that answers questions right in the
  chat, based on the message history.
solution: A system that indexes the full chat history and answers questions
  right in the chat with a /memory command, for example "what did we decide
  about deployment last week?". It keeps up with new, edited and deleted
  messages in real time, works in several languages and shows each person only
  the channels they belong to. It runs with local models or OpenAI.
result: The team now has its own AI assistant right in the work chat.
stack:
  - Python
  - FastAPI
  - PostgreSQL
  - pgvector
  - sentence-transformers
  - OpenAI
  - Docker
  - nginx
gallery: []
repo: ""
live: ""
credits: ""
---
