# F.R.I.D.A.Y - Delhivery Support Chatbot

F.R.I.D.A.Y is an intelligent Delhivery customer-support chatbot built using **Streamlit**, **Groq LLM**, and **ChromaDB vector search**.  
It can answer shipment queries, provide tracking info directly from CSV, and handle issues like lost/damaged parcels using LLM responses.  
It also supports smart document-based Q&A using Delhivery PDF knowledge files.

---

## 🚀 Features

### ✅ 1. Shipment Tracking (CSV-Based)
- If the user provides **ORDxxxx**, the bot fetches details from `logistics_data.csv`.
- Responds with live shipment info:  
  ✓ Status  
  ✓ Pickup location  
  ✓ Destination  
  ✓ Expected delivery date  
  ✓ Current transit hub  

---

### ✅ 2. Issue Detection (LLM-Powered)
If the user reports:
- delay  
- damaged  
- lost  
- wet / leaking  
- incorrect address  
- failed delivery  
- RTO (Return to Origin)

The bot **does NOT call CSV**.  
It immediately sends a helpful response:

> “Sorry to hear this… please email help@delhivery.com with Order ID.”

---

### ✅ 3. PDF-Based Knowledge Answering (RAG)
Just drop PDF documents into:

```
docs/Data_db/
```

The bot automatically:
- Reads all PDFs  
- Splits them into chunks  
- Creates embeddings  
- Stores them in ChromaDB  
- Answers any question using those documents  

Examples it can answer:
- Return policy  
- Reverse pickup rules  
- Damaged/lost claim timelines  
- Privacy policy  
- Pickup locations  
- ANY content inside your PDFs  

---

## 📦 Project Structure

```
project/
│── friday.py                  # Main chatbot script
│── requirements.txt
│── docs/
│     └── Data_db/
│            ├── logistics_data.csv
│            ├── *.pdf (any number of PDFs)
│── chroma_index/              # Auto-created vector DB folder
```

---

## 🔧 Installation & Setup

### 1. Clone the repository
```
git clone <your-repo-url>
cd your-repo-folder
```


### 2. Install dependencies
```
pip install -r requirements.txt
```

---

## 🔑 Add Your API Key

Create a `.env` file:

```
GROQ_API_KEY= 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
```

Or directly paste into your script (not recommended for GitHub).

---

## ▶️ Run the Chatbot

```
streamlit run friday.py
```

---

## 📘 How It Works (Logic Flow)

### 1️⃣ User sends a message  
→ Check for **issue keywords**  
→ If detected → LLM response (NO CSV)

### 2️⃣ If NOT issue  
→ Check for **Order ID (ORDxxxx)**  
→ If found → fetch tracking data from CSV

### 3️⃣ If no order ID  
→ Detect if user wants tracking  
→ Ask for Order ID

### 4️⃣ If not tracking  
→ Perform **RAG PDF search**  
→ Use LLM to answer from documents

### 5️⃣ Final answer sent to user.

---

## ✔ Recommended PDFs to Add
Place all PDFs inside `docs/Data_db/`

Examples:
- Return Policy  
- RTO Rules  
- Reverse Pickup  
- Lost & Damaged Claims  
- Privacy Policy  
- Pickup Locations  

---

## 📝 Notes
- Chroma index builds **automatically**.  
- No code changes required when adding new PDFs.  
- API key must be provided manually.

---

## 🙌 Acknowledgements
Built using:
- Streamlit  
- Groq LLM  
- LangChain  
- HuggingFace Embeddings  
- ChromaDB

---

## 📄 License
This project is open for educational use. No restrictions.
