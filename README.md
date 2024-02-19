# SQL-Restaurant

## Scenario
Imagine you're tasked with extracting complex insights from this restaurant management system to improve operational efficiency, enhance customer satisfaction, and optimize menu offerings. You'll need to perform advanced SQL queries to find the total revenue based on the category, total order of the items, who handled the orders and how many orders being handled, and the loyalty points. 

## Database and Tables
```
CREATE DATABASE sql_restaurant;

-- Create Menus table
CREATE TABLE Menus (
    menu_id INT PRIMARY KEY,
    item_name VARCHAR(100),
    description TEXT,
    price DECIMAL(10,2),
    category VARCHAR(50)
);

-- Create Customers table
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    loyalty_points INT
);

-- Create Employees table
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    position VARCHAR(50),
    hire_date DATE
);

-- Create Orders table
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    menu_id INT,
    customer_id INT,
    employee_id INT,
    order_date DATE,
    quantity INT,
    status VARCHAR(50),
    FOREIGN KEY (menu_id) REFERENCES Menus(menu_id),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id),
    FOREIGN KEY (employee_id) REFERENCES Employees(employee_id)
);

-- Insert data into Menus
INSERT INTO Menus (menu_id, item_name, description, price, category) VALUES
(1, 'Caesar Salad', 'Classic Caesar with romaine lettuce, croutons, and parmesan', 8.99, 'Appetizer'),
(2, 'Spaghetti Carbonara', 'Spaghetti with creamy sauce, pancetta, and parmesan', 12.99, 'Main Course'),
(3, 'Margherita Pizza', 'Pizza with tomato, mozzarella, and basil', 10.99, 'Main Course'),
(4, 'Grilled Salmon', 'Salmon fillet with a teriyaki glaze and vegetables', 15.99, 'Main Course'),
(5, 'Tiramisu', 'Classic Italian dessert with mascarpone and espresso', 6.99, 'Dessert'),
(6, 'Chicken Caesar Salad', 'Grilled chicken breast atop classic Caesar salad', 9.99, 'Appetizer'),
(7, 'Beef Burger', 'Beef patty with cheese, lettuce, tomato, on a brioche bun', 11.99, 'Main Course'),
(8, 'Vegetable Stir Fry', 'Mixed vegetables stir-fried with a soy-based sauce', 10.99, 'Main Course'),
(9, 'Chocolate Cake', 'Rich chocolate cake with chocolate ganache', 7.99, 'Dessert'),
(10, 'Lemonade', 'Freshly squeezed lemonade', 3.99, 'Beverage'),
(11, 'Mushroom Risotto', 'Creamy risotto with wild mushrooms', 13.99, 'Main Course'),
(12, 'Pumpkin Soup', 'Creamy pumpkin soup with spices', 5.99, 'Appetizer'),
(13, 'Iced Tea', 'Refreshing iced tea with a hint of lemon', 2.99, 'Beverage'),
(14, 'Ribeye Steak', '10 oz ribeye steak with herb butter', 22.99, 'Main Course'),
(15, 'Apple Pie', 'Classic apple pie with a scoop of vanilla ice cream', 5.99, 'Dessert'),
(16, 'Caprese Salad', 'Fresh tomatoes, mozzarella, basil, and balsamic glaze', 7.99, 'Appetizer'),
(17, 'Chicken Wings', 'Spicy chicken wings with blue cheese dressing', 8.99, 'Appetizer'),
(18, 'Espresso', 'Strong espresso coffee', 2.99, 'Beverage'),
(19, 'Fried Calamari', 'Crispy fried calamari with marinara sauce', 9.99, 'Appetizer'),
(20, 'Margarita Cocktail', 'Classic margarita with tequila, lime, and salt rim', 7.99, 'Beverage');


-- Insert data into Customers
INSERT INTO Customers (customer_id, name, email, phone, loyalty_points) VALUES
(1, 'John Doe', 'johndoe@example.com', '123-456-7890', 100),
(2, 'Jane Smith', 'janesmith@example.com', '123-456-7891', 150),
(3, 'Emily Johnson', 'emilyjohnson@example.com', '123-456-7892', 200),
(4, 'Michael Brown', 'michaelbrown@example.com', '123-456-7893', 250),
(5, 'Isabella Smith', 'isabellasmith@example.com', '123-456-7894', 50);

-- Insert data into Employees
INSERT INTO Employees (employee_id, name, position, hire_date) VALUES
(1, 'Alice Johnson', 'Chef', '2018-05-01'),
(2, 'Bob Lee', 'Waiter', '2019-06-15'),
(3, 'Charlie Davis', 'Manager', '2017-04-12'),
(4, 'Diana Adams', 'Chef', '2018-08-25');


-- Insert data into Orders
INSERT INTO Orders (order_id, menu_id, customer_id, employee_id, order_date, quantity, status) VALUES
(1, 1, 1, 2, '2023-01-15', 2, 'Served'),
(2, 2, 2, 1, '2023-02-20', 1, 'Served'),
(3, 3, 3, 4, '2023-01-20', 1, 'Served'),
(4, 4, 4, 3, '2023-01-25', 2, 'Served');

```

