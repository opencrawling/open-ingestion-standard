<!--
Copyright © 2026 the original author or authors (piergiorgio@apache.org)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

# The Open Ingestion Standard (OIS) Manifesto 📜


Data ingestion and secure routing are the backbone of modern search, analytics, and Artificial Intelligence (RAG) architectures. Yet, in most enterprise environments, data pipelines remain brittle, insecure, and heavily locked into proprietary vendor formats.

This Manifesto defines the core values and architectural principles required to build an open, secure, and vendor-neutral ecosystem for enterprise data ingestion.

---

## 🏛️ The Core Principles

All compliant implementations of the **Open Ingestion Standard (OIS)** must adhere to the following four principles:

### 1. Zero-Trust Ingestion (Security First)
* **Identity Preservation**: Document security permissions (Access Control Lists, User SIDs, and Group Identifiers) must be extracted alongside content and treated as first-class metadata.
* **Synchronized Access Enforcement**: Vector search engines and AI orchestrators must ingest security metadata dynamically, ensuring that user queries return only the information they are explicitly authorized to read at the source.

### 2. Vendor-Neutral Interoperability (Data Portability)
* **Standard Exchange Formats**: Document streams and metadata extracted from diverse source repositories (SharePoint, Amazon S3, databases, file shares, CMIS repositories, and BPMN 2.0 workflow engines) must be formatted using a uniform, vendor-neutral structure.
* **Declarative Pipeline Configuration**: Ingestion configurations, crawling schedules, connector profiles, and mapping tables must be represented using platform-agnostic, version-controlled formats (JSON/YAML).

### 3. Event-Driven Decoupling (Decoupled Scalability)
* **Decoupled Architecture**: Pipelines must be partitioned into independent, horizontally scalable workers (Scanners, Parsers, Embedders, and Writers) connected via asynchronous message queues.
* **Claim Check Pattern**: Bulky binary payloads must be separated from the primary message broker. Queue messages must carry lightweight reference claims, pulling binary files from shared storage only when needed for parsing.

### 4. Incremental Efficiency (Resource Protection)
* **Incremental Scans**: Ingestion systems must use stateful, cursor-based scans to discover changes, avoiding full-crawl resource spikes on source repositories.
* **Rate-Limiting & Backpressure**: Pipeline components must dynamically adapt ingestion rates to prevent service degradation in source repositories or destination vector databases.

---

## 🤝 Signatures & Adherence

By adopting this manifesto, vendors, platform architects, and developers pledge to design tools, connectors, and output adapters that conform to the OIS schemas, fostering a collaborative, lock-in-free future for enterprise data routing.
