# Proposal for the OASIS Open Ingestion Standard (OIS) Technical Committee 🌐

## 1. Charter of the Proposed Technical Committee

### (a) Proposed Name of the Technical Committee
**OASIS Open Ingestion Standard (OIS) Technical Committee**

***

### (b) Statement of Purpose
The purpose of the Open Ingestion Standard (OIS) Technical Committee is to define, govern, and stabilize a secure, decoupled, and vendor-neutral specification for enterprise data ingestion into downstream search engines, vector databases, and Large Language Model (LLM) Retrieval-Augmented Generation (RAG) architectures.

#### Background and Problem Statement
In modern enterprise AI architectures, the bottleneck has shifted from model intelligence to data logistics. Extracting structured and unstructured information from enterprise repositories (such as SharePoint, Amazon S3, relational databases, CMIS-compliant repositories, and BPMN 2.0 workflow engines) and routing it to vector databases remains a highly brittle, insecure, and vendor-locked endeavor. 

Three main issues persist:
1. **The security gap (ACL leaks):** Standard vector ingestion pipelines omit source document security permissions (Access Control Lists, active directory SIDs, or OAuth roles). Chunks of documents are embedded into vector databases without access restrictions, leading to leakage of restricted info.
2. **Vendor lock-in:** Ingestion jobs are configured using proprietary formats. There is no standard format to represent either document payloads or crawl configurations.
3. **Monolithic scaling bottlenecks:** Coupling document scanning, text extraction, embedding generation, and indexing in a single process degrades pipeline resilience under heavy workloads.

To address these issues and prove the viability of the standard in real-world environments, the **OpenCrawling** open-source project was published in July 2026 as the official reference implementation of the Open Ingestion Standard. OpenCrawling demonstrates a decoupled runtime leveraging Spring AI and the Model Context Protocol (MCP) to enforce Zero-Trust context retrieval and server-side ACL security filtering.

The OIS Technical Committee will standardize schemas and protocols that build on these concepts, ensuring that document security metadata is preserved from source to index, schemas are open and extensible, and pipelines can scale via decoupled architectures (e.g. using the Claim Check pattern).

***

### (c) Scope of Work
The Technical Committee will focus on the specification of schemas, protocols, and architectural guidelines that define the lifecycle of data ingestion for enterprise search and RAG platforms.

#### In-Scope Technical Work:
1. **Unified Document Payload Schema:** Standardizing the JSON Schema to represent extracted document text, extensible metadata envelopes, and security structures.
2. **Zero-Trust Security Preservation:** Preserving document permissions and mapping source identities (e.g. Active Directory Windows SIDs, OAuth groups, CMIS users/groups, BPMN assignees/candidates) directly to the document metadata envelope.
3. **Unified Job Configuration Schema:** A platform-agnostic configuration schema (JSON/YAML) declaring crawler connectors, scheduling execution, text extraction features (Tika, OCR), metadata transformations/narrativizations, chunking strategies, embedding provider endpoints, and output vector targets.
4. **Decoupled Architecture & Claim Check Protocol:** Specifying standard mechanisms for asynchronous message brokers (e.g. Apache Kafka) to exchange metadata envelopes while delegating large binary contents to temporary storage using the Claim Check pattern.
5. **CMIS and BPMN 2.0 Standard Mappings:** Formalizing extensions to map CMIS metadata (`cmis:*`) and BPMN 2.0 process variable/active task states (`bpmn:*`) to support real-time context indexing in enterprise search and RAG.

#### Out-of-Scope Work:
1. Creating or maintaining specific connector implementations or target database writers (which are left to external open source implementations, such as the [OpenCrawling Codebase](https://github.com/opencrawling/opencrawling) project).
2. Standardizing vector database internal algorithms or distance metrics.
3. Standardizing LLM model weights, training datasets, or prompt engineering languages.

***

### (d) Proposed Deliverables
The Technical Committee intends to produce the following deliverables:
1. **OIS Document Payload Specification (Version 1.0):** Standardizing JSON Schema, including mappings for active directory security permissions, CMIS metadata, and BPMN 2.0 variables/activities.
2. **OIS Job Configuration Specification (Version 1.0):** Standardizing YAML/JSON configuration schemas for crawler pipelines, chunking, and routing.
3. **OIS Architecture and Integration Guide (White Paper):** Formalizing recommendation practices for the Claim Check pattern, stateful delta crawls, and server-side ACL filter execution.

#### Proposed Schedule:
* **Month 1-3:** Charter approval and initial organization. Ingestion of the initial contribution from the OpenCrawling project.
* **Month 4-6:** RFC process for OIS Document Schema modifications and draft publication.
* **Month 7-9:** Public Review Drafts of the Document Payload and Job Configuration specifications.
* **Month 10-12:** Committee Specification approval and Submission for OASIS Standard status.

***

### (e) Intellectual Property Rights (IPR) Mode
The Technical Committee will operate under the **Non-Assertion Mode** as defined in the OASIS Intellectual Property Rights (IPR) Policy.

***

### (f) Anticipated Audience / Users
The deliverables are targeted towards:
* **Enterprise Software Architects & Security Officers** designing secure RAG/LLM applications.
* **Vector Database and Enterprise Search Providers** looking to support secure context filtering.
* **Connector Ingestion Platforms** (e.g., Apache ManifoldCF, LangChain, LlamaIndex) seeking a standard payload schema.
* **Enterprise Content Management (ECM) & Business Process Management (BPM) Vendors** wishing to index process states and repository content natively into vector databases.

***

### (g) Language
The Technical Committee will conduct its business and draft all deliverables in **English**.

---

## 2. Non-Charter Information

### (a) Identification of Proposers (Initial Sponsors)
The following eligible OASIS members propose the formation of the OIS Technical Committee:
1. **Piergiorgio Lucidi** (piergiorgio@apache.org), OpenCrawling Project Founder, Lead Architect, Member at The ASF and Apache ManifoldCF PMC Chair.
2. **Michael Cizmar**
(michael@michaelcizmar.com), OpenCrawling
Lead Architect
3. **Luis Cabaceira**
(luis.cabaceira@texter.ai), OpenCrawling
Lead Architect, Core Developer
4. *[Partner Organization Representative]* - Representing Document Management & CMIS Connector ecosystems.
5. *[Partner Organization Representative]* - Representing Vector Database & AI Ingestion ecosystems.

***

### (b) Proposed TC Convener
**Piergiorgio Lucidi** (piergiorgio@apache.org), OpenCrawling Initiative.

***

### (c) Proposed TC Chair(s)
**Piergiorgio Lucidi** (piergiorgio@apache.org), OpenCrawling Initiative.

***

### (d) Date and Time of First Meeting
The first meeting of the TC is proposed to be held on **Wednesday, September 16, 2026, at 16:00 UTC** (conducted virtually).

***

### (e) Meeting Schedule and Location / Platform
The TC will meet bi-weekly on Wednesdays at 16:00 UTC using a virtual conferencing platform (Zoom/Microsoft Teams). Technical discussions, drafts, and issue tracking will take place on GitHub under a dedicated OASIS Open repository.

***

### (f) Proposers' Statements of Support
Each proposer listed under 2(a) supports the creation of the OIS Technical Committee and intends to participate actively in its development.

***

### (g) Initial Contributions
The Technical Committee will begin its work using the following initial contributions donated by the OpenCrawling project:
1. **Open Ingestion Standard Manifesto** ([MANIFESTO.md](MANIFESTO.md)): Values and principles of zero-trust ingestion.
2. **OIS White Paper** ([ois-whitepaper.md](ois-whitepaper.md)): Detailed design guidelines and reference architectures.
3. **OIS Schemas** ([schemas/](schemas/)):
   * `document.schema.json` - Schema for secure document payloads with Active Directory SIDs, CMIS, and BPMN 2.0 properties.
   * `job.schema.json` - Schema for declarative crawler jobs.
4. **Validation Examples** ([examples/](examples/)): CMIS and BPMN 2.0 payload mapping samples.
5. **OpenCrawling Reference Implementation Codebase** ([OpenCrawling Codebase](https://github.com/opencrawling/opencrawling)): The open source reference implementation containing the runtime, connectors, and Secure MCP Server demonstrating compliant ingestion, embedding, and security-filtered context retrieval.

***

### (h) Drafting and Communication Tools
* **GitHub Repository:** For version control of schemas, specifications, issue tracking, and pull requests.
* **Mailing List:** OASIS-hosted TC mailing list for official notices and discussions.
* **Slack Workspace:** For informal community sync-ups and quick developer collaboration.
