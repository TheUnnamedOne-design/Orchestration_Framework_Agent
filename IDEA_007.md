# Multi-Agent Deep Research & Knowledge Synthesis Engine

## 1. Idea Overview

A **collaborative multi-agent system** that accepts a complex research question and deploys a coordinated team of specialized AI agents to produce a structured, cited, expert-level research document — automatically.

Unlike fast search-and-summarize tools (Perplexity, ChatGPT search), this system performs **deep, multi-source, multi-stage research** with agent specialization, parallel execution, cross-source fact-checking, a critic loop that identifies knowledge gaps, and a synthesis agent that combines all findings into a coherent publication-quality document.

The output is a **living document** — users can ask follow-up questions, request deeper dives into specific sections, or trigger a refresh when new information becomes available.

---

## 2. Problem Statement

Knowledge workers, researchers, developers, analysts, and students routinely face the same problem: a complex question that requires synthesizing information from many sources — academic papers, industry blogs, documentation, GitHub repositories, news, and expert discussions.

The current options are inadequate:

**Manual research** is slow. A thorough investigation of a single complex technical question can take hours or days of reading, note-taking, and synthesis.

**Web search** returns a list of links. The cognitive work of reading, filtering, and synthesizing remains entirely on the researcher.

**Perplexity and ChatGPT search** are fast but shallow. They return a summary of the top search results — typically surface-level, single-perspective, and lacking depth. They do not cross-validate sources, identify contradictions, or surface what is contested versus what is established.

**NotebookLM** requires the user to upload documents manually. It does not discover and collect its own sources.

**Google Deep Research** is an early product that does perform multi-step research but is a closed system with no customization, no domain specialization, and no ability to connect to private or internal knowledge bases.

```text
Question: "What are the tradeoffs of event sourcing vs CRUD in
           high-throughput financial systems?"

Current options:
  Google → 10 links
  Perplexity → 300-word summary, 5 sources
  Manual research → 6 hours

What we need:
  Structured analysis
  Multiple expert perspectives
  Academic + practical sources
  Contradictions identified
  Confidence levels
  Cited evidence
  Delivered in < 10 minutes
```

---

## 3. Proposed Solution

When the user submits a research question, a **Navigator Agent** analyzes it, identifies the key sub-questions and research angles, and dispatches a team of specialized agents to work in parallel. Each agent focuses on a specific source type or analytical task.

The agents report their findings back to the Navigator, which monitors completeness, identifies gaps, re-dispatches agents if needed, and finally triggers the Synthesis Agent to produce the structured output document.

```text
User submits: "What are the tradeoffs of event sourcing vs CRUD
              in high-throughput financial systems?"

Navigator Agent
    ↓
Decomposes into sub-questions:
    1. What is event sourcing? What is CRUD?
    2. What are the performance characteristics of each?
    3. How do financial systems specifically differ from general use cases?
    4. What do practitioners report from real-world implementations?
    5. What does academic research say?
    6. What does the open-source community say about tooling?

    ↓ (parallel dispatch)

┌───────────────┬────────────────┬──────────────────┬──────────────┐
↓               ↓                ↓                  ↓              ↓
Web Agent    Paper Agent    GitHub Agent     Reddit/HN Agent   Docs Agent
(blogs,      (arXiv,        (real-world      (practitioner     (official
 articles)   Semantic       implementations)  opinions)         docs)
             Scholar)

    ↓ (results collected)

Fact-Check Agent
    ↓ (validates conflicting claims across sources)

Critic Agent
    ↓ (identifies gaps: "missing coverage of CQRS as middle ground")

Navigator re-dispatches for gap coverage
    ↓

Synthesis Agent
    ↓

Structured Research Document
    ├── Executive Summary
    ├── Section 1: Core Concepts
    ├── Section 2: Performance Analysis
    ├── Section 3: Financial System Specifics
    ├── Section 4: Practitioner Perspectives
    ├── Section 5: Contested Claims
    ├── Section 6: Recommendation Framework
    └── Sources (cited, with confidence levels)
```

---

## 4. Core Components

### 4.1 Navigator Agent (Orchestrator)

The Navigator is the central coordinator. It understands the research goal, plans the investigation strategy, manages agent dispatch, monitors completeness, and decides when the research is sufficient.

**Responsibilities:**

```text
Parse and clarify the research question
Decompose into sub-questions and research tracks
Assign tracks to specialized agents
Monitor incoming findings
Detect gaps and contradictions
Re-dispatch agents for gap coverage
Trigger synthesis when coverage is satisfactory
```

**Completion criteria examples:**

```text
Minimum N sources per sub-question
Coverage of N distinct perspectives
No critical sub-question left unanswered
Fact-check agent has validated all major claims
Critic agent found no significant gaps
```

### 4.2 Web Research Agents (Parallel)

Multiple web research agents can run simultaneously, each focused on a different angle (practitioner blogs, company engineering posts, news sources, forums).

```text
For each assigned sub-question:
    ↓
Generate search queries (2-4 queries per sub-question)
    ↓
Execute web searches
    ↓
Scrape and clean full-text content from top results
    ↓
Extract key claims with source attribution
    ↓
Score relevance and credibility
    ↓
Report structured findings to Navigator
```

**Source quality scoring factors:**

```text
Domain authority (academic > industry blog > forum)
Publication recency
Author credentials (if discoverable)
Citation count (for papers)
Community upvotes (HackerNews, Reddit)
Consistency with other sources
```

### 4.3 Paper Analysis Agent

Searches academic databases and processes full paper content, not just abstracts.

**Connected sources:**

```text
arXiv
Semantic Scholar
PubMed (for relevant domains)
Google Scholar (via API)
ACM Digital Library
```

**Processing pipeline:**

```text
Search for relevant papers
    ↓
Download or access PDFs
    ↓
Extract: Abstract, Methodology, Results, Conclusion, Limitations
    ↓
Identify key claims with section citations
    ↓
Note methodology quality (sample size, evaluation rigor)
    ↓
Report to Navigator
```

### 4.4 Code & Implementation Analysis Agent

Searches GitHub and documentation for real-world implementations of the concepts being researched. This is particularly valuable for technical topics where theory and practice diverge.

```text
Search GitHub for repositories implementing the concept
    ↓
Analyze READMEs and documentation
    ↓
Look for issues discussing tradeoffs or failures
    ↓
Examine architecture documents if present
    ↓
Report patterns found across real implementations
```

**Example outputs:**

```text
"Found 43 GitHub repositories implementing event sourcing.
 12 are in financial/fintech domains.
 Common pattern: CQRS used alongside event sourcing in 38 of 43 cases.
 Common failure mode noted in issues: event schema migration."
```

### 4.5 Fact-Check Agent

Receives the collected claims from all research agents and cross-validates them against each other and against authoritative sources.

```text
Claim: "Event sourcing performs better than CRUD at scale"
    ↓
Check: Is this claim consistent across sources?
    ├── Paper A: Disagrees — performance depends on read/write ratio
    ├── Blog B: Agrees in write-heavy workloads
    ├── Practitioner C: Nuanced — event sourcing has higher write overhead
    └── GitHub issues: Mixed evidence

Result: CONTESTED — claim is context-dependent
    ↓
Flag for Synthesis Agent:
"This claim should be presented as contested with context,
 not as a settled fact."
```

### 4.6 Critic Agent

After the initial research pass, the Critic Agent reviews the collected findings and identifies what is missing, what is ambiguous, and what requires deeper investigation.

```text
Findings reviewed
    ↓
Identifies:
    ├── Sub-questions with insufficient coverage
    ├── Perspectives not yet represented
    ├── Conflicting claims that need resolution
    ├── Important concepts mentioned but not explained
    └── Recency gaps (all sources >3 years old on a fast-moving topic)
    ↓
Reports gaps to Navigator
    ↓
Navigator re-dispatches agents for gap coverage
```

### 4.7 Synthesis Agent

Combines all findings from all agents into a structured, coherent research document.

**Output document structure:**

```text
Title
Executive Summary (300 words, key conclusions)
    ↓
Section 1 — Background & Core Concepts
Section 2 — [Topic-specific section]
Section 3 — [Topic-specific section]
Section 4 — Practitioner Perspectives
Section 5 — Contested Claims & Open Questions
Section 6 — Recommendation Framework
    ↓
Limitations of This Research
Sources (numbered, with URL, date, credibility score)
Confidence Assessment
```

**Each claim in the document is tagged:**

```text
[ESTABLISHED] — Consistent across multiple high-credibility sources
[SUPPORTED] — Supported by majority of sources, some disagreement
[CONTESTED] — Significant disagreement exists; context-dependent
[SINGLE-SOURCE] — Found in only one source; treat with caution
[OPINION] — Practitioner opinion, not empirically validated
```

### 4.8 Living Document System

Research sessions are persisted and can be extended.

```text
User asks follow-up:
"Go deeper on the event schema migration problem"
    ↓
Navigator dispatches targeted research on that specific gap
    ↓
Synthesis Agent adds a new section to the existing document
    ↓
Document updated; previous sections unchanged
```

Users can also schedule research refreshes:

```text
"Update this research document every Monday morning
 with any new developments from the past week"
    ↓
Scheduled job re-runs targeted research
    ↓
Synthesis Agent generates a "New Developments" delta section
```

---

## 5. Key Technical Concepts Learned

```text
Multi-agent orchestration architecture
Agent-to-agent communication protocols
Parallel agent execution and job queue management
Dynamic task decomposition and assignment
Web scraping and full-text extraction at scale
Academic paper retrieval and parsing (arXiv, Semantic Scholar APIs)
RAG over dynamically collected heterogeneous documents
Claim extraction and citation linking
Cross-source conflict detection
LLM structured output (typed agent reports)
Streaming output (real-time report generation to the user)
Queue-based agent job distribution (BullMQ / Temporal)
Evaluation and quality scoring of agent outputs
Persistent research sessions and incremental document updates
Scheduled recurring research workflows
```

---

## 6. Why This Is Compelling

- **No one does this well yet.** Perplexity is fast and shallow. NotebookLM works only on uploaded documents. Google Deep Research is a closed, non-customizable product. A well-built, self-hosted, open version of this with a clean multi-agent architecture fills a genuine gap.
- **The orchestration architecture is the portfolio piece.** Building a production multi-agent system with real coordination, conflict resolution, parallel execution, and quality verification loops teaches skills that almost no other project type can provide. These are the frontier skills of applied AI engineering.
- **Broad and growing user base.** Researchers, analysts, consultants, developers, students, journalists, and legal professionals all need deep research assistance at a level that current tools cannot provide.
- **Naturally progressive in complexity.** Start with a single web-research agent producing a simple report. Progressively add parallel execution, agent specialization, fact-checking, the critic loop, and the living document system. Every phase is independently useful.
- **Bridges AI and information retrieval.** The combination of multi-agent orchestration, web scraping at scale, RAG over dynamic documents, and structured output generation covers a uniquely broad stack.

---

## 7. Progressive Build Path

```text
Phase 1 — Single-Agent Research MVP
  Single research agent (web search + scrape)
  Basic structured report generation
  Source citation
  Web UI for query submission and report display

Phase 2 — Parallel Agents + Specialization
  Navigator Agent with sub-question decomposition
  Parallel Web Research Agents
  Paper Analysis Agent (arXiv, Semantic Scholar)
  GitHub Analysis Agent
  Report merging and deduplication

Phase 3 — Quality & Validation
  Fact-Check Agent with conflict detection
  Claim confidence tagging
  Critic Agent with gap identification
  Navigator re-dispatch loop
  Quality score per research session

Phase 4 — Living Documents + Scheduling
  Persistent research sessions
  Follow-up question integration
  Incremental document updates
  Scheduled refresh workflows
  Research history and versioning
  Organization-level knowledge base
```
