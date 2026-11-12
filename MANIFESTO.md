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

### Conformance & Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

---

## 🏛️ The Core Principles

All compliant implementations of the **Open Ingestion Standard (OIS)** MUST adhere to the following four principles:

### 1. Zero-Trust Ingestion & Migration (Security First)
* **Identity & Relationship Preservation**: Document security permissions—including Access Control Lists (ACLs), User SIDs, Group Identifiers, and Relationship-Based Access Control (ReBAC) tuples—MUST be extracted alongside content and treated as first-class metadata.
* **Normative Fail-Closed Enforcement**: Downstream search engines, object storage gateways, and AI orchestrators MUST enforce `FAIL_CLOSED` security semantics. A payload with an absent or empty permissions array MUST default to **Deny-All** (never public), explicit `deny` rules MUST override `read`/`write`, and effective access MUST evaluate as the intersection ($\cap$) of repository, folder, and document permissions.
* **In-Flight Pre-Embedding Governance**: Sensitive entities (such as PII) SHOULD be evaluated and redacted in flight (`ALLOW`, `REDACT`, `DROP`) *before* irreversible vectorization or target persistence occurs.
* **Delegated Multi-Agent Identity**: When autonomous AI agents trigger discovery, ingestion, or migration jobs on behalf of a human user, the pipeline MUST preserve delegated provenance (`on_behalf_of` / OAuth 2.0 RFC 8693 `act.sub`) and strictly bound access to the human principal's source permissions.

### 2. Vendor-Neutral Interoperability (Data Portability, Cloud Migration & Lakehouse Tables)
* **Standard Exchange, Sidecar & Lakehouse Formats**: Document streams and metadata extracted from diverse source repositories (SharePoint, Amazon S3, databases, file shares, CMIS repositories, cloud enterprise content platforms, and BPMN 2.0 workflow engines) MUST be formatted using a uniform, vendor-neutral structure—usable as an in-flight event payload, as a persistent `<key>.ois.json` sidecar file stored alongside raw binaries in cloud/lakehouse object storage, or as structured records in open columnar lakehouse tables (e.g., Apache Iceberg / Parquet) with preserved Zero-Trust ACL columns.
* **Declarative Pipeline Configuration**: Scheduled, event-driven, and agent-triggered (`AGENTIC` / `ON_DEMAND`) jobs, governance gates, transformation templates, and target writers MUST be represented using platform-agnostic, version-controlled formats (JSON/YAML).

### 3. Event-Driven Decoupling (Decoupled Scalability)
* **Decoupled Architecture**: Pipelines MUST be partitioned into independent, horizontally scalable workers (Scanners, Parsers, Governance Gates, Embedders, and Vector/Object/Lakehouse Writers) connected via asynchronous message queues.
* **Claim Check, Persistent Sidecar & Lakehouse Table Pattern**: Bulky binary payloads MUST be separated from the primary message broker. Queue messages MUST carry lightweight reference claims (`claimCheckUri`) and cryptographic checksums (`sha256`), while cloud/lakehouse migrations persist companion `<key>.ois.json` sidecars (`sidecarUri`) or write open lakehouse tables so AI agents and analytics engines can inspect metadata, query Parquet data, and enforce ACLs without re-crawling legacy sources.

### 4. Incremental & Real-Time Efficiency (Resource Protection)
* **Incremental Scans & Real-Time Lifecycle Events**: Ingestion systems MUST use stateful, cursor-based delta scans or real-time workflow transition events (`bpmn:transitionEvent`) to publish updates (`UPSERT`) and immediate security revocations (`DELETE` tombstones).
* **Rate-Limiting & Backpressure**: Pipeline components MUST dynamically adapt ingestion rates to prevent service degradation in source repositories or destination targets.

---

## 🤝 Signatures & Adherence

By adopting this manifesto, vendors, platform architects, and developers pledge to design tools, connectors, and output adapters that conform to the OIS schemas, fostering a collaborative, lock-in-free future for enterprise data routing.
