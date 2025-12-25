### Handling `NULL` Values with `COALESCE` (PostgreSQL)

**Purpose**
`COALESCE` is used to replace `NULL` values with a default value. It returns the first non-`NULL` value from the given arguments.

---

### Query Example

```sql
SELECT 
  first_name,
  age,
  COALESCE(email, 'Not provided') AS email
FROM students;
```

---

### Sample Data

| first_name | age | email                                 |
| ---------- | --- | ------------------------------------- |
| Asif       | 22  | [asif@mail.com](mailto:asif@mail.com) |
| Rahim      | 21  | NULL                                  |

---

### Output

| first_name | age | email                                 |
| ---------- | --- | ------------------------------------- |
| Asif       | 22  | [asif@mail.com](mailto:asif@mail.com) |
| Rahim      | 21  | Not provided                          |

---

### Reason to Use `COALESCE`

* Prevents `NULL` values in query results
* Improves readability of output data
* Useful for reporting and user-facing responses
* Avoids handling `NULL` in application logic

This approach is commonly used when optional fields (like `email`) may not always contain data.


### Using `LIMIT` and `OFFSET` in PostgreSQL

**Purpose**
`LIMIT` controls how many rows are returned, and `OFFSET` skips a specific number of rows. They are commonly used for pagination.

---

### Query Examples

```sql
-- Page 1
SELECT * 
FROM students 
LIMIT 5 OFFSET 5 * 0;
```

```sql
-- Page 2
SELECT * 
FROM students 
LIMIT 5 OFFSET 5 * 1;
```

---

### How It Works

* `LIMIT 5` → returns 5 rows per page
* `OFFSET 5 * 0` → skips 0 rows (first page)
* `OFFSET 5 * 1` → skips 5 rows (second page)

---

### Sample Output (Conceptual)

**Page 1 (OFFSET 0)**

| student_id | first_name | age |
| ---------- | ---------- | --- |
| 1          | Asif       | 22  |
| 2          | Rahim      | 21  |
| 3          | Karim      | 23  |
| 4          | Nadia      | 20  |
| 5          | Tania      | 22  |

**Page 2 (OFFSET 5)**

| student_id | first_name | age |
| ---------- | ---------- | --- |
| 6          | Rafi       | 24  |
| 7          | Mim        | 21  |
| 8          | Hasan      | 22  |
| 9          | Rima       | 23  |
| 10         | Sakib      | 20  |

---

### Reason to Use `LIMIT` & `OFFSET`



### Using `UPDATE` in PostgreSQL

**Purpose**
The `UPDATE` statement is used to modify existing records in a table based on a condition.

---

### View Data (Before Update)

```sql
SELECT *
FROM students;
```

---

### Update Query

```sql
UPDATE students
SET grade = 'B'
WHERE student_id IN (1, 2);
```

---

### Sample Data (Before)

| student_id | first_name | grade |
| ---------- | ---------- | ----- |
| 1          | Asif       | A     |
| 2          | Rahim      | C     |
| 3          | Karim      | B     |

---

### Output (After Update)

| student_id | first_name | grade |
| ---------- | ---------- | ----- |
| 1          | Asif       | B     |
| 2          | Rahim      | B     |
| 3          | Karim      | B     |

---

### Reason to Use `UPDATE`

* Modify specific rows without affecting the entire table
* Apply changes based on conditions (`WHERE` clause)
* Commonly used for correcting or updating user data

> **Important:** Always use a `WHERE` clause with `UPDATE` to avoid updating all rows unintentionally.


* Implements pagination in APIs and dashboards
* Reduces data load by fetching small chunks
* Improves performance and user experience

This pattern is standard for page-based data retrieval in SQL-backed applications.
