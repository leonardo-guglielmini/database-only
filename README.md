### Selezionare tutti gli uffici, ordinati per nazione

```SQL
SELECT *
FROM `offices`
ORDER BY country
```

### e per città

```SQL
SELECT *
FROM `offices`
ORDER BY country, postal_code
```

### Selezionare tutti gli impiegati, ordinati per titolo e per nome

```SQL
SELECT *
FROM `employees`
ORDER BY title, lastname
```

### Contare quanti impiegati condividono lo stesso ufficio

```SQL
SELECT count(id) AS total_employees, office_id
FROM `employees`
GROUP BY office_id
```

### Contare quanti impiegati condividono la stessa estensione

```SQL
SELECT count(id) AS total_employees, extension
FROM `employees`
GROUP BY extension
```

### Selezionare tutti i prodotti con quantità inferiore a 500 pezzi

```SQL
SELECT *
FROM `products`
WHERE qty < 500
```

### Selezionare tutti i prodotti Ford

```SQL
SELECT *
FROM `products`
WHERE name LIKE '%Ford%'
```

### Contare quanti prodotti Ford hanno quantità inferiore a 500 pezzi

```SQL
SELECT count(id) AS total_products
FROM `products`
WHERE name LIKE '%Ford%' AND qty < 500
```

### Per ogni impiegato mostrare il suo diretto superiore

```SQL
SELECT e.id AS employee_id, e.lastname AS employee_lastname, e.name AS employee_name, s.id AS supervisor_id, s.lastname AS supervisor_lastname, s.name AS supervisor_name
FROM `employees` e
LEFT JOIN `employees` s
ON e.employee_id = s.id;
```

### Per ogni impiegato mostrare il numero di telefono completo

```SQL
SELECT name, lastname, CONCAT(office_id, extension) AS phone
FROM `employees`
```

### Selezionare i 10 ordini più recenti

```SQL
SELECT *
FROM `orders`
ORDER BY date DESC
LIMIT 10
```

### Per ogni cliente mostrare il numero di ordini che ha fatto

```SQL
SELECT c.name, c.lastname, COUNT(o.id) AS total_orders
FROM `customers` as c
LEFT JOIN `orders` as o /*Possibile utilizzare RIGHT JOIN in caso si vogliano escludere clienti senza ordini effettuati*/
ON c.id = o.customer_id
GROUP BY c.id
```

### Per ogni cliente mostrare la quantità di prodotti acquistati in ogni ordine, mostrando anche il nome del prodotto

```SQL
SELECT c.name, c.lastname, o.id, o.date, o.status, p.name, od.quantity
FROM `customers` as c
RIGHT JOIN `orders` as o
ON c.id = o.customer_id
RIGHT JOIN `orderdetails` as od
ON o.id = od.order_id
RIGHT JOIN `products` as p
ON od.product_id = p.id
ORDER BY od.quantity DESC, c.id ASC
```

### Per ogni cliente mostrare il totale speso sulla piattaforma, il costo sostenuto per ogni prodotto ed il guadagno netto per la piattaforma

### Da completare

```SQL
SELECT c.name, c.lastname, COUNT(o.id) as total_orders, SUM(od.quantity) as total_products, SUM(od.quantity*p.MSRP) AS total_spent
FROM `customers` as c
RIGHT JOIN `orders` as o
ON c.id = o.customer_id
RIGHT JOIN `orderdetails` as od
ON o.id = od.order_id
RIGHT JOIN `products` as p
ON od.product_id = p.id
GROUP BY c.id
```
