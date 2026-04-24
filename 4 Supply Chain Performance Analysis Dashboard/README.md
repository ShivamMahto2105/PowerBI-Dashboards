# 📦 Supply Chain Analysis Dashboard
### Built with Power BI | DAX | Star Schema

> ⚠️ **Disclaimer:** This dataset is **self-made / custom-built** for **practice and learning only**.
> Some values (e.g., *Days of Inventory*, ratios) may not reflect real-world data perfectly.
> If any result seems off — **ignore it**. This is a learning project. 🎓

---

## 📸 Dashboard Preview

> *Replace the links below with your actual screenshot URLs after uploading to GitHub*

| Overview Page | Inventory Page |
|:---:|:---:|
| ![Overview](https://github.com/ShivamMahto2105/PowerBI-Dashboards/blob/main/4%20Supply%20Chain%20Performance%20Analysis%20Dashboard/Preview/Overview.png) | ![Inventory](https://github.com/ShivamMahto2105/PowerBI-Dashboards/blob/main/4%20Supply%20Chain%20Performance%20Analysis%20Dashboard/Preview/Inventory%20%26%20Production.png) |

| Procurement Page | Shipment Page |
|:---:|:---:|
| ![Customer](https://github.com/ShivamMahto2105/PowerBI-Dashboards/blob/main/4%20Supply%20Chain%20Performance%20Analysis%20Dashboard/Preview/Customer.png) | ![Shipment](https://github.com/ShivamMahto2105/PowerBI-Dashboards/blob/main/4%20Supply%20Chain%20Performance%20Analysis%20Dashboard/Preview/Shipment.png) |

---

## 📌 Project Description

This Power BI dashboard delivers an **end-to-end supply chain performance view** built entirely on a self-made star-schema dataset. It is designed to practice real-world BI concepts across five core supply chain domains:

| Domain | What It Covers |
|---|---|
| 💰 **Sales & Revenue** | Net revenue, quantity sold, profit margin |
| 🛒 **Procurement** | Order quantity, lead time, supplier quality, unit cost |
| 🏭 **Inventory** | Stock levels, safety stock, reorder points, turnover rate |
| 🚚 **Shipment & Logistics** | Delivery status, shipping cost, delayed quantity |
| 🏆 **Quality & KPIs** | Defect rate, perfect order %, quality score |

### Key Highlights
- ⭐ **21 DAX measures** covering all major supply chain KPIs
- 🗂️ **10-table Star Schema** — 5 Dimension + 5 Fact tables
- 📊 Built with **Microsoft Power BI Desktop**
- 🔁 Dataset is fully self-created for hands-on learning

---

## 🗃️ Data Model

**Total Tables: 10** &nbsp;|&nbsp; **Dimension: 5** &nbsp;|&nbsp; **Fact: 5**

### Dimension Tables
| Table | Description |
|---|---|
| `dim_customer` | Customer details — names, segments, regions |
| `dim_date` | Calendar table for time intelligence |
| `dim_facility` | Warehouse / facility location data |
| `dim_product` | Product details including unit cost and category |
| `dim_supplier` | Supplier information for procurement analysis |

### Fact Tables
| Table | Description |
|---|---|
| `fact_inventory` | Stock levels, safety stock, reorder points |
| `fact_procurement` | Purchase orders, lead times, costs, quality scores |
| `fact_production` | Production output, defect rates, defective units |
| `fact_sales` | Sales transactions — revenue and quantity sold |
| `fact_shipment` | Shipment records — status, quantity, shipping cost |

---

## 🔗 Links

| Resource | Link |
|---|---|
| 📊 **Power BI Report (.pbix)** | [Download / View Report](https://drive.google.com/file/d/1Yi9yKaHnrNG8MUntTnIIgRqSVvla9RWD/view?usp=sharing) 
| 🗄️ **Dataset (Excel / CSV)** | [Download Dataset](https://github.com/ShivamMahto2105/PowerBI-Dashboards/tree/main/4%20Supply%20Chain%20Performance%20Analysis%20Dashboard/dataset) 
| 📄 **DAX Formulas Reference** | [View DAX.md](https://github.com/ShivamMahto2105/PowerBI-Dashboards/blob/main/4%20Supply%20Chain%20Performance%20Analysis%20Dashboard/DAX.md) 

---

## 🛠️ Tools & Technologies
- **BI Tool:** Microsoft Power BI Desktop
- **Formula Language:** DAX (Data Analysis Expressions)
- **Data Source:** Self-made custom dataset
- **Schema:** Star Schema

---

## 👤 Author

**Self-made Project** — Power BI Supply Chain Dashboard
*Built for learning DAX, data modeling, and supply chain analytics.*

---

*© Practice Project — Not for commercial use.*
