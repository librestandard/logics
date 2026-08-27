# Libre Operational and Governance Instructions for Company Structure (LOGICS) - V1 Draft Specification

| Attribute               | Details                                                                 |
| :---------------------- | :---------------------------------------------------------------------- |
| **Governing Board:**    | [Libre Collective][librecollective]                                     |
| **Title:**              | **Libre Operational and Governance Instructions for Company Structure** |
| **Status:**             | `DRAFT`                                                                 |
| **Version:**            | `V1`                                                                    |
| **Last Updated:**       | `2026-08-26`                                                            |
| **Classification:**     | [Libre Standard][librestandard]                                         |
| **Libre Type:**         | `LIBRE-STANDARD`                                                        |
| **Libre Identifier:**   | `LOGICS`                                                                |
| **Specification File:** | [logics-v1.md][specification]                                           |
| **Documentation:**      | [librestandard.github.io/documentation/logics][documentation]           |
| **Authors:**            | [Contributors][contributors]                                            |
| **License:**            | [Libre Single Source License V1 (LSSLV1)][lsslv1]                       |
| **Feedback:**           | [Submit Feedback][feedback]                                             |

> [!NOTE]
> **Specification Notice:** These are the official instructions and guide for
> **Libre Operational and Governance Instructions for Company Structure (LOGICS)**, managed by the
> [Libre Collective][librecollective].
> If you are building a tool or system that claims to use this standard, it must follow all the required rules
> outlined in this document.

---

## 1 Abstract and System Architecture

### 1.1 Overview and Purpose

The **Libre Operational and Governance Instructions for Company Structure (LOGICS)** establishes a predictable,
modular, and implementation-neutral directory and storage architecture that functions consistently across common
operating systems, local filesystems, cloud object stores, and collaborative storage systems.

_The goal is simple:_

> _Important company information should have a **clear, predictable**, and **logical place.**_

**LOGICS** is designed for:

- Small Businesses.
- Startups.
- Growing Companies.
- Large Organizations.
- Agencies.
- Manufacturers.
- Retailers.
- Software Companies.
- Service Companies.
- Media Businesses.
- Organizations That Manage Multiple Companies.

_Terminology Distinction (Organization vs. Company):_

- **Organization:** The general enterprise, institution, agency, firm, or adopter implementing LOGICS.
- **Company (`<company>`):** The standardized Level 1 structural name representing an organization's primary operating
  boundary or independent storage tree, even when the adopting entity is a sole proprietorship, partnership,
  non-profit, public agency, or unincorporated practice.

### 1.2 The Five-Level Architectural Model

Every LOGICS-compliant storage tree is structured according to a predictable, five-level architectural model:

```text
Level 0: <group>/           --> Optional parent holding, conglomerate, brand group, or multi-entity owner
Level 1: <company>/         --> The operating company, legal entity, subsidiary, or independent business unit
Level 2: <module>/          --> Primary operational business module (from the 16 standard LOGICS modules)
Level 3: <category>/        --> Standard business-information category
Level 4: <entry>              --> Dynamic content organization (Subcategory, State, Date, Workspace, Record)
```

**Path breakdown examples:**

- Single Document: `acme-tech/finance/invoice/2026/2026-08-20-invoice-001.pdf`
  - Mapping:
    `<company>` (`acme-tech/`) $\rightarrow$ `<module>` (`finance/`) $\rightarrow$
    `<category>` (`invoice/`) $\rightarrow$ `<date>` (`2026/`) $\rightarrow$
    `<record>` (`2026-08-20-invoice-001.pdf`)
- Nested Workspace: `acme-group/acme-media/customer/account/active/acme-tech/profile.pdf`
  - Mapping:
    `<group>` (`acme-group/`) $\rightarrow$ `<company>` (`acme-media/`) $\rightarrow$
    `<module>` (`customer/`) $\rightarrow$ `<category>` (`account/`) $\rightarrow$
    `<state>` (`active/`) $\rightarrow$ `<workspace>` (`acme-tech/`) $\rightarrow$
    `<record>` (`profile.pdf`)

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
│              (Level 4: Dynamic Structure)              │
│                                                        │
│ [subcategory]                                          │
│   └── [state]                                          │
│       └── [date]                                       │
│           └── [workspace]                              │
│               └── record                               │
└────────────────────────────────────────────────────────┘
```

#### 1.2.1 Stable Structural Namespace (Levels 0-3: Fixed Names / No Renaming)

Levels 0 through 3 form the permanent structural namespace. These structural identifiers are established by the
standard with fixed names and identities, regardless of whether a given directory is physically provisioned on disk yet.
An organization is NOT required to physically create every possible module or category directory from day one; rather,
when a structural directory is provisioned, its name is fixed and MUST NOT be renamed, moved, or deleted, guaranteeing
permanent reference stability:

- **Level 0: Group (`<group>/` - Optional):**
  Represents an optional parent container for multi-company holding groups, conglomerates, multi-brand owners, retail
  store networks, or multi-branch enterprises (for example: `acme-group/`, `acme-holdings/`, `acme-parent/`). Level 0
  exists strictly to contain one or more Level 1 Company directories. A Level 0 Group MUST NOT directly contain modules,
  categories, Level 4 entries, or records. Standalone companies omit Level 0 entirely, with Level 1 serving as the root.
- **Level 1: Company (`<company>/` - Required):**
  Represents the organizational boundary for which an independent LOGICS storage tree is maintained. A company normally
  represents an independent legal entity, but may also represent a separately managed subsidiary, operating division,
  branch office, retail store, or autonomous business unit (for example: `acme-tech/`, `acme-media/`, `acme-video/`, or
  `store-downtown/`).
- **Level 2: Module (`<module>/` - Required):**
  Represents the primary operational business function (for example: `finance/`, `legal/`, `people/`, `project/`,
  `sale/`, `service/`, `technology/`). LOGICS standardizes sixteen official Level 2 modules that organizations
  provision on demand. Every Level 2 module identifier is strictly a single, unhyphenated English singular noun or
  established collective noun (such as `people/`).
- **Level 3: Category (`<category>/` - Required):**
  Represents the standardized business-information classification (for example: `invoice/`, `agreement/`, `account/`,
  `policy/`, `repository/`, `patent/`). Every Level 3 category identifier is strictly a single, unhyphenated, singular
  English noun that identifies the concrete class of business information, unless an explicit justified exception is
  formally defined in the standard. Hyphenated compound names are permitted only at Level 0 (group), Level 1 (company),
  and Level 4 (subcategories, workspaces, and records). A category name must never duplicate its parent module name.

Structural identifiers at Levels 0 through 3 maintain permanent reference stability; deprecation, reservation, and
lifecycle rules governing structural identifiers are specified in Section 7.3.

#### 1.2.2 Dynamic Entry Namespace (Level 4: Dynamic Structure)

Level 4 houses the dynamic operational contents of a category. Content organization beneath a category unfolds
dynamically according to the strict **Entry Precedence Cascade** defined in Section 4.3.

### 1.3 Terminology and Conformance Conventions

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**,
**RECOMMENDED**, **MAY**, and **OPTIONAL** in this document are to be interpreted as described in standard
conformance terminology:

- **MUST / REQUIRED / SHALL:** Absolute mandatory requirement for standard conformance.
- **MUST NOT / SHALL NOT:** Absolute prohibition; violating implementations are non-conforming.
- **SHOULD / RECOMMENDED:** Valid reasons may exist in particular circumstances to ignore a particular item, but the
  full implications must be understood and carefully weighed before choosing a different course.
- **MAY / OPTIONAL:** Truly optional feature or behavior; implementations must interoperate whether or not it is used.

---

## 2 Fundamental Design Principles

### 2.1 Single Canonical Home and Structural Reference Stability

A single physical file or business record MUST have exactly one canonical home. It must never be copied, cloned, or
duplicated across modules or directories to represent relationships.

- **Canonical Reference Concept:** Cross-module and cross-category relationships are established exclusively via
  **canonical references** that point to the authoritative record's canonical path. Depending on the underlying storage
  architecture and infrastructure platform, canonical references may be implemented using:
  - **Standard Relative or Absolute Filesystem Paths:** (for example: `../../sale/order/order-2026-001.pdf` or
    `/acme-corp/sale/order/order-2026-001.pdf`).
  - **Object Storage Keys and Prefixes:** (for example: `s3://bucket/acme-corp/sale/order/order-2026-001.pdf`).
  - **Uniform Resource Identifiers (URIs) and Deep Links:** Web, database, or API references targeting the canonical
    path.
  - **Filesystem Symbolic Links, Aliases, or Platform-Native Shortcuts:** Native operating system pointers referencing
    the canonical source file.
- **Structural Namespace Stability (Levels 0 through 3):** Because Levels 0, 1, 2, and 3 have permanently fixed
  structural names that cannot be renamed, aliased, or moved, high-level canonical references maintain permanent
  structural stability across the enterprise storage tree.
- **Dynamic Level 4 Paths and Reference Updates:** In contrast to the fixed structural namespace, dynamic Level 4
  record and workspace paths MAY change over time (such as moving between state partitions during lifecycle transitions
  per Section 4.3, promoting a leaf record to a workspace per Section 3.5, or transferring records to `archive/` per
  Section 2.3). Whenever an entity's Level 4 path changes, any canonical references, external links, or shortcuts
  pointing to that specific entity MUST be updated to maintain reference integrity. Because state changes occur within
  the parent category namespace, relative path depth remains predictable.

### 2.2 System of Record and Canonical Ownership

A record is canonically stored strictly within the module responsible for maintaining and governing the authoritative
business record as the **System of Record**, rather than in modules that merely create, store transiently, consume, or
reference it.

- **Differentiating Operational Roles:**
  - **System of Record (Authoritative Owner):** The module bearing formal business accountability and governance for the
    canonical record. The file's single physical home is located strictly inside this module.
  - **Creator:** The module, agent, or operational unit that authors, generates, or initiates the record.
  - **Custodian:** The module, platform, or infrastructure that temporarily handles, processes, or facilitates the
    record.
  - **Consumer:** Any module, functional team, or user that reads, references, or utilizes the record.
- **Practical Governance Examples:**
  - _Client Legal Agreements:_ When Sales (Creator) negotiates and drafts an NDA that is formally reviewed,
    executed, and governed by Legal (System of Record), and referenced by Customer Support (Consumer):
    - `legal/agreement/active/2026-nda-acme-tech.pdf` (Correct: Canonical home governed by Legal).
    - `sale/pipeline/active/acme-tech/2026-nda-acme-tech.pdf` (Incorrect: Duplicate file in Sales; links to Legal).
  - _Automated Billing and Invoicing:_ When Technology / Platform Infrastructure (Custodian/Creator) automatically
    generates a customer billing statement that is formally accounted for and audited by Finance (System of Record):
    - `finance/invoice/receivable/2026/2026-08-20-acme-001.pdf` (Correct: Canonical home governed by Finance).
    - `technology/server/` or `customer/account/` (Incorrect: Duplicate file; Customer Support links to Finance).

### 2.3 Institutional Archive Module vs. Lifecycle `archived` State

LOGICS explicitly distinguishes between an entry's lifecycle state and institutional archiving:

- **Lifecycle State (`state = archived`):**
  Indicates that an individual record or workspace is no longer active within its operational category (for example:
  `customer/account/archived/acme-tech/` or `legal/agreement/archived/2020-lease.pdf`). The record remains in its native
  category.
- **Institutional Archive Module (`module = archive/`):**
  A dedicated retention destination for historical corporate records, entity snapshots, regulatory vaults, and legacy
  assets retired permanently from active operational workflows. It serves as an architectural retention destination,
  not an OS-enforced permission mechanism (underlying file permissions remain governed by OS policies per Section 2.9).
- **Archive Transfer and Relocation Rules:**
  - **Moving into `archive/`:** When an organization formally retires operational records to the institutional
    `archive/` module, the transfer relocates the file to its new canonical home. In accordance with the Single
    Canonical Home rule (Section 2.1), all existing cross-module references, relative links, and shortcuts
    pointing to the previous operational path MUST be updated to reference the new canonical path in `archive/`.
  - **Reactivating out of `archive/`:** Records retired to `archive/` are intended for long-term retention. If business,
    legal, or audit requirements dictate reactivating an archived record or workspace back into an operational module,
    the entity is moved to the appropriate operational category and assigned an active lifecycle state (for example:
    `legal/agreement/active/`), and any historical references are updated to the restored canonical path.

### 2.4 Internal Operations versus Commercial Work Separation

Internal organizational operations (such as administering, governing, or promoting the enterprise itself) live under
their respective functional modules (such as `marketing/` for internal brand identity or `people/` for staff records).
Commercial client deliverables, customer-facing projects, manufactured goods, and client services live within the
corresponding delivery modules (such as `product/`, `project/`, `sale/`, or `service/`).

- **Example:** A marketing agency's own brand guidelines live in `marketing/brand/core-identity/`. When the agency
  produces marketing collateral for a client, those deliverables reside in `service/deliverable/active/client-brand/`.

### 2.5 Distinct Names (No Segment Duplication)

Module names represent primary functional areas, while category names represent concrete business information classes.
To maintain predictable path structures:

1. **Module-Category Distinctness:** A category MUST NOT share the same identifier as its parent module (for example:
   `product/product/` or `customer/customer/` is strictly prohibited; valid forms include `product/catalog/` or
   `customer/account/`).
2. **No Identical Consecutive Segments:** A directory segment MUST NOT be identical to its immediate parent directory
   segment (for example: `people/profile/profile/` or `finance/invoice/invoice/` is strictly prohibited).
3. **Legitimate Descriptive Compounding:** Compound names that qualify an entity using descriptive words (for example:
   `marketing/content/active/summer-marketing-drive/` or `finance/invoice/payable/2026/finance-audit.pdf`) are fully
   permitted and valid.

### 2.6 Full Word Precision and Vocabulary Standard

All canonical module, category, and organization-defined subcategory identifiers must be complete, unshortened English
words adhering to American English naming conventions (for example: `procedure` not `sop`, `component` not `bom`,
`design` not `cad`, `specification` not `spec`, `repository` not `repo`, `quotation` not `quote`, `catalog` not
`catalogue`, and `organization` not `organisation`).

_Scope of the Full-Word Standard:_

- **Standard Structural Vocabulary (Strictly Enforced):** Applies strictly to globally standardized LOGICS module and
  category directories, as well as organization-defined subcategory directory identifiers. Abbreviated structural
  vocabulary is strictly prohibited across all directory levels.
- **Exemptions:** Does NOT apply to standard file extensions (for example: `.pdf`, `.md`, `.js`, `.py`),
  established technical file formats, or code files residing inside software repository workspaces governed by
  Section 6.4.

Valid canonical directory forms:

- `customer/account/` (not `customers/accounts/`)
- `product/component/` (not `products/components/` or `product/bom/`)
- `project/specification/` (not `projects/specifications/` or `project/spec/`)
- `finance/invoice/` (not `finances/invoices/`)

Invalid directory forms:

- `cust/acc/`, `proj/repo/`, `prod/cad/`, `ops/sops/`

### 2.7 Module-Specific Reporting

Reports are filed under their specific business categories within the responsible module (for example:
`finance/ledger/`, `finance/reconciliation/`, `marketing/analytics/`, `operation/incident/`, and `service/deliverable/`)
rather than an ambiguous catch-all `report/` folder.

### 2.8 On-Demand Module Provisioning

LOGICS defines sixteen standardized Level 2 modules. However, an organization is not required to physically create every
module directory in advance before it is needed. Organizations create directories on-demand as actual operational
records arise. A solo founder or startup only creates the active modules they need on day one (for example: `finance/`,
`legal/`, `people/`, `project/`), provisioning additional modules (such as `asset/`, `sale/`, or `archive/`) when
capital assets, commercial sales, or historical archives arise.

During organizational onboarding, provisioning the complete standard directory scaffold in advance is **recommended**
to help teams, users, and automation agents visualize the complete information architecture.

### 2.9 Security and Access Control Scope

LOGICS defines directory and storage architecture, not an identity and user permissions engine. Security restrictions
such as document confidentiality, file encryption, and access permissions are enforced through underlying filesystem
permissions, user accounts, role-based access controls, or storage system security policies, never through ad-hoc
directory names.

- **Example:** Managing confidential executive payroll records:
  - `finance/payroll/2026/2026-08-executive-payroll.xlsx`
    (Correct: Controlled via filesystem user and group permissions).
  - `finance/payroll/private-confidential/executive-payroll.xlsx`
    (Incorrect: Do not invent ad-hoc security-level directories).

---

## 3 Identifiers, Naming, and Syntactic Conventions

All identifiers, directory names, and file records governed by LOGICS MUST follow strict predictable naming and
formatting rules:

### 3.1 Primary Allowed Character Set and Period Character Rule

Standard file and directory names must use only the following characters:

- Lowercase English letters (`a-z`).
- Arabic numerals (`0-9`).
- Hyphens (`-`) for separating words.
- Periods (`.`) for file extensions and version decimal numbers in filenames (for example: `.pdf`, `.md`, `v1.2`).

_Period Character Rule in Directories:_

- **Filenames:** Periods are fully permitted to demarcate standard file extensions (such as `.pdf`, `.xlsx`, `.md`) and
  decimal version numbers in filenames (such as `v2.1` or `v1.2.3`).
- **Directories:** Periods are **prohibited** in ordinary LOGICS-managed directory names (for example: `sub.category/`,
  `client.v1/`, or `release-v2.1/` is prohibited; use hyphens instead: `sub-category/`, `client-v1/`, `release-v2-1/`).
  Periods in directory names are permitted ONLY when explicitly required by underlying system or tool conventions (such
  as leading-period configuration directories like `.agents/` or `.vscode/` per Section 6.3). Code trees residing inside
  software repository workspaces remain governed by Section 6.4.

Spaces, underscores (`_`), uppercase letters, and special symbols are strictly prohibited by default.

The `a-z` character restriction applies strictly to directory and file names. Document contents, text, and internal
data may be written in any language, script, or character encoding.

Examples of valid names:

- `financial-report.pdf`
- `2026-08-payroll-summary.xlsx`
- `client-contract-v1.2.pdf`
- `mobile-application-build/`

Examples of invalid names:

- `Financial Report.pdf` (contains uppercase and spaces)
- `financial_report.pdf` (contains underscores)
- `customer@account.pdf` (contains symbol `@`)
- `project(final).pdf` (contains parentheses)

### 3.2 Standalone Symbol Names Prohibition

A file or directory name must contain at least one alphanumeric character (`a-z` or `0-9`). Using only hyphens (`-`,
`--`) or periods (`.`, `..`) by themselves as the entire name of any file or directory is strictly prohibited.

### 3.3 Reserved Canonical Keyword and Redundant Directory Prohibition

To prevent confusing and redundant directory nesting:

1. **Directory Name Restriction:** Bare canonical module names (for example: `finance/`, `marketing/`, `governance/`)
   and standard category names MUST NOT be created as child directory names within a category or workspace path (for
   example: `finance/invoice/finance/` or `marketing/brand/marketing/` is strictly prohibited).
2. **Permitted Record Filenames:** Legitimate resource filenames matching the category noun (for example: `invoice.pdf`
   inside a workspace folder `finance/invoice/payable/2026/acme-tech/invoice.pdf`) or descriptive compound names (for
   example: `finance-annual-audit.pdf` or `marketing-campaign-guide.md`) are fully permitted and valid.

### 3.4 Date and Version Formatting Standards

1. **Date and Period Formatting in Filenames:**
   Filenames MAY embed dates or period designations using any of the following standard formats:
   - **Full Calendar Day Dates (Filenames Only):** Full day-level dates (`yyyy-mm-dd`, for example:
     `2026-08-19-executive-meeting.md`, `2026-08-19-invoice-001.pdf`) are permitted **strictly within leaf record
     filenames** and are **strictly prohibited** as Level 4 date directory partitions.
   - **Standard Period Partitions:** Any authorized single period token defined in Section 4.3 (for example:
     `2026-annual-financial-report.pdf`, `2026-08-monthly-summary.csv`, `2026-q3-budget-forecast.xlsx`,
     `2026-w34-throughput-log.csv`, `2026-fy-statutory-filing.pdf`, `2026-f1-close.xlsx`,
     `2026-p12-sprint-backlog.md`).
   - **Spanning Period Ranges:** Any authorized same-year or multi-year range token defined in Section 4.3
     (for example: `2026-q1-q3-progress-review.pdf`, `2026-m11-2027-m02-winter-campaign.pdf`,
     `2026-2028-fy-strategic-plan.pdf`).

   _Directory Date Formats Governed by Section 4.3:_ All Level 4 date directory partitions are governed strictly by
   Section 4.3 Item 3 (restricted to `YYYY/`, `YYYY-MM/`, `YYYY-q[1-4]/`, `YYYY-fy/`, and other authorized period
   partitions). Dates embedded within a record's filename belong strictly to the leaf file name and do not constitute
   or create a Level 4 date partition directory.

2. **Version Designations in Filenames and Directory Names:**
   - **In Filenames:** Version designations must use a lowercase `v` followed by Arabic numerals, and MAY use periods
     for decimal revisions per Section 3.1 (for example: `client-onboarding-checklist-v1.md`,
     `master-service-agreement-v2.1.pdf`, `software-specification-v1.0.4.pdf`).
   - **In Ordinary Directory Names:** Dotted versions are **prohibited** in ordinary LOGICS directory names;
     organizations must use hyphens instead (for example: `release-v1/`, `release-v2-1/`, `build-v1-0-4/`).
   - **Software Repository Code Trees:** Internal directory structures, version tags, and code files residing inside
     software repository workspaces remain governed by Section 6.4.

Preferred descriptive filenames:

- `2026-annual-financial-report.pdf`
- `product-specification-v2.pdf`
- `client-service-agreement-v1.pdf`

Avoid vague, lazy, or unversioned filenames:

- `file1.pdf`, `document.pdf`, `new.pdf`, `important.pdf`, `final-final-v2.pdf`, `stuff.pdf`

### 3.5 Leaf-to-Container Promotion Rule

When an individual leaf `<record>` accumulates supporting documents, receipts, revisions, or attachments, it is
promoted into a `<workspace>` container directory according to the following exact mapping rules:

1. **Workspace Identifier Mapping:** The new `<workspace>` directory name MUST be created using the **filename stem**
   (the exact filename without its file extension). For example: a leaf record named `2026-08-19-invoice-001.pdf` is
   promoted into a workspace directory named `2026-08-19-invoice-001/`.
2. **Preservation of the Original File:** The original resource file MUST be placed inside the newly created workspace
   directory, retaining its **exact original filename** (including full extension, dates, and version identifiers).
3. **Naming of Supporting Files:** All additional supporting files, attachments, or metadata placed inside the promoted
   workspace must retain full, self-describing names per Section 3.1 and Section 3.4.

_Canonical Promotion Example:_

Before Promotion (Direct Leaf Record):

```text
finance/invoice/payable/2026/2026-08-19-invoice-001.pdf
```

After Promotion (Workspace Container with Preserved Original Record and Attachments):

```text
finance/invoice/payable/2026/2026-08-19-invoice-001/
|-- 2026-08-19-invoice-001.pdf
`-- 2026-08-19-invoice-001-payment-confirmation.pdf
```

### 3.6 Prohibition of Vague and Generic Directories

Catch-all, ambiguous, or lazy directory names (for example: `misc/`, `other/`, `stuff/`, `general/`, `documents/`,
`files/`, `new/`, `old/`, `temp/`, `random/`) are strictly prohibited anywhere within a LOGICS storage hierarchy. Every
directory created MUST declare its explicit architectural and business meaning using one of the authorized structural
directory types:

- **`<group>` (Level 0):** Multi-entity holding or collective container.
- **`<company>` (Level 1):** Operating enterprise or independent company boundary.
- **`<module>` (Level 2):** One of the sixteen standardized functional modules.
- **`<category>` (Level 3):** One of the 112 standardized category nouns under its parent module.
- **`<subcategory>` (Level 4):** Precise, organization-defined classification partition.
- **`<state>` (Level 4):** One of the eight standardized lifecycle state partitions.
- **`<date>` (Level 4):** Authorized calendar, fiscal, or period partition.
- **`<workspace>` (Level 4):** Bounded entity, project, or subject container.

---

## 4 Standard Architecture and Structural Model

```text
┌────────────────────────────────────────────────────────┐
│              STABLE STRUCTURAL NAMESPACE               │
│        (Levels 0-3: Fixed Names / No Renaming)         │
│                                                        │
│ <group>/                                               │
│   └── <company>/                                       │
│       └── <module>/                                    │
│           └── <category>/                              │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│               DYNAMIC ENTRY NAMESPACE                  │
│             (Level 4: Dynamic Structure)               │
│                                                        │
│ [<subcategory>/]                                       │
│   └── [<state>/]                                       │
│       └── [<date>/]                                    │
│           └── [<workspace>/]                           │
│               └── <record>                             │
└────────────────────────────────────────────────────────┘
```

### 4.1 Canonical Core Architecture and Structural Vocabulary

LOGICS defines a multi-layered architectural vocabulary that balances global standardization with operational
flexibility across organizations:

1. **Global Level 2 Modules (Closed Standard Layer):** Exactly **sixteen standardized modules** that form the universal
   information architecture for organizational operations, governance, and commercial delivery. All sixteen modules
   belong to the globally fixed, closed universal standard and cannot be renamed, aliased, or extended with custom
   modules.
2. **Global Level 3 Categories (Closed V1 Standard Layer):** Exactly **112 standardized categories** across the sixteen
   modules. In LOGICS V1, these 112 categories form a fixed, closed catalog of singular English nouns. Organizations
   must not invent new category directories beneath Level 2 modules.
3. **Level 4 Subcategories (Extensible Organizational Layer):** **Organization-defined classification partitions**
   beneath Level 3 categories (such as `finance/invoice/payable/` or `marketing/content/newsletter/`). This layer is
   fully extensible by each adopting organization, governed strictly by standard naming syntax (see Section 4.3 and
   [`subcategory-reference.md`][subcategoryreference]).
4. **Level 4 Workspaces (Extensible Entity / Subject Layer):** **Organization-defined named containers** representing
   bounded business entities, client accounts, projects, or products (such as `customer/account/active/acme-tech/`).
   This layer is completely open and dynamic.

As specified in Section 2.8, organizations provision module and category directories **on demand** as actual
operational records arise; no organization is required to create empty or unused module directories in advance.

The sixteen standardized Level 2 modules are listed in alphabetical order below:

1. **`administration/`** - Facilities, office management, administrative policies, and executive logistics.
2. **`archive/`** - Institutional historical records, statutory retention, and permanent company state snapshots.
3. **`asset/`** - Capital asset register, equipment maintenance, property deeds, and fleet records.
4. **`customer/`** - Client relationship management, support ticketing, customer success, and client onboarding.
5. **`finance/`** - Accounting, fiscal budgeting, invoicing, payments, payroll, and tax filings.
6. **`governance/`** - Board of directors, shareholder records, executive resolutions, and corporate strategy.
7. **`knowledge/`** - Living internal knowledge base, standard operating procedures, and manuals.
8. **`legal/`** - Corporate compliance, contracts, non-disclosure agreements, intellectual property, and disputes.
9. **`marketing/`** - Brand identity, public relations, advertising campaigns, and market analysis.
10. **`operation/`** - Daily operational workflows, vendor logistics, health and safety, and task dispatch.
11. **`people/`** - Human resources, talent acquisition, personnel directory, benefits, and training.
12. **`product/`** - Manufacturing, hardware, industrial goods, physical products, and consumer packaged goods.
13. **`project/`** - Software engineering, architecture, construction, media production, and technical projects.
14. **`sale/`** - Retail, wholesale distribution, e-commerce, and commercial sales pipelines.
15. **`service/`** - Marketing agencies, healthcare clinics, consulting practices, and professional client services.
16. **`technology/`** - Internal IT infrastructure, server configurations, credential-system references, and tooling.

---

#### 4.1.1 Administration Module (`administration/`)

Organization-wide facilities, office management, administrative policies, and executive logistics.

- `facility/` - Office leases, floor plans, building maintenance records, and access control specs.
- `memorandum/` - Formal company-wide announcements and internal memos.
- `policy/` - Internal workplace policies regarding travel, remote work, security, and conduct.
- `schedule/` - Administrative timetables, executive calendars, and operational rosters.
- `template/` - Organization-wide document templates, corporate letterheads, and blank forms.

#### 4.1.2 Archive Module (`archive/`)

Centralized repository for permanent historical records, decommissioned systems, and legacy state snapshots intended
for long-term archival retention and compliance audits without ongoing operational modifications (actual filesystem
permissions are managed by underlying OS policies per Section 2.9).

- `legacy/` - Historical records transferred permanently out of operational modules for statutory retention.
- `snapshot/` - Periodic company-wide state snapshots and periodic system backups.
- `vault/` - Decommissioned corporate charters, founding documents, and cold-storage databases.

#### 4.1.3 Asset Module (`asset/`)

Physical and capital asset registers, company equipment, fleet vehicles, real estate, and facilities inventory.

- `equipment/` - Equipment maintenance logs, warranty certificates, and inspection reports.
- `property/` - Real estate deeds, land surveys, lease agreements, and title documents.
- `register/` - Master asset register tracking serial numbers, purchase dates, and depreciation.
- `vehicle/` - Company fleet registrations, mileage logs, and vehicle maintenance records.

#### 4.1.4 Customer Module (`customer/`)

Client relationship management, support ticketing, customer success, account management, and client onboarding.

- `account/` - Client master profiles, customer workspaces, and relationship plans.
- `feedback/` - Net Promoter Score logs, customer reviews, and satisfaction survey results.
- `onboarding/` - Client intake checklists, account setup records, and transition documentation.
- `ticket/` - Customer support transcripts, issue reports, and resolution logs.

#### 4.1.5 Finance Module (`finance/`)

Monetary operations, accounting, budgeting, banking, tax filings, payroll records, and fiscal audits.

- `budget/` - Annual and quarterly fiscal budgets, operating models, and financial forecasts.
- `invoice/` - Customer billing statements (receivables) and incoming vendor invoices (payables).
- `ledger/` - Accounting journal entries, general ledgers, trial balances, and cashbooks.
- `payment/` - Outgoing payment vouchers, wire confirmations, and payout records.
- `payroll/` - Salary sheets, compensation logs, tax withholdings, and contractor payouts.
- `receipt/` - Proof of payment, expense receipts, and transaction slips.
- `reconciliation/` - Bank reconciliation statements and payment settlement audits.
- `statement/` - Periodic banking statements, credit card summaries, and merchant processing logs.
- `tax/` - Tax returns, government remittances, assessments, and statutory filings.

#### 4.1.6 Governance Module (`governance/`)

Board of directors, executive strategy, shareholder records, bylaws, and charter resolutions.

- `charter/` - Founding articles of incorporation, company bylaws, and shareholder agreements.
- `decision/` - Executive decision logs, committee charters, and management minutes.
- `meeting/` - Agendas, minutes, and transcripts of board and shareholder sessions.
- `resolution/` - Formal board and executive binding resolutions.
- `strategy/` - Multi-year strategic visions, executive roadmaps, and corporate growth plans.

#### 4.1.7 Knowledge Module (`knowledge/`)

Living internal knowledge base, standard operating procedures, documentation, guides, and manuals.

- `documentation/` - System documentation, architecture overviews, and internal knowledge bases.
- `guide/` - Step-by-step how-to articles and onboarding workflows.
- `manual/` - Equipment manuals, software user guides, and operational instruction handbooks.
- `procedure/` - Standard operating procedures (SOPs) across organizational functions.
- `reference/` - Fact sheets, glossaries, cheat sheets, and lookup tables.

#### 4.1.8 Legal Module (`legal/`)

Corporate compliance, organizational contracts, intellectual property rights, litigation, and regulatory filings.

- `agreement/` - Non-disclosure agreements, mutual covenants, and vendor contracts.
- `compliance/` - Regulatory compliance records, audit certificates, and statutory licenses.
- `contract/` - Master service agreements, executive employment agreements, and formal deeds.
- `copyright/` - Copyright registrations, software code deposits, and creative (or IP) rights assignments.
- `dispute/` - Legal claims, litigation records, settlement agreements, and court filings.
- `patent/` - Patent applications, provisional filings, grant certificates, and invention disclosures.
- `trademark/` - Trademark registrations, brand protection filings, and service mark certificates.

#### 4.1.9 Marketing Module (`marketing/`)

Promoting the enterprise itself: brand identity, corporate website, public relations, and market analysis.

- `advertising/` - Paid advertisements, media buys, creative ad copies, and campaign analytics.
- `analytics/` - Marketing performance reports, web traffic metrics, and SEO audit records.
- `brand/` - Brand identity guidelines, logos, typography, color palettes, and visual assets.
- `collateral/` - Corporate pitch decks, one-pagers, brochures, and capability statements.
- `content/` - Content calendars, social media publications, articles, and scheduled campaign assets.
- `press/` - Press releases, media kits, and official public statements.
- `pricing/` - Master rate sheets, corporate pricing matrices, and service fee schedules.

#### 4.1.10 Operation Module (`operation/`)

Daily operational workflows, vendor logistics, health and safety, task dispatch, and facilities management.

- `checklist/` - Routine operational audit and inspection checklists.
- `incident/` - Operational outage reports, post-mortems, root cause analyses, and corrective actions.
- `logistics/` - Shipping manifests, bill of ladings, tracking records, and supply chain routes.
- `maintenance/` - Facility upkeep logs, equipment servicing records, and building maintenance schedules.
- `safety/` - Workplace health and safety audits, hazard logs, workplace safety records, and statutory safety filings.
- `task/` - Dispatched task orders, maintenance tickets, and work orders.
- `vendor/` - Supplier profiles, vendor rate cards, procurement contacts, and service agreements.
- `workflow/` - Daily operational schedules and business process flowcharts.

#### 4.1.11 People Module (`people/`)

Human resources, talent acquisition, personnel directory, benefits, internal culture, evaluations, and training.

- `benefit/` - Health insurance plans, retirement options, perk packages, and policy summaries.
- `evaluation/` - Performance reviews, 360 appraisals, and promotion records.
- `handbook/` - Employee onboarding handbooks, code of conduct, and cultural guides.
- `profile/` - Personnel records for employees, contractors, and advisors.
- `recruitment/` - Job descriptions, candidate resumes, interview scorecards, and hiring offers.
- `training/` - Internal training decks, professional development records, and certifications.

#### 4.1.12 Product Module (`product/`)

Manufacturing, hardware, industrial goods, physical products, and consumer packaged goods.

- `batch/` - Batch production records, lot manufacturing logs, and quality verification sheets.
- `catalog/` - Product catalog, SKU tables, and wholesale price lists for manufactured goods.
- `certificate/` - Certificates of analysis, lab testing sheets, and safety compliance certificates.
- `component/` - Bill of materials (BOM), component specifications, and raw material records.
- `design/` - Three-dimensional CAD models, product technical drawings, and physical schematics.
- `firmware/` - Embedded software binaries, micro-controller code, and firmware releases.
- `inspection/` - Quality assurance inspection logs, factory acceptance tests, and defect reports.
- `inventory/` - Stock levels, warehouse counts, safety stock models, and finished goods logs.
- `packaging/` - Packaging artwork, box dielines, label artwork, and barcode specifications.
- `research/` - Material research, product feasibility studies, and physical prototype testing data.
- `sample/` - Prototype inspection sheets and lab validation test reports.
- `schematic/` - Electronic circuit schematics, PCB board layouts, and wiring diagrams.

#### 4.1.13 Project Module (`project/`)

Software development, engineering, architecture, construction, media production, and technical consulting.

- `audio/` - Audio tracks, sound effect mixes, and recorded stems.
- `blueprint/` - Architectural blueprints, construction drawings, and civil engineering plans.
- `edit/` - Video project timelines, rough cuts, and intermediate edits.
- `footage/` - Video raw footage and audio-visual source recordings.
- `inspection/` - Field construction inspections and engineering site reviews.
- `milestone/` - Milestone deliverables, project sprint plans, and delivery schedules.
- `permit/` - Building permits, zoning approvals, and regulatory construction clearances.
- `release/` - Release notes, software changelogs, build artifacts, and deployment binaries.
- `render/` - Rendered video sequences, CGI visual effects, and graphic exports.
- `repository/` - Source code repositories and development workspaces (governed by Section 6.4).
- `research/` - Technical research, feasibility studies, competitor analyses, and exploratory spikes.
- `script/` - Screenplays, voiceover scripts, and production copy.
- `specification/` - Functional and technical software specifications, PRDs, and system requirements.
- `storyboard/` - Visual storyboards and scene sketches.
- `submittal/` - Contractor shop drawings and material submittals.
- `test/` - Quality assurance test plans, automated test cases, and validation suites.

#### 4.1.14 Sale Module (`sale/`)

Retail, wholesale distribution, business-to-business deal flow, and electronic commerce.

- `estimate/` - Preliminary cost estimates and budgetary sales quotes.
- `inquiry/` - Customer inbound product inquiries and lead requests.
- `lead/` - Prospect lists, lead scoring sheets, and discovery notes.
- `order/` - Executed purchase orders, sales contracts, and order confirmations.
- `pipeline/` - Sales funnel tracking, deal-stage summaries, and CRM exports.
- `proposal/` - Commercial sales pitches, RFP responses, and tender bids.
- `quotation/` - Formal price quotations and binding sales estimates.

#### 4.1.15 Service Module (`service/`)

Service providers, creative agencies, healthcare practices, consulting firms, and professional client services.

- `campaign/` - Client-specific marketing campaigns and creative media packages created by agencies.
- `deliverable/` - Client handoff documents, final reports, and finished service assets.
- `engagement/` - Client engagement plans, master statements of work, and kickoff packs.
- `intake/` - Patient and client intake forms, onboarding records, and assessment sheets.
- `prescription/` - Clinical prescriptions and treatment directives.
- `protocol/` - Clinical protocols and operational care pathways.
- `result/` - Diagnostic findings, lab reports, and clinical evaluation results.
- `retainer/` - Monthly service logs, retainer hour tracking, and service level reports.
- `scope/` - Formal statement of work documents and project scopes.

#### 4.1.16 Technology Module (`technology/`)

Internal information technology infrastructure, devices, networks, internal software, configurations, and IT tooling.
(Raw credentials, passwords, and API secrets must reside in dedicated, approved secrets-management systems; LOGICS
manages only non-secret technical configurations, public assets, and access records per Section 2.9).

- `backup/` - Machine-generated database dumps and infrastructure recovery snapshots.
- `configuration/` - Server configurations, infrastructure-as-code files, and environment definitions.
- `credential/` - Public encryption keys, SSL/TLS certificates, access audit records, and system pointer references
  to approved external credential-management vaults.
- `network/` - Network layout diagrams, IP allocations, firewall configurations, and routing maps.
- `tooling/` - Internal software tool directories, developer toolchains, and software license records.

---

### 4.2 Closed Standard vs. Extensible Layers

LOGICS structural naming rules depend strictly on the vocabulary layer:

1. **Closed Standard Layers (No Renaming, Aliasing, or Custom Additions):**
   - **Level 2 Modules:** The canonical names of the sixteen standard modules are globally fixed. Renaming, aliasing,
     translating, or abbreviating these directories (for example: renaming `people/` to `hr/`, `staff/`, or
     `employees/`) is **strictly prohibited**.
   - **Level 3 Categories:** The 112 standard V1 category names across the sixteen modules are globally fixed.
     Organizations must not rename, alias, translate, abbreviate, or add custom unstandardized category directories
     beneath Level 2 modules.
2. **Extensible Organizational Layers (Organization-Defined):**
   - **Level 4 Subcategories:** Fully extensible by each adopting organization to reflect domain-specific functional
     specializations (such as `payable`, `access-control`, `newsletter`), governed strictly by standard naming syntax,
     lowercase alphanumeric hyphenation, singular nouns, and full-word precision rules.
   - **Level 4 Workspaces:** Fully extensible and dynamic entity/project containers named after business subjects (such
     as `acme-tech/`, `mobile-app/`, `q1-release/`), governed by lowercase hyphenated identifier syntax.

### 4.3 Level 4 Dynamic Entry Namespace and Partitions

An `entry` is a Level 4 organizational component within a category path. Every canonical entry in a path MUST conform
to one of the five standardized entry types and follow the fixed precedence cascade (non-canonical temporary working
artifacts exist outside this structural entry namespace per Section 6.2):

1. **`<subcategory>` (Classification Partition):**
   An optional sub-classification or functional specialization directory. Subcategories are **organization-defined**
   rather than drawn from a globally standardized closed list (unless formally added to a maintained LOGICS standard
   vocabulary in future revisions). Organizations define subcategories according to their specific operational domains,
   subject strictly to the standard character set, lowercase hyphenation, singular noun conventions, and full-word
   precision rules defined in Section 2.6 and Section 3.1 (see
   [`subcategory-reference.md`][subcategoryreference] for a curated best-practice
   reference catalog across all sixteen modules).
   - `finance/invoice/payable/`
   - `administration/facility/access-control/`
   - `governance/strategy/acquisition/`

2. **`<state>` (Lifecycle State Partition):**
   An optional lifecycle state directory partition that explicitly classifies the operational status of the workspace
   or record placed within that directory branch. State rules are strictly structural: LOGICS does not introduce
   implicit metadata inheritance. If an entity or record requires an independent lifecycle state, it must be organized
   directly under its own corresponding state partition. A state directory MUST be one of the eight standard LOGICS
   state identifiers:
   - `lead`
   - `prospect`
   - `active`
   - `paused`
   - `review`
   - `archived`
   - `draft`
   - `closed`
     _(Example: `customer/account/active/`, `sale/pipeline/prospect/`, `legal/agreement/draft/`)_

3. **`<date>` (Date Partition):**
   An optional chronological partition directory. The pattern tokens `YYYY`, `MM`, `b[1-2]`, `q[1-4]`, `w[1-53]`,
   `f[1-13]`, and `p[1-99]` represent abstract notation placeholders for numeric calendar and cycle digits, not literal
   directory characters. Actual date directories MUST use only lowercase alphanumeric characters and hyphens in strict
   compliance with one of the following canonical formats:

   _Calendar Partitions:_
   - Calendar Year: `YYYY` (four numeric digits, for example: `2026/`)
   - Calendar Multi-Year Spanning Range: `YYYY-YYYY` (four-digit starting and ending years, for example: `2026-2027/`,
     `2024-2026/`)
   - Calendar Month: `YYYY-MM` (four-digit year and two-digit month, for example: `2026-08/`)
   - Calendar Same-Year Multi-Month Range: `YYYY-mMM-mMM` (four-digit year followed by `-m` prefix and two-digit start
     and end months, for example: `2026-m01-m03/`, `2026-m06-m08/`, `2026-m01-m06/`)
   - Calendar Multi-Year Spanning Month Range: `YYYY-mMM-YYYY-mMM` (four-digit starting year and month to four-digit
     ending year and month, for example: `2026-m11-2027-m02/`, `2026-m09-2027-m06/`)
   - Calendar Biannual / Half-Year: `YYYY-b[1-2]` (four numeric digits followed by `-b1` or `-b2` dividing the 12-month
     calendar into two 6-month blocks, for example: `2026-b1/`, `2026-b2/`)
   - Calendar Same-Year Biannual Range: `YYYY-b1-b2` (four-digit year spanning both biannual halves, for example:
     `2026-b1-b2/`)
   - Calendar Multi-Year Spanning Biannual Range: `YYYY-b[1-2]-YYYY-b[1-2]` (spanning half-years across calendar years,
     for example: `2026-b2-2027-b1/`)
   - Calendar Quarter: `YYYY-q[1-4]` (four numeric digits followed by `-q1` through `-q4`, for example: `2026-q1/`,
     `2026-q3/`)
   - Calendar Same-Year Multi-Quarter Range: `YYYY-q[1-4]-q[1-4]` (four-digit year followed by start and end quarter,
     for example: `2026-q1-q2/`, `2026-q1-q3/`, `2026-q2-q4/`)
   - Calendar Multi-Year Spanning Quarter Range: `YYYY-q[1-4]-YYYY-q[1-4]` (spanning quarters across calendar years,
     for example: `2026-q4-2027-q1/`, `2026-q3-2027-q2/`)
   - Calendar Week: `YYYY-w[1-53]` (four-digit year followed by `-w1` through `-w52` or `-w53` when the calendar year
     contains 53 weeks per ISO 8601 or the declared operational calendar, for example: `2026-w1/`, `2026-w34/`,
     `2026-w52/`, `2026-w53/`)
   - Calendar Same-Year Multi-Week Range: `YYYY-w[1-53]-w[1-53]` (four-digit year followed by start and end week,
     for example: `2026-w1-w13/`, `2026-w14-w26/`, `2026-w40-w53/`)
   - Calendar Multi-Year Spanning Week Range: `YYYY-w[1-53]-YYYY-w[1-53]` (spanning operational weeks across calendar
     years, for example: `2026-w48-2027-w06/`, `2026-w36-2027-w20/`)

   _Fiscal Partitions:_
   - Fiscal Year: `YYYY-fy` (four-digit starting year followed by `-fy`, for example: `2026-fy/`)
   - Fiscal Spanning Multi-Year Range: `YYYY-YYYY-fy` (four-digit starting year and four-digit ending year followed
     by `-fy`, for example: `2026-2028-fy/`, `2024-2026-fy/`)
   - Fiscal Period (Organizational Accounting Cycles): `YYYY-f[1-13]` (four-digit starting year followed by `-f1`
     through `-f13` representing numbered organizational accounting periods, such as 13 x 4-week cycles, 4-4-5 / 4-5-4
     retail calendars, or statutory fiscal reporting intervals, where `YYYY` indicates the cycle's starting year even
     if the period spans into the subsequent calendar year, for example: `2026-f1/`, `2026-f12/`, `2026-f13/`)
   - Fiscal Same-Year Multi-Period Range: `YYYY-f[1-13]-f[1-13]` (four-digit starting year followed by start and end
     fiscal period range, for example: `2026-f1-f6/`, `2026-f7-f13/`)
   - Fiscal Multi-Year Spanning Period Range: `YYYY-f[1-13]-YYYY-f[1-13]` (spanning accounting cycles across fiscal
     years, for example: `2026-f11-2027-f03/`, `2026-f10-2027-f04/`)

   _Custom / Operational Period:_
   - Custom Single Period: `YYYY-p[1-99]` (four-digit starting year followed by `-p1` through `-p99`, for example:
     `2026-p1/`, `2026-p12/`, `2026-p99/`)
   - Custom Same-Year Multi-Period Range: `YYYY-p[1-99]-p[1-99]` (four-digit starting year followed by start and end
     custom period range, for example: `2026-p2-p5/`, `2026-p1-p12/`)
   - Custom Multi-Year Spanning Period Range: `YYYY-p[1-99]-YYYY-p[1-99]` (spanning custom cycles across calendar
     years, for example: `2026-p10-2027-p04/`)

   _Canonical Date Partition Token Reference:_

   | Interval Type     | Single         | Same-Year Range        | Multi-Year Range            | Example Range        |
   | :---------------- | :------------- | :--------------------- | :-------------------------- | :------------------- |
   | **Year**          | `YYYY`         | -                      | `YYYY-YYYY`                 | `2024-2026/`         |
   | **Month**         | `YYYY-MM`      | `YYYY-mMM-mMM`         | `YYYY-mMM-YYYY-mMM`         | `2026-m11-2027-m02/` |
   | **Biannual**      | `YYYY-b[1-2]`  | `YYYY-b1-b2`           | `YYYY-b[1-2]-YYYY-b[1-2]`   | `2026-b2-2027-b1/`   |
   | **Quarter**       | `YYYY-q[1-4]`  | `YYYY-q[1-4]-q[1-4]`   | `YYYY-q[1-4]-YYYY-q[1-4]`   | `2026-q4-2027-q1/`   |
   | **Week**          | `YYYY-w[1-53]` | `YYYY-w[1-53]-w[1-53]` | `YYYY-w[1-53]-YYYY-w[1-53]` | `2026-w48-2027-w06/` |
   | **Fiscal Year**   | `YYYY-fy`      | -                      | `YYYY-YYYY-fy`              | `2026-2028-fy/`      |
   | **Fiscal Period** | `YYYY-f[1-13]` | `YYYY-f[1-13]-f[1-13]` | `YYYY-f[1-13]-YYYY-f[1-13]` | `2026-f11-2027-f03/` |
   | **Custom Period** | `YYYY-p[1-99]` | `YYYY-p[1-99]-p[1-99]` | `YYYY-p[1-99]-YYYY-p[1-99]` | `2026-p10-2027-p04/` |

   _Rules Governing Multi-Period and Spanning Ranges:_
   1. **Ascending Order Requirement:** The starting period or year MUST be strictly earlier than the ending period or
      year (`start < end`). Inverted ranges (for example: `2026-p5-p2/`, `2027-q1-2026-q4/`, or `2026-m08-m05/` where
      end month is earlier than start month) and single-interval ranges (for example: `2026-p3-p3/` or `2026-2026/`)
      are strictly prohibited; single intervals MUST use the standard single-period format.
   2. **Uniform Level Scope:** Multi-period ranges apply strictly to matching interval types (for example: week-to-week
      `YYYY-w[1-53]-w[1-53]` or month-to-month `YYYY-mMM-mMM`, such as `2026-m01-m06/`); mixing different interval
      types in a range (such as `2026-q4-2027-m03/` or `2026-w50-2027-q1/`) is strictly prohibited.
   3. **No Redundant Sub-directories:** A range directory represents a single, complete container partition. Nesting
      sub-period directories inside a range partition (for example: `2026-p2-p5/p3/` or `2026-2028-fy/2027-fy/`) is
      strictly prohibited.

   _Note on Custom and Organizational Periods:_ The exact starting dates, cycle definitions, and period boundaries for
   custom periods (such as an organization's fiscal year start date, for example: April 1 or October 1 for `YYYY-fy`),
   fiscal period accounting calendars (`YYYY-f[1-13]`), custom accounting cycles (`YYYY-p[1-99]`), and the official
   week start day and 52 vs. 53-week calendar cycles (for example: Monday vs. Sunday start for `YYYY-w[1-53]`), vary
   across organizations, jurisdictions, and statutory frameworks. In 13-period or 4-4-5 / 4-5-4 retail and manufacturing
   calendars, how remaining calendar days, leap days, or 53rd adjustment weeks are absorbed (such as adding extra days
   to Period 13 or reconciling via periodic adjustments) is governed by each organization's accounting policies.
   Organizations MUST document their specific operational calendar definitions, period start dates, extra-day
   reconciliation rules, and numbering conventions inside their internal `knowledge/` module (for example:
   `knowledge/procedure/operational-calendar.md` or `knowledge/manual/operational-calendar.md`).

   _Prohibition of Day-Level Directory Partitions:_ Day-level date directory partitions (such as `YYYY-MM-DD/`, for
   example: `2026-08-20/`) and multi-level nested date directories (for example: `2026/08/` or `2026/08/20/`) are
   **STRICTLY PROHIBITED** as Level 4 directory entries to prevent excessive folder proliferation.
   _Date Partition Directory vs. Filename Dates:_ While Level 4 date directories are restricted to the period partitions
   above, individual record filenames may embed full day-level dates (`yyyy-mm-dd`) or partial dates (`yyyy-mm`, `yyyy`)
   in accordance with Section 3.4; dates embedded within a filename do NOT constitute or create an additional Level 4
   date entry.

4. **`<workspace>` (Entity / Subject Container):**
   An optional named container directory representing a bounded business subject whose related records are managed
   together (such as a client account, product codebase, case file, or project).
   - `customer/account/active/acme-tech/`
   - `project/repository/mobile-app/`
   - `project/milestone/q1-release/`

   _Workspace Identity and Scoped Uniqueness:_ A workspace identifier MUST be unique within its complete parent
   directory path. However, the same workspace name MAY legitimately occur under different categories, modules,
   companies, or state paths (for example: a client named `acme-tech` may exist under
   `customer/account/active/acme-tech/` and also have related project workspaces under
   `service/deliverable/active/acme-tech/`). Global uniqueness across the entire storage tree is not required.

5. **`<record>` (Leaf File / Terminal Resource):**
   The terminal resource file representing an individual document, contract, image, data file, or report. A `record`
   is **strictly terminal** and represents an actual file; a `record` entry MUST NOT be a directory and cannot contain
   child entries. Container functionality is handled exclusively by `<workspace>` directories.
   - `legal/agreement/2026-nda-partner-corp.pdf`
   - `finance/invoice/payable/2026/2026-08-20-acme-001.pdf`

#### 4.3.1 Classification and State Lifecycle Partitions

##### 4.3.1.1 State Vocabulary and Semantic Applicability

LOGICS defines eight standard state identifiers for common organizational workflows.

These states are not a universal lifecycle sequence. A category MAY use only the states that are meaningful for its
records.

A category MUST NOT use a state merely because it is part of the standard vocabulary; the state MUST be semantically
appropriate for the records organized under that category.

A state partition directory explicitly classifies the operational status of the workspace or record placed within that
directory branch. State rules in LOGICS are strictly positional and structural: LOGICS does not introduce implicit
metadata inheritance. If an entity, workspace, or record requires an independent lifecycle state, it must be organized
under its own corresponding state partition.

LOGICS defines eight **standard state identifiers** that form the complete, closed global vocabulary:

- `lead` - Standard state commonly used for customer, commercial, and sales intake, inquiries, or unconfirmed
  discovery opportunities.
- `prospect` - Standard state commonly used for customer and sales pipelines, qualified prospects, and active commercial
  opportunities undergoing quotation or proposal.
- `active` - Engagements, client accounts, projects, or contracts currently in active execution.
- `paused` - Temporarily suspended or held initiatives awaiting external dependencies.
- `review` - Deliverables, drafts, or contracts undergoing formal evaluation, audit, or legal review.
- `closed` - Formally completed, fulfilled, or terminated engagements, projects, milestones, or customer transactions
  that have concluded operational execution (for example: a finished project milestone or settled sales deal).
- `archived` - Post-operational retention state for historical, superseded, or finalized records and workspaces retained
  for statutory, compliance, or historical reference within their native category (for example: tax records or expired
  contracts retained in place).
- `draft` - In-progress, unapproved, or provisional documents and specifications.

_Distinguishing `closed` from `archived`:_

- **`closed` (Operational Completion):** Represents the immediate conclusion of operational activity. The business
  transaction or workflow is complete, but the record remains part of recent or standard operational history (for
  example: a project workspace moved to `project/milestone/closed/q1-mobile-app/` upon delivery, or a won/lost deal
  moved to `sale/pipeline/closed/acme-deal/`).
- **`archived` (Post-Operational Retention):** Represents long-term, non-active retention within the native category
  after all active and near-term closure operations have concluded (for example: an expired lease preserved at
  `legal/agreement/archived/2020-office-lease.pdf`, or a deactivated client account at
  `customer/account/archived/acme-corp/`).
- **Distinction from Institutional `archive/` Module:** The `archived` lifecycle state retains records in their native
  operational category (for example: `legal/agreement/archived/`). In contrast, the top-level `archive/` module
  (Section 2.3) is a separate, permanent institutional repository for retired corporate vaults and legacy assets
  moved entirely out of operational modules.

_State Applicability Rule:_ A category MAY activate and use only the specific subset of standard states that are
meaningful for its operational context (for example: `legal/agreement/` may use only `draft/`, `review/`, `active/`, and
`archived/`, while `sale/pipeline/` may use only `lead/`, `prospect/`, `active/`, and `closed/`). Inventing
category-specific or custom state names outside of these eight standardized identifiers is strictly prohibited.

##### 4.3.1.2 State Entry Placement and Precedence

When state partitioning is used beneath a category, it MUST strictly follow the canonical Level 4 sequence:
`subcategory -> state -> date -> workspace -> record`.

```text
<module>/<category>/[<subcategory>/]<state>/[<date>/][<workspace>/]<record>
```

Examples of compliant state-partitioned paths:

- `customer/account/active/acme-tech/profile.pdf`
- `customer/account/lead/acme-corp/intake.pdf`
- `sale/pipeline/prospect/2026/acme-logistics/proposal.pdf`
- `legal/agreement/draft/2026-nda-partner.pdf`

##### 4.3.1.3 Single State Rule and In-Place Lifecycle Transitions

State partitioning is entirely **optional**; records and workspaces organized without state directory partitions remain
fully compliant with LOGICS.

However, when state partitioning is activated for a given category branch:

1. **Single State Partition Requirement:** An entity (whether a standalone leaf `<record>` or an entity/project
   `<workspace>`) MUST exist in exactly one applicable state partition directory at any given time. An entity MUST
   NOT exist in or be duplicated across multiple state partitions simultaneously.
2. **Lifecycle State Transition:** When an entity changes its lifecycle status, it is moved from its current state
   partition to the new applicable state partition within its parent category branch:
   - **Workspace Transitions:** A workspace container is moved in its entirety to the new state partition (for example:
     `customer/account/lead/acme-corp/` is moved to `customer/account/active/acme-corp/`, or `sale/pipeline/prospect/`
     to `sale/pipeline/closed/`).
   - **Record Transitions:** A direct standalone leaf record is moved to the new state partition (for example:
     `legal/agreement/draft/2026-nda-partner.pdf` is moved to `legal/agreement/review/2026-nda-partner.pdf`, and
     subsequently to `legal/agreement/active/2026-nda-partner.pdf`).
3. **Path Depth and Link Stability:** Because the parent module and category levels have fixed structural names, moving
   an entity between state partitions occurs strictly within the category branch, preserving overall path depth and
   maintaining relative link stability across the storage tree.

##### 4.3.1.4 Non-Exclusive Business Classifications (Tags)

Non-exclusive business attributes (such as `vip`, `credit-risk`, `confidential`, or `high-priority`) MUST NOT be created
as ad-hoc directory partitions. Such properties are stored as document metadata or attributes, leaving the directory
structure dedicated strictly to the canonical lifecycle states defined in Section 4.3.1.1.

---

### 4.4 Reference Adoption Profiles (Informational)

The adoption profiles in this section are **informational reference examples**. They illustrate how organizations in
different industries may select and activate specific modules and categories to match their commercial operating model.
An organization operating within a listed industry is NOT required to adopt exactly the combinations shown below;
organizations freely provision any subset of the sixteen standardized modules on-demand according to their unique
operational requirements per Section 2.8.

#### 4.4.1 Single-Company Reference Profiles

The following profiles illustrate practical adoption combinations, organized from lean operational baselines to
multi-extension enterprise operations:

##### 4.4.1.1 Core Operational Baseline

Activates foundational administrative, financial, governance, and technology modules (`administration`, `archive`,
`asset`, `finance`, `governance`, `knowledge`, `legal`, `marketing`, `operation`, `people`, `technology`). Suitable for
holding companies, investment entities, family offices, or organizations during preliminary formation.

##### 4.4.1.2 Education and Training Institution

Combines administrative and governance modules with `customer`, `knowledge`, `people`, and `service` (`deliverable`,
`engagement`, `intake`, `protocol`, and `scope`).

##### 4.4.1.3 Healthcare and Medical Practice

Combines foundational operations with `customer`, `knowledge`, and `service` (`engagement`, `intake`, `prescription`,
`protocol`, and `result`).

_Scope Note:_ LOGICS defines directory and storage organization only. It does NOT define or enforce clinical,
patient privacy, medical record retention, legal, or healthcare regulatory compliance rules (which remain governed
by external statutes and organizational IT security policies per Section 2.9).

##### 4.4.1.4 Marketing and Creative Agency

Combines foundational operations with `customer`, `marketing`, and `service` (`campaign`, `deliverable`, `engagement`,
`retainer`, and `scope`).

##### 4.4.1.5 Software Development Company

Combines foundational operations with `customer`, `technology`, and `project` (`blueprint`, `milestone`, `release`,
`repository`, `research`, `specification`, and `test`).

##### 4.4.1.6 Architecture and Construction Firm

Combines foundational operations with `customer`, `operation`, and `project` (`blueprint`, `inspection`,
`milestone`, `permit`, and `submittal`).

##### 4.4.1.7 Professional and Legal Services Practice

Combines foundational operations with `customer`, `service` (`deliverable`, `engagement`, `retainer`, `scope`), and
`sale` (`proposal`, `quotation`).

##### 4.4.1.8 Real Estate and Property Management Enterprise

Combines foundational operations with `asset`, `customer`, `sale` (`inquiry`, `lead`, `pipeline`), and `service`
(`engagement`, `retainer`, `scope`).

##### 4.4.1.9 Logistics and Transportation Carrier

Combines foundational operations with `asset`, `operation`, `sale` (`order`, `pipeline`, `quotation`), and `service`
(`deliverable`, `engagement`, `scope`).

##### 4.4.1.10 Video and Media Production Studio

Combines foundational operations with `marketing`, `project` (`audio`, `edit`, `footage`, `milestone`, `render`,
`script`, and `storyboard`), and `sale` (`order`, `pipeline`, `quotation`).

##### 4.4.1.11 Electronic Commerce and Online Retail Business

Combines foundational operations with `customer`, `marketing`, `product`, and `sale` (`catalog`, `inventory`, `order`,
`packaging`, and `pipeline`).

##### 4.4.1.12 Retail Store and Wholesale Distributor

Combines foundational operations with `customer`, `operation`, `product` (`catalog`, `inventory`, `packaging`), and
`sale` (`estimate`, `inquiry`, `order`, `pipeline`, `quotation`).

##### 4.4.1.13 Manufacturing and Hardware Enterprise

Combines foundational operations with `operation`, `technology`, `product`, and `sale` (`batch`, `catalog`,
`certificate`, `component`, `design`, `firmware`, `inspection`, `inventory`, `packaging`, `research`, `sample`, and
`schematic`).

##### 4.4.1.14 Hospitality and Food Service Establishment

Combines foundational operations with `operation`, `people`, `product`, `sale`, and `service` (`catalog`, `inventory`,
`order`, `packaging`, `retainer`, and `scope`).

#### 4.4.2 Multi-Company Group Architecture (Level 0 and Level 1)

Organizations that own, operate, or govern multiple distinct legal entities, holding groups, retail chains, or
subsidiaries use **Level 0: Group** (`<group>/`) as the root umbrella container, housing independent
**Level 1: Company** (`<company>/`) trees side-by-side:

```text
acme-group/                                 --> Level 0: Group (Optional holding umbrella)
|-- acme-media/                             --> Level 1: Company (Independent operating entity)
|   |-- administration/                     --> Level 2: Module
|   |-- finance/                            --> Level 2: Module
|   |   `-- invoice/                        --> Level 3: Category
|   |       `-- payable/                    --> Level 4: Entry (Subcategory)
|   |           `-- 2026/                   --> Level 4: Entry (Date)
|   |               `-- 2026-08-20-acme.pdf --> Level 4: Entry (Record)
|   |-- governance/
|   `-- project/                            --> Level 2: Module
|       `-- repository/                     --> Level 3: Category
|           `-- media-pipeline/             --> Level 4: Entry (Workspace)
`-- acme-video/                             --> Level 1: Company (Independent operating entity)
    |-- administration/
    |-- finance/
    |-- governance/
    `-- project/
        `-- repository/
            `-- stream-player/
```

In this enterprise multi-entity architecture:

- `Level 0: <group>/` represents the parent corporate group or holding conglomerate and exists strictly as an
  umbrella container housing one or more Level 1 Company directories. A Level 0 Group directory MUST NOT directly
  contain modules, categories, entries, or records.
- Each `Level 1: <company>/` represents an operating legal entity, store, branch, or subsidiary and maintains an
  independent LOGICS storage tree with its own active modules.
- Standalone companies omit Level 0 entirely and begin directly at Level 1 (`acme-corp/` or `./`).

---

## 5 Formal Rules, Schemas, and Validation

LOGICS conformance validation operates as a two-stage verification process:

1. **Syntactic Structural Validation (EBNF Grammar):** Verifies path layout, identifier token formats, delimiter usage,
   date token syntax, and strict adherence to the Level 4 entry precedence cascade.
2. **Semantic Closed-Catalog Validation (Vocabulary Membership):** Verifies that Level 2 modules belong strictly to the
   sixteen standardized module identifiers, that Level 3 categories belong strictly to the 112 authorized category nouns
   governed by their respective parent module (Section 4.1), and that subcategories comply with singular noun and
   full-word precision rules (Section 3.1).

Conforming validation daemons, automated linters, and toolchains MUST apply both validation stages; EBNF syntactic
parsing alone validates path grammar, but complete LOGICS standard conformance requires passing both structural and
closed-catalog vocabulary validation.

### 5.1 Level 4 Entry Precedence and Formal EBNF Path Grammar

When combining entry types beneath a category, entries MUST be ordered from broad classification to progressively
specific organization according to the **Precedence Cascade**:

```text
subcategory  -->  "What kind of thing?"
    ↓
  state      -->  "What condition is it in?"
    ↓
   date      -->  "When?"
    ↓
workspace    -->  "Which specific entity / project container?"
    ↓
  record     -->  "What actual resource file? (Terminal leaf file)"
```

**Formal Precedence Rule:**

```text
subcategory -> state -> date -> workspace -> record
```

Every entry type within Level 4 is **optional**. However, when multiple entry types are present within a path:

- Each entry type MUST appear at most once.
- Entry types MUST strictly follow the canonical sequence above (`subcategory -> state -> date -> workspace -> record`).

1. **Compliant Directory Paths (Containers / Partitions):**
   A valid directory path terminates at `category/` or any optional container/partition entry without requiring a
   leaf record:

   ```text
   category/
   category/[subcategory/]
   category/[subcategory/][state/]
   category/[subcategory/][state/][date/]
   category/[subcategory/][state/][date/][workspace/]
   ```

2. **Compliant Record Paths (Leaf Files):**
   A `record` represents an actual resource file and is **terminal**. It is required **only** when a path references
   an actual file, and it MUST be located directly beneath the category or its deepest specified container/partition:
   ```text
   category/[subcategory/][state/][date/][workspace/]record
   ```

**Examples of Valid Paths:**

- _Category root directory:_ `finance/invoice/`
- _Subcategory partition directory:_ `finance/invoice/payable/`
- _State partition directory:_ `customer/account/active/`
- _Date partition directory:_ `finance/invoice/2026/`
- _Workspace container directory:_ `customer/account/active/acme-tech/`
- _Direct record path:_ `legal/agreement/2026-nda-partner-corp.pdf`
- _Partitioned record path:_ `finance/invoice/payable/2026/2026-08-20-acme-001.pdf`
- _Workspace record path:_ `customer/account/active/acme-tech/profile.pdf`

**Formal Path Grammar (Extended Backus-Naur Form - EBNF):**

_The following formal grammar block defines the machine-readable path rules that automated tools, validation daemons,_
_and linters use to parse and verify LOGICS storage paths:_

```ebnf
(* Top-Level Storage Paths *)
logics_path         ::= [ root_prefix ] module "/" category "/" [ level4_entry ]
root_prefix         ::= [ group "/" ] company "/"

(* Canonical Fixed Levels 0 - 3 *)
group               ::= identifier
company             ::= identifier
module              ::= "administration" | "asset" | "customer" | "finance"
                      | "governance" | "knowledge" | "legal" | "marketing"
                      | "operation" | "people" | "product" | "project"
                      | "sale" | "service" | "technology" | "archive"
category            ::= identifier (* One of the 112 standardized category nouns *)

(* Dynamic Level 4 Entry Cascade *)
level4_entry        ::= subcategory_path | state_path | date_path | workspace_path | terminal_record

subcategory_path    ::= subcategory "/" [ state_path | date_path | workspace_path | terminal_record ]
state_path          ::= state "/" [ date_path | workspace_path | terminal_record ]
date_path           ::= date_partition "/" [ workspace_path | terminal_record ]
workspace_path      ::= workspace "/" [ terminal_record ]
terminal_record     ::= record_filename

(* Level 4 Token Identifiers *)
subcategory         ::= identifier
state               ::= "lead" | "prospect" | "active" | "paused"
                      | "review" | "closed" | "archived" | "draft"
workspace           ::= identifier
record_filename     ::= filename_stem "." extension
filename_stem       ::= identifier ( "." version_token | "-" version_token )*
version_token       ::= "v" [0-9]+ ( "." [0-9]+ )*

(* Date Partition Grammar *)
date_partition      ::= cal_year | cal_year_range | cal_month | cal_month_range
                      | cal_biannual | cal_biannual_range | cal_quarter | cal_quarter_range
                      | cal_week | cal_week_range | fiscal_year | fiscal_year_range
                      | fiscal_period | fiscal_period_range | custom_period | custom_period_range

cal_year            ::= DIGIT4
cal_year_range      ::= DIGIT4 "-" DIGIT4
cal_month           ::= DIGIT4 "-" MONTH2
cal_month_range     ::= DIGIT4 "-m" MONTH2 "-m" MONTH2 | DIGIT4 "-m" MONTH2 "-" DIGIT4 "-m" MONTH2
cal_biannual        ::= DIGIT4 "-b" ("1" | "2")
cal_biannual_range  ::= DIGIT4 "-b1-b2" | DIGIT4 "-b" ("1" | "2") "-" DIGIT4 "-b" ("1" | "2")
cal_quarter         ::= DIGIT4 "-q" QDIGIT
cal_quarter_range   ::= DIGIT4 "-q" QDIGIT "-q" QDIGIT | DIGIT4 "-q" QDIGIT "-" DIGIT4 "-q" QDIGIT
cal_week            ::= DIGIT4 "-w" WEEK_NUM
cal_week_range      ::= DIGIT4 "-w" WEEK_NUM "-w" WEEK_NUM | DIGIT4 "-w" WEEK_NUM "-" DIGIT4 "-w" WEEK_NUM
fiscal_year         ::= DIGIT4 "-fy"
fiscal_year_range   ::= DIGIT4 "-" DIGIT4 "-fy"
fiscal_period       ::= DIGIT4 "-f" PERIOD13
fiscal_period_range ::= DIGIT4 "-f" PERIOD13 "-f" PERIOD13 | DIGIT4 "-f" PERIOD13 "-" DIGIT4 "-f" PERIOD13
custom_period       ::= DIGIT4 "-p" PERIOD99
custom_period_range ::= DIGIT4 "-p" PERIOD99 "-p" PERIOD99 | DIGIT4 "-p" PERIOD99 "-" DIGIT4 "-p" PERIOD99

(* Lexical Terminals *)
identifier          ::= [a-z0-9]+ ( "-" [a-z0-9]+ )*
extension           ::= [a-z0-9]+
DIGIT4              ::= [0-9][0-9][0-9][0-9]
MONTH2              ::= "0" [1-9] | "1" [0-2]
QDIGIT              ::= "1" | "2" | "3" | "4"
WEEK_NUM            ::= [1-9] | "0" [1-9] | [1-4][0-9] | "5" [0-3]
PERIOD13            ::= [1-9] | "0" [1-9] | "1" [0-3]
PERIOD99            ::= [1-9] | "0" [1-9] | [1-9][0-9]
```

**Mandatory Ordering Rules:**

Within any Level 4 category path, entries MUST strictly follow the sequence
`subcategory -> state -> date -> workspace -> record`:

- **Strict Sequential Order:** A later entry type in the sequence (such as `workspace` or `record`) MUST NOT appear
  before an earlier entry type (such as `subcategory` or `state`).
- **Single Occurrence:** An entry type MUST NOT appear more than once within the same path.
- **Terminal Record:** A `record` is **strictly terminal**. It MUST always be the final element in any LOGICS record
  path; a directory MUST NOT be placed beneath a `record`.
- **Repository Boundary:** The repository container path itself (for example:
  `project/repository/active/logics/`) is a standard Level 4 workspace directory validated by LOGICS grammar.
  Files and source trees residing _inside_ that repository workspace boundary (such as `README.md`, `Makefile`, or
  `src/`) are completely exempt from LOGICS hierarchy rules as specified in Section 6.4.

**Invalid Ordering and Cascade Violation Examples:**

- `customer/account/acme-tech/active/` _(Invalid: workspace `acme-tech/` placed before state `active/`)_
- `finance/invoice/2026/payable/` _(Invalid: date `2026/` placed before subcategory `payable/`)_
- `legal/agreement/draft/2026-nda.pdf/review/` _(Invalid: directory `review/` placed beneath terminal record)_
- `sale/pipeline/prospect/lead/` _(Invalid: multiple state partitions within the same path)_
- `customer/account/active/2026-08-20/` _(Invalid: day-level directory partition prohibited per Section 4.3)_

### 5.2 Entry Type Transition and Promotion Rule

As business requirements and document collections expand, a Level 4 entry MAY transition from one entry type to another
to reflect new organizational needs:

1. **Dynamic Level 4 Structure:**
   A Level 4 entry may be modified, partitioned, or promoted. Most notably, when an individual leaf `record` accumulates
   supporting documents, attachments, or related files, it is promoted into a `workspace` container directory named
   after the record's filename stem (excluding extension) with the original record preserved inside it, as defined in
   Section 3.5. Similarly, a direct workspace or record path may be partitioned by inserting valid `subcategory`,
   `state`, or `date` entries above it.
2. **Strict Precedence and Naming Preservation:**
   Any path resulting from an entry type transition or promotion MUST strictly comply with the Level 4 Precedence
   Cascade (`subcategory -> state -> date -> workspace -> record`) and all canonical naming standards.
3. **Fixed Identity and Structure of Levels 0 through 3:**
   Levels 0 through 3 form the permanent structural namespace. While Level 4 entries are dynamic and may transition
   types, Levels 0, 1, 2, and 3 have fixed structural names and MUST NOT change their level type, structural position,
   or assigned canonical identity under any circumstances.

### 5.3 Valid and Compliant Path Examples

- `acme-tech/finance/invoice/2026/2026-08-20-invoice-001.pdf` - Single document in date partition.
- `acme-group/acme-media/customer/account/active/acme-tech/profile.pdf` - Multi-entity company with active workspace.
- `acme-software/project/repository/active/engine-core/` - Standard project repository workspace directory
  (internal contents such as `README.md` or source files are exempt per Section 6.4).
- `acme-corp/legal/agreement/draft/2026-partner-nda.pdf` - Draft legal agreement within lifecycle state.
- `acme-retail/finance/payroll/salary/2026-fy/annual-summary.csv` - Payroll record with subcategory and fiscal year.

### 5.4 Invalid Anti-Patterns and Violations

- `customer/account/acme-tech/active/` _(Invalid: workspace `acme-tech/` placed before state `active/`)_
- `finance/invoice/2026/payable/` _(Invalid: date `2026/` placed before subcategory `payable/`)_
- `legal/agreement/draft/2026-nda.pdf/review/` _(Invalid: directory `review/` placed beneath terminal record)_
- `sale/pipeline/prospect/lead/` _(Invalid: multiple state partitions within the same path)_
- `customer/account/active/2026-08-20/` _(Invalid: day-level directory partition prohibited per date partition rules)_

---

## 6 Security, Privacy, and Operational Considerations

LOGICS implementations MUST address the following security, privacy, and operational safeguards:

### 6.1 Data Privacy and Synthetic Information

- **Synthetic Data Requirement:** Public specifications, documentation, adoption profiles, and examples MUST contain
  exclusively synthetic, non-sensitive information.
- **Sensitive Data and Secret Isolation:** Access tokens, private cryptographic keys, API credentials, passwords, and
  confidential personnel records MUST NOT be exposed in open directories governed by LOGICS. Secret stores and key
  vaults must maintain isolated access perimeters.

### 6.2 Temporary Working Files and Directories

Temporary working files and directories are designated strictly for intermediate processing, transient operations, or
local staging. They are **non-canonical system artifacts** that exist outside the formal five-element Level 4 entry
namespace (`subcategory`, `state`, `date`, `workspace`, `record`). They do NOT constitute an independent Level 4 entry
type and must never be treated as permanent canonical records within the LOGICS architecture.

Any temporary directory or temporary file created within a LOGICS storage tree MUST use one of the following
standardized prefixes:

- **`temporary-`** (for example: `temporary-build/`, `temporary-export.csv`)
- **`scratch-`** (for example: `scratch-notes.md`, `scratch-data/`, `scratch-calc.xlsx`)
- **`working-`** (for example: `working-draft.md`, `working-pipeline/`, `working-summary.csv`)
- **`stage-`** (for example: `stage-output/`, `stage-render.mp4`, `stage-payload.json`)

_Rules Governing Temporary Working Artifacts:_

- **Non-Canonical Status:** Temporary files and directories are non-canonical transient artifacts. They exist outside
  the formal five Level 4 entry types and do not establish persistent structural hierarchy.
- **Standardized Temporary Prefixes:** The `temporary-`, `scratch-`, `working-`, and `stage-` prefixes form the
  closed vocabulary of recognized naming mechanisms for temporary artifacts within a LOGICS storage tree.
- **Prohibition of Alternate Schemes:** Other temporary naming conventions (such as `temp/`, `tmp/`, `.tmp/`,
  `.tmp-`, `scratch/`, or `_temp/`) are **strictly prohibited** within standard LOGICS storage directories unless
  explicitly mandated by an external toolchain under the system exemption in Section 6.3.
- **Transient Lifecycle:** Temporary artifacts are designated strictly for intermediate working stages, local
  processing, and transient caches; they must never be indexed as authoritative business records.

_Architectural Recommendation (State Partitions vs. Temporary Prefixes):_
Whenever business documents or project workspaces are undergoing active development, review, or provisional holding,
organizations are **strongly recommended** to use the standardized Level 4 `<state>` partitions (such as `draft/`,
`review/`, or `paused/` per Section 4.3.1.1) rather than manually prefixing every folder or file with temporary naming
prefixes. State directories provide clean, structural lifecycle management (for example:
`legal/agreement/draft/2026-nda.pdf`), allowing entities to transition seamlessly to `active/` or `archived/` without
requiring batch renaming of underlying files. The `temporary-`, `scratch-`, `working-`, and `stage-` prefixes should be
reserved primarily for disposable data exports, intermediate automated pipeline steps, and transient scratchpads.

### 6.3 Last Resort System Exemption

Characters outside the primary allowed character set (such as uppercase letters, underscores, or specific OS-required
symbols) are strictly prohibited unless genuinely required as an absolute last resort by an external system.

This exemption applies ONLY when an underlying operating system, compiler, version control system, or critical
software toolchain strictly demands a specific casing, filename, or symbol to function properly (for example:
`Dockerfile`, `.gitignore`, `LICENSE`, `Makefile`, `.git/`, `.agents/`, `.editorconfig`).

_Non-Canonical Status of System Metadata:_
System metadata, runtime configurations, and toolchain dotfiles fall under this technical exemption and exist strictly
**outside the canonical LOGICS Level 0 through Level 4 business hierarchy**. They represent infrastructure and tooling
enablers rather than authoritative business entities, categories, or records:

- **Distinction from Business Records:** System-exempt artifacts (such as `.gitignore` or `Makefile`) must never be
  indexed, categorized, or treated as standard business documents or canonical Level 4 `<record>` resources.
- **No Hierarchical Authority:** System metadata directories (such as `.agents/`, `.git/`, or `.vscode/`) do not
  constitute canonical Level 0 Groups, Level 1 Companies, Level 2 Modules, Level 3 Categories, or Level 4 structural
  entries.

_Strict Application and Documentation Requirements:_

- **No Convenience-Based Exemptions:** Deviations from standard LOGICS naming for personal preference, historical
  habit, or convenience are **strictly prohibited**.
- **Documented Justification:** Any non-standard filename introduced under this last-resort exemption must be
  genuinely mandated by the external toolchain and explicitly documented within the organization's governance or
  repository documentation as an approved technical exception.
- **Exhaustion of Compliant Options:** Whenever a compliant naming choice exists or is supported by the toolchain,
  the compliant lowercase alphanumeric format MUST be used.

### 6.4 The Repository Boundary and Code Exemption

Software source code trees, package dependencies, and development repositories contain file and folder naming
conventions dictated by programming languages and build toolchains. To accommodate technical codebases without
violating company architecture:

1. The repository workspace directory itself (for example: `project/repository/billing-engine/`) MUST strictly comply
   with all LOGICS naming rules.
2. The internal contents residing inside that repository directory are completely exempt from LOGICS naming rules,
   permitting language-specific casing, symbols, and vendor directory structures (for example:
   `project/repository/billing-engine/README.md` or `src/App_Controller.ts` is fully valid because it resides inside the
   exempted repository boundary).

---

## 7 Versioning, Evolution, and Deprecation Strategy

LOGICS specifications follow a discrete major-version evolution lifecycle:

### 7.1 Discrete Major Versioning Policy

All Libre Standards exclusively use **Discrete Major Versioning** (`V1`, `V2`, `V3`, ...):

- **No Semantic Versioning:** The Libre Standard framework strictly does NOT use semantic versioning (no minor or
  patch decimal numbers like `1.2.3`).
- **Major Version Releases (`V<N>`):** Each major version represents an authoritative, complete standard baseline.
  Any backward-incompatible structural changes, schema revisions, or vocabulary additions require the formal release
  of a new major version (for example: `V2`).
- **Working Draft Stage:** Active drafting and refinement occur under the current working draft stage before being
  frozen as a stable release.

### 7.2 Deprecation and Evolution Lifecycle

When a structure, token, schema, or rule is slated for retirement:

1. It is marked as **`DEPRECATED`** in the documentation and working notes of the current major version.
2. It remains part of the frozen specification for the duration of that major version to guarantee stability.
3. It is formally removed only in the subsequent major version release (for example: `V2`).

### 7.3 Lifecycle and Deprecation of Structural Identifiers (Levels 0-3)

Levels 0 through 3 are permanent structural identifiers. When a structural identifier at Level 0, 1, 2, or 3 is retired
or superseded by an organizational change:

1. **Deprecation Permitted:** An organization MAY mark a Level 0-3 structural identifier as deprecated.
2. **Permanent Reservation (No Reuse):** The identifier name and its historical identity remain permanently reserved. A
   deprecated identifier MUST NOT be reassigned, repurposed, or reused for another meaning.
3. **No Renaming, Moving, or Reassignment:** Renaming, moving, or reassigning Level 0-3 structural identifiers is
   strictly prohibited to preserve the permanent integrity of historical links and references.
4. **Historical Validity:** Existing records residing within deprecated structures remain valid and canonical. Unless
   explicitly permitted during a formal migration, deprecated structures must not receive new active entries.

---

## 8 Conformance and Verification Requirements

An implementation, storage system, toolchain, or daemon is considered **LOGICS Conforming** if and only if it satisfies
all mandatory clauses across the specification:

| Requirement ID   | Specification Clause | Level | Mandatory Requirement Summary                                    |
| :--------------- | :------------------- | :---- | :--------------------------------------------------------------- |
| `LOGICS-REQ-001` | §1 / §2              | MUST  | Follow five-level hierarchy and single canonical home principle. |
| `LOGICS-REQ-002` | §3                   | MUST  | Comply with lowercase alphanumeric names and character sets.     |
| `LOGICS-REQ-003` | §4                   | MUST  | Restrict structural identifiers to standard modules/categories.  |
| `LOGICS-REQ-004` | §5                   | MUST  | Conform to EBNF grammar and precedence cascade sequence.         |
| `LOGICS-REQ-005` | §6                   | MUST  | Enforce synthetic public data, secrets isolation, and prefixes.  |

---

[librecollective]: https://librecollective.github.io/
[librestandard]: https://librestandard.github.io/
[specification]: https://librestandard.github.io/standard/logics-v1.md
[documentation]: https://librestandard.github.io/documentation/logics/
[subcategoryreference]: https://librestandard.github.io/documentation/logics/subcategory-reference.md
[contributors]: https://github.com/librestandard/logics/graphs/contributors
[lsslv1]: https://librelicense.github.io/license/libre-single-source-license-v1.txt
[feedback]: https://github.com/orgs/librestandard/discussions/
