# Data Warehouse ER Diagram (Mermaid) - Final Complete Schema

## Snowflake Schema (115-Column Fact Table with Complete Dimensions)

```mermaid
erDiagram
    DIM_PRODUCT ||--o{ FACT_CONFIGURATION : "1:M"
    DIM_LOCATION_ADDRESS ||--o{ FACT_CONFIGURATION : "1:M (LocationA)"
    DIM_LOCATION_ADDRESS ||--o{ FACT_CONFIGURATION : "1:M (LocationZ)"
    DIM_CUSTOMER ||--o{ FACT_CONFIGURATION : "M:1"
    DIM_CUSTOMER ||--o{ DIM_OPPORTUNITY : "1:M"
    DIM_OPPORTUNITY ||--o{ FACT_CONFIGURATION : "M:1"

    DIM_PRODUCT {
        string ProductID PK
        string ProductName
        string ProductDescription
        string Tier1Product
        string Tier2Product
        string Tier3Product
        string Tier4Product
        string Tier5Product
        string SourceSystem
        timestamp xact_timestamp
    }

    DIM_LOCATION_ADDRESS {
        string GLMLocId PK
        string LocationType PK "A or Z"
        string LocationName
        string Address
        string City
        string State
        string PostalCode
        string CountryCode
        string Country
        decimal Latitude
        decimal Longitude
        string GLMOriginalLocId
        string ReportRegion
        string RevenueCity
        string RevenueState
        string RevenueCountryCode
        timestamp xact_timestamp
    }

    DIM_CUSTOMER {
        string CustomerID PK "AcctID"
        string CompanyName "AcctNm"
        string AcctType
        string Industry
        string BusOrg
        string EntTargetGroupInCountry
        string UltCustNm
        string UltCustNbr
        string CustEID
        string DunsNbr
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
        string SalesRegion
        string AcctOwnerFirstNm
        string AcctOwnerLastNm
        string AcctOwnerTitle
        string AcctOwnerCUID
        string AcctOwnerEmail
        string AcctOwnerRegion
        string AcctOwnerCountryCode
        string AcctOwnerManager
        string AcctOwnerDirector
        timestamp merge_timestamp
    }

    DIM_OPPORTUNITY {
        string OpportunityID PK
        string SMID PK "QuoteID"
        string CustomerID FK
        string OpportunityName
        string RecordType
        string StageName
        string OpptyType
        string OpptySubType
        string CompetitorInfo
        string IsHighImpactOpportunity
        string HasOpportunityLineItem
        string IsQuoted "Y/N"
        string IsClosed "Y/N"
        string IsWon "Y/N"
        string ReasonWonLostComments
        string PrimaryLostReason
        string Competitor
        string OpptyOwner
        string OpptyOwnerDir
        string SourcingAdvisor
        string AcctNm
        string AcctType
        string BusOrg
        string EntTargetGroupInCountry
        string UltCustNm
        string UltCustNbr
        string CustEID
        string DunsNbr
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
        string SalesRegion
        date CreatedDate
        date LastModifiedDate
        date OpportunityCloseDate
        date SendToOrderDate
        decimal TotalNewSalesMRC_USD
        decimal TotalNetRecurring_USD
        decimal TotalNRC_USD
        decimal TotalContractMRC_USD
        decimal TotalYRC_USD
        decimal TotalRevenue_USD
        timestamp merge_timestamp
    }

    FACT_CONFIGURATION {
        string ConfigurationId PK
        string ProductID FK
        string CustomerID FK
        string OpportunityID FK
        string SMID FK "QuoteID-Composite"
        string LocationIdA FK "Type=A"
        string LocationIdZ FK "Type=Z"
        string OrderQuoteId
        string PriceDealId
        string SmEntityIdLink
        string UnitCostId
        int LineNumber
        string SourceName
        string EXTERNALQUOTEID
        string PriceDealEntityProductItemId
        string DealStatus
        string DealState
        int Term
        string PetraPricing "Y/N"
        string PetraPromo
        string ColtIgnore "Y/N"
        string DQPID
        string Ignore "Y/N"
        string ReportRegionA
        string ReportRegionZ
        string AccessTypeA
        string AccessTypeZ
        string VendorA
        string VendorZ
        date ProposalSignedDate
        date CreateDate
        date UpdateDate
        date QuoteCreateDate
        date QuoteUpdateDate
        decimal IntentA
        decimal IntentZ
        decimal AccessQuantity
        decimal PortQuantity
        decimal PortBW
        decimal AccessABW
        decimal AccessZBW
        decimal AccessASubBW
        decimal AccessZSubBW
        decimal TotalListMRC
        decimal TotalDiscountedMRC
        decimal TotalAmortizedMRC
        decimal AccessListMRC
        decimal AccessDiscountedMRC
        decimal AccessAmortizedMRC
        decimal TotalListNRC
        decimal TotalAmortizedNRC
        decimal AccessListNRC
        decimal AccessAmortizedNRC
        decimal GrossMargin
        decimal GrossMarginTarget
        string IsGrossMarginSatisfied
        decimal Payback
        decimal PaybackTarget
        string IsPaybackSatisfied
        decimal ROI
        decimal ROITarget
        decimal TotalDiscountedMRCwAmortized
        decimal AccessDiscountedMRCwAmortized
        decimal TotalListMrcOriginal
        decimal TotalCommit
        decimal TotalMRCFloor1
        decimal TotalMRCFloor2
        decimal TotalMRCFloor3
        decimal TotalNRCFloor1
        decimal TotalNRCFloor2
        decimal TotalNRCFloor3
        decimal AccessMRCFloor1
        decimal AccessMRCFloor2
        decimal AccessMRCFloor3
        decimal AccessNRCFloor1
        decimal AccessNRCFloor2
        decimal AccessNRCFloor3
        decimal TotalIncrementalMRCost
        decimal TotalIncrementalNRCost
        decimal TotalIncrementalCapexCost
        decimal AccessIncrementalMRCost
        decimal AccessIncrementalNRCost
        decimal AccessIncrementalCapexCost
        decimal TotalMonthlyProfitUSD
        decimal TotalInitialCashFlowUSD
        decimal TotalTermRevenueUSD
        decimal TotalTermEbitdaCostUSD
        decimal TotalTermEbitdaDollarsUSD
        decimal TotalTermVGMDollarsUSD
        string EmployeeName
        string UserId
        string EmployeeRegion
        string EmployeeCountry
        string OrganizationalUnit
        string FunctionDivision
        string IsManaged
        decimal DiscountPercent
        string CurrencyCode
        string CSGResponse
        string CalculationType
        string CrossFunctionalUnitCode
        string ChannelTypeId
        string HasCAR
        timestamp xact_timestamp
        string xact_username
        string RecordStatus
        date RecordModifiedDate
    }
```

---

## Complete Schema Overview

| Table | Columns | Key Features |
|-------|---------|--------------|
| **DIM_PRODUCT** | 10 | Product hierarchy (Tier1-5) + ProductName |
| **DIM_LOCATION_ADDRESS** | 17 | Composite PK (GLMLocId + LocationType), Geo data, Revenue info |
| **DIM_CUSTOMER** | 31 | Customer master, Account owner info, Duplication removed |
| **DIM_OPPORTUNITY** | 50 | Composite Key (OpptyID + SMID), Denormalized account data |
| **FACT_CONFIGURATION** | 115 | Complete metrics, floors, employee info, audit trail |

**Total: 223 columns** across **5 tables**

---

## FACT_CONFIGURATION (115 Columns) - Complete Breakdown

### Primary & Foreign Keys (7)
- ConfigurationId (PK)
- ProductID (FK → DIM_PRODUCT)
- CustomerID (FK → DIM_CUSTOMER)
- OpportunityID (FK → DIM_OPPORTUNITY)
- SMID (FK → DIM_OPPORTUNITY, Composite)
- LocationIdA (FK → DIM_LOCATION_ADDRESS, Type=A)
- LocationIdZ (FK → DIM_LOCATION_ADDRESS, Type=Z)

### Configuration Identifiers (14)
- OrderQuoteId, PriceDealId, SmEntityIdLink, UnitCostId
- LineNumber, SourceName, EXTERNALQUOTEID
- PriceDealEntityProductItemId, DealStatus, DealState
- Term, PetraPricing, PetraPromo, ColtIgnore
- DQPID, Ignore

### Location & Vendor (6)
- ReportRegionA, ReportRegionZ
- AccessTypeA, AccessTypeZ
- VendorA, VendorZ

### Dates (4)
- ProposalSignedDate, CreateDate, UpdateDate
- QuoteCreateDate, QuoteUpdateDate

### Intent Metrics (2)
- IntentA, IntentZ

### Quantities (7)
- AccessQuantity, PortQuantity, PortBW
- AccessABW, AccessZBW, AccessASubBW, AccessZSubBW

### Revenue MRC (6)
- TotalListMRC, TotalDiscountedMRC, TotalAmortizedMRC
- AccessListMRC, AccessDiscountedMRC, AccessAmortizedMRC

### Revenue NRC (4)
- TotalListNRC, TotalAmortizedNRC
- AccessListNRC, AccessAmortizedNRC

### Margin & Financial (12)
- GrossMargin, GrossMarginTarget, IsGrossMarginSatisfied
- Payback, PaybackTarget, IsPaybackSatisfied
- ROI, ROITarget
- TotalDiscountedMRCwAmortized, AccessDiscountedMRCwAmortized
- TotalListMrcOriginal, TotalCommit

### Floors (12)
- TotalMRCFloor1-3, TotalNRCFloor1-3
- AccessMRCFloor1-3, AccessNRCFloor1-3

### Incremental Costs (6)
- TotalIncrementalMRCost, TotalIncrementalNRCost, TotalIncrementalCapexCost
- AccessIncrementalMRCost, AccessIncrementalNRCost, AccessIncrementalCapexCost

### Term Revenue (5)
- TotalMonthlyProfitUSD, TotalInitialCashFlowUSD
- TotalTermRevenueUSD, TotalTermEbitdaCostUSD
- TotalTermEbitdaDollarsUSD, TotalTermVGMDollarsUSD

### Employee Info (7)
- EmployeeName, UserId, EmployeeRegion
- EmployeeCountry, OrganizationalUnit
- FunctionDivision, IsManaged

### Miscellaneous (7)
- DiscountPercent, CurrencyCode, CSGResponse
- CalculationType, CrossFunctionalUnitCode
- ChannelTypeId, HasCAR

### Audit (4)
- xact_timestamp, xact_username
- RecordStatus, RecordModifiedDate

---

## Key Relationships

### Composite Keys
```
DIM_OPPORTUNITY: OpportunityID + SMID
FACT_CONFIGURATION: OpportunityID + SMID (Foreign Key)
```

### Location Support
```
DIM_LOCATION_ADDRESS: GLMLocId + LocationType (Composite PK)
FACT_CONFIGURATION: LocationIdA, LocationIdZ (separate references)
```

### Denormalization Strategy
- **DIM_OPPORTUNITY**: Includes denormalized account attributes (AcctNm, BusOrg, etc.)
- **FACT_CONFIGURATION**: Complete metric family for analysis

---

**Schema Type**: Snowflake Schema with Composite Keys & Denormalized Dimensions  
**Total Columns**: 223  
**Last Updated**: 2026-06-05  
**Version**: Final Production Schema
