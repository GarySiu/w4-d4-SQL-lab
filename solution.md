# Write SQL statements that:

### 1. Selects the names of all products that are not on sale.

```SQL
SELECT name FROM products WHERE on_sale = 'f';
```

    Teddy Bear
    Cat Ears
    Card Against Humanity
    Set of 12 Mason Jars

### 2. Selects the names of all products that cost less than £20.

```SQL
SELECT name FROM products WHERE price < 20;
```

    Teddy Bear
    The Ruby Programming Language
    Silicon Valley Monopoly
    Set of 12 Mason Jars

### 3. Selects the name and price of the most expensive product.

```SQL
SELECT name, MAX(price) FROM products;
```

name    | max(price)
--------|-----------
Cat Ears| 99.99

### 4. Selects the name and price of the second most expensive product.

```SQL 
SELECT name, MAX(price) FROM products 
WHERE price < (SELECT MAX(price) FROM products);
```

name               | max(price)
-------------------|-----------
Brown Leather Boots| 82.0

### 5. Selects the name and price of the least expensive product.

```SQL
SELECT name, MIN(price) FROM products;
```

name                 | min(price)
---------------------|-----------
Set of 12 Mason Jars | 6.22

### 6. Selects the names and prices of all products, ordered by price in descending order.

```SQL    
SELECT name, price FROM products ORDER BY price DESC;
```

name                          | price
------------------------------|-------
Cat Ears                      | 99.99
Brown Leather Boots           | 82.0
Lonely Pillow                 | 78.82
Card Against Humanity         | 25.0
Hoodie                        | 25.0
Set of silverware             | 22.99
The Ruby Programming Language | 19.99
Teddy Bear                    | 17.99
Silicon Valley Monopoly       | 10.99
Set of 12 Mason Jars          | 6.22
    
### 7. Selects the average price of all products.

```SQL
SELECT AVG(price) FROM products;
```
	AVG(price)
	38.899
	
### 8. Selects the sum of the price of all products.

```SQL
SELECT SUM(price) FROM products;
```
	SUM(price)
	388.99

### 9. Selects the sum of the price of all products whose prices is less than £20.

```SQL
SELECT SUM(price) FROM products WHERE price < 20;
```
	SUM(price)
	55.19

### 10. Selects the id of the user with your name.

😓 Lets just pretend I'm Gerry or something...

```SQL
SELECT id FROM users WHERE name = 'Gerry Mathe';
```
	id
	13
### 11. Selects the names of all users whose names start with the letter "J".

```SQL
SELECT name FROM users WHERE name LIKE 'J%';
```
	name
	Jon Rogers
	James Gotsell
	
### 12. Selects the number of users whose first names are "Spencer".

Not sure if you want ID number or count?

```SQL
SELECT id FROM users WHERE name LIKE "Spencer %";

--or--

SELECT COUNT(name) FROM users WHERE name LIKE "Spencer %";
```
	id
	11
	
	or 
	
	COUNT(name)
	1

### 13. Selects the number of users who want a "Teddy Bear".

```SQL
SELECT COUNT(product_id) FROM wishlists WHERE product_id =
(SELECT id FROM products WHERE name = 'Teddy Bear');
```
	COUNT(product_id)
	6

### 14. Selects the count of items on the wishlish of the user with your name.

```SQL
SELECT COUNT(user_id) FROM wishlists WHERE user_id = 
(SELECT id FROM users WHERE name = 'Gerry Mathe');
```

	COUNT(user_id)
	3

### 15. Selects the count and name of all products on the wishlist, ordered by count in descending order.

```SQL
SELECT users.name, COUNT(wishlists.product_id)
FROM wishlists
INNER JOIN users 
ON users.id = wishlists.user_id
GROUP BY users.name
ORDER BY COUNT(wishlists.product_id) DESC;
```

Name               | COUNT(wishlists.product_id)
-------------------|----------------------------
Elena Sanna        | 8
Dani Zraikat       | 7
Filippo Matoso     | 7
Hassan Mohammadi   | 7
Spencer Meyer      | 7
Tyrone Compton     | 7
Christabel Samuels | 6
Rane Gowan         | 6
Cheryl Wee         | 5
James Gotsell      | 5
Erica Porter       | 4
Gerry Mathe        | 3
Jon Rogers         | 3
ALex Chin          | 1

### 16. Selects the count and name of all products that are not on sale on the wishlist, ordered by count in descending order.


```SQL
SELECT products.name, COUNT(wishlists.product_id)
FROM wishlists
INNER JOIN products
ON products.id = wishlists.product_id
WHERE products.on_sale = 'f'
GROUP BY products.name
ORDER BY COUNT(wishlists.product_id) DESC;
```
name                  | COUNT(wishlists.product_id)
----------------------|----------------------------
Card Against Humanity | 16
Cat Ears              | 15
Teddy Bear            | 6
Set of 12 Mason Jars  | 2


### 17. Inserts a user with the name "Jonathan Anderson" into the users table. Ensure the created_at column is set to the current time.

```SQL
INSERT INTO users (created_at, name) 
VALUES (CURRENT_TIMESTAMP, 'Jonathan Anderson');
```

Can't get the timestamp formatting to match exactly

### 18. Selects the id of the user with the name "Jonathan Anderson"?

```SQL
SELECT id FROM users WHERE name = 'Jonathan Anderson';
```
	id
	18
### 19. Inserts a wishlist entry for the user with the name "Jonathan Anderson" for the product "The Ruby Programming Language".

```SQL
INSERT INTO wishlists (created_at, user_id, product_id)
VALUES (CURRENT_TIMESTAMP, 
(SELECT id FROM users WHERE name = 'Jonathan Anderson'),
(SELECT id FROM products WHERE name = 'The Ruby Programming Language')); 
```

Timestamp is still wrong

### 20. Updates the name of the "Jonathan Anderson" user to be "Jon Anderson".



### 21. Deletes the user with the name "Jon Anderson".

### 22. Deletes the wishlist item for the user you just deleted.
