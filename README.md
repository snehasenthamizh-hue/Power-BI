E-Commerce Sales Data Preparation and Modeling Using Power BI

Project Overview

This project focuses on preparing and modeling an E-commerce sales dataset using **Microsoft Power BI** and **Power Query Editor**.

The project uses three datasets: List of Orders, Order Details, and Sales Target. These datasets contain information about orders, customers, locations, product categories, sales amounts, profits, and sales targets.

The main goal is to clean and organize the data, create useful calculated columns, summarize business information, and establish relationships between tables so the data can be used for analysis.

 Project Objectives

- Import CSV files into Power BI.
- Clean and transform data using Power Query Editor.
- Correct data types and standardize text values.
- Create new columns for location, profit margin, and profit status.
- Identify and handle missing values and duplicate records.
- Merge related datasets using Order ID.
- Group and summarize data using aggregation operations.
- Create relationships between tables using common columns.

 Tools and Technologies

| Tool | Purpose |
|---|---|
| Microsoft Power BI Desktop | Data preparation and modeling |
| Power Query Editor | Data cleaning and transformation |
| Power BI Model View | Creating and checking table relationships |
| CSV files | Source datasets |

Dataset Description

The project uses three datasets.

 1. List of Orders

Contains order-level information about customers, dates, locations, sales amounts, and profits.

| Column | Description |
|---|---|
| Order ID | Unique identifier intended to identify an order |
| Order Date | Date on which the order was placed |
| Customer Name | Name of the customer |
| City | City associated with the order |
| State | State associated with the order |
| Category | Product category |
| Amount | Order amount |
| Profit | Profit earned or loss incurred |

 2. Order Details

Contains information about order items, quantities, categories, and financial values.

| Column | Description |
|---|---|
| Order ID | Identifier used to connect order details with orders |
| Category | Product category |
| Sub-Category | More specific product classification |
| Quantity | Quantity of products |
| Amount | Amount associated with the order detail |
| Profit | Profit associated with the order detail |

3. Sales Target

Contains sales targets associated with product categories and order months.

| Column | Description |
|---|---|
| Category | Product category |
| Month of Order Date | Month associated with the sales target |
| Target | Sales target value |

 Data Import and Transformation

The CSV datasets are imported into Power BI and prepared using Power Query Editor.

1. Import Data

- Import `List of Orders.csv`.
- Open Power Query Editor using **Transform Data**.
- Import `Order Details.csv` and `Sales Target.csv`.
- Review the columns and data before applying transformations.

 2. Limit Rows and Set Data Types

- Keep the first 500 rows in the List of Orders table.
- Change Order Date to the Date data type.
- Change Amount and Target to Fixed Decimal Number where applicable.

Correct data types help Power BI perform calculations and comparisons accurately.

3. Format Customer Names

The Customer Name column is formatted using **Capitalize Each Word** in Power Query.

This helps standardize capitalization and makes customer names more consistent.

 4. Create a Location Column

Merge the City and State columns to create a new column named `Location`.

**Example format:** `City, State`

This combines location information into one field, making it easier to filter orders by location.

 5. Create a Profit Margin Column

Create a custom column named `Profit Margin` using the formula:

```text
[Profit] / [Amount]
```

Set the resulting column to the Percentage data type.

Profit margin represents profit relative to the amount. Rows with missing or zero Amount values should be checked to avoid invalid or undefined calculations.

 6. Create a Profit Status Column

Create a conditional column named `Profit Status` based on the Profit value.

| Condition | Profit Status |
|---|---|
| Profit < 0 | Loss |
| Profit = 0 | Break-Even |
| Profit > 0 | Profit |

This classification makes it easier to distinguish profitable, loss-making, and break-even records.

### 7. Merge Order Tables

Merge List of Orders with Order Details using `Order ID`.

The assignment specifies a **Left Outer Join**, which keeps all rows from List of Orders and matches available records from Order Details.

Name the merged output table `Orders Data`.

This combined table brings order-level information together with product-level details.

 Data Cleaning

Data quality is important for reliable analysis. The project includes checking missing values and duplicate records across the tables.

Handling Missing Values

The appropriate action depends on the column and the reason for the missing value.

- **Replace missing values:** Only when the correct replacement value is known or can be justified.
- **Remove records:** When a record is invalid or unusable for the intended analysis.
- **Retain null values:** When information is unknown and cannot be safely determined.

Missing values should be reviewed before applying a cleaning rule. The actual number of missing values and the specific replacements made are not reported here because verified counts are not available in the supplied project materials.

 Handling Duplicate Records

Duplicate records should be checked using the appropriate identifying columns.

- Identify exact duplicate rows.
- Confirm whether repeated Order IDs represent valid multiple order items or genuine duplicate records.
- Remove records only when they are confirmed duplicates according to the business rules.
- Review the data after removing duplicates to ensure valid transactions are preserved.

An Order ID appearing more than once in Order Details does not automatically mean the records are duplicates.

Sorting and Filtering

Sort Orders by Date

Sort the `Orders Data` table by Order Date in descending order.

This places the latest order dates first.

 Filter Orders by State

Use the Location column to filter records for a particular state, such as Tamil Nadu.

This allows the dataset to be examined for a selected geographical area without claiming any specific regional sales result.

 Grouping and Aggregation

The project uses duplicated tables and Power Query's **Group By** feature to create summarized datasets.

1. Count of Order ID

Group the duplicated Order Details table by Order ID and use the **Count Rows** operation.

The resulting summary column is named `Count of Order ID`.

This counts the number of detail rows associated with each order ID; it does not necessarily represent the number of unique orders in the entire dataset.

2. Average Profit by Category

Group Order Details by Category and calculate the average of Profit.

Name the resulting column `Average Profit`.

This summary supports comparisons of average profit across categories.

 3. Total Amount by Sub-Category

Group Order Details by Sub-Category and calculate the sum of Amount.

Name the resulting column `Total Amount`.

This summarizes the amount associated with each sub-category.

 4. Total Target by Month

Duplicate the Sales Target table and prepare a monthly target summary.

The assignment describes deriving the month from Order Date and grouping the data by month using the Sum operation on Target.

Name the resulting column `Total Target`.

The month-matching logic should be validated against the actual data model because Sales Target contains a month field rather than an individual order date.

 Data Modeling and Relationships

The project uses common columns to connect related datasets in Power BI Model View.

 Relationship 1: List of Orders and Order Details

| Setting | Description |
|---|---|
| First table | List of Orders |
| Second table | Order Details |
| Common column | Order ID |
| Intended cardinality | One-to-many (1:*) when Order ID is unique in List of Orders |
| Relationship status | Should be active |

The relationship connects each order to its corresponding detail records.

 Relationship 2: Order Details and Sales Target

| Setting | Description |
|---|---|
| First table | Order Details |
| Second table | Sales Target |
| Common column | Category |
| Relationship status | Should be active |
| Cardinality | Must be selected based on the actual uniqueness of Category in each table |

The Category relationship connects product categories with their sales target information.

Because categories can appear multiple times in both tables, the correct cardinality and filter behavior must be verified. A separate category lookup table may be preferable if a direct relationship causes ambiguity or incorrect aggregation.

Both relationships should be checked in **Manage Relationships** to confirm that they are active and correctly configured.

 Project Workflow

The overall workflow follows these steps:

1. Import the three CSV datasets.
2. Limit rows and correct data types.
3. Standardize customer names.
4. Create Location, Profit Margin, and Profit Status columns.
5. Merge List of Orders and Order Details.
6. Review missing values and duplicate records.
7. Sort and filter the order data.
8. Create grouped summaries for order counts, profit, amounts, and targets.
9. Establish and validate relationships between tables.
10. Review the prepared data model for consistency.

 Expected Learning Outcomes

Through this project, I aim to develop practical skills in:

- Importing and transforming data in Power BI.
- Using Power Query for data cleansing.
- Creating custom and conditional columns.
- Joining tables using common keys.
- Applying grouping and aggregation operations.
- Understanding one-to-many relationships and relationship cardinality.
- Preparing structured data for business analysis.

 Project Files

| File | Description |
|---|---|
| `power bi first.pbix` | Power BI project file |
| `PowerBI Ass 1.docx` | Assignment instructions and transformation steps |
| `List of Orders.csv` | Source dataset required for the assignment |
| `Order Details.csv` | Source dataset required for the assignment |
| `Sales Target.csv` | Source dataset required for the assignment |
| `README.md` | Project documentation |

*Note: The three CSV datasets are listed as source files required by the assignment. Confirm that they are included in the GitHub repository before treating them as uploaded project files.*

Conclusion

This project demonstrates the process of preparing E-commerce sales data using Power BI and Power Query Editor. It covers data import, transformation, cleaning, merging, aggregation, and relationship modeling.

The prepared data model provides a foundation for further sales and profit analysis. Actual sales totals, category rankings, profit results, and target performance should be reported only after verifying the underlying data and calculations in Power BI.
