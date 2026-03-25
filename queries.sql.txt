-- Top Customers by Balance
SELECT c.name, a.balance
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id
ORDER BY a.balance DESC;

-- Monthly Transactions
SELECT 
    MONTH(transaction_date) AS month,
    SUM(amount) AS total_amount
FROM Transactions
GROUP BY MONTH(transaction_date);

-- Large Transactions (Fraud Detection)
SELECT *
FROM Transactions
WHERE amount > 5000;

-- Total Balance per Customer
SELECT c.name, SUM(a.balance) AS total_balance
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id
GROUP BY c.name;