# Sql6

## 1 Problem 1 : Game Play Analysis II	(https://leetcode.com/problems/game-play-analysis-ii/)
### Solution 1 Using Window Function Rank, Dense Rank or Row NUmber
<br>

WITH
    T AS (
        SELECT
            *,
            RANK() OVER (
                PARTITION BY player_id
                ORDER BY event_date
            ) AS rk
        FROM Activity
    )
SELECT player_id, device_id
FROM T
WHERE rk = 1;

<br>

### Solution 2 Using Subquery

SELECT
    player_id,
    device_id
FROM Activity
WHERE
    (player_id, event_date) IN (
        SELECT
            player_id,
            MIN(event_date) AS event_date
        FROM Activity
        GROUP BY 1
    );

## 2 Problem 2 : Game Play Analysis III		(https://leetcode.com/problems/game-play-analysis-iii/)
<br>

### Solution 1 USing Window Function
SELECT 	player_id, event_date,
	sum(games_played) over(partition by player_id order by event_date) as games_played_so_far
FROM Activity

<br>

### Solution 2 USing Self Join
SELECT 	t1.player_id, t1.event_date,
	sum(t2.games_played) as games_played_so_far
FROM Activity t1, Activity t2
ON t1.player_id=t2.player_id and t1.event_date>=t2.event_date
<br>

## 3 Problem 3 : Shortest Distance in a Plane		(https://leetcode.com/problems/shortest-distance-in-a-plane/)
<br>

### Solution 1 Using Self Join with Limit
<br>
SELECT ROUND(SQRT(POW(p1.x - p2.x, 2) + POW(p1.y - p2.y, 2)), 2) AS shortest
FROM
    Point2D AS p1
    JOIN Point2D AS p2 ON p1.x != p2.x OR p1.y != p2.y
ORDER BY 1
LIMIT 1;
<br>

### Solution 2 Using Self Join with Min
<br>
SELECT 
    ROUND(MIN(SQRT(POW(p1.x - p2.x, 2) + POW(p1.y - p2.y, 2))), 2) AS shortest_distance
FROM 
    Point2D p1
JOIN 
    Point2D p2 
ON 
    p1.x != p2.x OR p1.y != p2.y;


## 4 Problem 4 : Combine Two Tables	(https://leetcode.com/problems/combine-two-tables/)
<br>
SELECT p.firstName, p.lastName, a.city, a.state
FROM Person p Left Join Address a
ON p.personId=a.personId
<br>

## 5 Problem 5 : Customers with Strictly Increasing Purchases		(https://leetcode.com/problems/customers-with-strictly-increasing-purchases/)
<br>
select
    customer_id
from
    (
        select
            customer_id,
            year(order_date),
            sum(price) as total,
            year(order_date) - rank() over(
                partition by customer_id
                order by
                    sum(price)
            ) as rk
        from
            Orders
        group by
            customer_id,
            year(order_date)
    ) t
group by
    customer_id
having
    count(distinct rk) = 1; 
