## Input Relations

```sql
-- Course catalog
CREATE TABLE course (
  course_id VARCHAR(8),
  title     VARCHAR(50),
  dept_name VARCHAR(20),
  credits   INT
);

-- Prerequisite mapping
CREATE TABLE prereq (
  course_id VARCHAR(8),
  prereq_id VARCHAR(8)
);
```

| course_id | title       | dept_name  | credits |
|-----------|-------------|------------|---------|
| BIO-301   | Genetics    | Biology    | 4       |
| CS-190    | Game Design | Comp. Sci. | 4       |
| CS-315    | Robotics    | Comp. Sci. | 3       |

| course_id | prereq_id |
|-----------|-----------|
| BIO-301   | BIO-101   |
| CS-190    | CS-101    |
| CS-347    | CS-101    |

---

### 1. INNER JOIN  
**Definition:** Keep only rows with matching `course_id` in both tables.  

```sql
SELECT c.course_id, title, prereq_id
  FROM course AS c
  INNER JOIN prereq AS p
    ON c.course_id = p.course_id;
```

| course_id | title       | prereq_id |
|-----------|-------------|-----------|
| BIO-301   | Genetics    | BIO-101   |
| CS-190    | Game Design | CS-101    |

---

### 2. LEFT OUTER JOIN  
**Definition:** Keep _all_ `course` rows; match `prereq` when possible, else NULL.  

```sql
SELECT c.course_id, title, prereq_id
  FROM course AS c
  LEFT JOIN prereq AS p
    ON c.course_id = p.course_id;
```

| course_id | title       | prereq_id |
|-----------|-------------|-----------|
| BIO-301   | Genetics    | BIO-101   |
| CS-190    | Game Design | CS-101    |
| CS-315    | Robotics    | NULL      |

---

### 3. RIGHT OUTER JOIN  
**Definition:** Keep _all_ `prereq` rows; match `course` when possible, else NULL.  

```sql
SELECT p.course_id, title, prereq_id
  FROM course AS c
  RIGHT JOIN prereq AS p
    ON c.course_id = p.course_id;
```

| course_id | title       | prereq_id |
|-----------|-------------|-----------|
| BIO-301   | Genetics    | BIO-101   |
| CS-190    | Game Design | CS-101    |
| CS-347     | NULL        | CS-101    |

---

### 4. FULL OUTER JOIN  
**Definition:** Keep every row from _both_ `course` and `prereq`; NULL where no match.  

```sql
SELECT COALESCE(c.course_id, p.course_id) AS course_id,
       title,
       prereq_id
  FROM course AS c
  FULL OUTER JOIN prereq AS p
    ON c.course_id = p.course_id;
```

| course_id | title       | prereq_id |
|-----------|-------------|-----------|
| BIO-301   | Genetics    | BIO-101   |
| CS-190    | Game Design | CS-101    |
| CS-315    | Robotics    | NULL      |
| CS-347    | NULL        | CS-101    |

---

**Key Takeaways:**  
- **INNER JOIN** → intersection of both sets.  
- **LEFT JOIN** → all left‑side rows, plus matches.  
- **RIGHT JOIN** → all right‑side rows, plus matches.  
- **FULL JOIN** → union of both, padding unmatched sides with `NULL`.  
