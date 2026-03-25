INSERT INTO Customers VALUES
(1, 'Abel Tesfaye', 'Addis Ababa'),
(2, 'Sara Bekele', 'Adama'),
(3, 'John Doe', 'Hawassa');

INSERT INTO Accounts VALUES
(101, 1, 15000, 'Savings'),
(102, 2, 25000, 'Current'),
(103, 3, 5000, 'Savings');

INSERT INTO Transactions VALUES
(1001, 101, 2000, 'Deposit', '2025-01-01'),
(1002, 101, 500, 'Withdrawal', '2025-01-05'),
(1003, 102, 3000, 'Deposit', '2025-02-01'),
(1004, 103, 1000, 'Deposit', '2025-03-01'),
(1005, 102, 7000, 'Withdrawal', '2025-03-10');