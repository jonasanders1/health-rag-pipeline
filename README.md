# Health RAG Pipeline

---

This project is an agentic Retrieval-Augmented Generation (RAG) pipeline designed to deliver personalized health advice based on real-time data from Withings smart scales. It leverages a comprehensive knowledge base (KB) including structured nutrition data from various countries (e.g., Norway, Finland, Sweden, UK, Denmark, US) in CSV format, user body composition metrics (e.g., weight, fat mass, muscle mass trends), and unstructured resources like books on coaching behavior change and motivational interviewing, plus dietary guidelines PDFs/MDs (e.g., US and Norwegian guidelines).

The system processes scale data to analyze trends, retrieve relevant nutrition facts and guidelines, and apply motivational techniques for empathetic, evidence-based recommendations. It's built for serverless deployment on AWS, focusing on scalability, cost-efficiency, and factual accuracy to help users achieve health goals like weight management or improved body composition.

---

## Main Goal
The primary objective is to provide the best possible health advice immediately after a user steps on their Withings smart scale. This includes:

- Analyzing real-time metrics (e.g., body mass, fat percentage) and historical trends.
- Recommending nutrient-dense foods/meals from international databases to address gaps (e.g., high-protein options for muscle gain).
- Incorporating dietary guidelines for balanced patterns (e.g., limit added sugars per US guidelines).
- Using coaching/motivational strategies (e.g., Transtheoretical Model stages) to encourage sustainable behavior change.

---

## File structure
```
health-rag-pipeline/
├── src/
│   ├── __init__.py
│   ├── main.py
│   ├── app.py
│   ├── config.py
│   │
│   ├── kb_ingestion/
│   │   ├── __init__.py
│   │   ├── preprocess_structured.py
│   │   ├── preprocess_unstructured.py
│   │   └── indexer.py
│   │
│   ├── retrieval/
│   │   ├── __init__.py
│   │   ├── retriever.py
│   │   └── tools.py
│   │
│   ├── agent/
│   │   ├── __init__.py
│   │   ├── agent_builder.py
│   │   └── workflows.py
│   │
│   └── utils/
│       ├── __init__.py
│       ├── data_utils.py
│       ├── metrics_utils.py
│       └── withings_integration.py
│
├── tests/
│   ├── __init__.py
│   ├── test_preprocess.py
│   ├── test_indexer.py
│   ├── test_retriever.py
│   ├── test_agent.py
│   │
│   └── benchmarks/
│       ├── benchmark_retrieval.py
│       └── benchmark_agent.py
│
├── configs/
│   ├── bedrock_config.json
│   ├── pinecone_config.json
│   └── kb_metadata.json
│
├── deploy/
│   ├── lambda_function.py
│   ├── serverless.yml / sam.yaml
│   └── ci_cd/
│       └── (GitHub Actions / CodePipeline configs)
│
├── data/
│  ├── structured/
│  └── unstructured/
│
├── requirements.txt
├── Dockerfile
├── .gitignore
├── .env.example
├── pyproject.toml / setup.py
```
---

## Features
- **KB Ingestion**: Preprocess and index structured CSVs (nutrition data) and unstructured PDFs/MDs (guidelines/books).
- **RAG Retrieval**: Hybrid semantic/keyword search via LlamaIndex and Pinecone for factual grounding.
- **Agentic Workflow**: Multi-step reasoning (e.g., analyze data → retrieve KB → generate advice) using Bedrock LLMs.
- **Withings Integration**: Triggered by scale events via webhooks for real-time responses.
- **Output**: Personalized Markdown
