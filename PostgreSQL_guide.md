# SQL and PostgreSQL: The Complete Developer's Guide



### The largest cities example



#### Simple SQL Statements



```sql

# Create a table
CREATE TABLE cities(
  name VARCHAR(50),
  country VARCHAR(50),
  population INTEGER,
  area INTEGER
)

# Insert cities into a table
INSERT INTO cities (name, country, population, area)
VALUES
('Tokyo','Japan', 38505000, 8223),
('Delhi','India',28125000,2240),
('Shanghai','China',22125000,4015),
('Sao Paulo', 'Brazil', 20935000, 3043)

 
 # Query data from table
 SELECT name, population FROM cities;
 
 # Calculated Columns
 SELECT name, population / area AS density FROM cities;
 
 # String Operators and Functions
  
 # || Join Two Strings
 SELECT name || ', ' || country AS density FROM cities;
 
 CONCAT() Join Two Strings
 SELECT CONCAT(name,', ' ,country) AS location FROM cities;
 
 # UPPER()
 SELECT
   UPPER(CONCAT(name, ', ', country)) AS location
 FROM
   cities; 
   
 # LOWER()
 SELECT
   LOWER(CONCAT(name, ', ', country)) AS location
 FROM
   cities;
  
 # LENGTH() 
 SELECT
  LENGTH(CONCAT(name, ', ', country)) AS location
 FROM
  cities;
  
 #Query Result
 # location
 # 12
 # 12
 # 15
 # 17
 
```



#### Filtering Records

```sql

SELECT
  name,
  area
FROM
  cities
WHERE
  area > 4000

# BETWEEN
SELECT
  name,
  area
FROM
  cities
WHERE
  area BETWEEN 2000
  AND 4000;

# IN, NOT IN

SELECT
  name,
  area
FROM
  cities
WHERE
  NAME NOT IN ('Delhi', 'Shanghai')

# Combined Statement
SELECT
  name,
  area
FROM
  cities
WHERE
  area NOT IN (3043, 8223)
  OR name = 'Delhi'
  OR name = 'Tokyo'


# Calculations in "Where clauses"
SELECT
  name,
  area
FROM
  cities
WHERE
  population / area > 6000;
  

# Update
UPDATE
  cities
SET
  population = 39505000
WHERE
   name = 'Tokyo' AND country = 'Japan'
  
# Delete
DELETE FROM cities
WHERE name = 'Tokyo'
  
  
  
```



### User Photos and comments Example

```sql

# Create a users table
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50)
);

INSERT INTO users (username)
VALUES
	('monahan93'),
  ('pferrer'),
  ('si93oins'),
  ('99stroman');

# Create a photos table
CREATE TABLE photos (
  id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  user_id INTEGER REFERENCES users(id)
);


INSERT INTO photos (url, user_id)
VALUES
('http://one.jpg',4),
('http://2.jpg',1),
('http://3.jpg',2),
('http://4.jpg',1),
('http://5.jpg',3),
('http://6.jpg',3),
('http://7.jpg',4);


SELECT
  *
FROM
  photos
WHERE
  user_id = 3;

# Join statement

SELECT
  url,
  username
FROM
  photos
  JOIN users ON users.id = photos.user_id;

```



### Delete

```sql


# ON DELETE CASCADE
# Delete all realted data

CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id) ON DELETE CASCADE
);

INSERT INTO photos (url, user_id)
VALUES
  ('http:/one.jpg', 4),
  ('http:/two.jpg', 1),
  ('http:/25.jpg', 1),
  ('http:/36.jpg', 1),
  ('http:/754.jpg', 2),
  ('http:/35.jpg', 3),
  ('http:/256.jpg', 4);
    
   
# ON DELETE SET NULL
CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id) ON DELETE SET NULL
);
     
INSERT INTO photos (url, user_id)
VALUES
('http:/one.jpg', 4),
('http:/754.jpg', 2),
('http:/35.jpg', 3),
('http:/256.jpg', 4);
    

```







 
