--1
SELECT ship_city, COUNT(*) FROM orders
GROUP BY ship_city
ORDER BY count DESC

--2
SELECT LEFT (territory_id, 1), COUNT(*) FROM territories
GROUP BY LEFT (territory_id, 1)
ORDER BY COUNT(*) DESC

--3
