<div align="center">

# 🤖 AuraStyle AI
### RAG-Based Fashion Stylist Agent

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)](https://langchain.com)
[![Llama](https://img.shields.io/badge/Llama_3.1-0467DF?style=for-the-badge&logoColor=white)](https://ai.meta.com/llama/)
[![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io)
[![Live Demo](https://img.shields.io/badge/🌐_Live_Demo-epicfashionzone.in-FF6B6B?style=for-the-badge)](https://epicfashionzone.in)

**A production-ready AI stylist that recommends real products from live inventory — not hallucinated outfits.**

</div>

---

## 🎯 What Is AuraStyle AI?

AuraStyle AI is a **Retrieval-Augmented Generation (RAG)** agent deployed on [Epic Fashion Zone](https://epicfashionzone.in), a live e-commerce platform for handloom sarees and traditional Indian crafts.

Unlike generic AI chatbots that make up product recommendations, AuraStyle AI:
- **Searches actual inventory** using semantic vector search
- **Grounds every response** in real products with real prices
- **Renders product cards** with images and buy links directly in the chat
- **Responds in milliseconds** using Groq's LPU inference

> *"Tell me what to wear for a wedding under ₹3000"* → AuraStyle finds matching sarees from the real catalog, explains why they suit the occasion, and shows you the products.

---

## 🏗️ Architecture

```
User Query
    │
    ▼
┌─────────────────────────────────────────────┐
│              Streamlit Frontend             │
└──────────────────┬──────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────┐
│           LangChain RAG Pipeline            │
│                                             │
│  Query → Sentence-Transformer Embedding     │
│       → ChromaDB Semantic Search            │
│       → Top-K Product Retrieval             │
│       → Context Injection into Prompt       │
│       → Llama 3.1 via Groq LPU             │
│       → Styled Response + Product Cards     │
└─────────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────┐
│         ChromaDB Vector Database            │
│   (Product embeddings + metadata)           │
└─────────────────────────────────────────────┘
```

---

## ✨ Key Features

- **🔍 Semantic Search** — Uses `all-MiniLM-L6-v2` embeddings for meaning-based product retrieval, surpassing keyword search
- **⚡ Ultra-Low Latency** — Groq's LPU delivers near-instant LLM responses
- **🛍️ Real Inventory Grounding** — Every recommendation is a real product with real pricing
- **🖼️ Visual Product Cards** — Images, prices, and descriptions rendered in-chat
- **📦 Automated Data Pipeline** — Python scripts preprocess raw CSV catalogs into vector embeddings automatically

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| LLM | Llama 3.1 (via Groq API) |
| RAG Framework | LangChain |
| Vector Database | ChromaDB |
| Embeddings | Sentence-Transformers (`all-MiniLM-L6-v2`) |
| Frontend | Streamlit |
| Data Processing | Python, Pandas |
| Hosting | Live at epicfashionzone.in |

---

## 🚀 Getting Started

### Prerequisites
```bash
Python 3.10+
A Groq API key (free at console.groq.com)
```

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/Jidnyesha-403/AuraStyle-AI-RAG-Based-Fashion-Stylist-Agent.git
cd AuraStyle-AI-RAG-Based-Fashion-Stylist-Agent

# 2. Install dependencies
pip install -r requirements.txt

# 3. Set up environment variables
cp .env.example .env
# Add your GROQ_API_KEY to .env

# 4. Build the vector database from product catalog
python scripts/build_vectordb.py

# 5. Run the app
streamlit run app.py
```

### Environment Variables
```env
GROQ_API_KEY=your_groq_api_key_here
```

---

## 📁 Project Structure

```
AuraStyle-AI/
├── app.py                      # Main Streamlit application
├── rag_pipeline.py             # LangChain RAG chain setup
├── vectordb/                   # ChromaDB persistent storage
├── scripts/
│   └── build_vectordb.py       # CSV → vector embeddings pipeline
├── data/
│   └── products.csv            # Product catalog
├── requirements.txt
└── .env.example
```

---

## 💡 How RAG Works Here

**Traditional chatbot:** User asks → LLM makes up an answer (often hallucinated products)

**AuraStyle AI with RAG:**
1. User asks → query is converted to a vector embedding
2. ChromaDB finds the most semantically similar products in the catalog
3. Those real products are injected into the LLM's context
4. Llama 3.1 generates a response *grounded in actual inventory*
5. Product cards with images and prices are rendered in the UI

This means **zero hallucinations** on product recommendations.

---

## 📊 Performance

| Metric | Result |
|---|---|
| Average response latency | < 2 seconds (Groq LPU) |
| Retrieval method | Semantic (ChromaDB + MiniLM) |
| Deployed | Production (epicfashionzone.in) |

---

## 🙋 About the Developer

Built by **Jidnyesha Ahirrao** — AI & GenAI Engineering, Data Science, Python Development.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/jidnyesha-ahirrao-061401255/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat-square&logo=github)](https://github.com/Jidnyesha-403)

---

<div align="center">

⭐ **Star this repo if you found it useful!**

*Part of the [Epic Fashion Zone](https://epicfashionzone.in) platform*

</div>
