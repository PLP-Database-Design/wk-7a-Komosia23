-- Step 1NF: Create a new table with one product per row
CREATE TABLE ProductDetail_1NF (
    OrderID INT,
    CustomerName VARCHAR(100),
    Product VARCHAR(100)
);

-- Insert normalized data
INSERT INTO ProductDetail_1NF (OrderID, CustomerName, Product)
VALUES 
(101, 'John Doe', 'Laptop'),
(101, 'John Doe', 'Mouse'),
(102, 'Jane Smith', 'Tablet'),
(102, 'Jane Smith', 'Keyboard'),
(102, 'Jane Smith', 'Mouse'),
(103, 'Emily Clark', 'Phone');
-- Step 2NF: Create two separate tables

-- Table for orders (OrderID and CustomerName)
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerName VARCHAR(100)
);

-- Table for order details (OrderID and Product info)
CREATE TABLE OrderDetails_2NF (
    OrderID INT,
    Product VARCHAR(100),
    Quantity INT,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);

-- Insert data into Orders table
INSERT INTO Orders (OrderID, CustomerName)
VALUES 
(101, 'John Doe'),
(102, 'Jane Smith'),
(103, 'Emily Clark');

-- Insert data into OrderDetails_2NF
INSERT INTO OrderDetails_2NF (OrderID, Product, Quantity)
VALUES 
(101, 'Laptop', 2),
(101, 'Mouse', 1),
(102, 'Tablet', 3),
(102, 'Keyboard', 1),
(102, 'Mouse', 2),
(103, 'Phone', 1);
