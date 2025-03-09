# AI-Detective-Challenge-Postmortem

An AI-powered RAG system to assist detectives in solving a cryptocurrency exchange hack case. This system processes case files, retrieves relevant evidence, and generates detailed investigation reports.

## 🔍 System Features

- **Vector Embeddings**: Store case files as vector embeddings for semantic search
- **Multi-Step Retrieval**: Expand queries to find relevant evidence across case files
- **Evidence Reranking**: Rerank documents based on relevance to the query
- **Investigation Reports**: Generate detailed reports from the retrieved evidence
- **S3 Storage**: Save reports to an S3 bucket for future reference
- **Web UI**: User-friendly interface for detectives to interact with the system
- **Guard Agent**: AI-powered validation to ensure queries relate to the crypto hack investigation

## 🏗️ Architecture

The system uses a multi-component architecture:

1. **Guard Agent**: Validates incoming queries to ensure they're related to the investigation
2. **Document Processing**: Convert case files into embeddings with text-embedding-ada-002
3. **Vector Database**: Pinecone for storing and searching document embeddings
4. **Retrieval Engine**: Implement both single-step and multi-step retrieval strategies
5. **Reranking System**: Improve retrieval quality using LLM-based relevance scoring
6. **Report Generation**: Create investigation reports using gpt-mini-4o-mini
7. **Storage Layer**: Save reports to Amazon S3
8. **API Layer**: FastAPI backend for handling requests
9. **UI Layer**: Streamlit frontend for detective interaction

## 🛠️ Technical Stack

- **Embeddings**: OpenAI's text-embedding-ada-002
- **LLM**: OpenAI's gpt-4o-mini
- **Vector Database**: Pinecone
- **Backend**: FastAPI
- **Frontend**: Streamlit
- **Storage**: Amazon S3
- **Language**: Python 3.9+

## Project Structure

```
├── app
│   ├── api
│   │   ├── __init__.py
│   │   ├── main.py
│   │   ├── models.py
│   │   └── services.py
│   ├── core
│   │   ├── config.py
│   │   ├── __init__.py
│   ├── db
│   │   ├── __init__.py
│   │   ├── pinecone_db.py
│   │   └── s3_storage.py
│   ├── rag
│   │   ├── embeddings.py
│   │   ├── guard_agent.py
│   │   ├── __init__.py
│   │   ├── llm.py
│   │   ├── reranker.py
│   │   └── retriever.py
│   └── ui
│       ├── __init__.py
│       └── streamlit_app.py
├── data
│   └── case_files
│       ├── case_1.txt
│       ├── case_2.txt
│       ├── case_3.txt
│       ├── case_4.txt
│       ├── case_5.txt
│       ├── case_6.txt
│       ├── case_7.txt
│       └── case_8.txt
├── LICENSE
├── main.py
├── README.md
├── requirements.txt
└── scripts
    └── load_documents.py
```

## 📊 Post-Mortem Analysis

### What Went Well

1. **Architecture Design**: The system implemented a well-structured multi-component architecture with clear separation of concerns, modular code design, and proper dependency injection in the FastAPI implementation.

2. **Advanced RAG Features**: The implementation included several advanced RAG techniques beyond basic retrieval, including multi-step retrieval with query expansion, LLM-based reranking, confidence scoring, and a guard agent to filter irrelevant queries.

3. **User Experience**: The Streamlit UI was designed with a focus on investigator experience, featuring clear separation of content, evidence comparison with confidence ratings, transparent presentation of the AI's reasoning, and report download functionality.

### Future Improvements

1. **Chat History Cache**: In this project, we have not implemented the chat history cache for the chatbot so which it can not remember the previous chat conversation, so it can not fully understand the insight of the conversation.

2. **Intent Detection**: We can do a intent detection at first for latest user's query combined with history chat conversation to make the query clearer for chatbot to understand and analyze what user want to deliver.

3. **Classification Route**: Classification route can help the chatbot go straight to the best route and have a detailed explanation, answer for us in a specific use case or event.

2. **Prompt Engineering**: For RAG system or normal chatbot system, doing a good prompt can lead to a really good result and vice versa. We can apply CoT (Chain of Thought) prompting technique to improve the quality of generated answer.

4. **Containerization**: Develop Docker containers for consistent environments, use Docker Compose for local development, and create Kubernetes manifests for production deployment.

5. **Performance Optimizations**: Implement caching for common queries, more efficient API request batching, streaming responses for long-running operations, and progressive UI loading.

## Link Video Presentation

Link for Video Presentation: [HERE](https://drive.google.com/file/d/1Z-ALvcU8a4da1gfnz4bTqGCM16PY3L2i/view?usp=sharing)