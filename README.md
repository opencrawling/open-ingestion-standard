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

The **Open Ingestion Standard (OIS)** solves the challenge of moving data from enterprise source systems (such as SharePoint, S3 buckets, relational databases, CMIS repositories, and BPMN 2.0 workflow engines) to downstream vector stores, LLMs, and RAG architectures.

OIS defines:
1. **[MANIFESTO.md](MANIFESTO.md)**: The architectural pillars of zero-trust security mapping, asynchronous claiming, and vendor-neutrality.
2. **Unified Document Payload Schema**: A standard JSON schema to package extracted text, rich metadata, and source Access Control Lists (ACLs) containing Security SIDs.
3. **Unified Job Configuration Schema**: A platform-agnostic configuration schema (YAML/JSON) to declare crawlers, schedule execution rates, and map search endpoints.
4. **[ois-whitepaper.md](ois-whitepaper.md)**: Comprehensive architectural white paper detailing the enterprise ingestion crisis, pillars, schemas, and reference designs.

---

## 📂 Repository Structure

* **`MANIFESTO.md`**: Core values and engineering principles.
* **`ois-whitepaper.md`**: Comprehensive architectural white paper for OIS.
* **`schemas/`**: Formal JSON Schema definitions.
  * **`document.schema.json`**: Schema validation rules for data exchange payloads.
  * **`job.schema.json`**: Schema validation rules for job configurations.
* **`examples/`**: Payload examples.
  * **`sample-document.json`**: Complete OIS document payload showing nested ACL SIDs.
  * **`sample-job.json`**: Complete OIS job configuration file (JSON format).
  * **`sample-job.yaml`**: Complete OIS job configuration file (YAML format).
* **`spec/`**: In-depth markdown documentation covering claim check, ACL translation, and error schemas.

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

For general inquiries, community feedback, or partner inquiries, please email us at [info@opencrawling.org](mailto:info@opencrawling.org).

