# Data Warehouse ER Diagrams

High-quality Entity-Relationship diagrams and documentation for the data warehouse Snowflake schema architecture.

## 📊 Schema Overview

This repository contains comprehensive ER diagrams and documentation for a **Snowflake Schema** data warehouse with:

- **1 Fact Table**: FACT_CONFIGURATION (61 columns, normalized)
- **4 Dimension Tables**: DIM_PRODUCT, DIM_LOCATION_ADDRESS, DIM_CUSTOMER, DIM_OPPORTUNITY
- **1:M and M:1 Relationships**: Optimized for analytical queries
- **Complete Metrics**: Quantity, Revenue, Margin, Cost, and Payback metrics

## 📁 Files

| File | Description |
|------|-------------|
| `er_diagram_mermaid.md` | Interactive Mermaid ER diagram |
| `schema_documentation.md` | Complete table and column definitions |
| `sql_ddl_statements.sql` | DDL for all tables |
| `metrics_reference.md` | Metrics categorization and definitions |

## 🏗️ Architecture

### Fact Table: FACT_CONFIGURATION
- **Grain**: Configuration line item level
- **Columns**: 61 (identifiers, attributes, metrics)
- **Keys**: 
  - PK: ConfigurationId
  - FK: ProductID, CustomerID, OpportunityID, LocationIdA, LocationIdZ

### Dimension Tables

#### DIM_PRODUCT
- Product hierarchy (5 tiers)
- Source system tracking
- 9 columns

#### DIM_LOCATION_ADDRESS
- Dual location support (Type A/Z)
- Full address information
- GLM location mapping
- 9 columns

#### DIM_CUSTOMER
- SFDC Account information
- Account ownership hierarchy
- Market vertical & tier classifications
- 21 columns

#### DIM_OPPORTUNITY
- SFDC Opportunity details
- Sales pipeline tracking
- Revenue forecasting
- 35 columns

## 🔗 Relationships

```
DIM_PRODUCT ──1:M──→ FACT_CONFIGURATION ←──M:1── DIM_CUSTOMER
                              ↑
                              │
                           M:1 │
                              │
                     DIM_OPPORTUNITY
                     
DIM_LOCATION_ADDRESS ──1:M──→ FACT_CONFIGURATION
DIM_CUSTOMER ──1:M──→ DIM_OPPORTUNITY
```

## 📈 Metrics Coverage

### Quantity Metrics
- AccessQuantity, PortQuantity, PortBW
- AccessABW, AccessZBW, AccessASubBW, AccessZSubBW

### Revenue Metrics (MRC - Monthly Recurring)
- TotalListMRC, TotalDiscountedMRC, TotalAmortizedMRC
- AccessListMRC, AccessDiscountedMRC, AccessAmortizedMRC

### Revenue Metrics (NRC - Non-Recurring)
- TotalListNRC, TotalAmortizedNRC
- AccessListNRC, AccessAmortizedNRC

### Margin & Financial
- GrossMargin
- TotalDiscountedMRCwAmortized, AccessDiscountedMRCwAmortized
- TotalListMrcOriginal, TotalCommit

### Incremental Cost Metrics
- TotalIncrementalMRCost, TotalIncrementalNRCost, TotalIncrementalCapexCost
- AccessIncrementalMRCost, AccessIncrementalNRCost, AccessIncrementalCapexCost

### Term Revenue & Payback
- TotalTermRevenueUSD, TotalTermEbitdaCostUSD, TotalTermEbitdaDollarsUSD
- Payback (ROI payback period)

## 🎯 Use Cases

1. **Sales Analytics**: Track opportunities, configurations, and revenue
2. **Product Analysis**: Analyze product tiers and configuration patterns
3. **Customer Intelligence**: Understand customer portfolios and account hierarchies
4. **Financial Reporting**: Revenue, margin, and cost analysis
5. **Geographic Analysis**: Location-based opportunity and configuration tracking

## 📝 Notes

- Schema optimized for OLAP queries
- Supports drill-down from opportunity → configuration → product
- Audit timestamps (xact_timestamp, merge_timestamp) for change tracking
- Flexible location model supporting dual location types (A/Z)

---

**Last Updated**: 2026-06-04
