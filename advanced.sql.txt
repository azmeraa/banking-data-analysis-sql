-- Indexes
CREATE INDEX idx_customer_id ON Accounts(customer_id);
CREATE INDEX idx_account_id ON Transactions(account_id);
CREATE INDEX idx_transaction_date ON Transactions(transaction_date);

-- View
CREATE VIEW vw_customer_balance AS
SELECT 
    c.name,
    SUM(a.balance) AS total_balance
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id
GROUP BY c.name;

-- Stored Procedure
CREATE PROCEDURE GetCustomerTransactions
    @CustomerID INT
AS
BEGIN
    SELECT 
        c.name,
        t.transaction_id,
        t.amount,
        t.transaction_type,
        t.transaction_date
    FROM Customers c
    JOIN Accounts a ON c.customer_id = a.customer_id
    JOIN Transactions t ON a.account_id = t.account_id
    WHERE c.customer_id = @CustomerID;
END;

-- Trigger + Log Table
CREATE TABLE LargeTransactionsLog (
    log_id INT IDENTITY(1,1) PRIMARY KEY,
    transaction_id INT,
    amount DECIMAL(10,2),
    log_date DATETIME DEFAULT GETDATE()
);

GO

CREATE TRIGGER trg_large_transaction
ON Transactions
AFTER INSERT
AS
BEGIN
    INSERT INTO LargeTransactionsLog (transaction_id, amount)
    SELECT transaction_id, amount
    FROM inserted
    WHERE amount > 5000;
END;

-- Window Function
SELECT 
    c.name,
    a.balance,
    RANK() OVER (ORDER BY a.balance DESC) AS rank_position
FROM Customers c
JOIN Accounts a ON c.customer_id = a.customer_id;