# Product-Master-Data-Management
End to end Product MDM case studies from production implementations.
3 Domains. 3 entity types. The same governanace discipline applied at increasing complexity.

CASE STUDIES

01 -> Payment failure MDM
Real time BFSI payment failure canonical taxonomy design, zero shared toxonomy, 10,000+ daily transactions.

The Core Problem: The GW-A called a timeout "GW_TIMEOUT". GW-B called the same event "CONNECTION_EXCEEDED". A third returned null by API design. No governance framework existed to resolve this.

KEY DOCUMENTS:
1. Entity-model.md - canonical payment failure entity (12 attributes, 8 categories)
2. Taxonomy-design.md - affinity mapping methodology and category design
3. STTM-payment-failure.csv: Source to target mapping across 3 sources
4. Governance-operating-model.md: 3 layer governance framework

Outcome: 40% faster investigation time, 81% Straight Through processing, 23%-->0.2% null rate in 4 sprints

02 --> Cusotmer 360 MDM
Informatica Cloud MDM (IDMC) Customer 360 implementation across 5 source systems. Survivorship design backed by the statistical profiling evidence.

The Anchor: RADD A-002, a pre-production architectural discovery that prevented 100,000+ ghost duplicate entity records.

KEY DOCUMENTS:
1. Entity-model.md - Customer golden record entity design
2. survivorship-design.md - Evidence based trsut score methodology
3. STTM-customer-360.csv - Mapping 150+ rows across 5 sources
4. RADD-CaseStudy.md - The pre-production catch that prevented 3 sprints of rework

Outcome: 4 on-time go lives, zero critical defects, 18hrs/week reclaimed, 12% campaign ROI improvement

03 --> Financial Product MDM
FinTech/BFSI product master data governance, fianncial products(securities, funds, creadit products). Based on pimcore open source platform.

Challenge: Regulatory attribute changes (RBI, SEBI, BASE III) require controlled update processes. Product attributes cannot be changed without compliance sign-off. This case study documents the governance pattern.

KEY DOCUMENTS:
1. Financial-product-entity-model.md - Product entity for a retail banking catalogue
2. Attribute-governance-guide.md - REJECT/ALERT/APPLY_RULE for product attributes
3. Regulatory-attribute-change-process.md - Change request process for regulated attributes.

Methodology: Profile first -> Design the entity model -> Design the STTM -> Build the governance operating model -> Define the DQ monitoring -> Document every decision with evidence -> Write rules for Data only the ones 've seen.
