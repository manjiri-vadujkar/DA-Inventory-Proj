# DA-Inventory-Proj
**GitHub README Draft**

**Dataset Details**

**Background:**

Any Manufacturing Company is a medium-sized manufacturing company that produces electronic components. They have a wide range of products and maintain an inventory of raw materials, work-in-progress (WIP), and finished goods. The company has been experiencing issues with inventory management, including stockouts, excess inventory, and increased carrying costs. The management team wants to conduct an inventory analysis to identify areas for improvement and optimize their inventory management practices.

**Details Available:**

1. Inventory records: Detailed records of all inventory transactions, including purchases, production, sales, and adjustments.
2. Demand data: Historical sales data for different products.
3. Lead time data: Information on the time required to receive raw materials and produce finished goods.
4. Cost data: Information on the cost of raw materials, production, and carrying costs.

**Schema:**
Refer to the image uploaded in repo.

**Objectives:**

1. **Perform Data Cleaning and Validation**
   Objective: Clean and validate the data by removing duplicates, filling missing values, and ensuring correct formats in the dataset
   Steps:

   1. For each table (e.g., `inventory`, `begINV`, `endINV`, `purchases`, and `sales`), check for missing or null values, especially in key columns like `InventoryID`, `VendorNo`, `SalesDate`, etc.
   2. Ensure all dates (`StartDate`, `EndDate`, `SalesDate`, `PODate`, etc.) are properly formatted.
   3. Remove duplicates based on unique keys like `InventoryID`, `PONumber`, and `VendorNo`.
   4. Drop unnecessary or irrelevant columns if any exist, such as `classification` in some cases.

2. **Analyze Lead Time Variability**
   Objective: Identify variability in lead times for different products from purchase to receiving.
   Steps:

   1. Use the `purchases` table and calculate the lead time by subtracting `PODate` from `ReceivingDate`.
   2. Group by `InventoryID` and `VendorNo` to calculate the standard deviation and variance of lead times.
   3. Identify products or vendors with high lead time variability and store results for reporting.

3. **Calculate Average Lead Time for Products**
   Objective: Determine the average lead time for each product based on the `purchases` table.
   Steps:

   1. Calculate the average lead time for each product by grouping `InventoryID` and aggregating the lead time (difference between `PODate` and `ReceivingDate`).
   2. Store and visualize the results for understanding the typical delays in the procurement process.

4. **Calculate Average Cost per Product**
   Objective: Compute the average cost per product based on purchase price and quantity data in the `purchases` table.
   Steps:

   1. Group the `purchases` table by `InventoryID` and calculate the average purchase price (`Purchaseprice`).
   2. Use the `Dollars` column to calculate the total cost per product.
   3. Save the results for further financial analysis and inventory valuation.

5. **Determine Total Carrying Costs**
   Objective: Calculate the total carrying costs for the inventory based on `begINV` and `endINV` data.
   Steps:

   1. Use the `Price` column in `begINV` and `endINV` tables to estimate the value of inventory over time.
   2. Combine storage costs, depreciation, and opportunity costs (if available or estimated externally) to calculate total carrying costs.
   3. Group by `InventoryID` for product-level insights on carrying costs.

6. **Identify Overstocked Products**
   Objective: Identify overstocked products based on `begINV`, `endINV`, and `sales`
   Steps:

   1. Compare the `OnHand` quantities in `begINV` and `endINV` with the sales quantities in the `sales` table.
   2. Identify products where the ending inventory significantly exceeds sales over the period.
   3. Store and report overstocked products for decision-makers to act on stock reduction strategies.

7. **Analyze Stock Turnover Rate**
   Objective: Calculate the stock turnover rate using `begINV`, `endINV`, and `sales` data.
   Steps:

   1. Calculate the average inventory for each product using the `OnHand` values from `begINV` and `endINV`.
   2. Use the `SalesQuantity` from the `sales` table to compute stock turnover using the formula: `Stock Turnover Rate = SalesQuantity / Average Inventory`.
   3. Store and visualize results to identify slow-moving products.

8. **Identify Top-Selling Products**
   Objective: Analyze the `sales` data to find the top 10 products by sales volume.
   Steps:

   1. Group the `sales` table by `InventoryID` and sum the `SalesQuantity`.
   2. Sort the results by total sales and identify the top 10 selling products.
   3. Store this list for further analysis or visualization.

9. **Identify Seasonal Demand Trends**
   Objective: Analyze seasonal demand trends based on `sales` data.
   Steps:

   1. Convert `SalesDate` to a time series format and group by `InventoryID` and monthly/quarterly periods.
   2. Look for trends or patterns in sales quantities to identify seasonal peaks or lows.
   3. Store the seasonal analysis for product demand forecasting.

10. **Forecast Future Demand**
    Objective: Forecast future demand for top-selling products using historical `sales` data.
    Steps:

    1. Filter for the top products identified in the earlier step.
    2. Apply simple forecasting methods such as moving averages or more advanced models like ARIMA to predict future sales.
    3. Store the forecasts in S3 for future inventory and procurement planning.
