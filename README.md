# SQL-Restaurant

## Scenario
Imagine you're tasked with extracting complex insights from this restaurant management system to improve operational efficiency, enhance customer satisfaction, and optimize menu offerings. You'll need to perform advanced SQL queries to: 
1. Find the total revenue based on the category.
2. Investigate how many item have been ordered.
3. Determine who handled the orders and how many orders being handled.
4. Find the loyalty points. 

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
## Solutions
1. Find the total revenue based on the category:
```
SELECT m.category, SUM(m.price * o.quantity) AS revenueCategory
FROM menus m
JOIN orders o
ON m.menu_id = o.menu_id
GROUP BY m.category
ORDER BY revenueCategory DESC;
```
This query will print the total revenue based on the food category.
* First, I set the initials. `m` stands for `menus`, and `o` stands for `order`. I selected `category` and `revenueCategory`.
* Second, from `menus` table, I joined it with `orders` table on the condition that `menu_id` from `menus` table matches the `menu_id` on the table `orders`.
* Third, `SUM` is an aggregate function so I wrote `GROUP BY` and `ORDER BY`.
* The output:
  
![heidisql_OBNlVoSJWd](https://github.com/Kwangsa19/SQL-Restaurant/assets/135963482/3ec9302e-4e82-4d5b-b974-8c0124c6b386)



2. Investigate how many item have been ordered:
```
SELECT m.item_name, SUM(o.quantity) AS TotalOrdered
FROM menus m 
JOIN orders o
ON m.menu_id = o.menu_id
GROUP BY m.item_name
ORDER BY TotalOrdered DESC
LIMIT 5;
```
This query will print the quantity of the items ordered by customers. 
* First, I selected `item_name` in the table `menus` and `OrderedCount` to appear in the output.
* Second, I joined `menus` table and `orders` table on the condition that `menu_id` from table menus matches `menu_id` on the table `orders`.
* Third, I grouped them by `item_name`.
* Fourth, I sorted them with `ORDER BY TotalOrdered DESC`.
* The output: 

![heidisql_uKVinNUlO6](https://github.com/Kwangsa19/SQL-Restaurant/assets/135963482/e5c663dd-8188-4420-96aa-f98f22192776)


3. Determine who handled the orders and how many orders being handled:

```
SELECT e.name, e.position, COUNT(o.order_id) AS orders_handled
FROM employees e
JOIN orders o
ON e.employee_id = o.order_id
GROUP BY e.employee_id
ORDER BY orders_handled DESC;
```
This query will print who handled the orders and how many orders being handled by the respective employees. 
* First, I selected `e.name`, `e.position`, and `orders_handled`.
* Second, I joined `employees` and `orders` tables on the condition `employee_id` from `employees` table matches `order_id` from `orders` table.
* Third, I grouped by  `e.employee_id`.
* Fourth, I sorted by `ORDER BY orders_handled DESC;`
* The output: 

![heidisql_qBnfOX1CLW](https://github.com/Kwangsa19/SQL-Restaurant/assets/135963482/c9223eaf-9fd8-4a79-8723-e7736d8328f0)


4. Find the loyalty points:
```
SELECT c.name, c.loyalty_points 
FROM customers c
ORDER BY c.loyalty_points DESC;
```
This will show loyalty points owned by each customer. 
* First, I selected `c.name` and `c.loyalty_points` to appear in the output.
* Second, I selected those columns from `customers` table.
* Third, I sorted out the `loyalty_points` DESC.
* The output:
  
![heidisql_kQURoNaswW](https://github.com/Kwangsa19/SQL-Restaurant/assets/135963482/d4ba3a84-790c-421f-aba7-69c770b24e5f)

## Conclusion
1. Find the total revenue based on the category: `Main_courrse` with `55,95` and `Appetizer` with `17.98`. 
2. Investigate how many item have been ordered: `caesar salad`, `grilled salmon`, and followed by `spaghethi carbonara` and `magherita pizza` (tied).
3. Determine who handled the orders and how many orders being handled: `Alicia Johnson`, `Bob Lee`, `Charlie Davis`, and `Diana Adams`. 
4. Find the top 3 loyalty points for each customer: `Michael Brown`, `Emily Johnson`, and `Jane Smith`.
