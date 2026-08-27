# Libre Operational and Governance Instructions for Company Structure (LOGICS)

| Attribute               | Details                                                                             |
| :---------------------- | :---------------------------------------------------------------------------------- |
| **Governing Board:**    | [Libre Collective][librecollective]                                                 |
| **Title:**              | **LIBRE OPERATIONAL AND GOVERNANCE INSTRUCTIONS FOR COMPANY STRUCTURE**             |
| **Status:**             | `DRAFT`                                                                             |
| **Version:**            | `V1`                                                                                |
| **Last Updated:**       | `2026-08-26`                                                                        |
| **Classification:**     | [Libre Standard][librestandard]                                                     |
| **Libre Type:**         | `LIBRE-STANDARD`                                                                    |
| **Libre Identifier:**   | `LOGICS`                                                                            |
| **Specification File:** | [logics-v1.md][specification]                                                       |
| **Documentation:**      | [librestandard.github.io/documentation/logics][documentation]                       |
| **Authors:**            | [Contributors][contributors]                                                        |
| **License:**            | [Libre Single Source License V1 (LSSLV1)][lsslv1]                                   |
| **Feedback:**           | [Submit Feedback][feedback]                                                         |

---

## 1 Executive Summary

Libre Operational and Governance Instructions for Company Structure (**LOGICS**) is an open,
implementation-independent standard developed by the [Libre Collective][librecollective] to establish a predictable,
modular, and clear storage architecture for company files, records, and data environments.

By replacing messy, random, or proprietary folder setups with a **predictable, openly governed specification**,
LOGICS ensures consistency, easy navigation, and long-term organization across local hard drives, cloud storage,
servers, and automated systems.

---

## 2 Core Principles and Conceptual Model

LOGICS is governed by fundamental design principles:

```text
┌────────────────────────────────────────────────────────┐
│              STABLE STRUCTURAL NAMESPACE               │
│        (Levels 0-3: Fixed Names / No Renaming)         │
│                                                        │
│ [group]                                                │
│   └── company                                          │
│       └── module                                       │
│           └── category                                 │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│                DYNAMIC ENTRY NAMESPACE                 │
│       (Level 4: Business Workspaces and Files)         │
│                                                        │
│   └── entry (subcategory / state / date / workspace)   │
│       └── record (files, documents, data assets)       │
└────────────────────────────────────────────────────────┘
```

- **Predictable Layout:** Important company information has an obvious, fixed, and logical home.
- **Strict Lowercase Naming:** Every folder and file uses clean lowercase letters, numbers, and hyphens.
- **Stable Foundation:** Main structural categories are standardized so systems and people always know where to look.
- **Universal Compatibility:** Works smoothly on Windows, macOS, Linux, cloud storage, and automated toolchains.

---

## 3 Standard Architecture and Specification Details

A conforming LOGICS implementation structures its storage tree according to a clear five-level hierarchy:

```text
Level 0: <group>/     --> Optional parent company, brand group, or holding entity
Level 1: <company>/   --> The operating business, subsidiary, or legal entity
Level 2: <module>/    --> Primary business module (such as finance, customer, or product)
Level 3: <category>/  --> Standard business information category (such as invoice or contract)
Level 4: <entry>      --> Dynamic records, dates, states, workspaces, and files
```

| Level | Name | Purpose | Example |
| :--- | :--- | :--- | :--- |
| **Level 0** | `<group>` | Optional group or parent organization | `acme-group/` |
| **Level 1** | `<company>` | Operating company or business boundary | `acme-tech/` |
| **Level 2** | `<module>` | Core operational business module | `finance/` |
| **Level 3** | `<category>` | Standard business information category | `invoice/` |
| **Level 4** | `<entry>` | Specific dates, workspaces, and record files | `2026/2026-08-20-invoice-001.pdf` |

---

## 4 Technical Rules and Conformance Requirements

Implementations, tools, and systems governed by LOGICS must satisfy the following technical requirements:

| Conformance Area           | Compliant Standard          | Examples                       | Prohibited Anti-Patterns        |
| :------------------------- | :-------------------------- | :----------------------------- | :------------------------------ |
| **Character Set**          | Lowercase alphanumeric only | `invoice/`, `legal-agreements` | `Finance/`, `Legal Agreements/` |
| **Word Separators**        | Single hyphens only         | `tax-returns/`, `annual-plan`  | `tax_returns/`, `tax returns/`  |
| **Structural Renaming**    | Fixed Level 0 to 3 names    | `finance/tax/`                 | Renaming standard modules       |
| **Temporary Files**        | Standard prefixes only      | `temporary-draft.pdf`          | `temp/`, `tmp/`, `_drafts/`     |

---

## 5 Adoption and Implementation Roadmap

Adopting LOGICS follows a structured, step-by-step methodology:

```text
Phase 1: Assessment and Scope Definition
         └── Identify your companies, active operations, and standard modules needed.
         └── Review the official specification for module and category naming rules.

Phase 2: Baseline Implementation
         └── Create standard Level 1 company folders and Level 2 operational modules.
         └── Set up standardized Level 3 categories for business records.

Phase 3: Validation and Verification
         └── Move existing documents and records into the matching standard categories.
         └── Rename files to use lowercase letters, numbers, and hyphens.

Phase 4: Automated Governance and Toolchain Integration
         └── Apply automated file checkers, backup routines, and validation rules.
```

---

## 6 Ecosystem, Tooling, and Governance

- **Authoritative Specification:** For complete mandatory clauses, grammar, and architectural rules, consult
  **[logics-v1.md][specification]**.
- **Automated Validation and Enforcement:** Supported by official Libre Standard enforcement tools, linters, and
  automated validation suites.
- **AI Agent Interoperability:** Engineered for seamless interpretation by autonomous agents following standardized
  meta-governance rules.
- **Libre Collective:** Governed openly by the **[Libre Collective][librecollective]**.

[librecollective]: https://librecollective.github.io/
[librestandard]: https://librestandard.github.io/
[specification]: ./logics-v1.md
[documentation]: https://librestandard.github.io/documentation/logics/
[contributors]: https://github.com/librestandard/logics/graphs/contributors
[lsslv1]: https://librelicense.github.io/license/libre-single-source-license-v1.txt
[feedback]: https://github.com/orgs/librestandard/discussions/
