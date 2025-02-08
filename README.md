# Maven Toys Sales & Inventory Analysis - Power BI Edition

## 📌 Project Overview
This Power BI analysis explores sales performance and inventory management for Maven Toys, a fictional toy store chain in Mexico. The interactive dashboard transforms raw transactional data from 5 CSV files into strategic insights through:

- **Executive Dashboard**: High-level KPIs and trend analysis
- **Product Details Page**: Granular product performance metrics
- **Key Features**: 
  - 12+ interactive visualizations
  - Dynamic DAX measures for business calculations
  - Cross-filtering between retail locations and product categories

**Data Sources**: 
1. `calendar.csv` - Date dimension table
2. `inventory.csv` - Daily stock levels
3. `products.csv` - Product attributes & pricing
4. `stores.csv` - Store locations & metadata
5. `sales.csv` - Transaction records

## 🎯 Analysis Objectives
1. **Performance Tracking**
   - Monitor revenue, profit, and order metrics across 50 store locations
   - Identify top-performing product categories and cities

2. **Strategic Planning**
   - Evaluate price point effectiveness (Low/Medium/High)
   - Compare urban vs suburban market performance

## 🔬 Analysis Methodology

### **Data Modeling**
- Created star schema with `sales` as fact table
- Established relationships:
  - Calendar ↔ Sales (Date)
  - Products ↔ Sales 
  - Stores ↔ Sales ↔ Inventory

## 🔍 Key Findings

### 📈 Financial Performance
- **Year-over-Year Growth**:
  - Revenue: $658.2K (-0.41% vs PY $660.9K)
  - Profit: $180.4K (+3.09% vs PY $175.0K)
  - Orders: 41.8K (+3.08% vs PY 40.6K)
  
- **Purchase Patterns**:
  - 17.27% of orders were single-item purchases
  - Low-price items (<$20) drove **80.95% of total profits**

- **Pricing Insights**:
  - Colorbuds achieved **114.45% profit margin** (data anomaly under review)
  - Premium products underperformed vs budget-friendly toys

### 🧸 Product & Category Insights
- **Top 3 Profit Drivers**:
  1. Toys 
  2. Art & Crafts  
  3. Electronics

- **Star Performers**:
  - Colorbuds
  - Lego Bricks
  - Magic Sand 
  - Action Figures 

- **Underperforming Products**:
  ```diff
  - Classic Dominos
  - UNO Card Game 
  - Teddy Bears 
  - Supersoaker Water Guns 
  - Monopoly 
  - PlayDoh Playsets 
  - Mini Basketball Hoops 
  
### **DAX Measures**
```dax
// Core KPIs
Revenue = SUMX(
    FactSales, 
    FactSales[Units] * FactSales[Product Price])

Total Cost = SUMX(
    FactSales,
    FactSales[Units] *
    RELATED(
        DimProducts[Product_Cost]
    ))

Profit = [Revenue] - [Total Cost]

YTD Revenue = CALCULATE(
    [Revenue],
    DATESYTD(
        DimCalendar[Date]
    ))

// Purchase Type Classification
Unit Type = 
IF(SUM(Sales[Units_Sold]) = 1, "Single Item", "Multi-Item")


