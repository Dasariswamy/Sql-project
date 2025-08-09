select * from Pizza_types;

1. Retrieve the total number of orders placed
SELECT COUNT(order_id) AS Total_sales FROM orders_details;

2 . Calculate the total revenue generated from pizza sales.

select ROUND(sum(quantity * price),2) as total_sales  from orders_details
join pizzas on 
orders_details.pizza_id=pizzas.pizza_id ; 

3 . Identify the highest-priced pizza.

SELECT pizza_types .NAME, pizzaS.PRICE
FROM PIZZA_TYPES
JOIN PIZZAS 
ON PIZZA_TYPES.PIZZA_TYPE_ID = PIZZAS.PIZZA_TYPE_ID
ORDER BY PRICE DESC
LIMIT 1;


4. Identify the most common pizza size ordered

SELECT SIZE, COUNT(ORDER_DETAILS_ID) FROM PIZZAS
JOIN ORDERS_DETAILS ON 
ORDERS_DETAILS.PIZZA_ID=PIZZAS.PIZZA_ID 
GROUP BY SIZE
ORDER BY COUNT(ORDER_DETAILS_ID) DESC ;

5. List the top 5 most ordered pizza types along with their quantities.

SELECT sum(ORDERS_DETAILS.QUANTITY) as Most_ordered, PIZZA_TYPES.NAME FROM pIZZA_TYPES
JOIN PIZZAS ON
PIZZA_TYPES.PIZZA_TYPE_ID=PIZZAS.PIZZA_TYPE_ID
JOIN ORDERS_DETAILS ON 
ORDERS_DETAILS.pIZZA_ID=PIZZAS.PIZZA_ID
group by name
order by most_ordered desc
limit 5 ;

6. Join the necessary tables to find the total quantity of each pizza category ordered.

select category, sum(quantity) as total_quantity from pizza_types 
join Pizzas on
pizzas.pizza_type_id=pizza_types.pizza_type_id
join orders_details on 
orders_details.pizza_id=pizzas.Pizza_id 
group by category
order by Total_quantity desc

7. Determine the distribution of orders by hour of the day
 
 select hour(order_time) as hour , count(order_id) as Order_count  from orders 
 group by Hour(order_time) ;
 
 10. Determine the top 3 most ordered pizza types based on revenue for each pizza category.
     
     select pizza_types.name, 
      sum(orders_details.quantity * pizzas.price)  as revenue 
      from pizza_types join pizzas
      on pizzas.pizza_type_id= pizza_types. Pizza_type_id
      join orders_details
      on orders_details.pizza_id= pizzas.pizza_id 
      group by pizza_types.name 
      order by revenue desc 
      limit  3;
      
   
   SELECT order_date,
       SUM(revenue) OVER (ORDER BY order_date) AS cum_revenue
FROM (
    SELECT orders.order_date,
           SUM(orders_details.quantity * pizzas.price) AS revenue
    FROM orders_details
    JOIN pizzas
        ON orders_details.pizza_id = pizzas.pizza_id
    JOIN orders
        ON orders.order_id = orders_details.order_id
    GROUP BY orders.order_date
) AS sales;

    
    

  
