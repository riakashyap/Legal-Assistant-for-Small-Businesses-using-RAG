# Legal-Assistant-for-Small-Businesses-using-RAG
Small businesses often face difficulty understanding contracts, agreements, and regulatory documents. Misinterpreting clauses can lead to legal disputes, penalties, or financial loss. Traditional legal services are expensive and time-consuming. We can build a RAG system to resolve this.

# Architecture
<pre> 
+---------------------+        +----------------------+        +----------------------+
|  Document Ingestion |  -->   |  Embedding + Index   |  -->   |  Query + Generation  |
| (PDF, DOCX, TXT)    |        |  (Sentence-Txf +     |        |  (Retriever + LLM)   |
| pypdf, python-docx  |        |   FAISS/Milvus)      |        |  FastAPI service     |
+---------------------+        +----------------------+        +----------------------+
                                                   \          /
                                                    \        /
                                                 +----------------+
                                                 |  Risk Scoring  |
                                                 | (keywords/ML)  |
                                                 +----------------+

                    +---------------------------+
                    |      Observability        |
                    |   MLflow + JSON logs      |
                    +---------------------------+

                    +---------------------------+
                    | Frontend (optional)       |
                    | Streamlit or React        |
                    +---------------------------+
</pre>
# Project Structure
<pre>
legal-assistant-rag/
├─ api/
│  ├─ main.py                # FastAPI app
│  ├─ schemas.py             # Pydantic request/response
│  ├─ deps.py                # DI: clients, configs
├─ rag_core/
│  ├─ ingest.py              # parsers, chunking, metadata
│  ├─ embedder.py            # ST/OpenAI embeddings
│  ├─ vectorstore.py         # FAISS/Milvus/Pinecone adapters
│  ├─ retriever.py           # BM25+Vector hybrid (optional)
│  ├─ generator.py           # LLM call + prompt
│  ├─ risk.py                # keyword risk scoring
│  ├─ evaluate.py            # offline eval: retrieval & answer quality
├─ monitoring/
│  ├─ mlflow_utils.py        # start mlflow, log params/metrics/artifacts
│  ├─ service_metrics.py     # latency, hit-rate, errors
├─ configs/
│  ├─ default.yaml
│  ├─ local.yaml
├─ tests/
│  ├─ test_ingest.py
│  ├─ test_retrieve.py
│  ├─ test_risk.py
├─ scripts/
│  ├─ run_mlflow.sh
│  ├─ ingest_folder.py
│  ├─ eval_run.py
├─ .env.example
├─ requirements.txt
├─ README.md
├─ docker-compose.yaml       # api + mlflow + minio (optional)
</pre>

