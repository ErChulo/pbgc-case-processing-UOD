# PBGC Case Processing Universe of Discourse

**Version:** v0.7  
**Repository:** `ErChulo/pbgc-case-processing-UOD`

This repository is a semantic and computational workbench for understanding, mapping, visualizing, and eventually implementing the provisions of terminated defined-benefit pension plans in a Pension Benefit Guaranty Corporation style case-processing environment.

The repository is organized around one central idea:

```text
Plan documents + case artifacts
        ↓
Defined terms + plan provisions + data elements
        ↓
Canonical Pension Benefit Guaranty Corporation concept map
        ↓
Clusters, dependency graphs, set maps, distance measures
        ↓
Implementation logic for benefit calculation, validation, and review
```

The practical goal is to reduce a pension plan from dense legal prose into a structured universe of concepts that can be queried, compared, visualized, and translated into calculation logic.

---

## Purpose

This project supports the analysis of any defined-benefit pension plan by extracting and organizing the following objects:

1. **Defined Terms**  
   Terms explicitly defined in the plan document, such as `Accrued Benefit`, `Actuarial Equivalent`, `Average Compensation`, `Credited Service`, `Normal Retirement Date`, `Early Retirement Date`, `Spouse`, `Beneficiary`, and related terms.

2. **Plan Provisions**  
   Rules governing eligibility, participation, benefit accrual, vesting, retirement dates, early retirement, late retirement, disability, death benefits, payment forms, lump sums, required beginning dates, top-heavy provisions, benefit restrictions, and termination provisions.

3. **Pension Benefit Guaranty Corporation Concepts**  
   A canonical field-level vocabulary drawn from the data dictionary artifact, including fields for dates, ages, service, compensation, benefits, forms, lump sums, offsets, guarantees, liabilities, entitlement priority categories, input fields, calculated fields, and system-generated fields.

4. **Calculation and Implementation Primitives**  
   Concepts that can be mapped to spreadsheet formulas, actuarial add-in functions, engine fields, validation checks, and dependency graphs.

5. **Semantic Geometry**  
   Distances, clusters, concept maps, and graph structures that show how plan concepts relate to one another.

The repository is not merely a document archive. It is intended to become a reusable framework for turning plan language into formal, inspectable, and computable structures.

---

## Core Mathematical View

Let a pension plan be represented as:

```text
P = (D, R, F, A)
```

where:

- `D` = defined terms;
- `R` = operative rules and plan provisions;
- `F` = data fields required for calculation;
- `A` = actuarial assumptions and calculation primitives.

Let:

```text
U = canonical Pension Benefit Guaranty Corporation universe of discourse
```

The main mapping problem is:

```text
φ : D ∪ R ∪ F ∪ A → U
```

That is, each extracted plan concept is mapped to one or more canonical case-processing concepts.

Once this mapping exists, the project can compute:

```text
semantic similarity
set membership distance
graph dependency distance
implementation distance
benefit entitlement distance
```

between plans, plan versions, engines, data dictionaries, and benefit-calculation artifacts.

---

## Completed Project Artifacts Used as Examples

The current project has already produced or uses the following artifacts as working examples.

### 1. Canonical concept dictionary

`DD-no-UDFs-subsets-indicators.csv`

This file is the main concept table. It contains:

- `FIELD_NAME`
- `DESCRIPTION`
- `DATA_TYPE`
- `FIELD_SIZE`
- set-membership indicators such as age, service, compensation, benefit, form, lump sum, liability, guaranteed benefit, priority category, date, input, calculated, validation, system-generated, and add-in function fields.

This file is the base universe for semantic mapping, field classification, clustering, and set-theoretic visualization.

### 2. Pension Benefit Guaranty Corporation actuarial add-in documentation

`BCV ATPBGC (Add-ins).pdf`

This file documents actuarial spreadsheet functions used as calculation primitives. Examples include:

- age functions;
- retirement date functions;
- required beginning date functions;
- service functions;
- vesting functions;
- early retirement factors;
- late retirement factors;
- actuarial equivalence and present value related functions.

This artifact connects abstract plan provisions to executable calculation components.

### 3. Sample pension plan documents

The project includes several plan documents used as source material for extraction and comparison:

- `2019 Plan Document.pdf`
- `2011 - Plan Document.pdf`
- `2003-Plan Document-UChargers.pdf`
- `2011-Plan Document-UChargers.pdf`

These documents are used to extract defined terms, article structures, benefit formulas, payment forms, death benefits, disability provisions, top-heavy rules, actuarial equivalence assumptions, and retirement eligibility conditions.

### 4. Directed graph visualization template

`d3-force-layout-template.html`

This artifact is used to display dependency graphs, concept maps, and engine field flows. Nodes can represent plan terms, data fields, spreadsheet cells, calculation outputs, benefit provisions, or canonical concepts. Edges can represent definition-dependence, formula-dependence, semantic dependence, or calculation flow.

### 5. Set visualization templates

`subsets.html`  
`index.html`  
`venn.js`

These artifacts support set-theoretic visualization of concept families. For example:

```text
BENEFIT_FIELD ∩ FORM_FIELD
SERVICE_FIELD ∩ CALCULATED_FIELD
LIABILITY_FIELD ∩ GUARANTEED_BENEFIT_FIELD
QPSA_FIELD ∩ DEATH_BENEFIT_FIELD
INPUT_FIELD ∩ DATE_FIELD
```

The purpose is to make the geometry of the data dictionary visible.

---

## Analyses Supported by This Repository

### 1. Defined Terms extraction

For any plan document, the repository can support extraction of the plan's defined terms into a structured table:

```text
term | section | exact text | normalized meaning | referenced terms | canonical concept candidates
```

Typical questions:

- Which terms are primitive?
- Which terms are composite?
- Which terms define other terms?
- Which terms are circular or mutually dependent?
- Which terms are central to the calculation of benefits?

Graph interpretation:

```text
Term A → Term B
```

means that the definition or operation of `Term A` depends on `Term B`.

This produces a defined-terms directed graph.

---

### 2. Plan provision extraction

The repository can support extraction of operative rules, including:

- eligibility and participation;
- vesting service;
- credited service;
- benefit service;
- compensation and average compensation;
- accrued benefit formula;
- normal retirement benefit;
- early retirement benefit;
- deferred vested benefit;
- late retirement adjustment;
- disability benefit;
- pre-retirement death benefit;
- post-retirement death benefit;
- normal form of payment;
- optional forms of payment;
- lump-sum cash-out rules;
- required beginning date rules;
- top-heavy rules;
- benefit restrictions;
- amendment and termination provisions.

A provision can be normalized as:

```text
provision = condition → entitlement → amount → form → commencement → adjustment
```

Example pattern:

```text
If participant satisfies early-retirement eligibility
then participant may commence early retirement benefit
with accrued benefit adjusted by early-retirement factor
payable in permitted form of payment.
```

---

### 3. Semantic mapping to canonical Pension Benefit Guaranty Corporation fields

Each extracted plan term or provision can be mapped to canonical fields from the data dictionary.

Example mappings:

```text
Normal Retirement Date      → NRD_FIELD / retirement date concept
Date of Hire                → DOH / input date concept
Date of Participation       → DOP / participation date concept
Credited Service            → SERVICE_FIELD / calculated service concept
Average Compensation        → COMPENSATION_FIELD / benefit formula input
Accrued Monthly Benefit     → BENEFIT_FIELD / amount concept
Joint and Survivor Annuity  → FORM_FIELD / annuity form concept
Required Beginning Date     → RBD_FIELD / statutory commencement concept
```

The mapping should preserve evidence:

```text
source text → extracted concept → canonical field → implementation use
```

The governing rule is:

```text
No source sentence ⇒ no asserted plan rule.
```

---

### 4. Concept clustering

The repository supports clustering of concepts by:

- semantic similarity of descriptions;
- data type;
- field-size structure;
- set-membership indicators;
- provision category;
- graph adjacency;
- calculation dependency;
- plan-document location.

Possible methods:

- term-sentence embeddings;
- hierarchical clustering;
- principal component analysis;
- multidimensional scaling;
- uniform manifold approximation and projection;
- graph layout algorithms;
- nearest-neighbor search;
- cosine distance;
- Jaccard distance over set indicators.

Typical outputs:

```text
2-dimensional semantic map
3-dimensional semantic map
cluster table
nearest-neighbor table
minimum spanning tree
concept dendrogram
```

---

### 5. Concept maps and dependency graphs

The repository can generate several graph types.

#### Defined-terms graph

```text
Defined Term → Defined Term used in its definition
```

Purpose: identify primitive and composite terms.

#### Plan-provision graph

```text
Eligibility condition → Benefit entitlement → Benefit amount → Form of payment
```

Purpose: identify the architecture of the plan promise.

#### Field dependency graph

```text
Input field → Intermediate calculated field → Output field
```

Purpose: identify what data must exist before a benefit can be computed.

#### Engine comparison graph

```text
Engine 1 concept → Canonical concept ← Engine 2 concept
```

Purpose: compare two implementation summaries without requiring identical field names.

---

### 6. Set-theoretic analysis of fields

The data dictionary permits field subsets such as:

```text
AGE_FIELD
SERVICE_FIELD
COMPENSATION_FIELD
BENEFIT_FIELD
FORM_FIELD
LUMP_SUM_FIELD
OFFSET_FIELD
QPSA_FIELD
LIABILITY_FIELD
INPUT_FIELD
CALCULATED_FIELD
SYSTEM_GENERATED_FIELD
```

The repository can compute:

```text
intersection size
union size
Jaccard similarity
Jaccard distance
subset inclusion
exclusive membership
field overlap matrix
```

Example:

```text
J(A, B) = |A ∩ B| / |A ∪ B|
d(A, B) = 1 - J(A, B)
```

This is useful for discovering hidden relationships among calculation domains.

---

### 7. Plan-to-plan and engine-to-engine comparison

The repository can compare two plans or two engine summaries using layered distances.

Let `E1` and `E2` be two summarized engines.

A useful comparison decomposes into:

```text
D(E1, E2) = weighted combination of:

1. benefit entitlement distance
2. architecture distance
3. implementation distance
4. semantic mapping distance
5. missing-artifact penalty
```

Interpretation:

- **Benefit entitlement distance** compares what benefits exist.
- **Architecture distance** compares the branching structure of entitlement logic.
- **Implementation distance** compares fields, formulas, tabs, and calculation order.
- **Semantic mapping distance** compares whether different labels mean the same pension concept.
- **Missing-artifact penalty** measures how much cannot be inferred from available evidence.

This is essential when one plan has an approved implementation and a new plan needs a first-pass design.

---

### 8. Historical restatement comparison

When multiple plan documents exist for the same plan, the repository can compare provisions across restatements.

Example comparisons:

```text
2003 plan document → 2011 plan document
2011 plan document → 2019 plan document
```

Possible outputs:

```text
changed defined terms
changed actuarial equivalence assumptions
changed normal retirement provisions
changed early retirement provisions
changed optional forms
changed death benefits
changed disability rules
changed lump-sum rules
changed required beginning date provisions
changed top-heavy provisions
```

This helps determine which document governs a participant based on date of termination, retirement, death, or other relevant status date.

---

### 9. Data sufficiency and missing-artifact analysis

The repository can also classify whether a plan can be implemented from the available artifacts.

Typical required artifacts:

```text
plan document
amendments
summary plan description
prior benefit calculation engine
prior data element listing
benefit statement samples
population data layout
sample participant records
annuity form table
actuarial equivalence assumptions
interest and mortality assumptions
letter-generation configuration
approved case memo or review notes
```

The output is not merely:

```text
complete / incomplete
```

but rather:

```text
which provision is blocked
which field is missing
which assumption is missing
which participant class is affected
which calculation cannot be independently reproduced
```

---

### 10. Audit trail and validation analysis

Every extracted concept should be traceable by this chain:

```text
plan source location
        ↓
quoted source language
        ↓
normalized provision
        ↓
canonical concept
        ↓
calculation field
        ↓
formula or function
        ↓
output value
```

This supports review, validation, and reproducibility.

---

## Example Use Cases

### Use case 1: Explain the plan promise quickly

Given a plan document, extract:

```text
who is covered
when participation begins
how service is counted
how the accrued benefit is calculated
when benefits can commence
what forms are available
what death benefits exist
what actuarial assumptions apply
```

### Use case 2: Build a benefit entitlement map

Construct a state and entitlement map for:

```text
active participant
terminated vested participant
retired participant
disabled participant
surviving spouse
beneficiary
alternate payee
```

### Use case 3: Map plan language to engine fields

Convert plan terms to canonical case-processing fields:

```text
date fields
age fields
service fields
compensation fields
form fields
benefit amount fields
liability fields
priority category fields
```

### Use case 4: Compare two plan versions

Determine which provisions changed and whether the change affects:

```text
eligibility
service
accrual
vesting
normal retirement
early retirement
late retirement
death benefits
optional forms
lump sums
actuarial equivalence
```

### Use case 5: Compare two engines

Compare two summarized calculation engines by asking:

```text
Do they compute the same benefit entitlements?
Do they use the same canonical concepts?
Do they branch on the same participant states?
Do they require the same input data?
Do they produce comparable outputs?
```

---

## Proposed Repository Structure

```text
pbgc-case-processing-UOD/
│
├── README.md
│
├── data/
│   ├── raw/                  # original plan documents and source artifacts
│   ├── dictionary/           # canonical concept dictionaries
│   ├── extracted/            # extracted defined terms and provisions
│   └── normalized/           # normalized concept tables
│
├── mappings/
│   ├── plan_to_dictionary/   # plan concept → canonical field mappings
│   ├── field_aliases/        # label normalization and synonym tables
│   └── engine_mappings/      # engine field → canonical field mappings
│
├── graphs/
│   ├── defined_terms/        # term-dependency graphs
│   ├── provisions/           # provision and entitlement graphs
│   ├── fields/               # field-dependency graphs
│   └── engines/              # engine-comparison graphs
│
├── visualizations/
│   ├── force_graphs/         # D3.js force-directed maps
│   ├── venn/                 # set-overlap visualizations
│   ├── clusters/             # two-dimensional and three-dimensional maps
│   └── dashboards/           # exploratory browser interfaces
│
├── reports/
│   ├── plan_summaries/       # readable plan summaries
│   ├── comparison_reports/   # plan-to-plan and engine-to-engine comparisons
│   └── validation/           # audit trails and missing-artifact reports
│
└── src/
    ├── extraction/           # parsing and extraction scripts
    ├── clustering/           # semantic and set-theoretic clustering
    ├── graphing/             # graph construction utilities
    └── export/               # output writers
```

This structure is aspirational and may evolve as the repository matures.

---

## Visualization Targets

The project emphasizes visual understanding.

Supported visualization families:

```text
Venn and Euler diagrams
force-directed graphs
directed acyclic graphs
minimum spanning trees
semantic scatterplots
cluster dendrograms
field-overlap matrices
topological ordering diagrams
state-machine diagrams
```

The preferred visualization stack includes:

```text
D3.js
Graphviz
Graphology with Sigma.js
Plotly.js
Three.js
Mermaid
Python
R
Wolfram Language
```

The strongest preference is for local, single-file, browser-readable artifacts whenever possible.

---

## What This Repository Is Not

This repository is not:

- an official Pension Benefit Guaranty Corporation system;
- a substitute for legal review;
- a substitute for enrolled actuary review;
- a final benefit determination system;
- a secure repository for participant-level protected data.

Do not commit protected participant data, personally identifiable information, or confidential production files unless the repository is private and appropriately controlled.

---

## Guiding Rule

The project should preserve this invariant:

```text
plan text evidence
    precedes
semantic interpretation
    precedes
canonical mapping
    precedes
calculation logic
    precedes
numerical output
```

In short:

```text
No evidence → no rule.
No rule → no calculation.
No calculation → no liability conclusion.
```

---

## Long-Term Objective

The long-term objective is to make plan comprehension and case-processing design less opaque by building a formal bridge between:

```text
legal pension language
actuarial benefit promises
Pension Benefit Guaranty Corporation data fields
calculation engines
visual concept geometry
```

The repository should eventually allow a user to upload a new plan document and receive:

```text
1. a defined-terms table;
2. a provision summary;
3. a canonical concept mapping;
4. a benefit entitlement map;
5. a missing-data report;
6. a graph of dependencies;
7. a similarity measure against prior plans or engines;
8. a first-pass implementation specification.
```

That is the working definition of the Pension Benefit Guaranty Corporation case-processing universe of discourse.
