# Project Overview: Pizza Delivery Data Analysis Project

### Introduction

The Pizza Delivery Data Analysis Project is a comprehensive exploration of pizza order and delivery data using SQL queries. This project aims to extract actionable insights from the dataset to understand customer behavior, delivery performance, and pizza preferences in the context of a pizza delivery service.

### Dataset

The dataset used for this analysis includes tables related to customer orders, pizza types, delivery information, and customer details. Each table contains key information such as order IDs, customer IDs, pizza types, delivery statuses, timestamps, and additional order details.

### Goals

The main objectives of this project are:

- Calculate the total number of pizzas ordered.
  
- Identify unique customer orders and analyze customer order patterns.
  
- Assess delivery performance by analyzing successful deliveries made by each runner.
  
- Analyze the distribution of pizza types and customer preferences (e.g., Vegetarian vs. Meatlovers).
  
- Determine peak order volumes by hour of the day and day of the week.
  
### Methodology

SQL queries are used to query and analyze the dataset. Various SQL operations such as aggregations, joins, and conditional filtering are applied to extract relevant information and derive insights from the data.

### Technologies used:

- Excel - Data cleaning.
- MYSQL - Data exploration.

## SQL Queries

1. How many pizzas were ordered?
   ``` SQL
   SELECT COUNT(order_id) AS Total_Pizza_ordered FROM customer_orders;
   ```
   ![Screenshot 2024-05-02 104748](https://github.com/Emmaue/pizza-delivery-data-analysis-using-MYSQL/assets/87420794/f55ff143-92f6-4f61-8cba-7a83c88954f8)

   Explanation: This query calculates the total number of pizzas ordered by counting distinct order_id values from the customer_orders table.

2. How many unique customer orders were made?
   ``` SQL
   SELECT customer_id, COUNT(DISTINCT order_id) AS unique_customer_orders FROM customer_orders GROUP BY customer_id;
   ```
   Explanation: This query counts the number of unique orders per customer by grouping customer_orders by customer_id and counting the distinct order_id.

3. How many successful orders were delivered by each runner?
   ``` SQL
   SELECT runner_id, COUNT(*) AS Succesful_delivery FROM customer_orders C JOIN runner_orders R ON C.order_id = R.order_id WHERE cancellation IS NULL GROUP BY runner_id;
   ```
   
![Screenshot 2024-05-02 105550](https://github.com/Emmaue/pizza-delivery-data-analysis-using-MYSQL/assets/87420794/1a9da734-c0c8-4699-8f8c-100d6e2b2d59)

Explanation: This query counts successful deliveries by each runner by joining customer_orders with runner_orders on order_id and filtering out cancelled orders.

4. How many of each type of pizza was delivered?
   ``` SQL
   SELECT pizza_id, COUNT(*) AS Delivered_pizza_type FROM customer_orders C JOIN runner_orders R ON C.order_id = R.order_id WHERE cancellation IS NULL GROUP BY pizza_id;
   ```
   
![Screenshot 2024-05-02 105851](https://github.com/Emmaue/pizza-delivery-data-analysis-using-MYSQL/assets/87420794/c2ad7363-e11c-4240-9a33-1e1872c00ed9)
Explanation: This query counts the number of each type of pizza delivered by joining customer_orders with runner_orders and grouping by pizza_id.

5. How many Vegetarian and Meatlovers were ordered by each customer?
  ``` SQL
   SELECT N.pizza_name1, COUNT(C.customer_id) AS No_customers_ordered FROM customer_orders C JOIN pizza_names N ON C.pizza_id = N.pizza_id GROUP BY N.pizza_name1;
   ```


 ![Screenshot 2024-05-02 110139](https://github.com/Emmaue/pizza-delivery-data-analysis-using-MYSQL/assets/87420794/ad9331a6-1c30-4757-a847-840b0357b8dd)

 Explanation: This query counts the number of Vegetarian and Meatlovers pizzas ordered by each customer after joining customer_orders with pizza_names.

6. What was the maximum number of pizzas delivered in a single order?
   ``` SQL
   SELECT C.order_id, COUNT(*) AS Num_pizzas_delivered FROM customer_orders C JOIN runner_orders R ON C.order_id = R.order_id WHERE cancellation IS NULL GROUP BY C.order_id ORDER BY Num_pizzas_delivered DESC;
   ```

![Screenshot 2024-05-02 112320](https://github.com/Emmaue/pizza-delivery-data-analysis-using-MYSQL/assets/87420794/541a7446-5566-445c-94ca-e71c442c2044)

Explanation: This query identifies the order with the maximum number of pizzas delivered by grouping orders and sorting in descending order.

7. How many pizzas were delivered that had both exclusions and extras?
   ``` SQL
   SELECT COUNT(*) AS Pizza_delivered FROM customer_orders C JOIN runner_orders R ON C.order_id = R.order_id WHERE cancellation IS NULL AND exclusions IS NOT NULL AND extras IS NOT NULL;
   ```

   ![Screenshot 2024-05-02 112629](https://github.com/Emmaue/pizza-delivery-data-analysis-using-MYSQL/assets/87420794/52ded0b8-9689-4e00-9498-ce576b9165a9)

Explanation: This query counts pizzas with both exclusions and extras from customer_orders joined with runner_orders.

8. What was the total volume of pizzas ordered for each hour of the day?
   ``` SQL
   SELECT COUNT(*) AS total_pizzas_ordered, HOUR(order_time) AS hour_of_day  FROM customer_orders C JOIN runner_orders R ON C.order_id = R.order_id GROUP BY HOUR(order_time) ORDER BY hour_of_day;
   ```
9. What was the volume of orders for each day of the week?
     ``` SQL
   SELECT COUNT(*) AS total_pizzas_ordered, WEEKDAY(order_time) AS Day_of_week  FROM customer_orders C JOIN runner_orders R ON C.order_id = R.order_id GROUP BY WEEKDAY(order_time) ORDER BY Day_of_week;
   ```

     ![Screenshot 2024-05-02 113132](https://github.com/Emmaue/pizza-delivery-data-analysis-using-MYSQL/assets/87420794/f0c0ea75-4e59-4eb5-9149-9da36891ba3e)

Explanation: This query calculates the volume of orders for each day of the week by extracting the weekday from order_time.

### Conclusion

By completing this analysis, we aim to provide valuable insights that can guide decision-making processes for optimizing pizza delivery services, improving customer satisfaction, and enhancing overall operational efficiency within the pizza delivery industry. The project showcases the importance of data analysis in deriving actionable insights and driving informed business decisions.
