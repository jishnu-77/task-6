# Online Sales Analysis Using SQL
```markdown
# SQL Sales Analysis Queries

This repository contains SQL queries for analyzing sales data, including monthly revenue, order volume, and filtered results by specific months.

## Dataset Structure

The dataset consists of a sales table with the following columns:

| Column Name       | Description                            |
|-------------------|----------------------------------------|
| Transaction ID    | Unique identifier for each transaction |
| Date              | Date of the transaction (YYYY-MM-DD)   |
| Product Category  | Category of the product sold           |
| Product Name      | Name of the product                    |
| Units Sold        | Quantity sold                          |
| Unit Price        | Price per unit                         |
| Total Revenue     | Units Sold × Unit Price                |
| Region            | Geographical region of the sale        |
| Payment Method    | Method of payment                      |


## Extracting Month from `Date` Column

### Month as a Number
```sql
SELECT 
  `Transaction ID`,
  `Date`,
  MONTH(`Date`) AS `Month`
FROM 
  your_table_name;
```

### Month as a Name
```sql
SELECT 
  `Transaction ID`,
  `Date`,
  MONTHNAME(`Date`) AS `Month_Name`
FROM 
  your_table_name;
```

## Monthly Revenue Grouping

### Total Revenue by Month (Sorted)
```sql
SELECT 
  MONTH(`Date`) AS `Month_Number`,
  MONTHNAME(`Date`) AS `Month_Name`,
  SUM(`Total Revenue`) AS `Monthly_Revenue`
FROM 
  your_table_name
GROUP BY 
  MONTH(`Date`), MONTHNAME(`Date`)
ORDER BY 
  MONTH(`Date`);
```

## Monthly Order Volume

### Count of Unique Orders by Month
```sql
SELECT 
  MONTH(`Date`) AS `Month_Number`,
  MONTHNAME(`Date`) AS `Month_Name`,
  COUNT(DISTINCT `Transaction ID`) AS `Order_Volume`
FROM 
  your_table_name
GROUP BY 
  MONTH(`Date`), MONTHNAME(`Date`)
ORDER BY 
  MONTH(`Date`);
```

## Filter: Sales Only in July

### Using Month Number
```sql
SELECT *
FROM your_table_name
WHERE MONTH(`Date`) = 7;
```

### Using Month Name
```sql
SELECT *
FROM your_table_name
WHERE MONTHNAME(`Date`) = 'July';
```

## Notes

- `MONTH()` and `MONTHNAME()` are MySQL date functions.
- Prefer `MONTH()` for indexing and performance on large datasets.
- Make sure `Date` is in `DATE` or `DATETIME` format for accurate results.
