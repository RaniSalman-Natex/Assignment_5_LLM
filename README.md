# 🎥 Retrieval-Augmented Generation (RAG) for Video Question Answering

This project implements a multimodal **Retrieval-Augmented Generation (RAG)** system that allows users to ask natural language questions about a video and receive relevant video segments in response. It combines **semantic** and **lexical** search over a lecture video using text and audio content.

## 🔗 Live Demo

🌐 [Click to try the Streamlit App]([https://share.streamlit.io/your-username/your-repo/main_app.py](https://assignment5llm-dddxmahcjfbbpg47yfbeek.streamlit.app/))

> Note: Replace with your actual Streamlit Cloud URL.

---

## 📽️ Video Used

**Title:** Token Jumping and Token Sliding – Parametrized Complexity  
**Link:** [https://www.youtube.com/watch?v=dARr3lGKwk8](https://www.youtube.com/watch?v=dARr3lGKwk8)

---

## 🧠 Features

- Natural language question input
- Top-1 results from:
  - ✅ FAISS (semantic search)
  - ✅ TF-IDF
  - ✅ BM25
- Timestamp + transcript snippet returned
- Embedded YouTube video plays from relevant timestamp
- Handles "not in video" queries gracefully

---

## ⚙️ Architecture Overview

### 🎧 Speech-to-Text
- OpenAI Whisper model transcribes the full video

### 📝 Transcript Segmentation
- Chunks generated every ~10–15 seconds with start/end times

### 📷 Keyframe Sampling
- Frames sampled every 5 seconds using OpenCV (not shown in UI but extracted)

### 🔎 Embedding Models
- **Text:** `all-MiniLM-L6-v2` (via `sentence-transformers`)  
- **Image:** CLIP model available but not used in current retrieval (only text-based)

### 🧠 Retrieval Engines
- **FAISS** (Flat L2 index)
- **TF-IDF** (via scikit-learn)
- **BM25** (via `rank_bm25`)

---

## 🧪 Gold Test Set

A manually constructed test set with:
- 10 answerable questions (with ground truth timestamps)
- 5 unanswerable questions

See: `test_set.json`

---

## 📊 Evaluation (Manual)

- Accuracy: Top-1 retrieval compared to gold timestamps
- False positives: Verified for unanswerable cases
- Latency: Low (real-time) using cached model + FAISS index

---

## 📂 Project Structure

├── main_app.py # Streamlit app
├── transcript_chunks.json # Segmented transcript with timestamps
├── test_set.json # Gold test set (10 answerable + 5 unanswerable)
├── requirements.txt # Python dependencies
├── README.md # Project overview (this file)


---

## 📦 Setup Instructions

### ▶️ Run Locally

```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
pip install -r requirements.txt
streamlit run main_app.py
