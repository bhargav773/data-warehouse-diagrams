# Data Warehouse ER Diagram — dbo Schema

## Star / Snowflake Schema for Financial Metrics

```mermaid
erDiagram
    dim_location ||--o{ dim_network_entity : "LOCATIONID"
    dim_location ||--o{ dim_service_location : "LOCATIONID"
    dim_opportunity ||--o{ fact_financial_metrics : "OPPORTUNITYID + QUOTEID"
    dim_opportunity ||--o{ fact_financial_metrics_hl2 : "OPPORTUNITYID + QUOTEID"

    dim_location {
        string LOCATIONID PK "Primary Key"
        string ADDRESS "Street Address"
        string CITY "City"
        string STATE "State / Province"
        string POSTALCODE "Postal Code"
        string COUNTRYCODE "Country Code"
        decimal LATITUDE "Latitude Coordinate"
        decimal LONGITUDE "Longitude Coordinate"
        string PRICINGREGION "Pricing Region"
        string PRICINGSUBREGION "Pricing Sub Region"
        string ISON_NET "Is On-Net (Y/N)"
        string WIRCENTERCLLI "Wire Center CLLI"
        string NETWORKTYPE "Network Type"
        timestamp xact_timestamp "Audit Timestamp"
    }

    dim_network_entity {
        string NETWORKENTITYID PK "Primary Key"
        string LOCATIONID FK "FK → dim_location.LOCATIONID"
        string ENTITYNAME "Entity Name"
        string ENTITYTYPE "Entity Type"
        string ENTITYSTATUS "Entity Status"
        string NETWORKTYPE "Network Type"
        string CLLICODE "CLLI Code"
        string SOURCESYSTEM "Source System"
        timestamp xact_timestamp "Audit Timestamp"
    }

    dim_service_location {
        string SERVICELOCATIONID PK "Primary Key"
        string LOCATIONID FK "FK → dim_location.LOCATIONID"
        string SERVICETYPE "Service Type"
        string SERVICESTATUS "Service Status"
        string ACCESSTYPE "Access Type"
        decimal BANDWIDTH "Bandwidth (Mbps)"
        string VENDORNAME "Vendor Name"
        string SOURCESYSTEM "Source System"
        timestamp xact_timestamp "Audit Timestamp"
    }

    dim_opportunity {
        string OPPORTUNITYID PK "Primary Key (Part 1)"
        string QUOTEID PK "Primary Key (Part 2)"
        string BUSORGID "Business Org ID"
        string OPPORTUNITYNAME "Opportunity Name"
        string OPPORTUNITYTYPE "Opportunity Type"
        string OPPORTUNITYSUBTYPE "Opportunity Sub Type"
        string STAGENAME "Stage Name"
        string FORECASTCATEGORY "Forecast Category"
        string ISCLOSED "Is Closed (Y/N)"
        string ISWON "Is Won (Y/N)"
        string ISQUOTED "Is Quoted (Y/N)"
        string PRIMARYLOSSREASON "Primary Loss Reason"
        string COMPETITOR "Competitor Name"
        date OPPORTUNITYCLOSEDATE "Opportunity Close Date"
        date EXPECTEDCLOSEDATE "Expected Close Date"
        date SENDTOORDERDATE "Send To Order Date"
        string OPPORTUNITYOWNER "Opportunity Owner"
        string ACCTCHANNEL "Account Channel"
        string MKTVERTICAL "Market Vertical"
        string SALESREGION "Sales Region"
        string BUSINESSSEGMENT "Business Segment"
        string ULTCUSTNM "Ultimate Customer Name"
        string ULTCUSTNBR "Ultimate Customer Number"
        timestamp xact_timestamp "Audit Timestamp"
    }

    fact_financial_metrics {
        string FINANCIALMETRICSID PK "Primary Key"
        string OPPORTUNITYID FK "FK → dim_opportunity.OPPORTUNITYID"
        string QUOTEID FK "FK → dim_opportunity.QUOTEID"
        int TERM "Term (Months)"
        string DEALSTATE "Deal State"
        string CURRENCYCODE "Currency Code"
        string SOURCESYSTEM "Source System"
        decimal TOTALLISTMRC "Total List MRC"
        decimal TOTALDISCOUNTEDMRC "Total Discounted MRC"
        decimal TOTALAMORTIZEDMRC "Total Amortized MRC"
        decimal TOTALLISTNRC "Total List NRC"
        decimal TOTALAMORTIZEDNRC "Total Amortized NRC"
        decimal ACCESSLISTMRC "Access List MRC"
        decimal ACCESSDISCOUNTEDMRC "Access Discounted MRC"
        decimal ACCESSLISTNRC "Access List NRC"
        decimal ACCESSAMORTIZEDNRC "Access Amortized NRC"
        decimal TOTALINCREMENTALMRCOST "Total Incremental MR Cost"
        decimal TOTALINCREMENTALNRCOST "Total Incremental NR Cost"
        decimal TOTALINCREMENTALCAPEXCOST "Total Incremental Capex Cost"
        decimal GROSSMARGIN "Gross Margin"
        decimal PAYBACK "Payback Period"
        decimal TOTALTERMREVENUEUSD "Total Term Revenue USD"
        decimal TOTALTERMEBITDACOSTUSD "Total Term EBITDA Cost USD"
        decimal TOTALTERMEBITDADOLLARSUSD "Total Term EBITDA Dollars USD"
        decimal TOTALCOMMIT "Total Commit"
        string EMPLOYEENAME "Employee Name"
        int LINENUMBER "Line Number"
        date QUOTECREATDATE "Quote Create Date"
        date QUOTEUPDATEDATE "Quote Update Date"
        timestamp xact_timestamp "Audit Timestamp"
    }

    fact_financial_metrics_hl2 {
        string OPPORTUNITYID FK "FK → dim_opportunity.OPPORTUNITYID"
        string QUOTEID FK "FK → dim_opportunity.QUOTEID"
        string HL2NBR PK "HL2 Number (Part of PK)"
        string BUSORGID "Business Org ID"
        string ACTIVEINDICATOR "Active Indicator (Y/N)"
        string CURRENCYCODE "Currency Code"
        decimal REVENUEAMT "Revenue Amount"
        decimal NETEXDIRECTAMT "Netex Direct Amount"
        decimal NETEXSHAREDAMT "Netex Shared Amount"
        decimal GROSSMARGINAMT "Gross Margin Amount"
        decimal GROSSMARGINPCT "Gross Margin Percentage"
        decimal OPEXAMT "Operating Expense Amount"
        decimal EBITDAAMT "EBITDA Amount"
        decimal EBITDAPCT "EBITDA Percentage"
        decimal CAPEXSHAREDAMT "Capex Shared Amount"
        decimal CAPEXDIRECTAMT "Capex Direct Amount"
        decimal EBITDALESSEXPEXPCT "EBITDA Less Capex Percentage"
        decimal NETPRESENTVALUE "Net Present Value"
        decimal DISCOUNTPAYBACKPERIODMONTH "Discount Payback Period (Months)"
        decimal INTERNALRATEOFRETURN "Internal Rate of Return"
        decimal SIMPLEPAYBACKPERIODMONTH "Simple Payback Period (Months)"
        string APPROVED "Approval Status"
        timestamp RESPONSEDATE "Response Date"
        timestamp xact_timestamp "Audit Timestamp"
    }
```

---

## Schema Summary

| Table | Type | Rows (approx.) | Description |
|-------|------|----------------|-------------|
| `dbo.dim_location` | Dimension | — | Master location records (address, geo, network attributes) |
| `dbo.dim_network_entity` | Dimension | — | Network entity records keyed to a location |
| `dbo.dim_service_location` | Dimension | — | Service availability per location |
| `dbo.dim_opportunity` | Dimension | — | SFDC opportunity & quote records |
| `dbo.fact_financial_metrics` | Fact | — | Configuration-level financial metrics |
| `dbo.fact_financial_metrics_hl2` | Fact | — | Quote-level (HL2) profitability metrics |

---

## Relationships

| From | Column(s) | To | Column(s) | Cardinality |
|------|-----------|----|-----------|-------------|
| `dim_network_entity` | `LOCATIONID` | `dim_location` | `LOCATIONID` | M:1 |
| `dim_service_location` | `LOCATIONID` | `dim_location` | `LOCATIONID` | M:1 |
| `fact_financial_metrics` | `OPPORTUNITYID`, `QUOTEID` | `dim_opportunity` | `OPPORTUNITYID`, `QUOTEID` | M:1 |
| `fact_financial_metrics_hl2` | `OPPORTUNITYID`, `QUOTEID` | `dim_opportunity` | `OPPORTUNITYID`, `QUOTEID` | M:1 |

---

**Schema Version**: v1.0  
**Last Updated**: 2026-07-01
