# 🍕 Pizza Sales Analysis Dashboard (Power BI)

An interactive Power BI dashboard analyzing one full year (2015) of sales from a pizza restaurant: revenue, best and worst selling pizzas, busiest hours and monthly trends.

![Dashboard](Pizza_Sales_Analysis_Dashboard.png)

## 📊 Key Numbers

| Metric | Value |
|---|---|
| Total Revenue | $817,860 |
| Total Orders | 21,350 |
| Total Pizzas Sold | 49,574 |
| Average Order Value | $38.31 |

## 🗂️ Data

- **Source:** Kaggle "Pizza Place Sales" dataset
- **4 tables:** `orders`, `order_details`, `pizzas`, `pizza_types`
- **Period:** January to December 2015

## 🔗 Data Model

The four tables are connected with one-to-many relationships:

- `orders` (order_id) → `order_details`
- `pizzas` (pizza_id) → `order_details`
- `pizza_types` (pizza_type_id) → `pizzas`

## 🧮 DAX Measures

```
Total Revenue = SUMX(order_details, order_details[quantity] * RELATED(pizzas[price]))
Total Orders = DISTINCTCOUNT(order_details[order_id])
Total Pizzas Sold = SUM(order_details[quantity])
Avg Order Value = DIVIDE([Total Revenue], [Total Orders])
```

Calculated columns: `Order Hour = HOUR(orders[time])` and `Hour Label = FORMAT(orders[time], "h AM/PM")` (sorted by Order Hour).

## 💡 Key Findings

- **Classic** is the top category (~$220K) and **Veggie** the lowest (~$194K), but all four categories are close.
- The top 3 individual pizzas are all **Chicken** (Thai, Barbecue, California), even though Classic leads as a category, because Classic has more items on the menu.
- **Large** pizzas bring in ~46% of revenue. **XL and XXL** together bring less than 2%.
- Orders peak at **12 to 1 PM** (lunch) and **5 to 6 PM** (dinner), with a dip at 2 to 3 PM.
- **July** was the best month (~$72.5K) and **September/October** the weakest (~$64K). The gap between the best and worst month is only ~13%, so sales were fairly stable through the year.
- **The Brie Carre Pizza** is the weakest seller (~$11.6K), about 4 times less than the top pizza.

## ✅ Recommendations

- Add more staff during lunch and dinner peaks.
- Run an afternoon deal (2 to 4 PM) to fill the slow hours.
- Review XL/XXL sizes and the bottom 5 pizzas, especially Brie Carre.

## 🛠️ Skills Used

Power Query (importing multiple CSVs, promoting headers, data types) · Data modeling and relationships · DAX (SUMX, RELATED, DISTINCTCOUNT, DIVIDE, HOUR, FORMAT) · Sort by column · Top N filter · Button slicer · Custom JSON theme · Page layout

## 📁 Files

| File | Description |
|---|---|
| `Pizza_sales_analysis.pbix` | Power BI report |
| `Pizza_Sales_Analysis_Dashboard.png` | Dashboard image |
| `Pizza_Sales_Dashboard.pdf` | Dashboard PDF |
| `Pizza_Theme.json` | Custom color theme |
| `Pizza_Data/` | The 4 raw CSV files |
