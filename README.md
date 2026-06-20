# 🛍️ AuraStyle AI — RAG-Based Fashion Stylist Agent

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white"/>
  <img src="https://img.shields.io/badge/ChromaDB-1C1C1C?style=for-the-badge&logo=databricks&logoColor=white"/>
  <img src="https://img.shields.io/badge/Llama_3.1-00A67E?style=for-the-badge&logo=meta&logoColor=white"/>
  <img src="https://img.shields.io/badge/Groq_API-FF6B00?style=for-the-badge&logoColor=white"/>
  <img src="https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black"/>
</p>

<p align="center">
  <b>A conversational AI stylist that gives personalised fashion advice grounded in real product inventory — built for <a href="https://epicfashionzone.in">Epic Fashion Zone</a></b>
</p>

---

## 🧠 What is AuraStyle AI?

AuraStyle AI is a **Retrieval-Augmented Generation (RAG) agent** designed for the fashion e-commerce domain. Unlike a standard chatbot that generates generic responses, AuraStyle grounds every reply in **real product data** from the Epic Fashion Zone catalog.

This means when a user asks *"What should I wear to a wedding?"*, AuraStyle doesn't just suggest generic outfits — it finds **actual products available in the store**, retrieves them using **semantic similarity**, and delivers styling advice with real prices and product visuals.

> 💡 **RAG = Retrieval + Generation** — The AI *retrieves* relevant products from a vector database, then *generates* a personalised response using an LLM. This ensures responses are accurate, context-aware, and inventory-grounded.

---

## ✨ Key Features

- 🔍 **Semantic Search** — Finds products based on *meaning*, not just keywords. Asking for "wedding wear" retrieves sarees even if the word "wedding" isn't in the product name
- 🤖 **LLM-Powered Responses** — Llama 3.1 via Groq's LPU delivers ultra-low latency, conversational styling advice
- 🗄️ **Vector Database** — ChromaDB stores product embeddings persistently for fast retrieval
- 💰 **Real-Time Product Data** — Price extraction and product metadata injected into every response
- 🖼️ **Visual Product Rendering** — Product images rendered directly in the Streamlit UI
- 📦 **Automated Data Ingestion** — Python scripts preprocess raw CSV catalogs into structured vector embeddings

---

## 🏗️ Architecture

```
User Query (Natural Language)
        │
        ▼
┌─────────────────────┐
│   Streamlit UI      │  ← User types: "I need a saree for a festival"
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  Sentence-Transformer│  ← Converts query to vector embedding
│  (all-MiniLM-L6-v2) │     using Hugging Face model
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│     ChromaDB        │  ← Searches vector store for semantically
│  (Vector Database)  │     similar products (Top-K retrieval)
└────────┬────────────┘
         │  Retrieved products + metadata (price, image, description)
         ▼
┌─────────────────────┐
│   Llama 3.1 via     │  ← LLM reads product context and generates
│     Groq API        │     personalised styling advice
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│   Streamlit UI      │  ← Displays response + product cards with
│  (Rich Response)    │     images, prices, and recommendations
└─────────────────────┘
```

---

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| **Frontend / UI** | Streamlit | Interactive web interface |
| **LLM** | Llama 3.1 (via Groq API) | Response generation |
| **Vector Database** | ChromaDB | Persistent product embedding store |
| **Embeddings** | Sentence-Transformers `all-MiniLM-L6-v2` | Semantic similarity encoding |
| **Data Handling** | Pandas, Python | CSV ingestion and preprocessing |
| **Environment** | python-dotenv | API key management |
| **Language** | Python 3.10+ | Core language |

---

## 📁 Project Structure

```
AuraStyle-AI/
│
├── data/
│   └── products.csv             # Epic Fashion Zone product catalog
│
├── embeddings/
│   └── ingest.py                # Script to create vector embeddings from CSV
│
├── chroma_db/                   # Persistent ChromaDB vector store (auto-generated)
│
├── app.py                       # Main Streamlit app
├── rag_pipeline.py              # Core RAG logic — retrieval + generation
├── requirements.txt             # All dependencies
├── .env.example                 # Template for environment variables
├── .gitignore                   # Excludes .env and chroma_db
└── README.md
```

---

## ⚙️ Setup & Installation

### 1. Clone the Repository
```bash
git clone https://github.com/Jidnyesha-403/AuraStyle-AI.git
cd AuraStyle-AI
```

### 2. Create a Virtual Environment
```bash
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Set Up Environment Variables
```bash
cp .env.example .env
```
Open `.env` and add your Groq API key:
```
GROQ_API_KEY=your_groq_api_key_here
```
> Get your free Groq API key at [console.groq.com](https://console.groq.com)

### 5. Ingest Product Data into Vector Database
```bash
python embeddings/ingest.py
```
This reads `data/products.csv`, converts product descriptions into vector embeddings using Sentence-Transformers, and stores them in ChromaDB.

### 6. Run the App
```bash
streamlit run app.py
```
Visit `http://localhost:8501` in your browser.

---

## 📋 Requirements

```txt
streamlit
chromadb
sentence-transformers
groq
pandas
python-dotenv
```

---

## 💬 Example Interactions

**User:** *"I'm attending a traditional wedding. Suggest something elegant."*

**AuraStyle AI:** *"For a traditional wedding, I'd recommend our Kanjivaram Pure Silk Saree in deep burgundy — ₹4,599. Its rich zari border and classic drape make it perfect for wedding ceremonies. Pair it with gold jewellery for a complete look."* [Product image + price displayed]

---

**User:** *"Show me sarees under ₹2000 in bright colours."*

**AuraStyle AI:** *"Here are 3 vibrant options under ₹2000 from our collection..."* [Products with price filtering applied]

---

## 🔑 Key Technical Concepts

| Term | What It Means in This Project |
|---|---|
| **RAG (Retrieval-Augmented Generation)** | AI retrieves real product data before generating responses — ensuring accuracy |
| **Semantic Retrieval** | Finding products by meaning (e.g., "festive wear" matches "Banarasi saree") not just keywords |
| **Vector Embeddings** | Products converted to numerical vectors so similarity can be mathematically computed |
| **Metadata Injection** | Price, image URL, and product details passed alongside vectors into the LLM context |
| **In-Context Learning** | LLM reads retrieved product info before replying — no hallucination of fake products |

---

## 🚀 Future Improvements

- [ ] Deploy on Streamlit Cloud
- [ ] Add user session memory for multi-turn conversations
- [ ] Integrate with Epic Fashion Zone live product database
- [ ] Add voice input support
- [ ] Implement feedback loop to improve recommendations
- [ ] Add cart functionality directly from chat

---

## 👩‍💻 Built By

**Jidnyesha Ahirrao**
B.Tech CS (Data Science)_26 @ SRM Institute of Science and Technology

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/jidnyesha-ahirrao-061401255/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/Jidnyesha-403)
[![Live Project](https://img.shields.io/badge/Live_Site-epicfashionzone.in-1A7A4A?style=flat-square)](https://epicfashionzone.in)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">Built with ❤️ for <a href="https://epicfashionzone.in">Epic Fashion Zone</a> — Authentic Handloom Sarees & Traditional Crafts</p>
