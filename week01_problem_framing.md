# Week 1 - Problem Framing

## 1. Project Track
- **Track**: AI Research Assistant [6, 8]
- **Project Name**: Grounded Literature Evidence Assistant [6, 9]

## 2. Business Pain
Graduate researchers working with large collections of technical documents spend significant manual effort locating passages relevant to a research question, comparing evidence across papers, and preserving the source context needed to justify conclusions [6, 9].
- **Primary Consequence**: Evidence discovery is slow, repeated searches waste time, and manual note-taking risks losing source context [6, 9].
- **Evidence Status**:
  - **Observed**: Researchers opening multiple PDFs and running manual keyword searches [10, 11].
  - **Estimated**: Manual search takes ~20 minutes per question [12-14].
  - **Assumed**: Semantic search will reduce search friction without losing accuracy [14, 15].

## 3. Target User
- **Role**: Graduate Researcher / Technical Analyst [7, 13].
- **Context**: Reviewing 10–50 complex technical PDF papers during active literature synthesis [7, 13].
- **Primary Goal**: Locate reliable, source-grounded answers with verifiable citations [7, 13].
- **Secondary Stakeholders**: Research supervisors, peer reviewers, and engineering maintainers [12, 13].

## 4. Current Workflow
1. Formulate research question [7, 10].
2. Collect candidate PDF documents [7, 10].
3. Open individual papers and run keyword searches (`Ctrl+F`) [7, 10].
4. **Inspect surrounding paragraphs (Highest Friction Step)** [7, 10, 12].
5. Copy evidence and record findings [7, 10].
6. Synthesize evidence across papers [7, 10].

## 5. Current Baseline
- **Metric**: \\(B_0 = T_{\text{manual}}\\) (Time to locate usable evidence per query) [12, 16, 17].
- **Current Value**: 20 minutes / question [12, 16, 17].
- **How Measured**: Workflow observation and timing during pilot research sessions [12, 16, 18].
- **Confidence**: Estimated [13, 18].

## 6. Primary Data / Knowledge
- **Available Sources**: User-uploaded technical PDF reports, research papers, and domain manuals [7, 19].
- **Access**: Read-only local/containerized filesystem [19, 20].
- **Quality Concerns**: Scanned PDFs, complex tables, and multi-column layouts [19, 21].
- **Sensitivity / Privacy**: Non-sensitive / internal local storage [19, 20].

## 7. AI Opportunity
- **Primary Capability**: **Retrieval + Generation** [7, 21, 22].
- **Why AI May Help**: Semantic vector search captures conceptual matches that simple keyword search misses, and LLMs synthesize scattered passages into concise answers [12, 21, 23].
- **Why Rules Alone Aren't Enough**: Terminology varies widely across papers, making static keyword rules brittle [12, 24].

## 8. Minimum Useful MVP
Given a small trusted collection of research documents and a natural-language question, the system should return a concise answer together with the source passages and document metadata that support the answer [7, 25, 26].

## 9. Success Metrics
- **User / Business Metric**: Reduce task time from \\(T_0 = 20\text{ min}\\) to \\(T_1 \le 8\text{ min}\\) per query [7, 25, 27].
- **AI Quality Metric**: Retrieval Recall \\(\ge 80\%\\) at \\(k=5\\); \\(\ge 80\%\\) of answers judged supported by cited passages [7, 28, 29].
- **Operational Metric**: Interactive query response latency \\(< 10\text{ seconds}\\) [25, 28, 29].

## 10. Acceptance Criteria
- **Critical**:
  1. Every factual claim shown must display a supporting source passage and citation [28-30].
  2. The evaluation benchmark must use known questions with manually verified ground-truth evidence [27, 31].
- **Target**:
  1. Relevant evidence appears in retrieved results for \\(\ge 80\%\\) of test questions [28, 29].
  2. Reviewers judge \\(\ge 80\%\\) of generated answers as fully grounded [28, 29].
- **Operational**:
  1. Median end-to-end response time stays under 10 seconds [28, 29].

## 11. Interface
A simple web UI featuring a question input box, a generated answer pane, and an interactive sidebar displaying supporting source passages with page numbers [30, 32, 33].

## 12. Deployment Target
- **Development**: Local Docker Python container [20, 34, 35].
- **Expected Production Target**: Cloud-hosted API microservice on AWS [20, 34, 35].

## 13. Constraints
1. Must operate on user-provided local PDFs without querying external web search engines [20, 36].
2. Must preserve strict source traceability for every claim [20, 30].
3. Initial MVP must run on standard developer hardware [20, 36].

## 14. Risks
1. **Hallucination / Unsupported Claims**: Mitigated by mandatory inline citations [36-38].
2. **PDF Parsing Corruption**: Mitigated by testing extraction tools on a benchmark PDF set upfront [21, 36, 38].
3. **User Over-Trust**: Mitigated by highlighting source text for instant user verification [37, 38].

## 15. Non-Goals
1. No autonomous research paper writing or synthetic manuscript generation [35, 36, 38].
2. No automated API write operations or external database modifications [35, 36, 38].
3. No unrestricted internet research agents in the initial MVP [35, 36, 38].

## 16. Expected Value
A 60% reduction in evidence search time, freeing up researcher hours for higher-level analysis and scientific judgment [35, 39, 40].

## 17. Assumptions to Validate
1. **A1 (High Risk)**: Users will trust generated answers when source citations are clearly shown [15, 41].
2. **A2 (High Risk)**: Semantic vector retrieval will outperform simple keyword search on technical PDFs [15, 41].
3. **A3 (Medium Risk)**: End-to-end response latency under 10 seconds will maintain researcher focus [15, 41].
