# Super Store Sales Dashboard

A reference guide for the Super Store sales visualization built from `SuperStore_Sales_Dataset.csv`. The dashboard is designed as an executive sales overview: it combines trend analysis, KPI cards, regional filtering, geographic performance, and product/category breakdowns in one screen.

![Super Store Sales Dashboard](Dashboard%20Final.png)

_Dashboard preview: monthly trends, KPI cards, regional map, and sales breakdowns._

## Dataset Summary

| Item              |                                  Value |
| ----------------- | -------------------------------------: |
| Source file       |         `SuperStore_Sales_Dataset.csv` |
| Transaction lines |                                  5,901 |
| Date range        |   January 1, 2019 to December 31, 2020 |
| Orders            |               3,003 distinct order IDs |
| Customers         |              773 distinct customer IDs |
| States            |                                     49 |
| Product IDs       |                                  1,755 |
| Product names     |                                  1,742 |
| Country           |                          United States |
| Regions           |             Central, East, South, West |
| Categories        | Furniture, Office Supplies, Technology |
| Sub-categories    |                                     17 |

The source contains one row per product line rather than one row per order. Therefore, sales, profit, and quantity are normally summed across rows, while customer and order counts should use distinct IDs.

## Dashboard Purpose

The visualization answers these questions:

- How are sales and profit changing month by month and year by year?
- Which region, state, segment, payment method, and shipping method contribute most?
- Which products and categories drive sales?
- Where are the strongest geographic markets?
- How do quantity and sales relate for the most profitable products?

## Dashboard Layout

The reference view uses a dark navy analytical canvas with blue grid accents, outlined panels, and orange/blue chart highlights. It is organized into three working areas:

1. **Trend area on the left**: monthly sales and monthly profit for 2019 and 2020, followed by segment and payment-mode donut charts.
2. **KPI and product area in the center**: headline cards, a most-profitable product chart, and horizontal rankings for ship mode and products.
3. **Filter and geography area on the right**: region selector, state sales/profit map, and category sales ranking.

## Filters and Controls

### Region filter

The visible selector contains four region values:

- Central
- East
- South
- West

Selecting a region should cross-filter the KPI cards and every chart that uses the same dataset. A clear/reset action should restore all four regions.

### Visual controls

The reference image also shows filter and more-options controls on the chart headers. These are expected to provide the standard filtering, focus, export, or drill options supplied by the visualization platform.

## Visual Catalog

### 1. Sales Monthly

- **Chart type**: area or line chart
- **Subtitle**: `Sum of Sales by Month and Year`
- **Axis**: January through December
- **Series**: 2019 and 2020
- **Measure**: `SUM(Sales)`
- **Purpose**: compare seasonality and year-over-year sales movement

### 2. Monthly Profit

- **Chart type**: area or line chart
- **Subtitle**: `Sum of Profit by Month and Year`
- **Axis**: January through December
- **Series**: 2019 and 2020
- **Measure**: `SUM(Profit)`
- **Purpose**: show whether sales growth is translating into profit

### 3. KPI cards

The dashboard presents these headline measures:

| Card                      | Recommended calculation                                                            |
| ------------------------- | ---------------------------------------------------------------------------------- |
| Average Ordering Quantity | `AVERAGE(Quantity)` per transaction line, or a clearly defined order-level average |
| Average Delivery Days     | `AVERAGE(Ship Date - Order Date)`                                                  |
| New Customers             | Distinct customers in the selected period or filter context                        |
| Total Sales               | `SUM(Sales)`                                                                       |
| Total Quantity Sold       | `SUM(Quantity)`                                                                    |
| Profit                    | `SUM(Profit)`                                                                      |

Because the CSV is line-level data, the definition of `Average Ordering Quantity` and `New Customers` should be stated in the implementation. The values below use transaction-line quantity and distinct `Customer ID` unless noted otherwise.

### 4. Most Profit

- **Chart type**: line and area chart with point markers
- **Subtitle**: `Quantity of Product v/s Sales`
- **X-axis**: product quantity
- **Y-axis**: sales value
- **Measure**: sales, with product-level or grouped product detail
- **Purpose**: identify high-value products and quantities associated with strong sales/profit performance

The title suggests profit-oriented analysis, while the subtitle describes quantity versus sales. The implementation should keep the selected metric explicit in the chart tooltip.

### 5. Sales in States

- **Chart type**: filled map or bubble map of the United States
- **Subtitle**: `Sum of Sales and Sum of Profit by State`
- **Geography**: `State`
- **Measures**: `SUM(Sales)` and `SUM(Profit)`
- **Purpose**: locate high-sales and high-profit states
- **Tooltip fields**: state, sales, profit, quantity, and profit margin if available

The supplied data contains state names but no latitude/longitude columns. A map visual therefore needs a geographic lookup or a mapping engine that recognizes US state names.

### 6. Sales by Ship Mode

- **Chart type**: horizontal bar chart
- **Subtitle**: `Shipment Mode v/s Sales`
- **Dimension**: `Ship Mode`
- **Measure**: `SUM(Sales)`
- **Purpose**: compare sales volume by fulfillment speed/type

### 7. Sales by Product

- **Chart type**: horizontal bar chart
- **Subtitle**: `Top Product v/s Sales`
- **Dimension**: `Product Name`
- **Measure**: `SUM(Sales)`
- **Purpose**: rank the best-selling products
- **Recommended display**: top 5 or top 10 products, sorted descending

### 8. Sales by Category

- **Chart type**: horizontal bar chart
- **Subtitle**: `Category v/s Sales`
- **Dimension**: `Category`
- **Measure**: `SUM(Sales)`
- **Purpose**: compare Furniture, Office Supplies, and Technology

### 9. Sales on different Segments

- **Chart type**: donut chart
- **Dimension**: `Segment`
- **Measure**: `SUM(Sales)`
- **Values**: Consumer, Corporate, and Home Office
- **Purpose**: show the sales mix by customer segment

### 10. Sales on Payment Mode

- **Chart type**: donut chart
- **Dimension**: `Payment Mode`
- **Measure**: `SUM(Sales)`
- **Values**: COD, Cards, and Online
- **Purpose**: show the sales mix by payment method

## Verified CSV Metrics

These figures are calculated from the supplied CSV with dates parsed as day-month-year and with no region filter applied.

| Metric                                | Calculated value |
| ------------------------------------- | ---------------: |
| Total sales                           |     1,565,804.32 |
| Total quantity                        |           22,317 |
| Total profit                          |       175,262.11 |
| Average quantity per transaction line |             3.78 |
| Average sales per transaction line    |           265.35 |
| Average profit per transaction line   |            29.70 |
| Average delivery time                 |        3.93 days |
| Median delivery time                  |           4 days |
| Distinct customers                    |              773 |

### Sales and profit by region

| Region  |      Sales |    Profit | Quantity |
| ------- | ---------: | --------: | -------: |
| West    | 522,441.05 | 67,859.96 |    7,298 |
| East    | 450,234.67 | 53,400.42 |    6,251 |
| Central | 341,007.52 | 27,450.01 |    5,239 |
| South   | 252,121.08 | 26,551.72 |    3,529 |

### Sales and profit by category

| Category        |      Sales |    Profit | Quantity |
| --------------- | ---------: | --------: | -------: |
| Office Supplies | 643,707.69 | 74,797.25 |   13,625 |
| Technology      | 470,587.99 | 90,458.25 |    4,061 |
| Furniture       | 451,508.65 | 10,006.61 |    4,631 |

Technology produces the highest profit among the three categories despite having lower quantity than Office Supplies. Furniture has substantial sales but comparatively low profit.

### Sales by ship mode

| Ship mode      |      Sales |    Profit |
| -------------- | ---------: | --------: |
| Standard Class | 912,401.04 | 99,767.39 |
| Second Class   | 314,508.06 | 36,936.03 |
| First Class    | 242,936.72 | 29,749.87 |
| Same Day       |  95,958.50 |  8,808.82 |

### Sales by customer segment

| Segment     |      Sales |    Profit |
| ----------- | ---------: | --------: |
| Consumer    | 753,002.13 | 81,338.59 |
| Corporate   | 509,743.13 | 57,805.80 |
| Home Office | 303,059.07 | 36,117.72 |

### Sales by payment mode

| Payment mode |      Sales |    Profit |
| ------------ | ---------: | --------: |
| COD          | 667,417.75 | 82,092.42 |
| Online       | 553,993.46 | 54,047.52 |
| Cards        | 344,393.11 | 39,122.16 |

### Top sales categories within the product hierarchy

| Sub-category |      Sales |
| ------------ | ---------: |
| Phones       | 196,563.55 |
| Chairs       | 181,946.00 |
| Binders      | 174,978.39 |
| Storage      | 150,341.32 |
| Accessories  | 122,301.09 |

The top product by summed sales is `3D Systems Cube Printer, 2nd Generation, Magenta` at 14,334.89.

### Sales by year

| Year |        Sales |    Profit | Quantity |
| ---- | -----------: | --------: | -------: |
| 2019 |   564,679.54 | 81,823.44 |    9,838 |
| 2020 | 1,001,124.79 | 93,438.66 |   12,479 |

2020 contributes approximately 63.9% of total sales in this extract.

## Calculated Fields

The following fields support the visuals and should be created in the BI model or preparation layer:

```text
Order Year       = YEAR(Order Date)
Order Month      = MONTH(Order Date)
Order Month Name = FORMAT(Order Date, "MMMM")
Delivery Days    = DATEDIFF(Order Date, Ship Date, DAY)
Profit Margin    = SUM(Profit) / SUM(Sales)
```

Sort `Order Month Name` by `Order Month` so that the monthly charts remain chronological. Use a proper date hierarchy or a calendar table when the BI tool supports one.

## Data Quality Notes

- `Order Date` and `Ship Date` are stored as text in `DD-MM-YYYY` format and must be parsed explicitly.
- `Returns` is populated with `1` on 287 rows and is missing on 5,614 rows. Missing values should not automatically be interpreted as a confirmed return unless that is the intended business rule.
- `ind1` and `ind2` are completely empty in the supplied file and are not used by the visualization.
- No duplicate rows were detected by a full-row comparison.
- There are 1,098 transaction lines with negative profit. These should remain in profit calculations because they represent loss-making sales lines.
- The first column is named `Row ID+O6G3A1:R6`, which appears to be a malformed or inherited column name. It can be renamed to `Row ID` in a cleaned model without changing the data.
- All rows belong to the United States, although only 49 states appear in the file.

## Reference Image Versus Supplied CSV

The reference screenshot shows rounded headline values such as approximately 445.4K total sales, 59.45K profit, 6K quantity, 515 customers, and 102.96 average delivery days. Those values do not match an unfiltered calculation from the supplied CSV. For example, the CSV calculates 1.57M total sales, 175.26K total profit, 22,317 quantity, 773 customers, and 3.93 average delivery days.

This indicates that the screenshot likely uses a filtered subset, a different version of the dataset, or different measure definitions. The screenshot should therefore be treated as the visual design reference, while the CSV-derived figures in this README are the reproducible source-of-truth metrics for the attached file.

## Suggested Tooltip Content

Each visual should expose enough context to explain its value:

- **Trend charts**: month, year, sales/profit, and year-over-year comparison
- **KPI cards**: selected filter context and measure definition
- **Map**: state, sales, profit, quantity, and profit margin
- **Rankings**: item name, sales, profit, quantity, and rank
- **Donuts**: category value, sales, percentage of total, and profit

## Reproduction Checklist

1. Load `SuperStore_Sales_Dataset.csv`.
2. Parse both date columns using day-first parsing.
3. Rename the malformed row ID header if a clean model is required.
4. Create year, month, delivery-days, and profit-margin fields.
5. Add the region slicer and enable cross-filtering.
6. Build the ten visuals listed above.
7. Sort month names chronologically and product rankings by descending sales.
8. Validate totals against the verified CSV metrics in this README.
9. Confirm whether empty `Returns` values mean no return before presenting return-related analysis.
