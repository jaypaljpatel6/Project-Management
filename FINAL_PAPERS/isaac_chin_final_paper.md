# Designing a LLM-Based MVP Information System

**Isaac Chin, Fall 2025**

## Abstract

This paper outlines the design and implementation strategy for a Minimum Viable Product (MVP) information system driven by Large Language Models (LLMs). The project addresses the critical issue of "information silos" within modern enterprises, a phenomenon where valuable organizational knowledge is fragmented across disparate repositories such as policy documents, technical wikis, and onboarding materials. Drawing on professional internship experiences, this research argues that traditional keyword-based search methods impose a high cognitive burden on users, often failing to retrieve relevant data due to terminology mismatches. The proposed solution is a Retrieval-Augmented Generation (RAG) system that acts as an intelligent "router" rather than a mere content generator. By utilizing a "Lean CSV-based" prototyping approach via KrAIG (Knowledge Retrieval augmented Information Generation), the project aims to validate the utility of LLMs in reducing search friction before committing to a full-scale infrastructure build. This paper details the system architecture, a six-month Agile implementation roadmap, and an evaluation framework based on user trust and perceived usefulness. Ultimately, the project demonstrates how human-centered AI design can bridge departmental gaps, ensuring transparency and accountability in knowledge retrieval.

## Introduction

### Background

In large organizations, knowledge is the primary currency of productivity. However, this capital is often locked away in fragmented storage systems, creating a persistent challenge known as "information silos". Organizational knowledge is not stored in a single, accessible library; rather, it is dispersed across a multitude of formats and locations, including official policy documents, technical documentation, internal wikis, and transient onboarding materials.

The creation of these silos is rarely intentional but is instead the result of systemic organizational friction. As illustrated in the provided research, silos are driven by a combination of intricate organizational structures, a lack of inter-departmental communication, and the persistence of legacy systems that do not communicate with one another.

![infosilo](isaac_chin_images/infosilo.png)

As shown in the figure above, cultural barriers also play a significant role. Different departments often operate with varying priorities and distinct vocabularies, meaning that a search term used by an engineer might yield no results in a database managed by Human Resources, even if the relevant document exists.

Legacy technologies exacerbate this disconnect by relying on keyword-based search mechanisms. These traditional tools assume that the user already possesses a high degree of domain knowledge: they must know the correct document name or the precise terminology used by the author. When these conditions are not met, the search fails, or worse, returns a flood of "noisy" results that leads to information overload. Over time, these limitations solidify the silos, ensuring that valuable knowledge remains difficult to access or apply.

### Motivation and Problem Statement

The motivation for this project stems from direct professional experience. During my internship, it became evident that critical organizational knowledge was fragmented across multiple internal systems. Users, ranging from new interns to seasoned employees, often struggled to identify where relevant information was stored or even which system to search.

The core problem is not that the information is missing, but that it is hard to access. Traditional search tools place a high cognitive burden on the user, requiring them to act as human filters for irrelevant search results. This friction leads to low perceived usefulness of internal tools, a concept grounded in the Technology Acceptance Model (Davis, 1989), which posits that if a system is difficult to use, it will not be adopted regardless of its potential utility.

### Project Vision and Key Question

The goal of this project is to design an information system that reduces cognitive load and improves access to relevant internal knowledge. The central research question guiding this design is: How can an information system help users find the right information across siloed data sources?.

To answer this, I propose a hypothetical LLM-mediated retrieval system. The system is designed not as a "knowledge source" that might hallucinate facts, but as an information router. The key innovation is that decision-making happens before retrieval: the LLM reviews document metadata, selects the most relevant files, and then generates a response grounded strictly in those documents. This approach aims to transform the user experience from a manual "hunt-and-peck" process into a conversational, decision-supported workflow.

## Technology Involved in System Development

The system architecture is designed to prioritize transparency and interpretability over "black box" complexity. It avoids fully opaque ranking algorithms and untraceable embeddings, ensuring that users can always verify the source of the information provided. The development strategy compares two distinct technological pathways: a Full RAG Pipeline and a Lean MVP Prototype.

### The Full RAG Pipeline (Long-Term Vision)

The comprehensive solution for this problem is a "Full RAG (Retrieval-Augmented Generation) pipeline". This architecture involves significant infrastructure investment and a build time of 3 to 5 months.

![rag](isaac_chin_images/rag.png)

As detailed in the architecture diagram, the full pipeline follows a complex data journey:

- **Data Sourcing:** Ingesting raw data from across the organization.
- **Clean & Preprocess:** Stripping formatting and normalizing text.
- **Embed & Vector Store:** Converting text into high-dimensional vector embeddings to enable semantic search.
- **RAG App + Index Layer:** A sophisticated application layer that manages retrieval logic.
- **LLM + Post-Process:** The final generation step where the model synthesizes an answer.

This approach leverages semantic search, allowing the system to understand the meaning of a query (e.g., "how do I take time off?") even if the documents only use the term "PTO" or "Leave of Absence."

### The Lean CSV-Based Prototype (MVP Strategy)

To validate the hypothesis quickly, within a 2-week turnaround, this project utilizes a "Lean CSV-based" prototype. This Minimum Viable Product (MVP) simplifies the stack to test the user experience without the heavy backend engineering.

- **Clean & Summarize Documents:** Instead of full embedding, documents are summarized to their core metadata and content.
- **CSV As Lightweight Vector Store:** A simple structured CSV file acts as the index, reducing the need for expensive vector databases like Pinecone or Milvus.
- **KrAIG Retrieval:** A prompt-engineered retrieval mechanism (KrAIG) fetches relevant rows from the CSV based on the user's natural language query.

This "Lean" approach allows the project to act as a decision-support tool and retrieval router immediately. It validates the core "router" concept, using AI to select the right document, before the organization commits to the costly infrastructure of the full pipeline.

### User Interface Design

The user interface (UI) is the bridge between the complex retrieval logic and the employee. The design prioritizes natural language input, allowing users to ask questions as if they were speaking to a human assistant.

![ui](isaac_chin_images/ui.png)

As shown in the prototype above, the interface includes:

- **Natural Language Input:** A chat bar prompting, "Ask me anything about 84.51 policies, benefits, or procedures...".
- **Source Selection:** To enhance trust, users can explicitly select data sources such as "Benefits & HR" or "Documentation & Wikis". This feature gives users control and visibility into where the AI is looking, addressing the issue of "opaque" algorithms.
- **Disclaimer:** A clear warning that "GenAI Studio is powered by AI and may occasionally provide incorrect information," reinforcing the need for human verification.

## Implementation Roadmap

The implementation of this system follows an Agile, sprint-based methodology spanning six months. The goal is to build and deploy an internal AI tool while actively managing technical debt.

![roadmap](isaac_chin_images/roadmap.png)

### Phase 1: Planning & Design (Month 1)

The first month is dedicated to "Conceptual Design". The primary objective is to define the product vision and success metrics. During this phase, the team conducts research into user needs to identify exactly which data sources (e.g., HR benefits vs. technical wikis) are causing the most friction. We also select the modular architecture and tools, identifying initial technical debt risks such as the scalability limits of the CSV approach.

### Phase 2: MVP Development (Months 2-4)

This phase focuses on the "MVP Development" and is broken into specific sprints.

- **Sprint 1-2 (MVP Build):** The team builds the data ingestion pipelines and integrates the model. "Glue code" is written to connect APIs, and the team explicitly documents known limitations (e.g., inability to read scanned PDFs) to manage expectations.
- **Sprint 3-6 (Iteration & Testing):** Once the basic prototype is live, the focus shifts to gathering feedback from internal users. Based on this feedback, inefficient components are refactored. A crucial step here is separating experimental features from the core system to ensure that the primary retrieval function remains stable while new features are tested.

### Phase 3: Scaling and Optimization (Month 5)

In the fifth month, the project moves toward "Scaling and Optimization". To prepare for a wider release, the team adds CI/CD (Continuous Integration/Continuous Deployment) pipelines and monitoring dashboards. Load testing and security testing are conducted to ensure the system is robust enough for enterprise use. Additionally, the team prepares cost and scalability reviews to determine if the transition from the CSV prototype to the Full RAG pipeline is financially viable.

### Phase 4: Review & Deployment (Month 6)

The final month is for "Review & Deployment". A pilot is launched with a limited user group to track metrics and performance data in a real-world setting. The project concludes with a retrospective meeting to document technical debt and create a mitigation plan for future development.

## Evaluation and Methodology

The success of an LLM-based information system cannot be measured by accuracy alone. Because the system is designed to be a "router" rather than a "creator," the evaluation framework focuses on system effectiveness and user interaction.

### Key Evaluation Criteria

- **Relevance of Retrieved Information:** The primary metric is whether the system retrieves the correct document for a given query. For example, if a user asks about "maternity leave," does the system retrieve the "Parental Leave Policy" document?
- **User Trust:** Trust is the cornerstone of adoption. We measure "user trust in responses" to gauge if employees feel comfortable relying on the system. If trust is low, users will revert to manual searching.
- **Clarity of System Behavior:** The system must be transparent. Users need to understand why a document was returned. We evaluate if the "source selection" features improve the clarity of the system's behavior.
- **Reduction in Search Time:** The ultimate business value is efficiency. We measure the reduction in search time compared to the legacy keyword-based systems.

### Evaluation Methods

To gather this data, the project employs a mixed-methods approach:

- **User Surveys:** Adapted from Davis (1989), these surveys measure "Perceived Usefulness" and "Perceived Ease of Use".
- **Task Completion Analysis:** We observe users performing standard information retrieval tasks (e.g., "Find the 2025 holiday schedule") and time their performance.
- **Qualitative Feedback:** Open-ended feedback is collected to understand the nuances of the user experience and identify "delight" or frustration points.

## Theoretical Framework and Governance

### Community Governance and Ethics

While this system is currently an internal tool, its design is informed by principles of community governance and ethical AI. The system acts as a "mediator", which implies a responsibility to present information neutrally and accurately.

The "Stochastic Parrots" paper (Bender et al., 2021) warns of the dangers of large language models simply repeating training data without understanding truth. To mitigate this, our system is explicitly designed not to be a knowledge source. It uses the RAG architecture to ground every response in a retrieved document, ensuring that the AI is only summarizing existing, validated corporate data, not inventing it. This adherence to "grounded generation" is a key governance principle for the project.

Furthermore, the design emphasizes Human-in-the-Loop accountability. The disclaimer on the UI, "Always verify important details with official sources or HR", reminds users that the AI is a tool, not the final authority. This project demonstrates how AI can enhance access without replacing human judgment or accountability.

### Contributors and Future Pathways

Currently, the project is scoped as an MVP designed by Isaac Chin. However, the roadmap includes phases for "Gathering feedback from internal users" and "Reviewer Discussion," implying a collaborative future.

Future pathways for this project include moving from the "Lean CSV" prototype to the "Full RAG pipeline" with semantic search and embeddings. This evolution would allow the system to handle millions of documents and more complex queries. Additionally, the system could expand to include "Social features," such as showing users which documents are most frequently accessed by their team, thereby breaking down silos through shared behavioral data.

Another extension involves integrating "decision-support" features. Rather than just finding a policy, the system could help a user understand the implications of that policy, for example, calculating the exact number of vacation days remaining based on the retrieved policy and the user's start date.

## Conclusion

The "Designing a LLM-Based MVP Information System" project represents a critical step toward solving the pervasive problem of information silos in modern organizations. By acknowledging that traditional search tools are failing to meet the needs of a dynamic workforce, this project proposes a solution that is both technically innovative and deeply human-centered.

The shift from "keyword search" to "LLM-mediated routing" addresses the root causes of the silo problem: the disconnect between how information is stored (technical jargon, disparate systems) and how users ask for it (natural language, varying terminology). The "Lean CSV" prototype offers a pragmatic, low-risk method to validate this value proposition without overcommitting resources.

Ultimately, this project prioritizes design over implementation. It focuses on the user experience, transparency, trust, and ease of use, rather than just algorithmic power. It demonstrates that AI, when properly constrained and architected, can be a powerful force for organizational clarity. By transforming the "invisible" knowledge hidden in silos into accessible, actionable insights, the system empowers employees to focus on their work rather than the search for information.

## References

Bender, E. M., Gebru, T., McMillan-Major, A., & Shmitchell, S. (2021). On the Dangers of Stochastic Parrots: Can Language Models Be Too Big? *FAccT '21 Proceedings*.

Davis, F. D. (1989). Perceived usefulness, perceived ease of use, and user acceptance of information technology. *MIS Quarterly*, 13(3), 319–340.

Laudon, K. C., & Laudon, J. P. (2020). *Management Information Systems: Managing the Digital Firm*. Pearson.

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., ... & Kiela, D. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. *NeurIPS*.

Savolainen, R. (2007). Information behavior and information practice: Reviewing the "umbrella concepts" of information-seeking studies. *The Library Quarterly*, 77(2), 109–132.
