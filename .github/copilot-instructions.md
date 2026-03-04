# AI Engineering Cohort - Copilot Instructions

## Project Structure
This repository contains 5 progressive AI engineering projects (project_1/ through project_5/), each building on the previous. Each project folder includes:
- A main notebook (e.g., `rag_chatbot.ipynb`) with guided exercises
- A solution notebook (e.g., `rag_chatbot_solution.ipynb`) for reference
- Environment files (`environment.yml` and/or `requirements.txt`) for dependency management
- Optional data/ and assets/ folders

## Development Workflow
1. **Environment Setup**: Use `conda env create -f environment.yml` or `uv pip install -r requirements.txt` for isolated dependencies
2. **Notebook Execution**: Run cells sequentially in VS Code or Jupyter; cells build incrementally (data prep → indexing → retrieval → generation)
3. **Validation**: Test RAG systems with sample queries like "What is your return policy?"; expect context-aware responses
4. **UI Deployment**: For chatbot projects, create `app.py` with Streamlit; run via `streamlit run app.py`

## Key Patterns & Conventions
- **RAG Pipeline**: Follow the standard flow in [project_2/rag_chatbot_solution.ipynb](project_2/rag_chatbot_solution.ipynb): load docs → chunk with LangChain → embed with sentence-transformers → index with FAISS → retrieve k=8 chunks → generate with Ollama/Gemma
- **Agent Loops**: Use LangChain/LangGraph for tool-calling agents; parse model responses for function calls as shown in [project_3/ask_the_web_agent_solution.ipynb](project_3/ask_the_web_agent_solution.ipynb)
- **Multimodal Routing**: Route queries to text/image/video generators based on intent; prefer GPU environments for heavy models like Stable Diffusion
- **Error Handling**: Wrap API calls (OpenAI, HuggingFace) in try-except; handle rate limits and authentication
- **Data Ingestion**: Use unstructured library for PDF processing; chunk text into 1000-char segments with overlap
- **Model Selection**: Default to Ollama for local inference (gemma3:1b); fall back to OpenAI API for cloud models

## Integration Points
- **Local LLMs**: Ollama for Gemma/Llama models; ensure model is pulled before use
- **Vector Stores**: FAISS for CPU-based indexing; ChromaDB mentioned in docs but not implemented
- **APIs**: OpenAI for embeddings/chat; HuggingFace for model downloads
- **UIs**: Streamlit for chatbots; Gradio for multimodal demos; Chainlit for agent interfaces

## Common Pitfalls
- Forget to activate conda environment before running notebooks
- Run cells out of order - data prep must complete before indexing
- Exceed API rate limits - implement exponential backoff
- GPU memory issues in project_5 - use Colab or reduce model size
- Path issues in Colab - adjust file paths to `/content/...`

## Dependencies
Pinned versions in environment.yml ensure reproducibility. Core stack: LangChain ecosystem, FAISS, sentence-transformers, OpenAI SDK, Ollama.