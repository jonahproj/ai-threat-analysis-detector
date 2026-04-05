# Week 7: RAG Security Knowledge Assistant — Evaluation Report

## 1. Setup Summary 
- **LLM:** [model name used, e.g., llama-3.3-70b-versatile via Groq] 
- **Embeddings:** [model name, e.g., sentence-transformers/all-MiniLM-L6-v2 via HuggingFace] 
- **Vector Store:** In-Memory Vector Store
- **Documents loaded:** [list your 3–5 documents and approximate page counts]


## 2. Test Results
| # | Question | Used Documents? | Quality | Notes | 
|---|----------|----------------|---------|-------|
| 1 | "What are common techniques for credential access according to MITRE? | Yes | Good |  | 
| 2 | "How does phishing relate to initial access in the ATT&CK framework?"  | Yes | Good |  | 
| 3 | "What is lateral movement and what techniques do attackers use?"  | Yes | Good | This specific data was not fed into it. It said it wasn't sure but tried to send documents still  | 
| 4 | "What does the NIST framework recommend for the Detect function? | Yes | Good | This specific data was not fed into it. It said it wasn't sure but tried to send documents still | 
| 5 | "What is the difference between spearphishing attachment and spearphishing link? | Yes | Good | This specific data was not fed into it. It said it wasn't sure but tried to send documents still |

## 3. Edge Case Observations 
- **Unrelated question:** It said that it wasn't sure but used documents to find the answers 
- **Topic not in documents:** It admitted that it didn't know

## 4. Settings Experiments (if completed) 
- **Temperature change:** Did not perform
- **Chunk size change:** Did not perform
- **Top K change:** Did not perform

## 5. Reflection 
- What surprised you about how RAG works? What surprised me most is how much the system relies on the retrieval step rather than just the language model itself. Even when information is missing, it can still generate reasonable responses while acknowledging uncertainty. I would improve retrieval accuracy by tuning chunk size, Top-K results, and using better embedding models. Adding source citations and fallback data sources would also make the system more reliable and trustworthy. I can use RAG to retrieve real-time threat intelligence data and generate summaries, IOC extraction, and explanations. This would improve the accuracy and relevance of insights in the Threat Intelligence Feed Dashboard.