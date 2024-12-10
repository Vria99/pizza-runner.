# pizza-runner.


1stQ.-How many pizzas were ordered? 
```
SELECT
COUNT(order_id) as pizzas_ordered
FROM customer_orders
```

2ndQ.-How many unique customer orders were made?
```
SELECT 
COUNT(DISTINCT order_id) as pizzas_ordered
FROM customer_orders
```

3rdQ.-How many successful orders were delivered by each runner?
```
SELECT 
runner_id,
SUM (CASE
  WHEN cancellation = 'Restaurant Cancellation' THEN 0
  WHEN cancellation = 'Customer Cancellation'THEN 0
  ELSE 1
  END) as sucessfull_delivery
FROM runner_orders
GROUP BY runner_id
```

4thQ.-How many of each type of pizza was delivered?
```
SELECT 
p.pizza_name,
COUNT (c.pizza_id)as pizzas_delivered
FROM customer_orders as c
INNER JOIN runner_orders as r ON c.order_id = r.order_id
INNER JOIN pizza_names as p  ON p.pizza_id= c.pizza_id
WHERE pickup_time <>'null'
GROUP BY p.pizza_name
```

5thQ.-How many Vegetarian and Meatlovers were ordered by each customer?
```
SELECT 
c.customer_id,
p.pizza_name,
COUNT ( p.pizza_name)as pizza_orders
FROM customer_orders as c
INNER JOIN runner_orders as r ON c.order_id = r.order_id
INNER JOIN pizza_names as p  ON p.pizza_id= c.pizza_id
GROUP BY c.customer_id, p.pizza_name
```

6thQ.--What was the maximum number of pizzas delivered in a single order?
```
SELECT order_id, 
COUNT (order_id) as total_orders
FROM customer_orders
GROUP BY order_id 
ORDER BY total_orders DESC
LIMIT 1

```
7thQ--

```

