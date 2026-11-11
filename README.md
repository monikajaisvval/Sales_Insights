## Sales Insights Data Analysis Project

### Instructions to setup mysql on your local computer

1. SQL database dump is in db_dump.sql file above. Download `db_dump.sql` file to your local computer and import it as per instructions given in the tutorial video

### Data Analysis Using SQL

1. Show all customer records

    `SELECT * FROM customers;`

2. Show total number of customers

SELECT count(*) FROM customers;`

3. Alter name of currency to INR and USD to INR#/r and USD#/r

    SET SQL_SAFE_UPDATES = 0;
    UPDATE transactions
    SET currency = REPLACE(currency, '\r', '')
    WHERE currency LIKE '%\r';
    SET SQL_SAFE_UPDATES = 1;

4. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

5. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

6. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`

7. Show transactions in 2020 join by date table

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

8. Show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR" or transactions.currency="USD";`
	
9. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR" or transactions.currency="USD");`

10. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`


Data Analysis Using Power BI
============================

1. Formula to create Norm_Sales_Amount column

`= Table.AddColumn(#"Remove -1/0 in sales_amount", "Norm_Sales_Amount", each if [currency] = "USD" then [sales_amount]*75 else [sales_amount])



