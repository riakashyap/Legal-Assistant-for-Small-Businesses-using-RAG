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

