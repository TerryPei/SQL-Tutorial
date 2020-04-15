# SQL-Tutorial
SQL practice







# LESSON 7: OUTER JOINs

```SQL
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table
    ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

## Lab 7:
1.Find the list of all buildings that have employees 

```SQL
SELECT DISTINCT Building FROM Employees
LEFT JOIN Buildings on Buildings.Building_name = Employees.Building
```

2.Find the list of all buildings and their capacity

```SQL
SELECT * FROM Buildings
```

3.List all buildings and the distinct employee roles in each building (including empty buildings)

```SQL
SELECT DISTINCT building_name, role
FROM Buildings 
LEFT JOIN Employees
        ON  Buildings.building_name = Employees.building

```



# LESSON 8: A short note on NULLs

```SQL
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
AND/OR …;
```

## Lab 8
1.Find the name and role of all employees who have not been assigned to a building ✓

```SQL
SELECT Role, Name FROM Employees
WHERE Building IS NULL
```

2.Find the names of the buildings that hold no employees

```SQL
SELECT * FROM Buildings
LEFT JOIN Employees 
ON Buildings.Building_name = Employees.Building
WHERE name IS NULL
```

# LESSON 9: Queries with expressions

```SQL
SELECT column AS better_column_name, …
FROM a_long_widgets_table_name AS mywidgets
INNER JOIN widget_sales
  ON mywidgets.id = widget_sales.widget_id;
```

```SQL
SELECT particle_speed / 2.0 AS half_particle_speed
FROM physics_data
WHERE ABS(particle_position) * 10.0 > 500;
```

## Lab 9

1.List all movies and their combined sales in millions of dollars ✓

```SQL
SELECT 
    title, 
    (International_sales + Domestic_sales) / 1000000 AS total_sales
FROM  Movies
INNER JOIN Boxoffice
        ON Movies.id = Boxoffice.movie_id
```

2.List all movies and their ratings in percent

```SQL
SELECT 
    title,
    rating * 10 AS percent
FROM Movies
INNER JOIN Boxoffice 
        ON Movies.id = Boxoffice.movie_id
```

3.List all movies that were released on even number years

```SQL
SELECT title, year
FROM movies
WHERE year % 2 == 0
```

# LESSON 10: Queries with aggregates(1)

```SQL
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, …
FROM mytable
WHERE constraint_expression
GROUP BY column;
```

## Lab 10

1.Find the longest time that an employee has been at the studio 

```SQL
SELECT MAX(Years_employed) FROM employees
```

2.For each role, find the average number of years employed by employees in that role

```SQL
SELECT 
    role, 
    AVG(Years_employed) AS Average_year
FROM Employees
GROUP BY role
```

3.Find the total number of employee years worked in each building

```SQL
SELECT
    building,
    SUM(years_employed) AS total_year
FROM Employees
GROUP BY building
```


# LESSON 10: Queries with aggregates(2)

One thing that we might have noticed is that if the GROUP BY clause is executed after the WHERE clause (which filters the rows which are to be grouped), then how exactly do we filter the grouped rows?

Luckily, SQL allows us to do this by adding an additional HAVING clause which is used specifically with the GROUP BY clause to allow us to filter grouped rows from the result set.

```SQL
SELECT group_by_column, AGG_FUNC(column_expression) AS aggregate_result_alias, …
FROM mytable
WHERE condition
GROUP BY column
HAVING group_condition;
```

## Lab 11
1. Find the number of Artists in the studio (without a HAVING clause)

```SQL
SELECT COUNT(Name) FROM Employees
WHERE Role == "Artist"
```
2. Find the number of Employees of each role in the studio

```SQL
SELECT 
    role,
    COUNT(name)
FROM Employees
GROUP BY role
```
3. Find the total number of years employed by all Engineers

```SQL
SELECT 
    role, 
    name,
    SUM(years_employed)
FROM Employees
WHERE role == "Engineer"
```
# Lesson 12 Order of execution of a Query

```SQL
SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHERE constraint_expression
    GROUP BY column
    HAVING constraint_expression
    ORDER BY column ASC/DESC
    LIMIT count OFFSET COUNT;
```

## Order of query excution:
    1. `FROM and JOINs`
    2. `WHERE`
    3. `GROUP BY`
    4. `HAVING`
    5. `SELECT`
    6. `DISTINCT`
    7. `ORDER BY`
    8. `LIMIT / OFFSET`

## Lab 12

1. Find the number of movies each director has directed.

```SQL
SELECT 
    Director,
    COUNT(Director) AS number
FROM movies
GROUP BY Director
```

```SQL
SELECT
	director,
	COUNT(*)
FROM movies
GROUP BY director;
```

2.Find the total domestic and international sales that can be attributed to each director

```SQL
SELECT
    director,
    SUM(domestic_sales + international_sales) AS total_sales
FROM movies
LEFT JOIN boxoffice 
ON movies.id = boxoffice.movie_id
GROUP BY director
```

# Lesson 13 Inserting rows
    Insert statement with values for all columns
```SQL
INSERT INTO mytable
VALUES (value_or_expr, another_value_or_expr, …),
       (value_or_expr_2, another_value_or_expr_2, …),
       …;
```

    Insert statement with specific columns
```SQL
INSERT INTO mytable
(column, another_column, …)
VALUES (value_or_expr, another_value_or_expr, …),
      (value_or_expr_2, another_value_or_expr_2, …),
      …;
```

    Example Insert statement with expressions
```SQL
INSERT INTO boxoffice
(movie_id, rating, sales_in_millions)
VALUES (1, 9.9, 283742034 / 1000000);
```


## lab 13
1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
```SQL
INSERT INTO movies
    (Title, Director, Year, Length_minutes)
VALUES
    ('Toy Story 4', 'Brad Bird', 2020, 103)
```

2. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table.


```SQL
INSERT INTO boxoffice
    (movie_id, rating, domestic_sales, international_sales)
VALUES
    (15, 8.7, 340000000, 270000000);
```


# Lesson 14 Updating rows

    One helpful tip is to always write the constraint first and test it in a SELECT query to make sure you are updating the right rows, and only then writing the column/value pairs to update.

```SQL
UPDATE mytable
SET column = value_or_expr, 
    other_column = another_value_or_expr, 
    …
WHERE condition;
```

## Lab 14

1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter 

```SQL
Update movies
SET Director = "John Lasseter"
WHERE Title = "A Bug's Life"
```

2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999 

```SQL
UPDATE movies
SET year = 1999
WHERE title = "Toy Story 2"
```
3. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich Stuck.

```SQL
UPDATE movies
SET title = "Toy Story 3",
    director = "Lee Unkrich"
WHERE title = "Toy Story 8"
```

# Lesson 15 Deleting rows
    
    Delete statement with condition
```SQL
DELETE FROM mytable
WHERE condition;
```

1.This database is getting too big, lets remove all movies that were released before 2005.

```SQL
DELETE FROM movies
WHERE year < 2005
```
2. Andrew Stanton has also left the studio, so please remove all movies directed by him.

```SQL
DELETE FROM movies
WHERE director = "Andrew Stanton"
```


