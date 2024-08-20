# SQL-Solution---The-Most-Recent-Three-Orders

## Problem

<img width="733" alt="Screenshot 2024-08-20 at 15 31 14" src="https://github.com/user-attachments/assets/93f0145e-f3f7-4e5a-8bce-1144bc1d38d1">


## Example

<img width="512" alt="Screenshot 2024-08-20 at 15 32 20" src="https://github.com/user-attachments/assets/4c32bb4e-f3c7-4848-9016-5de0fa8c8285">


<img width="691" alt="Screenshot 2024-08-20 at 15 32 40" src="https://github.com/user-attachments/assets/e00023b7-0bfc-4404-a1e7-69ee1a7211f2">


## Solution - MySQL

<img width="792" alt="Screenshot 2024-08-20 at 15 33 11" src="https://github.com/user-attachments/assets/b13b4873-6dcf-4794-82f3-535d746e6f72">

WITH Order_rank AS (
    SELECT customer_id,
           order_id, 
           order_date,
           ROW_NUMBER() OVER(PARTITION BY customer_id ORDER BY order_date DESC) AS rnk
    FROM Orders
)

SELECT Customers.name AS customer_name,
       Order_rank.customer_id,
       Order_rank.order_id,
       Order_rank.order_date
FROM Order_rank
RIGHT JOIN Customers
ON Order_rank.customer_id = Customers.customer_id
WHERE rnk <= 3
ORDER BY Customers.name, 
         Order_rank.customer_id,
         Order_rank.order_date DESC;
