# SQL Practice Problems - Beginner Level

## Setup: Sample Data

First, let's create and populate our sample tables:

```sql
-- Create students table
CREATE TABLE students (
    student_id INT,
    name VARCHAR(50),
    age INT,
    grade CHAR(1),
    city VARCHAR(30),
    marks INT
);

-- Insert sample data
INSERT INTO students VALUES (1, 'Alice Johnson', 20, 'A', 'New York', 85);
INSERT INTO students VALUES (2, 'Bob Smith', 19, 'B', 'Chicago', 78);
INSERT INTO students VALUES (3, 'Carol Davis', 21, 'A', 'New York', 92);
INSERT INTO students VALUES (4, 'David Wilson', 20, 'C', 'Boston', 65);
INSERT INTO students VALUES (5, 'Eva Brown', 19, 'B', 'Chicago', 88);
INSERT INTO students VALUES (6, 'Frank Miller', 22, 'A', 'Boston', 95);
INSERT INTO students VALUES (7, 'Grace Lee', 20, 'B', 'New York', 82);
INSERT INTO students VALUES (8, 'Henry Taylor', 21, 'C', 'Chicago', 70);
```

---

## Problem 1: WHERE Clause with Comparison Operators
**Concept**: Filter data using WHERE clause with different comparison operators.

**Question**: Find all students who are 20 years old or younger and have marks greater than 80.

**Expected Output**:
```
name          | age | marks
Alice Johnson | 20  | 85
Eva Brown     | 19  | 88
Grace Lee     | 20  | 82
```

**Solution**:
```sql
SELECT name, age, marks 
FROM students 
WHERE age <= 20 AND marks > 80;
```

---

## Problem 2: ORDER BY with Multiple Columns
**Concept**: Sort results using ORDER BY clause with multiple criteria.

**Question**: Display all students' information, ordered by grade (ascending), then by marks (descending).

**Expected Output**:
```
name          | age | grade | city      | marks
Frank Miller  | 22  | A     | Boston    | 95
Carol Davis   | 21  | A     | New York  | 92
Alice Johnson | 20  | A     | New York  | 85
Eva Brown     | 19  | B     | Chicago   | 88
Grace Lee     | 20  | B     | New York  | 82
Bob Smith     | 19  | B     | Chicago   | 78
Henry Taylor  | 21  | C     | Chicago   | 70
David Wilson  | 20  | C     | Boston    | 65
```

**Solution**:
```sql
SELECT name, age, grade, city, marks 
FROM students 
ORDER BY grade ASC, marks DESC;
```

---

## Problem 3: Aggregate Functions (MAX, MIN, AVG)
**Concept**: Use aggregate functions to calculate summary statistics.

**Question**: Find the highest marks, lowest marks, and average marks of all students.

**Expected Output**:
```
highest_marks | lowest_marks | average_marks
95           | 65           | 81.875
```

**Solution**:
```sql
SELECT MAX(marks) AS highest_marks, 
       MIN(marks) AS lowest_marks, 
       AVG(marks) AS average_marks 
FROM students;
```

---

## Problem 4: WHERE Clause with Aggregate Functions
**Concept**: Combine WHERE clause with aggregate functions to filter before calculation.

**Question**: Find the maximum and minimum marks for students from 'New York' only.

**Expected Output**:
```
max_marks_ny | min_marks_ny
92          | 82
```

**Solution**:
```sql
SELECT MAX(marks) AS max_marks_ny, 
       MIN(marks) AS min_marks_ny 
FROM students 
WHERE city = 'New York';
```

---

## Problem 5: GROUP BY with HAVING Clause
**Concept**: Group data and filter groups using HAVING clause.

**Question**: Find cities that have more than 2 students, and show the average marks for each of these cities, ordered by average marks in descending order.

**Expected Output**:
```
city     | student_count | avg_marks
New York | 3            | 86.33
Chicago  | 3            | 78.67
```

**Solution**:
```sql
SELECT city, 
       COUNT(*) AS student_count, 
       AVG(marks) AS avg_marks 
FROM students 
GROUP BY city 
HAVING COUNT(*) > 2 
ORDER BY avg_marks DESC;
```

---

## Additional Practice Data (Optional)

If you want more practice, insert these additional records:

```sql
INSERT INTO students VALUES (9, 'Ivy Chen', 19, 'A', 'Seattle', 90);
INSERT INTO students VALUES (10, 'Jack White', 22, 'B', 'Seattle', 75);
INSERT INTO students VALUES (11, 'Kelly Green', 20, 'C', 'Miami', 68);
INSERT INTO students VALUES (12, 'Liam Black', 21, 'A', 'Miami', 93);
```

---

## Key Learning Points

1. **WHERE Clause**: Filters rows before processing
2. **ORDER BY**: Sorts the final result set
3. **Aggregate Functions**: 
   - MAX() - finds maximum value
   - MIN() - finds minimum value  
   - AVG() - calculates average
4. **GROUP BY**: Groups rows with same values
5. **HAVING**: Filters groups (used with GROUP BY)

## Common Mistakes to Avoid

- Don't use HAVING without GROUP BY
- Remember WHERE filters rows, HAVING filters groups
- Use single quotes for string values
- Column aliases make output more readable
- ORDER BY comes last in SELECT statements