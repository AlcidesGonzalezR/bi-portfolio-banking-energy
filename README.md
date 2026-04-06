# 📊 Alcides González - Data Portfolio

## Excel to Power BI | Financial & Logistics Analytics

> *Especialista en Business Intelligence | 25+ años en Banca y Energía*

---

## 📋 Table of Contents

1. [Objective](#objective)
2. [Data Source](#data-source)
3. [Dataset](#dataset)
4. [Data Model](#data-model)
5. [ETL Process](#etl-process)
6. [Power Query Transformations](#power-query-transformations)
7. [DAX Measures](#dax-measures)
8. [Calculated Columns](#calculated-columns)
9. [Parameters](#parameters)
10. [Filters](#filters)
11. [Key Calculations](#key-calculations)
12. [Visualizations](#visualizations)
13. [Reports](#reports)
14. [Dashboards](#dashboards)
15. [Data Connections](#data-connections)
16. [Repository Structure](#repository-structure)
17. [Technologies Used](#technologies-used)

---

## 🎯 Objective

Build a complete Business Intelligence solution transforming raw Excel data into interactive Power BI dashboards for **Banking (Financial Control)** and **Energy (Logistics & Inventory)** sectors.

---

## 📁 Data Source

| Source | Format | Description |
|--------|--------|-------------|
| Kaggle | Excel (.xlsx) | Public financial datasets |
| Internal (anonymized) | CSV | Banking transaction logs |
| Public API | JSON | Fuel prices and logistics data |

---

## 📊 Dataset

### Banking Dataset
| Column | Type | Description |
|--------|------|-------------|
| TransactionID | VARCHAR(50) | Unique transaction identifier |
| Date | DATE | Transaction date |
| Amount | DECIMAL(18,2) | Transaction amount |
| CustomerSegment | VARCHAR(20) | Retail / Corporate / SME |
| AccountType | VARCHAR(30) | Checking / Savings / Credit |
| Branch | VARCHAR(50) | Bank branch location |
| Status | VARCHAR(20) | Completed / Pending / Rejected |

### Energy & Logistics Dataset
| Column | Type | Description |
|--------|------|-------------|
| PlantID | VARCHAR(10) | Fuel plant identifier |
| ProductType | VARCHAR(30) | Gasoline / Diesel / Kerosene |
| InventoryLevel | INT | Current stock in liters |
| ShipmentDate | DATE | Delivery date |
| Destination | VARCHAR(50) | Service station location |
| TransportCost | DECIMAL(18,2) | Logistics cost per shipment |

---

## 📐 Data Model

---

## 🔄 ETL Process

### Step by Step:
1. **Extract** - Load Excel files from source folder
2. **Transform** - Clean, filter, and aggregate using Power Query
3. **Model** - Create relationships and hierarchies in Power Pivot
4. **Calculate** - Write DAX measures and calculated columns
5. **Visualize** - Build interactive dashboards in Power BI Desktop

---

## ⚙️ Power Query Transformations

| Step | Action | M Code Example |
|------|--------|----------------|
| 1 | Remove duplicates | `Table.Distinct(#"Previous Step")` |
| 2 | Filter nulls | `Table.SelectRows(#"Previous Step", each [Amount] <> null)` |
| 3 | Change types | `Table.TransformColumnTypes(#"Previous Step", {{"Date", type date}})` |
| 4 | Add conditional column | `Table.AddColumn(#"Previous Step", "Segment", each if [Amount] > 10000 then "High Value" else "Standard")` |
| 5 | Group by | `Table.Group(#"Previous Step", {"Branch"}, {{"TotalSales", each List.Sum([Amount]), type number}})` |

---

## 📏 DAX Measures

### Financial KPIs (Banking)

```dax
// Total Portfolio
Total Portfolio = SUM(FactTransactions[Amount])

// NPL Ratio (Non-Performing Loans)
NPL Ratio = 
DIVIDE(
    CALCULATE([Total Portfolio], FactTransactions[Status] = "Default"),
    [Total Portfolio]
)

// Portfolio at Risk (PAR > 30 days)
PAR 30 = 
CALCULATE(
    [Total Portfolio],
    FactTransactions[DaysOverdue] >= 30
)

// Efficiency Ratio
Efficiency Ratio = 
DIVIDE(
    SUM(Expenses[OperatingExpenses]),
    SUM(Income[NetRevenue])
)

// ROE (Return on Equity)
ROE = 
DIVIDE(
    SUM(Income[NetProfit]),
    SUM(BalanceSheet[Equity])
)
// Inventory Turnover
Inventory Turnover = 
DIVIDE(
    SUM(Shipments[TotalLiters]),
    AVERAGE(Inventory[AverageStock])
)

// On-Time Delivery Rate
OTD Rate = 
DIVIDE(
    CALCULATE(COUNT(Shipments[ShipmentID]), Shipments[Status] = "On Time"),
    COUNT(Shipments[ShipmentID])
)

// Cost per Liter Transported
Cost per Liter = 
DIVIDE(
    SUM(Shipments[TransportCost]),
    SUM(Shipments[TotalLiters])
)

// Days of Inventory
Days of Inventory = 
DIVIDE(
    AVERAGE(Inventory[CurrentStock]),
    SUMX(Shipments, Shipments[TotalLiters]) / 365
)

// Plant Utilization Rate
Plant Utilization = 
DIVIDE(
    SUM(Production[ActualOutput]),
    SUM(Production[Capacity])
)
📁 bi-portfolio-banking-energy/
├── 📁 data/
│   ├── 📁 raw/
│   │   ├── banking_transactions.xlsx
│   │   └── logistics_shipments.csv
│   └── 📁 processed/
│       ├── clean_banking_data.xlsx
│       └── clean_logistics_data.csv
├── 📁 powerbi/
│   ├── banking_dashboard.pbix
│   ├── logistics_dashboard.pbix
│   └── executive_dashboard.pbix
├── 📁 scripts/
│   ├── 📁 powerquery/
│   │   ├── banking_etl.txt
│   │   └── logistics_etl.txt
│   └── 📁 dax/
│       ├── financial_measures.txt
│       └── logistics_measures.txt
├── 📁 images/
│   ├── banking_dashboard.png
│   ├── logistics_dashboard.png
│   └── data_model.png
├── 📁 docs/
│   ├── requirements.md
│   └── user_guide.md
└── README.md
