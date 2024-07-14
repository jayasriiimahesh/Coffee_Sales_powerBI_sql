# Coffee_Sales_powerBI_sql

1.YTD to total sales

SELECT SUM(price) AS YTD_Total_Sales
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE());

2. Month-To-Date total sales

SELECT SUM(price) AS MTD_Total_Sales
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE())
  AND MONTH(date) = MONTH(CURDATE());

3. Year-To-Date Average sales

SELECT AVG(price) AS YTD_Average_Price
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE());

4. MTD Average Sales

SELECT AVG(price) AS MTD_Average_Price
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE())
  AND MONTH(date) = MONTH(CURDATE());

5. YoY growth average price

SELECT (AVG(current_year.price) - AVG(previous_year.price)) / AVG(previous_year.price) * 100 AS YOY_Growth_Average_Price
FROM coffee_sales current_year, coffee_sales previous_year
WHERE YEAR(current_year.date) = YEAR(CURDATE())
  AND YEAR(previous_year.date) = YEAR(CURDATE()) - 1;

6. Difference between YTD Average Price and PTYD Average Price:

SELECT AVG(current_year.price) - AVG(previous_year.price) AS Difference_YTD_PTYD_Average_Price
FROM coffee_sales current_year, coffee_sales previous_year
WHERE YEAR(current_year.date) = YEAR(CURDATE())
  AND YEAR(previous_year.date) = YEAR(CURDATE()) - 1;

7. YTD Cars Sold:

SELECT COUNT(*) AS YTD_Cars_Sold
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE());

8. MTD Cars Sold:

SELECT COUNT(*) AS MTD_Cars_Sold
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE())
  AND MONTH(date) = MONTH(CURDATE());

9. YOY Growth in Cars Sold:

SELECT (COUNT(current_year.id) - COUNT(previous_year.id)) / COUNT(previous_year.id) * 100 AS YOY_Growth_Cars_Sold
FROM coffee_sales current_year, coffee_sales previous_year
WHERE YEAR(current_year.date) = YEAR(CURDATE())
  AND YEAR(previous_year.date) = YEAR(CURDATE()) - 1;

10. Difference between YTD Cars Sold and PTYD Cars Sold:

SELECT COUNT(current_year.id) - COUNT(previous_year.id) AS Difference_YTD_PTYD_Cars_Sold
FROM coffee_sales current_year, coffee_sales previous_year
WHERE YEAR(current_year.date) = YEAR(CURDATE())
  AND YEAR(previous_year.date) = YEAR(CURDATE()) - 1;

11. YTD Sales Weekly Trend:

SELECT WEEK(date) AS Week, SUM(price) AS Total_Sales
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE())
GROUP BY WEEK(date)
ORDER BY Week;

12. YTD Total Sales by Body Style:

SELECT body_style, SUM(price) AS Total_Sales
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE())
GROUP BY body_style;

13. YTD Total Sales by Color:

SELECT color, SUM(price) AS Total_Sales
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE())
GROUP BY color;

14. YTD Cars Sold by Dealer Region:

SELECT dealer_region, COUNT(*) AS Cars_Sold
FROM coffee_sales
WHERE YEAR(date) = YEAR(CURDATE())
GROUP BY dealer_region;
