# SQL之DLL语句

---

## 第一阶段

------

### 1. 创建数据库（CREATE DATABASE）

在开始操作表之前，我们需要一个数据库。

**语法：**
```sql
CREATE DATABASE 数据库名;
```

**举例：**
创建一个名为 `school` 的数据库：
```sql
CREATE DATABASE school;
```

**使用数据库：**
```sql
USE school;
```

---

### 2. 创建表（CREATE TABLE）
这是 DDL 的基础，用于定义表结构。我们之前简单提过，现在详细展开。

**语法：**
```sql
CREATE TABLE 表名 (
    列名1 数据类型 [约束],
    列名2 数据类型 [约束],
    ...
);
```

#### 常见数据类型：
- `INT`：整数
- `VARCHAR(n)`：变长字符串，n 是最大长度
- `DECIMAL(m,n)`：精确小数，m 是总位数，n 是小数位
- `DATE`：日期（格式：YYYY-MM-DD）

#### 常见约束：
- `PRIMARY KEY`：主键，唯一标识每行
- `NOT NULL`：不能为空
- `AUTO_INCREMENT`：自增（常用于 ID）
- `FOREIGN KEY`：外键，关联其他表

**举例：**
创建一个 `students` 表：
```sql
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    birth_date DATE,
    score DECIMAL(5,2)
);
```

---

### 3. 查看表结构（DESCRIBE）
创建表后，可以查看它的结构。

**语法：**
```sql
DESCRIBE 表名;
```

**举例：**
```sql
DESCRIBE students;
```
结果：
```
Field      | Type         | Null | Key | Default | Extra
id         | int          | NO   | PRI | NULL    | auto_increment
name       | varchar(50)  | NO   |     | NULL    |
birth_date | date         | YES  |     | NULL    |
score      | decimal(5,2) | YES  |     | NULL    |
```

---

### 4. 修改表结构（ALTER TABLE）
`ALTER TABLE` 用于修改已有表的结构，比如添加列、删除列或修改列属性。

#### (1) 添加列（ADD）
**语法：**
```sql
ALTER TABLE 表名 ADD 列名 数据类型 [约束];
```

**举例：**
给 `students` 表添加 `class_id` 列：
```sql
ALTER TABLE students ADD class_id INT;
```

#### (2) 修改列（MODIFY）
**语法：**
```sql
ALTER TABLE 表名 MODIFY 列名 新数据类型 [新约束];
```

**举例：**
将 `name` 列的最大长度改为 100：
```sql
ALTER TABLE students MODIFY name VARCHAR(100) NOT NULL;
```

#### (3) 删除列（DROP）
**语法：**
```sql
ALTER TABLE 表名 DROP 列名;
```

**举例：**
删除 `birth_date` 列：
```sql
ALTER TABLE students DROP birth_date;
```

#### (4) 添加主键或外键
**语法：**
```sql
ALTER TABLE 表名 ADD PRIMARY KEY (列名);
ALTER TABLE 表名 ADD FOREIGN KEY (列名) REFERENCES 其他表(列名);
```

**举例：**
假设有 `classes` 表：
```sql
CREATE TABLE classes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    class_name VARCHAR(50)
);
```
给 `students` 的 `class_id` 添加外键约束：
```sql
ALTER TABLE students ADD FOREIGN KEY (class_id) REFERENCES classes(id);
```

---

### 5. 删除表（DROP TABLE）
删除整个表及其数据。

**语法：**
```sql
DROP TABLE 表名;
```

**举例：**
删除 `students` 表：
```sql
DROP TABLE students;
```

---

### 6. 删除数据库（DROP DATABASE）
删除整个数据库及其所有表。

**语法：**
```sql
DROP DATABASE 数据库名;
```

**举例：**
删除 `school` 数据库：
```sql
DROP DATABASE school;
```

---

### 小练习
请根据以下要求写出 DDL 语句：
1. 创建一个名为 `library` 的数据库。
2. 在 `library` 中创建 `books` 表，包含以下列：
   - `id`（整数，主键，自增）
   - `title`（字符串，最长100，不可为空）
   - `price`（小数，总位数6，小数位2）
3. 给 `books` 表添加一个 `publish_date`（日期类型）列。
4. 将 `price` 列改为总位数7，小数位2。
5. 删除 `publish_date` 列。

完成后可以给我答案，我帮你检查！



------

## 第二阶段

---

### 1. 创建索引（CREATE INDEX）
索引用于加速查询，尤其是对经常用于 `WHERE` 或 `JOIN` 的列。主键会自动创建索引，但其他列可以手动添加。

#### 普通索引
**语法：**
```sql
CREATE INDEX 索引名 ON 表名 (列名);
```

**举例：**
假设 `students` 表：
```sql
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    class_id INT
);
```
为 `name` 列创建索引：
```sql
CREATE INDEX idx_name ON students (name);
```

#### 唯一索引（UNIQUE INDEX）
确保列值唯一。

**语法：**
```sql
CREATE UNIQUE INDEX 索引名 ON 表名 (列名);
```

**举例：**
为 `class_id` 创建唯一索引：
```sql
CREATE UNIQUE INDEX idx_class_id ON students (class_id);
```

#### 删除索引
**语法：**
```sql
DROP INDEX 索引名 ON 表名;
```

**举例：**
删除 `idx_name` 索引：
```sql
DROP INDEX idx_name ON students;
```

---

### 2. 创建视图（CREATE VIEW）
视图是一个虚拟表，基于查询结果生成，可以简化复杂查询或限制数据访问。

**语法：**
```sql
CREATE VIEW 视图名 AS
SELECT 列名 FROM 表名 [WHERE 条件];
```

**举例：**
假设 `students` 表有数据：
```
id | name    | class_id | score
1  | 张三    | 1        | 85
2  | 李四    | 2        | 90
3  | 王五    | 1        | 78
```
创建一个视图，只显示成绩大于80的学生：
```sql
CREATE VIEW high_score_students AS
SELECT name, score
FROM students
WHERE score > 80;
```

查询视图：
```sql
SELECT * FROM high_score_students;
```
结果：
```
name  | score
张三  | 85
李四  | 90
```

#### 修改视图
**语法：**
```sql
CREATE OR REPLACE VIEW 视图名 AS
新查询语句;
```

**举例：**
修改视图，显示成绩大于85的学生：
```sql
CREATE OR REPLACE VIEW high_score_students AS
SELECT name, score
FROM students
WHERE score > 85;
```

#### 删除视图
**语法：**
```sql
DROP VIEW 视图名;
```

**举例：**
```sql
DROP VIEW high_score_students;
```

---

### 3. 表分区（PARTITION）
当表数据量很大时，可以通过分区将数据分片存储，提高查询效率。MySQL 支持多种分区方式，这里以范围分区（RANGE）为例。

**语法：**
```sql
CREATE TABLE 表名 (
    列定义
) PARTITION BY RANGE (列名) (
    PARTITION 分区名1 VALUES LESS THAN (值1),
    PARTITION 分区名2 VALUES LESS THAN (值2),
    ...
);
```

**举例：**
创建一个 `orders` 表，按订单年份分区：
```sql
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_date DATE,
    amount DECIMAL(10,2)
) PARTITION BY RANGE (YEAR(order_date)) (
    PARTITION p_2023 VALUES LESS THAN (2024),
    PARTITION p_2024 VALUES LESS THAN (2025),
    PARTITION p_future VALUES LESS THAN (MAXVALUE)
);
```

插入数据：
```sql
INSERT INTO orders (order_date, amount) VALUES ('2023-05-10', 100.00);
INSERT INTO orders (order_date, amount) VALUES ('2024-01-15', 200.00);
```

查询时，MySQL 会自动定位到对应分区，提高效率。

#### 查看分区
**语法：**
```sql
SELECT * FROM information_schema.partitions WHERE table_name = 'orders';
```

#### 删除分区
**语法：**
```sql
ALTER TABLE 表名 DROP PARTITION 分区名;
```

**举例：**
```sql
ALTER TABLE orders DROP PARTITION p_2023;
```

---

### 小练习
请根据以下要求写出 DDL 语句：
1. 创建一个 `employees` 表，包含：
   - `id`（整数，主键，自增）
   - `name`（字符串，最长50，不可为空）
   - `hire_date`（日期）
2. 为 `name` 列创建普通索引。
3. 创建一个视图 `recent_employees`，显示最近一年（假设当前是2025年3月19日）入职的员工。
4. 将 `employees` 表按 `hire_date` 的年份分区，分为 2024 和 2025 两个分区，其余归为未来分区。

完成后可以给我答案，我帮你检查！

---

## 第三阶段

------

好的！我们现在进入 DDL 的更高级部分：**触发器（TRIGGER）** 和 **存储过程（PROCEDURE）**。这两者虽然属于数据库编程的范畴，但在 MySQL 中是通过 DDL 语句定义的，非常适合管理复杂逻辑和自动化任务。我们继续以 MySQL 为例，从简单到复杂逐步学习。

---

### 1. 触发器（CREATE TRIGGER）
触发器是一种自动执行的特殊程序，在特定表上发生 `INSERT`、`UPDATE` 或 `DELETE` 操作时触发。可以用来确保数据一致性或记录日志。

#### 基本语法
```sql
CREATE TRIGGER 触发器名
{BEFORE | AFTER} {INSERT | UPDATE | DELETE}
ON 表名
FOR EACH ROW
BEGIN
    触发器逻辑;
END;
```

- `BEFORE`：在操作前执行
- `AFTER`：在操作后执行
- `FOR EACH ROW`：对每行操作都触发
- `NEW`：新插入或更新的行数据
- `OLD`：被更新或删除的旧行数据

#### 举例 1：记录插入日志
假设有 `students` 表和 `student_logs` 表：
```sql
CREATE TABLE students (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    score INT
);

CREATE TABLE student_logs (
    log_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    action VARCHAR(50),
    log_time TIMESTAMP
);
```

创建一个触发器，在插入学生时记录日志：
```sql
DELIMITER //
CREATE TRIGGER after_student_insert
AFTER INSERT ON students
FOR EACH ROW
BEGIN
    INSERT INTO student_logs (student_id, action, log_time)
    VALUES (NEW.id, 'INSERT', NOW());
END //
DELIMITER ;
```

测试：
```sql
INSERT INTO students (name, score) VALUES ('张三', 85);
```
查询 `student_logs`：
```
log_id | student_id | action | log_time
1      | 1          | INSERT | 2025-03-19 08:00:00
```

#### 举例 2：阻止非法更新
防止 `score` 更新为负数：
```sql
DELIMITER //
CREATE TRIGGER before_student_update
BEFORE UPDATE ON students
FOR EACH ROW
BEGIN
    IF NEW.score < 0 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Score cannot be negative';
    END IF;
END //
DELIMITER ;
```

测试：
```sql
UPDATE students SET score = -10 WHERE id = 1; -- 会报错
```

#### 删除触发器
**语法：**
```sql
DROP TRIGGER 触发器名;
```

**举例：**
```sql
DROP TRIGGER after_student_insert;
```

---

### 2. 存储过程（CREATE PROCEDURE）
存储过程是一组预定义的 SQL 语句集合，可以接受参数并执行复杂逻辑。适合重复使用的任务，比如批量操作或报表生成。

#### 基本语法
```sql
CREATE PROCEDURE 存储过程名 ([参数])
BEGIN
    逻辑语句;
END;
```

- 参数类型：
  - `IN`：输入参数（默认）
  - `OUT`：输出参数
  - `INOUT`：输入输出参数

#### 举例 1：简单存储过程
计算学生的总分：
```sql
DELIMITER //
CREATE PROCEDURE get_total_score()
BEGIN
    SELECT SUM(score) AS total_score FROM students;
END //
DELIMITER ;
```

调用：
```sql
CALL get_total_score();
```

#### 举例 2：带输入参数
根据班级 ID 获取学生数量：
```sql
DELIMITER //
CREATE PROCEDURE get_student_count(IN class_id_param INT)
BEGIN
    SELECT COUNT(*) AS student_count
    FROM students
    WHERE class_id = class_id_param;
END //
DELIMITER ;
```

调用：
```sql
CALL get_student_count(1);
```

#### 举例 3：带输出参数
返回平均成绩：
```sql
DELIMITER //
CREATE PROCEDURE get_avg_score(OUT avg_score DECIMAL(5,2))
BEGIN
    SELECT AVG(score) INTO avg_score FROM students;
END //
DELIMITER ;
```

调用：
```sql
CALL get_avg_score(@avg);
SELECT @avg;
```

#### 删除存储过程
**语法：**
```sql
DROP PROCEDURE 存储过程名;
```

**举例：**
```sql
DROP PROCEDURE get_total_score;
```

---

### 小练习
请根据以下要求写出 DDL 语句：
1. 创建 `orders` 表和 `order_logs` 表：
   - `orders`：`id`（主键，自增）、`amount`（DECIMAL(10,2)）、`order_date`（DATE）
   - `order_logs`：`log_id`（主键，自增）、`order_id`（整数）、`action`（字符串）、`log_time`（TIMESTAMP）
2. 创建一个触发器，在 `orders` 表插入新订单时，自动在 `order_logs` 中记录“NEW ORDER”。
3. 创建一个存储过程 `get_order_total`，接受一个日期参数，返回该日期的总订单金额。

