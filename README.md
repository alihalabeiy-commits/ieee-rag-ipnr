# ieee-rag-ipnr
QudsGuide AI
Your Academic Journey, Simplified.
مرشدك الأكاديمي الذكي، بلغتك، وبمصادر موثوقة

A bilingual academic guidance prototype that uses Retrieval-Augmented Generation (RAG) to help students find information in Al-Quds University documents.

Prepared for the IEEE RAG Hackathon at Bethlehem University.
Team: Raafat Al-Habil and Ali Al-Halabiya.
The problem
Academic regulations, registration procedures, and study plans are spread across PDFs and websites. Students may ask in Palestinian Arabic or mix Arabic with English course names, making relevant information harder to find.

QudsGuide AI aims to make these documents easier to search and understand while keeping the supporting source visible.
Intended capabilities
- Arabic and English interaction, including Palestinian Arabic queries.
- Retrieval from academic regulations, study plans, and other selected university documents.
- Concise answers supported by document references and page numbers where available.
- Refusal when the available documents do not provide sufficient evidence.
- Local answer generation using Qwen3 through Ollama.
- A Streamlit interface with Arabic and English layouts.
These describe the prototype's design. Their reliability must be checked on the final integrated version.
How it works
1. Extract text from PDF, TXT, and JSON sources, retaining document metadata and page numbers where available.
2. Clean and split the text into overlapping chunks.
3. Generate multilingual embeddings and store them in ChromaDB.
4. Normalize the student's question and retrieve relevant passages using lexical and semantic matching.
5. Check whether the retrieved evidence is sufficient.
6. Ask the local language model to answer using the retrieved context, or return an insufficient-evidence response.
Documents provide retrieval context. The project does not train or fine-tune a model on university documents.
Technology
Component	Technology described in the project materials
Application	Python and Streamlit
Embeddings	sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2
Vector storage	ChromaDB with persistent storage
Retrieval	Lexical matching, trigram matching, and Chroma similarity
Answer generation	Ollama with qwen3:4b-instruct
Knowledge sources	PDF, TXT, and JSON documents


Local setup
The commands below follow the project report. Application code and dependencies must be present in the repository; this README does not include them.
1. Install Python and Ollama.
2. Open a terminal in the project folder containing app.py, rag_engine.py, and requirements.txt.
3. Install the project dependencies:
   python -m pip install -r requirements.txt
4. Download the configured local model:
   ollama pull qwen3:4b-instruct
5. Ensure the Ollama service is running. The documented local endpoint is http://127.0.0.1:11434.
6. Place permitted reference documents in documents/ and follow the indexing process implemented by the application. Rebuild the index after changing sources.
7. Check Python syntax and launch the interface:
   python -m py_compile app.py rag_engine.py
   python -m streamlit run app.py
The first run may require internet access to download dependencies, embedding weights, and the language model. Local generation requires sufficient memory and compute. Confirm that the model name in the code matches the installed Ollama model.
Example questions
- “شو المتطلب السابق لمادة هياكل البيانات؟”
- “What documents explain the registration process?”
- “Where can I find the graduation requirements for my study plan?”
- “متى موعد الامتحان النهائي؟”
Answers depend on the indexed documents. A question about an unavailable exam schedule should receive an insufficient-evidence response. Course prerequisites must be checked against the correct major, study-plan year, and source page.
AI usage disclosure
The team used ChatGPT to assist with planning and drafting versions of the code, project report, and presentation. AI-generated material requires human review and testing before submission or use.

The application uses Qwen3 through Ollama to generate answers from retrieved document passages. A multilingual embedding model represents questions and passages for semantic retrieval. These models serve different roles: embeddings help locate evidence, while Qwen3 writes the response.

The team remains responsible for source selection, code review, document accuracy, citation checks, evaluation, and all final project claims. AI assistance does not establish that the implementation is correct or that an answer is authoritative.
Evaluation and current status
The project report describes a working Streamlit interface during development and a successful independent local Ollama request. It does not provide a final documented evaluation of the complete system after the latest changes.

Before reporting performance, test the final version on:
- Questions with explicit supporting passages.
- Palestinian Arabic and mixed-language queries.
- Questions whose answers are absent from the sources.
- Correct document titles and page references.
- Conflicting or outdated study plans.
- Follow-up questions and information in tables.
For each case, record the question, retrieved evidence, source page, answer, outcome, and response time. Do not report an accuracy percentage or a zero-hallucination guarantee without supporting measurements.

The report describes an initial survey of 35 respondents, of whom 28 (80%) said they definitely wanted an AI academic guide. This is preliminary evidence of interest within that sample, not a measure of system accuracy or a representative estimate for all university students.
Sources, privacy, and limitations
- This is an independent student prototype, not an official Al-Quds University service.
- Check source publication dates and study-plan versions before relying on an answer. Historical documents may conflict with current requirements.
- RAG can reduce unsupported answers but cannot eliminate model or retrieval errors.
- Refer unresolved or personal academic decisions to the relevant advisor or registration office.
- Publish only documents that may lawfully be redistributed. Keep student records, credentials, API keys, and private files out of the repository.
- Local inference does not by itself establish the privacy of the entire application; review logging and any external services used.
Future work
Priorities include testing retrieval and citation quality, improving dialect handling, reviewing source freshness, and expanding coverage to additional majors.

The presentation also proposes a separate remote-exam integrity concept. It is future work outside the academic RAG prototype and is not presented here as an implemented or evaluated feature.
License
No software license was specified in the supplied project materials. The team should select and add a license before inviting reuse. University documents and model components retain their respective rights and terms.
