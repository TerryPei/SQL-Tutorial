# SQL-Tutorial
SQL practice







# LESSON 7: OUTER JOINs

```
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

```
SELECT * FROM Buildings
```

3.List all buildings and the distinct employee roles in each building (including empty buildings)

```
SELECT DISTINCT building_name, role
FROM Buildings 
LEFT JOIN Employees
        ON  Buildings.building_name = Employees.building

```









