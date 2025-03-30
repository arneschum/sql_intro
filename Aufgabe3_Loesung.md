--1
SELECT ship_city, COUNT(*) FROM orders
GROUP BY ship_city
ORDER BY count DESC

--2
SELECT LEFT (territory_id, 1), COUNT(*) FROM territories
GROUP BY LEFT (territory_id, 1)
ORDER BY COUNT(*) DESC

--5
SELECT category_name,  
SUM(od.unit_price*quantity*(1-discount))
FROM orders o
LEFT JOIN order_details od ON o.order_id=od.order_id	
LEFT JOIN products p ON od.product_id=p.product_id
LEFT JOIN categories ct ON p.category_id=ct.category_id
--WHERE EXTRACT(YEAR FROM shipped_date) = 1997
WHERE date_part('year', shipped_date) = 1997
--AND category_name IN ('Meat/Poultry', 'Seafood')
GROUP BY category_name            
HAVING category_name IN ('Meat/Poultry', 'Seafood')

--7
SELECT c.company_name, c.contact_name, c.address, c.postal_code, c.city, 
SUM(quantity * od.unit_price) AS umsatz
FROM customers c
LEFT JOIN orders o ON c.customer_id=o.customer_id 
LEFT JOIN order_details od ON o.order_id=od.order_id	
LEFT JOIN products p ON od.product_id=p.product_id
LEFT JOIN suppliers s ON p.supplier_id=s.supplier_id
LEFT JOIN categories ct ON p.category_id=ct.category_id
WHERE category_name='Beverages'
GROUP BY c.customer_id
HAVING SUM(quantity * od.unit_price) > 1000
ORDER BY SUM(quantity * od.unit_price) DESC

QUICK-Stop: 28272
