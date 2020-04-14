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
    1. FROM and JOINs
    2. WHERE
    3. GROUP BY
    4. HAVING
    5. SELECT
    6. DISTINCT
    7. ORDER BY
    8. LIMIT / OFFSET

## Lab 12

```SQL

```


```SQL

```




