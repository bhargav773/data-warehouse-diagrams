# Data Warehouse ER Diagram (Mermaid) - Simplified

## Snowflake Schema with Essential Columns Only

```mermaid
erDiagram
    DIM_PRODUCT ||--o{ FACT_CONFIGURATION : "1:M"
    DIM_CUSTOMER ||--o{ FACT_CONFIGURATION : "M:1"
    DIM_CUSTOMER ||--o{ DIM_OPPORTUNITY : "1:M"
    DIM_OPPORTUNITY ||--o{ FACT_CONFIGURATION : "M:1"

    DIM_PRODUCT {
        string ProductID PK
        string ProductDescription
        string Tier1Product
        string Tier2Product
        string Tier3Product
        string Tier4Product
        string Tier5Product
        timestamp xact_timestamp
    }

    DIM_CUSTOMER {
        string CustomerID PK
        string CompanyName
        string BusOrg
        string EntTargetGroupInCountry
        string UltCustNm
        string UltCustNbr
        string CustEID
        string ExtRptRollup
        string AcctChannel
        string AcctSubChannel
        string MktVertical
        string MktSubVertical
        string TargetTier
        string TargetGroup
        string PricingTier
        decimal GM
        string SalesOffice
        string BusinessSegment
        string AcctOwnerFirstNm
        string AcctOwnerLastNm
        string AcctOwnerCUID
        string AcctOwnerEmail
        string AcctOwnerCountryCode
        string AcctOwnerRegion
        string AcctOwnerManager
        string AcctOwnerDirector
        timestamp merge_timestamp
    }

    DIM_OPPORTUNITY {
        string OpportunityID PK
        string CustomerID FK
        string OpportunityName
        string SMID
        string SalesRegion
        string PreDeploy
        string PreDeployStatus
        string PreDeploySelected
        string CampaignCode
        string PrimaryCampaignSource
        string CIESales
        string RVP
        string OpportunityOwnerVPNAME
        string SubType
        string SubTypeMotion
        string MigratingFromProduct
        string SalesClassification
        date ExpectedOrderCreateDate
        date CreatedDate
        date LastModifiedDate
        date OpportunityCloseDate
        string OpptyOwner
        string OpptyOwnerCUID
        string OpptyOwnerDir
        string OpptyOwnerEmail
        string OpptyOwnerCountryCode
        string OpptyOwnerRegion
        timestamp merge_timestamp
    }

    FACT_CONFIGURATION {
        string ConfigurationId PK
        string ProductID FK
        string CustomerID FK
        string OpportunityID FK
    }
```

## Relationship Details

### 1:M Relationships

#### DIM_PRODUCT → FACT_CONFIGURATION (1:M)
- One product can be associated with many configurations
- Product hierarchy (Tier1-5) enables drill-down analysis

#### DIM_CUSTOMER → DIM_OPPORTUNITY (1:M)
- One customer can have many opportunities
- Enables customer lifetime value analysis

#### DIM_CUSTOMER → FACT_CONFIGURATION (M:1)
- Many configurations belong to a single customer
- Customer master data centralized

#### DIM_OPPORTUNITY → FACT_CONFIGURATION (M:1)
- Many configurations can be associated with a single opportunity
- Links configurations back to sales opportunities

---

## Schema Overview

| Table | Columns | Purpose |
|-------|---------|---------|
| **DIM_PRODUCT** | 9 | Product master with 5-tier hierarchy |
| **DIM_CUSTOMER** | 26 | Customer/Account data from SFDC |
| **DIM_OPPORTUNITY** | 27 | Sales opportunity data from SFDC |
| **FACT_CONFIGURATION** | 4 | Key relationships (Bridge table) |

---

**Schema Type**: Snowflake Schema (Star Schema with normalized dimensions)  
**Total Columns**: 66  
**Last Updated**: 2026-06-04
