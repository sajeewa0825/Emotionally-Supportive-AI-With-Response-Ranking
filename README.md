# Emotion-Aware Response Ranking System

## 🧠 Overview

This project introduces an advanced response ranking mechanism for emotionally sensitive conversational AI systems. The architecture integrates **emotion intensity scoring** and **contextual relevance** via a weighted formula to generate **empathetic and context-aware responses**.

The system aims to:
- **Enhance empathetic dialogue** using emotional intensity and classification.
- **Optimize response selection** by balancing factual relevance and emotional alignment.
- **Track emotional change** in users over time, supporting mental health and emotional growth.

---

## 🚀 Key Features

- **Emotion Intensity Scoring** using NRC Emotion Intensity Lexicon.
- **Emotion Categorization** based on Plutchik’s 8 primary emotions.
- **Response Generation** via fine-tuned `google/gemma-1.3b-it` with GRPO and RAG.
- **Dynamic Response Ranking** using a tunable `α` parameter.
- **Privacy-First Architecture** (no raw message storage).

---

## 📊 Response Ranking Formula

Each user message generates **five response candidates**. These are scored using:

FinalScore[i] = (1 - α) × RAGscore[i] + α × Intensityscore[i]


- `RAGscore[i]`: Relevance score via Retrieval-Augmented Generation
- `Intensityscore[i]`: Emotional depth score using NRC-based scoring
- `α`: A value between `0` and `1` to balance factual vs emotional preference

**Tuning α:**
- `α ≈ 0`: Prioritize factual accuracy
- `α ≈ 1`: Prioritize emotional alignment

This formula allows adaptive prioritization depending on the conversation context (e.g., mental health support vs informative QA).

---

---

## 🔄 Workflow

1. **User Input**  
   → Sent to Emotion Intensity Scorer + Emotion Classifier + RAG Retriever

2. **Candidate Generation**  
   → Fine-tuned Gemma model (`gemma-1.3b-it`) generates 5 responses via GRPO

3. **Scoring & Ranking**  
   → Each response is scored by:
   - Emotional intensity scorer (BERT + NRC)
   - RAG relevance system

4. **Best Response Selection**  
   → FinalScore is calculated for each response  
   → Top-scoring response is selected



