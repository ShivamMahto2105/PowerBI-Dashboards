# 📐 DAX Formula Reference — Supply Chain Dashboard

> Full reference for all **22 DAX measures** used in the Supply Chain Analysis Power BI Dashboard.
> → Back to [README.md](./README.md)

---

## 💰 Revenue & Profitability

---

### 1. Total Revenue
```dax
Total_Revenue = SUM(fact_sales[net_revenue])
```
> Calculates the total net revenue generated from all sales transactions.

---

### 2. Profit Margin %
```dax
Profit_Margin % = DIVIDE([Profit], [Total_Revenue])
```
> Returns profit margin as a percentage.
> Uses `DIVIDE()` to safely handle division-by-zero cases.
> Requires a separate `[Profit]` measure to be defined.

---

## 📦 Sales & Quantity

---

### 3. Total Sales Quantity
```dax
Total_Sales_Quantity = SUM(fact_sales[quantity_sold])
```
> Total number of units sold across all products and time periods.

---

### 4. Total Sales Delivered
```dax
Total_Sales_Delivered = CALCULATE(
    [Total_Sales_Quantity],
    fact_shipment[status] = "Delivered"
)
```
> Filters total sales quantity to only orders that have been successfully delivered.

---

### 5. Total Quantity Delayed
```dax
Total_QTY_Delay = CALCULATE(
    [Total_Sales_Quantity],
    fact_shipment[status] = "Delayed"
)
```
> Shows quantity tied to delayed shipments — useful for identifying fulfillment bottlenecks.

---

## 🛒 Procurement & Costs

---

### 6. Total Sales Cost
```dax
Total_Sales_Cost = SUM(fact_procurement[total_cost])
```
> Aggregates total procurement cost across all purchase orders.

---

### 7. Average Lead Time
```dax
Avg_Lead_Time = AVERAGE(fact_procurement[lead_time_days])
```
> Average days between placing a purchase order and receiving goods.
> Lower lead time = more responsive supply chain.

---

### 8. Order Quantity
```dax
Order_Quantity = SUM(fact_procurement[order_quantity])
```
> Total units ordered via procurement.
> Compare against `Total_Sales_Quantity` to spot over/under-ordering.

---

### 9. Total Unit Cost
```dax
Total_Unit_Cost = SUM(fact_procurement[total_cost])
```
> Summed total cost from procurement — used as a COGS base.

---

### 10. Average Quality Score
```dax
Avg_Quality_Score = AVERAGE(fact_procurement[quality_score])
```
> Average quality rating of procured goods from suppliers.
> Higher = better supplier performance.

---

### 11. Average Unit Cost
```dax
Avg_Unit_Cost = AVERAGE(dim_product[unit_cost])
```
> Average cost per unit across all products in the product dimension.

---

## 🏭 Inventory Management

---

### 12. Inventory Value
```dax
Inventory-Value = SUM(fact_inventory[stock_level])
```
> Total current stock level across all inventory locations and products.

> ⚠️ *Practice dataset — Inventory Value does not account for unit cost weighting. Treat as a volume proxy.*

---

### 13. Safety Stock
```dax
Safety_Stock = SUM(fact_inventory[safety_stock_level])
```
> Total buffer stock maintained to prevent stockouts from demand or supply variability.

---

### 14. Inventory Turnover Rate
```dax
Turnover Rate = DIVIDE([Total_Sales_Quantity], [Inventory-Value])
```
> Measures how efficiently inventory is sold. Higher rate = faster inventory movement.

> ⚠️ *Days of Inventory (DOI) is derived from this measure. Since this is a self-made dataset, DOI figures may look unrealistic — this is expected and can be ignored.*

---

### 15. Reorder Point
```dax
Reorder Point = SUM(fact_inventory[reorder_point])
```
> Stock level that triggers a new purchase order.
> Compare with `Inventory-Value` to flag products at risk of stockout.

---

## 🚚 Shipment & Logistics

---

### 16. Total Shipments
```dax
Total_Shipment = DISTINCTCOUNT(fact_shipment[shipment_id])
```
> Total unique shipments dispatched.
> Uses `DISTINCTCOUNT` to avoid double-counting the same shipment ID.

---

### 17. Total Shipment Quantity
```dax
Total_Shipment_Quantity = SUM(fact_shipment[quantity])
```
> Total units included across all shipment records.

---

### 18. Shipment Cost
```dax
Shipment_Cost = SUM(fact_shipment[shipping_cost])
```
> Total logistics and shipping cost across all dispatched shipments.

---

### 19. Total Delivered Shipments
```dax
Total_delivered_ship = CALCULATE(
    [Total_Shipment],
    fact_shipment[status] = "Delivered"
)
```
> Count of shipments with "Delivered" status.
> Used as the numerator in the `Perfect_Order %` measure.

---

## 🏆 Quality & Performance KPIs

---

### 20. Perfect Order %
```dax
Perfect_Order % =
VAR perfectOrder =
    CALCULATE(
        [Total_Shipment],
        fact_shipment[status] = "Delivered",
        fact_production[defect_rate_pct] < 1
    )
RETURN
    DIVIDE(perfectOrder, [Total_Shipment])
```
> One of the most critical supply chain KPIs.
> A **Perfect Order** must satisfy **both** conditions:
> - ✅ Shipment status = **"Delivered"**
> - ✅ Production defect rate **< 1%**
>
> Returns the % of total shipments qualifying as perfect.

---

### 21. Defect Rate
```dax
Defect_Rate = SUM(fact_production[defective_units])
```
> Total defective units from production.
> Use alongside `Avg_Quality_Score` to assess production and supplier quality.

---

## 📊 KPI Summary Table

| # | Measure Name | Category | Key Use |
|---|---|---|---|
| 1 | `Total_Revenue` | Revenue | Top-line sales performance |
| 2 | `Profit_Margin %` | Profitability | Business health indicator |
| 3 | `Total_Sales_Quantity` | Sales | Total units sold |
| 4 | `Total_Sales_Cost` | Cost | Total procurement spend |
| 5 | `Inventory-Value` | Inventory | Current stock on hand |
| 6 | `Avg_Lead_Time` | Procurement | Supplier responsiveness |
| 7 | `Total_Shipment` | Logistics | Unique dispatches |
| 8 | `Perfect_Order %` | Performance | Fulfillment excellence |
| 9 | `Order_Quantity` | Procurement | Purchasing volume |
| 10 | `Total_Shipment_Quantity` | Logistics | Total units shipped |
| 11 | `Total_Sales_Delivered` | Sales | Fulfilled sales volume |
| 12 | `Defect_Rate` | Quality | Total defective units |
| 13 | `Safety_Stock` | Inventory | Buffer stock level |
| 14 | `Total_QTY_Delay` | Logistics | Delayed quantity |
| 15 | `Total_Unit_Cost` | Cost | COGS base |
| 17 | `Avg_Quality_Score` | Quality | Supplier quality rating |
| 18 | `Avg_Unit_Cost` | Cost | Per-unit cost average |
| 19 | `Turnover Rate` | Inventory | Inventory efficiency |
| 20 | `Reorder Point` | Inventory | Restocking trigger level |
| 21 | `Shipment_Cost` | Logistics | Total logistics spend |
| 22 | `Total_delivered_ship` | Logistics | Delivered shipment count |

---

## 📝 Notes & Limitations

- 🔧 Dataset is **manually created** — values may be simplified or approximate.
- 📉 **Days of Inventory** and some ratio KPIs may appear unrealistic — this is **expected**; ignore them.
- 🎓 Primary goal: **practice DAX writing**, data modeling, and supply chain KPI design in Power BI.

---

*→ Back to [README.md](./README.md)*
