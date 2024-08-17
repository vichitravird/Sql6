# Sql6

1 Problem 1 : Game Play Analysis II	(https://leetcode.com/problems/game-play-analysis-ii/)

2 Problem 2 : Game Play Analysis III		(https://leetcode.com/problems/game-play-analysis-iii/)

## 3 Problem 3 : Shortest Distance in a Plane		(https://leetcode.com/problems/shortest-distance-in-a-plane/)
<br>
### Solution 1
<br>
SELECT ROUND(SQRT(POW(p1.x - p2.x, 2) + POW(p1.y - p2.y, 2)), 2) AS shortest
FROM
    Point2D AS p1
    JOIN Point2D AS p2 ON p1.x != p2.x OR p1.y != p2.y
ORDER BY 1
LIMIT 1;
<br>
### Solution 2
<br>
SELECT 
    ROUND(MIN(SQRT(POW(p1.x - p2.x, 2) + POW(p1.y - p2.y, 2))), 2) AS shortest_distance
FROM 
    Point2D p1
JOIN 
    Point2D p2 
ON 
    p1.x != p2.x OR p1.y != p2.y;


4 Problem 4 : Combine Two Tables	(https://leetcode.com/problems/combine-two-tables/)

5 Problem 5 : Customers with Strictly Increasing Purchases		(https://leetcode.com/problems/customers-with-strictly-increasing-purchases/)
