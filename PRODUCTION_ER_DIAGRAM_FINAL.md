# Data Warehouse ER Diagram - Final Production Schema v3.1

## Complete Snowflake Schema (Optimized) - Final

```mermaid
erDiagram
    DIM_PRODUCT ||--o{ FACT_CONFIGURATION : "1:M"
    DIM_LOCATION_ADDRESS ||--o{ FACT_CONFIGURATION : "1:M (LocationA)"
    DIM_LOCATION_ADDRESS ||--o{ FACT_CONFIGURATION : "1:M (LocationZ)"
    DIM_CUSTOMER ||--o{ FACT_CONFIGURATION : "M:1"
    DIM_CUSTOMER ||--o{ DIM_OPPORTUNITY : "1:M"
    DIM_OPPORTUNITY ||--o{ FACT_CONFIGURATION : "M:1 (Composite FK)"

    DIM_PRODUCT {
        string ProductID PK
        string Product "ProductName"
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
        string GLMLocId PK "GLMLocIdA/Z"
        string LocationType PK "A or Z"
        string LocationName "LocationNameA/Z"
        string Address "AddressA/Z"
        string City "CityA/Z"
        string State "StateA/Z"
        string PostalCode "PostalCodeA/Z"
        string CountryCode "CountryCodeA/Z"
        string Country "CountryA/Z"
        decimal Latitude "LatitudeA/Z"
        decimal Longitude "LongitudeA/Z"
        string GLMOriginalLocId "GLMOriginalLocIdA/Z"
        string ReportRegion "ReportRegionA/Z"
        string RevenueCity "RevenueCityA/Z"
        string RevenueState "RevenueStateA/Z"
        string RevenueCountryCode "RevenueCountryCodeA/Z"
        int ADDRESS_ID "GLMShort"
        string SITE_ID "GLMShort"
        string STREET_NUMBER "GLMShort"
        string STREET_NUMBER_FRACTION "GLMShort"
        string STREET_DIRECTION_PREFIX "GLMShort"
        string STREET_NAME "GLMShort"
        string STREET_NAME_SUFFIX "GLMShort"
        string STREET_DIRECTION_SUFFIX "GLMShort"
        string ADDRESS_LINE1 "GLMShort"
        string CITY "GLMShort"
        string STATE "GLMShort"
        string POSTAL_CODE "GLMShort"
        string COUNTRY_CODE "GLMShort"
        decimal LATITUDE "GLMShort"
        decimal LONGITUDE "GLMShort"
        string CLONES_CLLI_PREFIX "GLMShort"
        string WIRE_CENTER_CLLI "GLMShort"
        string IS_ON_NET "GLMShort"
        string LocalAccess "GLMShort"
        string PRICINGREGION "GLMShort"
        string PRICINGSUBREGION "GLMShort"
        string PRICINGAREA "GLMShort"
        string ETHERNET "GLMShort"
        string WAVE "GLMShort"
        string TDM "GLMShort"
        string NETWORK "GLMShort"
        string BULIDING_STRUCTURE "GLMShort"
        string BUILDING_PROGRAM "GLMShort"
        string OCN_TYPE "GLMShort"
        string CONNECTION_TYPE "GLMShort"
        int SITE_COMPETITIVE_ENVIRON_ID "GLMShort"
        string METRO_3 "GLMShort"
        string LUMEN_NETWORK "GLMShort"
        string LOADTIME "GLMShort"
        timestamp xact_timestamp
    }

    DIM_CUSTOMER {
        string CustomerID PK "BusOrgID"
        string CompanyName
        string Industry
        string SfdcAcctNm
        string SfdcAcctChannel
        string SfdcAcctSubChannel
        string SfdcMktVertical
        string SfdcMktSubVertical
        string SfdcTargetTier
        string SfdcTargetGroup
        string SfdcPricingTier
        decimal SfdcGM
        string SfdcSalesOffice
        string SfdcAcctOwnerFirstNm
        string SfdcAcctOwnerLastNm
        string SfdcAcctOwnerTitle
        string SfdcBusOrg
        string SfdcUltCustNm
        string SfdcUltCustNbr
        string SfdcCustEID
        string SfdcDunsNbr
        string SfdcExtRptRollup
        string SfdcBusinessSegment
        string SfdcSalesRegion
        timestamp CreatedTimestamp
    }

    DIM_OPPORTUNITY {
        string OpportunityID PK "SfdcOpportunityID"
        string QuoteID PK "SfdcSMID"
        string CustomerID FK "SfdcAccountID"
        string OpportunityName "SfdcOpportunityName"
        string StageName "SfdcStageName"
        string OpptySubType "SfdcSubType"
        string IsClosed "SfdcIsClosed"
        string IsWon "SfdcIsWon"
        int IsActive "SfdcIsActive"
        string QuoteSystem "SfdcSourceSystem"
        string SalesClassification "SfdcSalesClassification"
        string AcctNm "SfdcAcctNm"
        string BusOrg "SfdcBusOrg"
        string UltCustNm "SfdcUltCustNm"
        string UltCustNbr "SfdcUltCustNbr"
        string CustEID "SfdcCustEID"
        string DunsNbr "SfdcDunsNbr"
        string ExtRptRollup "SfdcExtRptRollup"
        string AcctChannel "SfdcAcctChannel"
        string AcctSubChannel "SfdcAcctSubChannel"
        string MktVertical "SfdcMktVertical"
        string MktSubVertical "SfdcMktSubVertical"
        string TargetTier "SfdcTargetTier"
        string TargetGroup "SfdcTargetGroup"
        string PricingTier "SfdcPricingTier"
        decimal GM "SfdcGM"
        string SalesOffice "SfdcSalesOffice"
        string SalesRegion "SfdcSalesRegion"
        string BusinessSegment "SfdcBusinessSegment"
        timestamp CreatedTimestamp
    }

    FACT_CONFIGURATION {
        string ConfigurationId PK
        string ProductID FK "refs DIM_PRODUCT"
        string BusOrgID FK "refs DIM_CUSTOMER"
        string OpportunityID FK "Composite Key"
        string QuoteID FK "Composite Key"
        string GLMLocIdA FK "refs DIM_LOCATION_ADDRESS(Type=A)"
        string GLMLocIdZ FK "refs DIM_LOCATION_ADDRESS(Type=Z)"
        string PriceDealId
        string UnitCostId
        string ProductDescription
        string DealState
        int Term
        decimal AccessQuantity
        string CompanyName
        string AddressA
        string CityA
        string StateA
        string PostalCodeA
        string CountryCodeA
        string ReportRegionA
        string AddressZ
        string CityZ
        string StateZ
        string PostalCodeZ
        string CountryCodeZ
        string ReportRegionZ
        decimal AccessABW
        decimal AccessZBW
        decimal PortQuantity
        decimal PortBW
        string SourceSystem
        decimal GrossMargin
        decimal Payback
        decimal TotalListMRC
        decimal TotalDiscountedMRC
        decimal TotalAmortizedMRC
        decimal TotalListNRC
        decimal TotalAmortizedNRC
        decimal TotalIncrementalMRCost
        decimal TotalIncrementalNRCost
        decimal TotalIncrementalCapexCost
        string AccessTypeA
        string AccessTypeZ
        decimal AccessListMRC
        decimal AccessDiscountedMRC
        decimal AccessAmortizedMRC
        decimal AccessListNRC
        decimal AccessAmortizedNRC
        decimal AccessIncrementalMRCost
        decimal AccessIncrementalNRCost
        decimal AccessIncrementalCapexCost
        decimal TotalTermRevenueUSD
        decimal TotalTermEbitdaCostUSD
        decimal TotalTermEbitdaDollarsUSD
        string CurrencyCode
        string EmployeeName
        string Ignore "Y/N"
        decimal AccessASubBW
        decimal AccessZSubBW
        string PriceDealEntityProductItemId
        string VendorA
        string VendorZ
        int LineNumber
        decimal TotalCommit
        string xact_username
        timestamp xact_timestamp
        string SourceName
        string EXTERNALQUOTEID
        string PetraPricing "Y/N"
        string ColtIgnore "Y/N"
        string GLMOriginalLocIdA
        string GLMOriginalLocIdZ
        string DQPID
        decimal IntentA
        decimal IntentZ
        string Tier1Product
        string Tier2Product
        string Tier3Product
        string Tier4Product
        string Tier5Product
        decimal TotalDiscountedMRCwAmortized
        decimal AccessDiscountedMRCwAmortized
        date QuoteCreateDate
        date QuoteUpdateDate
        decimal TotalListMrcOriginal
    }
```

---

## Final Production Schema v3.1

### Schema Architecture

#### **DIM_PRODUCT** (10 Columns)
Product master dimension with simplified naming

| # | Column | Type | Description |
|---|--------|------|-------------|
| 1 | ProductID | STRING | Product identifier (PK) |
| 2 | Product | STRING | ProductName |
| 3 | ProductDescription | STRING | Detailed description |
| 4-8 | Tier1-5Product | STRING | Hierarchy levels |
| 9 | SourceSystem | STRING | Source system |
| 10 | xact_timestamp | TIMESTAMP | Audit timestamp |

---

#### **DIM_LOCATION_ADDRESS** (51 Columns)
Location dimension with composite key (GLMLocId + LocationType) and complete GLMShort integration

**Core Location with A/Z Denormalization (16 cols)**
- GLMLocId (Composite PK), LocationType (Composite PK)
- LocationName, Address, City, State, PostalCode
- CountryCode, Country, Latitude, Longitude
- GLMOriginalLocId, ReportRegion
- RevenueCity, RevenueState, RevenueCountryCode

**GLMShort Street Data (9 cols)**
- ADDRESS_ID, SITE_ID, STREET_NUMBER, STREET_NUMBER_FRACTION
- STREET_DIRECTION_PREFIX, STREET_NAME, STREET_NAME_SUFFIX
- STREET_DIRECTION_SUFFIX, ADDRESS_LINE1

**GLMShort Geographic Data (5 cols)**
- CITY, STATE, POSTAL_CODE, COUNTRY_CODE
- LATITUDE, LONGITUDE

**GLMShort Telecom Data (2 cols)**
- CLONES_CLLI_PREFIX, WIRE_CENTER_CLLI

**GLMShort Network Capabilities (8 cols)**
- IS_ON_NET, LocalAccess, ETHERNET, WAVE
- TDM, NETWORK, BULIDING_STRUCTURE, BUILDING_PROGRAM

**GLMShort Business Classifications (7 cols)**
- PRICINGREGION, PRICINGSUBREGION, PRICINGAREA
- OCN_TYPE, CONNECTION_TYPE, SITE_COMPETITIVE_ENVIRON_ID
- METRO_3, LUMEN_NETWORK

**Audit (2 cols)**
- LOADTIME, xact_timestamp

---

#### **DIM_CUSTOMER** (24 Columns)
Account master dimension (simplified)

**Core Account (2 cols)**
- CustomerID (PK) "BusOrgID"
- CompanyName

**Industry Classification (1 col)** ⭐
- Industry

**Account Classification (8 cols)**
- SfdcAcctChannel, SfdcAcctSubChannel
- SfdcMktVertical, SfdcMktSubVertical
- SfdcTargetTier, SfdcTargetGroup
- SfdcPricingTier, SfdcGM

**Account Office & Region (2 cols)**
- SfdcSalesOffice, SfdcSalesRegion

**Account Owner (3 cols)**
- SfdcAcctOwnerFirstNm, SfdcAcctOwnerLastNm
- SfdcAcctOwnerTitle

**Business Organization (5 cols)**
- SfdcBusOrg, SfdcUltCustNm, SfdcUltCustNbr
- SfdcCustEID, SfdcDunsNbr

**Miscellaneous (2 cols)**
- SfdcExtRptRollup, SfdcBusinessSegment

**Audit (1 col)**
- CreatedTimestamp

---

#### **DIM_OPPORTUNITY** (30 Columns)
Opportunity dimension with composite key (OpportunityID + QuoteID)

**Primary Keys (2 cols)**
- OpportunityID (PK) "SfdcOpportunityID"
- QuoteID (PK) "SfdcSMID"

**Foreign Keys (1 col)**
- CustomerID (FK) "SfdcAccountID"

**Opportunity Info (8 cols)**
- OpportunityName, StageName, OpptySubType
- IsClosed, IsWon, IsActive
- QuoteSystem, SalesClassification

**Denormalized Account Data (18 cols)**
- AcctNm, BusOrg, UltCustNm, UltCustNbr
- CustEID, DunsNbr, ExtRptRollup
- AcctChannel, AcctSubChannel
- MktVertical, MktSubVertical
- TargetTier, TargetGroup, PricingTier
- GM, SalesOffice, SalesRegion, BusinessSegment

**Audit (1 col)**
- CreatedTimestamp

---

#### **FACT_CONFIGURATION** (67 Columns)
Central fact table with optimized metrics

**Keys (7 cols)**
- ConfigurationId (PK)
- ProductID (FK → DIM_PRODUCT)
- BusOrgID (FK → DIM_CUSTOMER)
- OpportunityID, QuoteID (FK → DIM_OPPORTUNITY - Composite)
- GLMLocIdA, GLMLocIdZ (FK → DIM_LOCATION_ADDRESS)

**Configuration & Deal (10 cols)**
- PriceDealId, UnitCostId, ProductDescription
- DealState, Term, PriceDealEntityProductItemId
- LineNumber, SourceName, EXTERNALQUOTEID, DQPID

**Product Hierarchy (5 cols)**
- Tier1Product, Tier2Product, Tier3Product
- Tier4Product, Tier5Product

**Location Data - A (6 cols)**
- AddressA, CityA, StateA, PostalCodeA
- CountryCodeA, ReportRegionA

**Location Data - Z (6 cols)**
- AddressZ, CityZ, StateZ, PostalCodeZ
- CountryCodeZ, ReportRegionZ

**Customer/Company (2 cols)**
- CompanyName, SourceSystem

**Access & Port Quantities (6 cols)**
- AccessQuantity, AccessABW, AccessZBW
- AccessASubBW, AccessZSubBW, PortQuantity, PortBW

**Vendor & Access Type (4 cols)**
- VendorA, VendorZ, AccessTypeA, AccessTypeZ

**Revenue - MRC (6 cols)**
- TotalListMRC, TotalDiscountedMRC, TotalAmortizedMRC
- AccessListMRC, AccessDiscountedMRC, AccessAmortizedMRC

**Revenue - NRC (4 cols)**
- TotalListNRC, TotalAmortizedNRC
- AccessListNRC, AccessAmortizedNRC

**Financial Metrics (6 cols)**
- GrossMargin, Payback, TotalCommit
- TotalListMrcOriginal, TotalDiscountedMRCwAmortized
- AccessDiscountedMRCwAmortized

**Incremental Costs (6 cols)**
- TotalIncrementalMRCost, TotalIncrementalNRCost
- TotalIncrementalCapexCost
- AccessIncrementalMRCost, AccessIncrementalNRCost
- AccessIncrementalCapexCost

**Term Revenue (3 cols)**
- TotalTermRevenueUSD, TotalTermEbitdaCostUSD
- TotalTermEbitdaDollarsUSD

**Intent Metrics (2 cols)**
- IntentA, IntentZ

**Flags & Classifications (5 cols)**
- PetraPricing (Y/N), ColtIgnore (Y/N), Ignore (Y/N)
- GLMOriginalLocIdA, GLMOriginalLocIdZ

**Employee & Audit (5 cols)**
- EmployeeName, CurrencyCode
- xact_username, xact_timestamp

**Dates (2 cols)**
- QuoteCreateDate, QuoteUpdateDate

---

## Schema Statistics

| Metric | Value |
|--------|-------|
| **Total Tables** | 4 |
| **DIM_PRODUCT** | 10 columns |
| **DIM_LOCATION_ADDRESS** | 51 columns |
| **DIM_CUSTOMER** | 24 columns ⭐ (Added Industry) |
| **DIM_OPPORTUNITY** | 30 columns |
| **FACT_CONFIGURATION** | 67 columns |
| **Total Columns** | 182 |
| **Primary Keys** | 5 |
| **Foreign Keys** | 7 |
| **Composite Keys** | 2 |

---

## Cardinality Summary

| Relationship | Cardinality | Description |
|--------------|-------------|-------------|
| DIM_PRODUCT → FACT_CONFIGURATION | 1:M | One product → Many configurations |
| DIM_LOCATION_ADDRESS → FACT_CONFIGURATION (A) | 1:M | One location (Type=A) → Many configs |
| DIM_LOCATION_ADDRESS → FACT_CONFIGURATION (Z) | 1:M | One location (Type=Z) → Many configs |
| DIM_CUSTOMER → FACT_CONFIGURATION | M:1 | Many configs → One customer |
| DIM_CUSTOMER → DIM_OPPORTUNITY | 1:M | One customer → Many opportunities |
| DIM_OPPORTUNITY → FACT_CONFIGURATION | M:1 | Many configs → One opportunity (composite) |

---

## Key Design Features v3.1

### ✨ Schema Highlights:
✅ **Industry Added** to DIM_CUSTOMER for better segmentation  
✅ **Simplified Dimensions** - Only essential business attributes  
✅ **Optimized Fact Table** - 67 columns with all necessary metrics  
✅ **Denormalized Location A/Z** - Address data in FACT table for fast access  
✅ **Product Tiers** - Included in FACT for configuration-level analysis  
✅ **Composite Keys** - GLMLocId+LocationType, OpportunityID+QuoteID  
✅ **Dual Location Support** - Separate A/Z references with complete attributes  

### 🎯 Total Columns: 182
- **DIM_PRODUCT**: 10
- **DIM_LOCATION_ADDRESS**: 51
- **DIM_CUSTOMER**: 24 (with Industry)
- **DIM_OPPORTUNITY**: 30
- **FACT_CONFIGURATION**: 67

---

**Schema Version**: Production Ready v3.1  
**Total Columns**: 182  
**Last Updated**: 2026-06-08  
**Status**: ✓ Final Production Schema - APPROVED
