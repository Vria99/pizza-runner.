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
