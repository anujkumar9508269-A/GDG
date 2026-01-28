# GDG
# Financial Intelligence Chatbot: My AI/ML Learning Journey

## 🚀 Project Overview
As a newcomer to the world of AI and Machine Learning, this project served as my "deep dive" into building a functional, real-time application. Initially, I perceived this project as a simple tool to query stock prices. However, it quickly evolved into a sophisticated system integrating **Retrieval-Augmented Generation (RAG)**, live data streaming, and autonomous agent orchestration.

The goal was to move beyond static data and create a tool that not only reports the "what" (price) but also explains the "why" (news and market trends) in real-time.

---

## 🧠 My Growth & Problem-Solving Evolution

### 1. From Static to Streaming
At the start, I viewed data as a fixed resource. My first challenge was realizing that financial markets require constant monitoring.
* **The Learning Curve:** I mastered live data ingestion using WebSockets.
* **The Shift:** I implemented a **Finnhub WebSocket client** that listens for trades, updates a local buffer, and populates a vector database simultaneously.

### 2. Overcoming Constraints: Chunking Data
I encountered a major hurdle with `yfinance` limitations regarding long periods of 1-minute data.
* **The Solution:** I improved my logic by creating a **backfilling function** that fetches data in 7-day "chunks" and stitches them together. This taught me to handle API limitations with graceful, iterative logic.

### 3. Implementing Intelligent Orchestration
Initially, I planned to use simple conditional logic to handle user queries.
* **The Upgrade:** I discovered **LangGraph**, which allowed me to build a "Supervisor Agent". This manager dynamically decides whether to invoke the "Research Agent" for news or the "Plotting Agent" for visual charts.

---

## 🛠 Technical Deep Dive: What I Learned

### Key Functions & Methods
* **`backfill_historical_data()`**: Taught me to use `pandas` for concatenating complex time-series dataframes and ensuring continuity.
* **`on_message(ws, message)`**: My introduction to asynchronous programming, converting raw JSON trade data into structured `Document` formats.
* **`vectorstore.similarity_search()`**: A core RAG concept; I learned to use embeddings to find relevant news articles that correlate with specific stock movements.

### System Architecture
1.  **Real-Time Stream**: Uses `websocket-client` to maintain a heartbeat with the market.
2.  **Vector Memory**: Uses **FAISS** to store and retrieve financial news articles, providing the LLM with necessary context.
3.  **Brain (LLM)**: Integrates the **Hugging Face `flan-t5-small`** model to summarize findings.

---

## ⚡ Challenges & Personal Insights
* **The "Ambiguous Truth" Error**: I spent significant time debugging Python's "Series is ambiguous" error. It taught me to be precise by extracting scalar values using `.item()` or `.iloc[]`.
* **LLM Verbosity**: I learned to use **Prompt Engineering** to refine the `google/flan-t5-small` responses, keeping the output concise and relevant.

---

## 📖 How to Use
1.  **Set your `HF_TOKEN`**: Ensure your Hugging Face API key is stored in your environment or Colab secrets.
2.  **Initialize the System**: Run the setup cells to build the FAISS vector store and load the LLM.
3.  **Start the Stream**: Execute the WebSocket cell to begin capturing live trade data for **AAPL** and **MSFT**.
4.  **Engage the Chatbot**: Query the bot about significant moves or general stock information.

---

## 🔮 For task 3 : 
i tried and almost did the backend part but could not complete the code .

Tried to implement a real-time dashboard using **Plotly** to visualize trades as they hit the buffer.

