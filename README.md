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

## Lab Answers:
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

## Lab Answers:
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

## Lab Answers:

1.
```SQL

```

2.
```SQL

```
