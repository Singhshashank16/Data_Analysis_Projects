One to Many SQL Queries


Que1. Report the account representative for each customer.

SELECT customers.customerNumber, customers.customerName, employees.employeeNumber, concat(employees.firstName , employees.lastName) AS Account_Representative, employees.jobTitle
FROM classicmodels.employees
RIGHT JOIN customers ON employees.employeeNumber = customers.salesRepEmployeeNumber
order by customerName;




Que2. Report total payments for Atelier graphique.

SELECT customers.customerName, SUM(amount) AS Total_Payments
From payments
JOIN customers ON payments.customerNumber = customers.customerNumber
WHERE customers.customerName = 'Atelier graphique';





Que3.  Report the total payments by date.

SELECT paymentDate, SUM(payments.amount) AS Total_payment
FROM payments
GROUP BY paymentDate;





Que 4. Report the products that have not been sold.

SELECT products.productCode, products.productName
FROM products
LEFT JOIN orderdetails ON products.productCode = oederdetails.productCode
WHERE orderdetails.oederNumber IS NULL;




Que5.  List the amount paid by each customer.

SELECT customers.customerName, SUM(payments.amount) AS AMOUNT_PAID
FROM customers 
JOIN payments ON customers.customerNumber = payments.customerNumber
group by customers.customerName;





Que6. How many orders have been placed by Herkku Gifts?

Select customers.customerName, SUM(orderdetails.quantityOrdered) As TOTAL_PRODUCTS_ORDERED
FROM orderdetails
JOIN orders ON orderdetails.orderNumber = orders.orderNumber
JOIN customers ON orders.customerNumber = customers.customerNumber
WHERE customers.customerName = 'Herkku Gifts'
GROUP BY customers.customerName;





Que7. Who are the employees in Boston?

SELECT CONCAT(employees.firstName, CONCAT(' ', employees.lastName)) AS Employees
FROM employees
JOIN offices ON employees.officeCode = offices.officeCode
WHERE offices.city = 'Boston';





Que8.  Report those payments greater than $100,000. Sort the report so the customer who made the highest payment appears first.

SELECT customers.customerName, SUM(payments.amount) AS AMOUNT_PAID
FROM customers
JOIN payments ON customers.customerNumber = payments.customerNumber
Group by customers.customerName
Having AMOUNT_PAID > 100000
order by AMOUNT_PAID DESC;





Que9. List the value of 'On Hold' orders.

SELECT sum(quantityOrdered*priceEach) AS Value_ON_HOLD
FROM orderdetails
JOIN orders ON orderdetails.orderNumber = orders.orderNumber
WHERE orders.status = 'On Hold'





Que10. Report the number of orders 'On Hold' for each customer.

SELECT customers.customerName, count(orders.status) AS ORDERS_ON_HOLD
FROM customers
LEFT JOIN orders ON customers.customerNumber = orders.customerNumber
AND orders.status = 'on hold'
GROUP BY customerName
order by 2 DESC;
