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

# Open Ingestion Standard (OIS) 🌐

An open specification, community manifesto, and schema standard for secure, decoupled, and vendor-neutral enterprise data ingestion pipelines.

---

## 📖 Overview

The **Open Ingestion Standard (OIS)** solves the challenge of moving data from enterprise source systems (such as SharePoint, S3 buckets, relational databases, CMIS repositories, cloud enterprise content platforms, BPMN 2.0 workflow engines, and streaming push protocols) to downstream **Vector Databases / RAG architectures**, **Cloud / Lakehouse Object Storage** (such as Apache Ozone and AWS S3), and **Open Lakehouse Table Formats** (such as Apache Iceberg).

OIS defines:
1. **[MANIFESTO.md](MANIFESTO.md)**: The architectural pillars of zero-trust fail-closed security mapping, in-flight pre-embedding governance, asynchronous claim checks & persistent `.ois.json` sidecar envelopes, open lakehouse tables, and vendor-neutrality.
2. **Unified Document Payload & Sidecar Schema (`schemas/document.schema.json`)**: A standard JSON schema to package extracted text, `SHA-256` binary checksums, rich metadata (`cmis:*`, `bpmn:*`, `ois:provenance`, `ois:governance`), and Fail-Closed Security structures (ACLs + ReBAC relationship tuples) — usable as an in-flight streaming message, as a persistent `<key>.ois.json` sidecar file in object storage, and as structured records in open lakehouse tables (Apache Iceberg).
3. **Unified Job Configuration Schema (`schemas/job.schema.json`)**: A platform-agnostic configuration schema (YAML/JSON) to declare scheduled or agent-triggered (`AGENTIC` / `ON_DEMAND`) crawlers, pre-embedding PII governance gates, and vector, lakehouse table, or object-storage target writers.
4. **[ois-whitepaper.md](ois-whitepaper.md)**: Comprehensive architectural white paper detailing the enterprise ingestion and migration crisis, core pillars, schemas, and reference designs.

---

## 📂 Repository Structure

* **`MANIFESTO.md`**: Core values and engineering principles.
* **`ois-whitepaper.md`**: Comprehensive architectural white paper for OIS.
* **`OASIS-PROPOSAL.md` / `OASIS-CHARTER.txt`**: Formal Technical Committee charter proposal for OASIS Open.
* **`schemas/`**: Formal JSON Schema definitions.
  * **`document.schema.json`**: Schema validation rules for streaming document payloads and persistent `<key>.ois.json` sidecar envelopes.
  * **`job.schema.json`**: Schema validation rules for scheduled, event-driven, and agent-triggered ingestion/migration job configurations.
* **`examples/`**: Payload examples.
  * **`sample-document.json`**: Complete OIS document payload showing nested ACL SIDs.
  * **`sample-document-cmis.json`**: OIS document payload with `cmis:*` repository properties and ACLs.
  * **`sample-document-bpmn2.json`**: OIS document payload with `bpmn:*` process instance state and active task permissions.
  * **`sample-document-sidecar-migration.json`**: Persistent `<key>.ois.json` cloud migration sidecar with `sha256` checksum, `ois:provenance` (`RFC 8693` delegated agent identity), `ois:governance` PII redaction record, and ReBAC `relationships`.
  * **`sample-document-delete.json`**: OIS document tombstone payload (`action: "DELETE"`).
  * **`sample-job.json` / `sample-job.yaml`**: Complete OIS scheduled job configuration file.
  * **`sample-job-agentic-migration.json`**: Agent-triggered (`AGENTIC`) CMIS-to-Ozone migration job with four-eyes approval, pre-embedding PII redaction, and `.ois.json` sidecar output.

---

## 🚀 Getting Started

### Validating Payload Files
You can validate your document payloads and job configurations against the OIS schemas using any JSON Schema validator (such as `ajv` for Node.js, `jsonschema` for Python, or `everit-org/json-schema` for Java).

#### Using Node.js (AJV CLI):
```bash
# Install AJV validator globally
npm install -g ajv-cli

# Validate a document payload against the OIS schema
ajv validate -s schemas/document.schema.json -d examples/sample-document.json

# Validate a job configuration (YAML) against the OIS schema
ajv validate -s schemas/job.schema.json -d examples/sample-job.yaml

# Validate a job configuration (JSON) against the OIS schema
ajv validate -s schemas/job.schema.json -d examples/sample-job.json
```

---

## 🤝 How to Contribute

We welcome standard designers, platform developers, and enterprise search vendors to participate.
1. Review the [MANIFESTO.md](MANIFESTO.md).
2. Read the specifications in the `spec/` folder.
3. Open a **Request for Comments (RFC)** issue or submit a Pull Request to refine schemas.

---

## 📬 Contact & Support

Join our [Slack Community](https://join.slack.com/t/opencrawling/shared_invite/zt-43r2anb6q-YLoBsOrxCCcBWU5Up3P1rw) to discuss standard specifications, request schema enhancements, or talk with the maintainers.

For general inquiries, community feedback, or partner inquiries, please email us at [info@opencrawling.org](mailto:info@opencrawling.org).

