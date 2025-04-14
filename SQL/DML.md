# SQL之DML

---

## 第一阶段

------

### 前置准备：创建示例表

为了方便讲解，我们先创建两张表：`students` 和 `classes`。
```sql
CREATE TABLE classes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    class_name VARCHAR(50)
);

CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    class_id INT,
    score INT,
    FOREIGN KEY (class_id) REFERENCES classes(id)
);
```

插入初始数据：
```sql
INSERT INTO classes (class_name) VALUES ('一班'), ('二班');

INSERT INTO students (name, class_id, score) VALUES 
('张三', 1, 85),
('李四', 2, 90),
('王五', 1, 78);
```

当前数据：
- `classes`：
```
id | class_name
1  | 一班
2  | 二班
```
- `students`：
```
id | name  | class_id | score
1  | 张三  | 1        | 85
2  | 李四  | 2        | 90
3  | 王五  | 1        | 78
```

---

### 1. 插入数据（INSERT INTO）
向表中添加新记录。

#### 基本语法
```sql
INSERT INTO 表名 (列名1, 列名2, ...) VALUES (值1, 值2, ...);
```

#### 举例
插入一个新学生：
```sql
INSERT INTO students (name, class_id, score) VALUES ('赵六', 2, 95);
```
结果：
```
id | name  | class_id | score
1  | 张三  | 1        | 85
2  | 李四  | 2        | 90
3  | 王五  | 1        | 78
4  | 赵六  | 2        | 95
```

#### 批量插入
```sql
INSERT INTO students (name, class_id, score) VALUES 
('钱七', 1, 88),
('孙八', 2, 82);
```

---

### 2. 查询数据（SELECT）
从表中检索数据，是 DML 的核心。

#### 基本语法
```sql
SELECT 列名 FROM 表名 [WHERE 条件];
```

#### 举例
- 查询所有学生：
```sql
SELECT * FROM students;
```

- 查询特定列：
```sql
SELECT name, score FROM students;
```
结果：
```
name  | score
张三  | 85
李四  | 90
王五  | 78
赵六  | 95
钱七  | 88
孙八  | 82
```

- 带条件查询：
```sql
SELECT name, score FROM students WHERE score > 85;
```
结果：
```
name  | score
李四  | 90
赵六  | 95
钱七  | 88
```

---

### 3. 更新数据（UPDATE）
修改表中的现有数据。

#### 基本语法
```sql
UPDATE 表名 SET 列名1 = 新值1, 列名2 = 新值2 [WHERE 条件];
```

#### 举例
将张三的成绩改为 87：
```sql
UPDATE students SET score = 87 WHERE name = '张三';
```
结果：
```
id | name  | class_id | score
1  | 张三  | 1        | 87
2  | 李四  | 2        | 90
...
```

批量更新：
```sql
UPDATE students SET score = score + 5 WHERE class_id = 2;
```
结果：
```
id | name  | class_id | score
1  | 张三  | 1        | 87
2  | 李四  | 2        | 95
3  | 王五  | 1        | 78
4  | 赵六  | 2        | 100
...
```

---

### 4. 删除数据（DELETE）
删除表中的记录。

#### 基本语法
```sql
DELETE FROM 表名 [WHERE 条件];
```

#### 举例
删除成绩低于 80 的学生：
```sql
DELETE FROM students WHERE score < 80;
```
结果：
```
id | name  | class_id | score
1  | 张三  | 1        | 87
2  | 李四  | 2        | 95
4  | 赵六  | 2        | 100
5  | 钱七  | 1        | 88
...
```

删除所有数据（但保留表结构）：
```sql
DELETE FROM students;
```

---

### 小练习
基于当前 `students` 和 `classes` 表，请写出以下 DML 语句：
1. 向 `students` 表插入一个新学生：姓名“周九”，班级 ID 为 1，成绩 92。
2. 查询所有二班（class_id = 2）的学生姓名和成绩。
3. 将一班（class_id = 1）学生的成绩全部增加 3 分。
4. 删除成绩低于 90 的学生。

------

## 第二阶段

---

### 当前数据回顾
- `classes`：
```
id | class_name
1  | 一班
2  | 二班
```
- `students`（假设练习后的最新状态）：
```
id | name  | class_id | score
1  | 张三  | 1        | 87
2  | 李四  | 2        | 95
3  | 王五  | 1        | 78
4  | 赵六  | 2        | 100
5  | 钱七  | 1        | 88
6  | 孙八  | 2        | 82
```

---

### 1. 高级条件查询
除了基本的 `WHERE`，我们可以用更灵活的条件来筛选数据。

#### (1) LIKE - 模糊查询
使用通配符 `%`（任意字符）和 `_`（单个字符）进行模式匹配。

**语法：**
```sql
SELECT 列名 FROM 表名 WHERE 列名 LIKE 模式;
```

**举例：**
查询姓名以“张”开头的学生：
```sql
SELECT name, score FROM students WHERE name LIKE '张%';
```
结果：
```
name  | score
张三  | 87
```

#### (2) BETWEEN - 范围查询
筛选某个范围内的值。

**语法：**
```sql
SELECT 列名 FROM 表名 WHERE 列名 BETWEEN 值1 AND 值2;
```

**举例：**
查询成绩在 85 到 95 之间的学生：
```sql
SELECT name, score FROM students WHERE score BETWEEN 85 AND 95;
```
结果：
```
name  | score
张三  | 87
李四  | 95
钱七  | 88
```

#### (3) IN - 枚举查询
筛选列值在特定集合中的记录。

**语法：**
```sql
SELECT 列名 FROM 表名 WHERE 列名 IN (值1, 值2, ...);
```

**举例：**
查询班级 ID 为 1 或 2 的学生：
```sql
SELECT name, class_id FROM students WHERE class_id IN (1, 2);
```
结果：（所有学生都在这两个班级，结果略）

---

### 2. 排序（ORDER BY）
对查询结果按某列排序，默认升序（ASC），可以用 `DESC` 降序。

**语法：**
```sql
SELECT 列名 FROM 表名 [WHERE 条件] ORDER BY 列名 [ASC|DESC];
```

**举例：**
按成绩降序排列学生：
```sql
SELECT name, score FROM students ORDER BY score DESC;
```
结果：
```
name  | score
赵六  | 100
李四  | 95
钱七  | 88
张三  | 87
孙八  | 82
王五  | 78
```

多列排序：
```sql
SELECT name, class_id, score FROM students ORDER BY class_id ASC, score DESC;
```
结果：
```
name  | class_id | score
钱七  | 1        | 88
张三  | 1        | 87
王五  | 1        | 78
赵六  | 2        | 100
李四  | 2        | 95
孙八  | 2        | 82
```

---

### 3. 聚合函数
用于统计数据，常见的有 `COUNT`（计数）、`SUM`（求和）、`AVG`（平均值）、`MAX`（最大值）、`MIN`（最小值）。

**语法：**
```sql
SELECT 聚合函数(列名) FROM 表名 [WHERE 条件];
```

**举例：**
- 统计学生人数：
```sql
SELECT COUNT(*) AS total_students FROM students;
```
结果：
```
total_students
6
```

- 计算平均成绩：
```sql
SELECT AVG(score) AS avg_score FROM students;
```
结果：
```
avg_score
88.3333
```

- 查找最高成绩：
```sql
SELECT MAX(score) AS max_score FROM students;
```
结果：
```
max_score
100
```

---

### 4. 表连接（JOIN）
将多个表关联起来查询数据，常用类型有 `INNER JOIN`、`LEFT JOIN` 和 `RIGHT JOIN`。

#### (1) INNER JOIN - 内连接
只返回匹配的记录。

**语法：**
```sql
SELECT 列名 FROM 表1 INNER JOIN 表2 ON 表1.列名 = 表2.列名;
```

**举例：**
查询学生姓名和班级名称：
```sql
SELECT students.name, classes.class_name
FROM students
INNER JOIN classes ON students.class_id = classes.id;
```
结果：
```
name  | class_name
张三  | 一班
李四  | 二班
王五  | 一班
赵六  | 二班
钱七  | 一班
孙八  | 二班
```

#### (2) LEFT JOIN - 左连接
返回左表所有记录，右表无匹配则为 NULL。

**举例：**
假设有学生未分配班级：
```sql
INSERT INTO students (name, score) VALUES ('周九', 92); -- class_id 为 NULL
```
查询：
```sql
SELECT students.name, classes.class_name
FROM students
LEFT JOIN classes ON students.class_id = classes.id;
```
结果：
```
name  | class_name
张三  | 一班
李四  | 二班
王五  | 一班
赵六  | 二班
钱七  | 一班
孙八  | 二班
周九  | NULL
```

---

### 小练习
基于当前 `students` 和 `classes` 表，请写出以下 DML 语句：
1. 查询姓名包含“五”的学生姓名和成绩。
2. 查询成绩在 80 到 90 之间的学生，按成绩升序排列。
3. 计算二班（class_id = 2）的平均成绩。
4. 用 `INNER JOIN` 查询一班（class_id = 1）的所有学生姓名和班级名称。

---

## 第三阶段

---

### 当前数据回顾
- `classes`：
```
id | class_name
1  | 一班
2  | 二班
```
- `students`：
```
id | name  | class_id | score
1  | 张三  | 1        | 87
2  | 李四  | 2        | 95
3  | 王五  | 1        | 78
4  | 赵六  | 2        | 100
5  | 钱七  | 1        | 88
6  | 孙八  | 2        | 82
7  | 周九  | NULL     | 92
```

---

### 1. 分组查询（GROUP BY）与 HAVING
`GROUP BY` 用于按某列分组统计，结合聚合函数使用。`HAVING` 是对分组后的结果进行筛选。

#### 基本语法
```sql
SELECT 列名, 聚合函数(列名)
FROM 表名
[WHERE 条件]
GROUP BY 列名
[HAVING 聚合条件];
```

#### 举例
- 按班级统计平均成绩：
```sql
SELECT class_id, AVG(score) AS avg_score
FROM students
GROUP BY class_id;
```
结果：
```
class_id | avg_score
1        | 84.3333
2        | 92.3333
NULL     | 92.0000
```

- 筛选平均成绩大于 90 的班级：
```sql
SELECT class_id, AVG(score) AS avg_score
FROM students
GROUP BY class_id
HAVING AVG(score) > 90;
```
结果：
```
class_id | avg_score
2        | 92.3333
```

---

### 2. 子查询
子查询是嵌套在另一个查询中的查询，常用于分步解决问题。

#### 基本语法
```sql
SELECT 列名
FROM 表名
WHERE 列名 运算符 (SELECT 列名 FROM 表名 WHERE 条件);
```

#### 举例
- 查询成绩高于平均成绩的学生：
```sql
SELECT name, score
FROM students
WHERE score > (SELECT AVG(score) FROM students);
```
假设平均成绩为 `(87 + 95 + 78 + 100 + 88 + 82 + 92) / 7 ≈ 88.86`，结果：
```
name  | score
李四  | 95
赵六  | 100
周九  | 92
```

- 查询一班中成绩最高的学生的班级名称：
```sql
SELECT class_name
FROM classes
WHERE id = (
    SELECT class_id
    FROM students
    WHERE class_id = 1
    ORDER BY score DESC
    LIMIT 1
);
```
结果：
```
class_name
一班
```

---

### 3. 联合查询（UNION）
`UNION` 合并多个查询结果，自动去重（用 `UNION ALL` 保留重复行）。

#### 基本语法
```sql
SELECT 列名 FROM 表1
UNION
SELECT 列名 FROM 表2;
```

#### 举例
假设有另一张表 `teachers`：
```sql
CREATE TABLE teachers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50)
);
INSERT INTO teachers (name) VALUES ('张老师'), ('李老师');
```

合并学生和老师的名字：
```sql
SELECT name FROM students
UNION
SELECT name FROM teachers;
```
结果：
```
name
张三
李四
王五
赵六
钱七
孙八
周九
张老师
李老师
```

---

### 4. 窗口函数
窗口函数在每行上计算结果，但保留所有行，常用于排名、累计等。需要 MySQL 8.0+ 支持。

#### 常用函数
- `ROW_NUMBER()`：分配唯一行号
- `RANK()`：排名（重复值同排名，后续跳号）
- `DENSE_RANK()`：排名（重复值同排名，后续不跳号）
- `SUM() OVER`：累计求和

#### 基本语法
```sql
SELECT 列名, 窗口函数() OVER (PARTITION BY 列名 ORDER BY 列名)
FROM 表名;
```

#### 举例
- 按班级给学生成绩排名：
```sql
SELECT name, class_id, score,
       ROW_NUMBER() OVER (PARTITION BY class_id ORDER BY score DESC) AS rank
FROM students;
```
结果：
```
name  | class_id | score | rank
钱七  | 1        | 88    | 1
张三  | 1        | 87    | 2
王五  | 1        | 78    | 3
赵六  | 2        | 100   | 1
李四  | 2        | 95    | 2
孙八  | 2        | 82    | 3
周九  | NULL     | 92    | 1
```

- 计算每个班级的累计成绩：
```sql
SELECT name, class_id, score,
       SUM(score) OVER (PARTITION BY class_id ORDER BY score DESC) AS cumulative_score
FROM students;
```
结果：
```
name  | class_id | score | cumulative_score
钱七  | 1        | 88    | 88
张三  | 1        | 87    | 175
王五  | 1        | 78    | 253
赵六  | 2        | 100   | 100
李四  | 2        | 95    | 195
孙八  | 2        | 82    | 277
周九  | NULL     | 92    | 92
```

---

### 小练习
基于当前 `students` 和 `classes` 表，请写出以下 DML 语句：
1. 按班级统计学生人数，筛选人数大于 2 的班级。
2. 用子查询找出成绩低于一班平均成绩的学生姓名和成绩。
3. 用 `UNION` 合并 `students` 和 `teachers` 表中的姓名。
4. 用窗口函数计算每个学生的成绩在全表中的 `DENSE_RANK` 排名。

---

## 第四阶段

---

### 当前数据回顾
- `classes`：
```
id | class_name
1  | 一班
2  | 二班
```
- `students`：
```
id | name  | class_id | score
1  | 张三  | 1        | 87
2  | 李四  | 2        | 95
3  | 王五  | 1        | 78
4  | 赵六  | 2        | 100
5  | 钱七  | 1        | 88
6  | 孙八  | 2        | 82
7  | 周九  | NULL     | 92
```

---

### 1. 事务管理（Transaction Management）
事务是一组操作，要么全部成功，要么全部失败，确保数据一致性。MySQL 中通过 `BEGIN`、`COMMIT` 和 `ROLLBACK` 控制事务。

#### 基本语法
```sql
BEGIN;  -- 开始事务
-- SQL 操作
COMMIT; -- 提交事务
-- 或
ROLLBACK; -- 回滚事务
```

#### 事务特性（ACID）
- **A（Atomicity，原子性）**：事务是一个不可分割的整体。
- **C（Consistency，一致性）**：事务完成后，数据保持一致。
- **I（Isolation，隔离性）**：事务之间互不干扰。
- **D（Durability，持久性）**：提交后的数据永久保存。

#### 举例 1：简单事务
将张三的成绩增加 5 分，同时记录日志：
```sql
CREATE TABLE score_logs (
    log_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    old_score INT,
    new_score INT,
    log_time TIMESTAMP
);

BEGIN;
UPDATE students SET score = score + 5 WHERE name = '张三';
INSERT INTO score_logs (student_id, old_score, new_score, log_time)
VALUES (1, 87, 92, NOW());
COMMIT;
```

查询结果：
- `students`：
```
id | name  | class_id | score
1  | 张三  | 1        | 92
...
```
- `score_logs`：
```
log_id | student_id | old_score | new_score | log_time
1      | 1          | 87        | 92        | 2025-03-19 08:00:00
```

#### 举例 2：回滚事务
如果操作失败，回滚到初始状态：
```sql
BEGIN;
UPDATE students SET score = 100 WHERE name = '李四';
-- 假设这里发生错误（比如外键约束）
ROLLBACK;
```
`students` 表保持不变。

#### 隔离级别
MySQL 支持多种隔离级别（如 `READ UNCOMMITTED`、`REPEATABLE READ`），可以用以下命令查看或设置：
```sql
SELECT @@transaction_isolation; -- 查看当前隔离级别
SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED; -- 设置隔离级别
```

---

### 2. 复杂查询优化
当查询变复杂或数据量增加时，性能可能下降。优化可以通过索引、查询重写和分析执行计划实现。

#### (1) 使用索引
索引能加速 `WHERE`、`JOIN` 和 `ORDER BY` 的查询。

**举例：**
为 `students` 表的 `class_id` 创建索引：
```sql
CREATE INDEX idx_class_id ON students (class_id);
```
优化查询：
```sql
SELECT name, score
FROM students
WHERE class_id = 1;
```

#### (2) EXPLAIN 分析执行计划
`EXPLAIN` 显示 MySQL 如何执行查询，帮助识别瓶颈。

**语法：**
```sql
EXPLAIN SELECT 列名 FROM 表名 WHERE 条件;
```

**举例：**
```sql
EXPLAIN SELECT name, score
FROM students
WHERE class_id = 1
ORDER BY score DESC;
```
结果（简化）：
```
id | select_type | table    | type  | key         | rows | Extra
1  | SIMPLE      | students | ref   | idx_class_id | 3    | Using index condition; Using filesort
```
- `type`：访问类型（`ref` 表示使用索引）
- `key`：使用的索引
- `rows`：扫描的行数

#### (3) 查询重写
优化复杂查询，避免嵌套过多或重复计算。

**举例：**
原始查询（效率低）：
```sql
SELECT name
FROM students
WHERE score > (SELECT AVG(score) FROM students);
```

优化为带临时表的查询：
```sql
WITH avg_score AS (SELECT AVG(score) AS avg FROM students)
SELECT name
FROM students, avg_score
WHERE score > avg_score.avg;
```

#### (4) 避免全表扫描
确保 `WHERE` 和 `JOIN` 条件使用索引列。

**举例：**
低效查询（无索引）：
```sql
SELECT name FROM students WHERE name LIKE '%三';
```
优化：如果需要前缀匹配，改为：
```sql
SELECT name FROM students WHERE name LIKE '张%';
```

---

### 小练习
请根据以下要求写出 SQL 语句：
1. 开始一个事务，将二班（class_id = 2）所有学生的成绩减少 5 分，并记录到 `score_logs` 表，提交事务。
2. 用 `EXPLAIN` 分析以下查询的执行计划：
   ```sql
   SELECT name, class_name
   FROM students
   INNER JOIN classes ON students.class_id = classes.id
   WHERE score > 90;
   ```
3. 优化以下查询（假设 `score` 无索引）：
   ```sql
   SELECT name FROM students WHERE score BETWEEN 80 AND 90;
   ```

完成后可以给我答案，我帮你检查！

---

### 下一步建议
如果这些没问题，我们可以：
- 结合 DDL 和 DML 做综合案例（比如设计一个小型系统）
- 学习 MySQL 的性能调优（如配置参数）
- 探讨其他数据库特性（如 JSON 支持）
